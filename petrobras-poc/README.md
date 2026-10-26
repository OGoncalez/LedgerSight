# Gateway Zero Trust para Assistência Operacional

Este projeto apresenta uma arquitetura de prova de conceito para validação de acesso seguro em ambientes industriais, com foco em operações de campo e suporte inteligente a trabalhadores por meio de dispositivos simulados de óculos inteligentes. A solução combina autenticação criptográfica, controle de acesso baseado em blockchain e análise de comportamento para bloquear acessos anômalos antes que uma requisição alcance um modelo de linguagem.

A proposta central é simples: apenas dispositivos autenticados, autorizados e com contexto operacional válido conseguem solicitar processamento em um ambiente de IA. Isso reduz a superfície de risco em cenários em que a integridade do hardware, a origem da rede e a geolocalização podem indicar tentativa de abuso ou comprometimento.

## Visão geral

O sistema foi concebido para demonstrar um fluxo de Zero Trust em um cenário industrial, com os seguintes princípios:

- autenticação do hardware por assinatura criptográfica;
- validação de autorização em contrato inteligente na blockchain;
- análise contextual do pedido para detectar comportamento suspeito;
- registro de eventos em um ledger distribuído para auditoria;
- interface simulada de assistente operacional para demonstrações.

## Arquitetura

O projeto está organizado em três camadas principais:

### 1. Frontend

A interface em JavaScript simula um dispositivo de óculos inteligentes usado em planta industrial. Ela permite:

- modificar a origem de rede;
- alterar o horário operacional;
- manipular a variância de GPS;
- gerar assinaturas criptográficas para autenticação;
- simular tentativas de comprometimento do dispositivo.

### 2. Backend

O serviço em FastAPI atua como gateway de segurança. Antes de aceitar uma requisição, ele:

- valida a assinatura digital do payload;
- verifica se o dispositivo está autorizado no contrato blockchain;
- aplica a análise de risco comportamental;
- permite ou bloqueia a resposta final.

### 3. Blockchain

Um contrato inteligente em Solidity armazena a autorização dos dispositivos e registra eventos de acesso. Esse mecanismo fornece um histórico imutável e um mecanismo de política de acessos para a camada de decisão.

## Fluxo de operação

O fluxo funcional do sistema é o seguinte:

1. O frontend gera uma identidade de dispositivo e assina os metadados da requisição.
2. O backend recupera os metadados assinados e verifica a assinatura com a chave pública do dispositivo.
3. O backend consulta a blockchain para confirmar se o dispositivo está autorizado.
4. O módulo SentinelAI avalia anomalias com base em IP, horário e variância de GPS.
5. Se todos os controles forem aprovados, a requisição é processada.
6. Em caso de falha, a ação é bloqueada e registrada no ledger.

## Principais componentes

### Backend

- `backend/main.py`: API principal e orquestração do fluxo de validação.
- `backend/sentinel.py`: módulo de análise de comportamento com Isolation Forest.
- `backend/blockchain_client.py`: cliente para leitura e gravação de eventos na blockchain.
- `backend/contract_data.json`: dados do contrato implantado e ABI.

### Blockchain

- `blockchain/contracts/AccessControl.sol`: contrato responsável por autorização e auditoria.
- `blockchain/deploy.py`: script para compilação e implantação local do contrato.

### Frontend

- `frontend/index.html`: estrutura visual da simulação operacional.
- `frontend/styles.css`: definições visuais da interface.
- `frontend/app.js`: lógica de autenticação, interação com a API e simulação de contexto de risco.

## Tecnologias utilizadas

- Python 3.10+
- FastAPI
- Web3.py
- Solidity
- scikit-learn
- pandas
- NumPy
- JavaScript no navegador
- Ganache ou rede local Ethereum equivalente

## Requisitos

Antes de iniciar o projeto, verifique se os seguintes elementos estão disponíveis:

- Python instalado e configurado no ambiente.
- Ambiente virtual para isolamento das dependências.
- Rede local Ethereum em execução, como Ganache, na porta 7545.
- Acesso a um navegador para a interface frontend.

## Instalação

No diretório do projeto, execute os passos a seguir:

1. Crie um ambiente virtual:

   python -m venv .venv

2. Ative o ambiente virtual:

   No Windows:
   .venv\Scripts\activate

   No Linux/macOS:
   source .venv/bin/activate

3. Instale as dependências:

   pip install -r requirements.txt

4. Inicie a rede blockchain local. Recomenda-se o Ganache com a porta 7545.

5. Implante o contrato inteligente:

   python blockchain/deploy.py

6. Inicie a API backend:

   uvicorn backend.main:app --host 0.0.0.0 --port 8000 --reload

7. Abra a interface frontend em um navegador usando o arquivo `frontend/index.html`.

## Como utilizar

Depois da inicialização:

- a interface gera ou recupera a identidade do dispositivo;
- o backend verifica a autorização do aparelho;
- o usuário pode realizar requisições de teste na área de chat;
- alterações em rede, tempo e geolocalização influenciam a decisão de acesso;
- tentativas de identidade fraudulenta ou condições fora do padrão podem resultar em bloqueio.

## Casos de uso representados

Este projeto simula cenários típicos de segurança operacional, incluindo:

- dispositivos com falha de integridade;
- uso de redes públicas ou não confiáveis;
- deslocamento físico fora do perímetro operacional;
- acesso em horários fora da janela permitida;
- tentativa de registro de hardware não autorizado.

## Observações de segurança

Este é um projeto de demonstração e prova de conceito. A implementação foi pensada para ilustrar a arquitetura de Zero Trust e não deve ser utilizada diretamente como ambiente de produção sem revisão adicional de segurança, governança e políticas de autenticação mais robustas.

Entre os pontos que exigiriam refinamento para uso real, destacam-se:

- autenticação de usuários e dispositivos com identidade pública e privada robusta;
- gestão de chaves em ambiente seguro do tipo HSM;
- integrações reais com modelos de linguagem e provedores de IA;
- validação avançada de geolocalização e contexto de risco;
- política de retenção e auditoria de registros em blockchain.

## Limites do escopo atual

A solução atual foi desenhada para demonstrar a lógica de controle de acesso e análise contextual, e não para substituir uma solução completa de governança de identidade, segurança perimetral e integração com infraestrutura corporativa.

## Estrutura de diretórios

petrobras-poc/

- backend/
- blockchain/
- frontend/
- requirements.txt

## Conclusão

Este projeto demonstra como um modelo de segurança baseado em Zero Trust pode ser aplicado em uma arquitetura de assistente operacional. Ao combinar autenticação de dispositivo, autorização imutável, análise de contexto e controle de acesso antes da geração da resposta, a solução aumenta a resiliência e a confiabilidade de processos automatizados em ambientes sensíveis.

A implementação serve como base para extensões em áreas como inspeção industrial, suporte técnico em campo, operação remota e gestão de risco em ambientes críticos.
