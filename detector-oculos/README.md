# Detector de Óculos com Privacidade por Design

Este módulo tem como objetivo demonstrar um sistema de visão computacional em tempo real para proteção de dados sensíveis em cenários de realidade aumentada. A solução identifica rostos, telas e documentos, aplica censura visual e salva capturas criptografadas para garantir a privacidade das informações capturadas.

## Objetivo

O projeto simula um ambiente de óculos inteligentes operacionais em que a câmera coleta imagens do ambiente. Antes que o conteúdo seja armazenado ou transmitido, o sistema bloqueia regiões sensíveis e mantém a confidencialidade dos dados. Isso reduz o risco de vazamento de informações pessoais ou corporativas.

## Como funciona

O fluxo da aplicação é organizado em etapas:

1. A câmera captura o ambiente em tempo real.
2. O sistema identifica faces por meio de um modelo SSD baseado em Caffe.
3. O modelo YOLO é usado para detectar telas, celulares e documentos.
4. Cada área sensível é coberta com redigitação visual e overlay de segurança.
5. A aplicação sobrepõe elementos de HUD para indicar o estado do sistema.
6. Quando solicitado, a imagem processada é salva em um arquivo criptografado.

## Funcionalidades principais

- detecção de rostos em tempo real;
- identificação de telas e documentos sensíveis;
- redigitação visual das regiões detectadas;
- alertas visuais em HUD;
- criptografia de snapshots armazenados;
- suporte à simulação de ambiente operacional com proteção de privacidade.

## Arquitetura do módulo

### Detecção facial

A aplicação usa um modelo de redes neurais profundas baseado em Caffe SSD para localizar faces. O algoritmo calcula a caixa delimitadora e aplica uma máscara de proteção para ocultar a identidade da pessoa.

### Detecção de dispositivos e documentos

O módulo também utiliza YOLOv8 para detectar objetos como:

- monitores;
- celulares;
- livros ou documentos físicos.

Esses elementos são tratados como dados potencialmente sensíveis, sendo redigidos e protegidos imediatamente.

### Criptografia

As capturas protegidas são transformadas em payloads em JSON, codificadas em Base64 e criptografadas com Fernet, utilizando uma chave mestre gerada localmente. Isso garante que o conteúdo salvo não fique exposto em texto simples em disco.

## Estrutura de arquivos

- `visaoborrada.py`: script principal com pipeline completo de processamento, detecção, redação e salvamento seguro.
- `descriptador.py`: utilitário para leitura e interpretação das capturas protegidas.
- `deploy.prototxt`: arquivo de configuração do modelo facial SSD.
- `res10_300x300_ssd_iter_140000.caffemodel`: pesos do modelo de detecção facial.

## Dependências

O módulo depende dos seguintes componentes:

- OpenCV
- NumPy
- cryptography
- ultralytics

## Requisitos de execução

- Python 3.9 ou superior
- câmera disponível no ambiente local
- modelos de detecção corretamente presentes no diretório do projeto
- instalação das dependências necessárias

## Instalação

1. Crie e ative um ambiente virtual:

   python -m venv .venv
   .venv\Scripts\activate

2. Instale as dependências:

   pip install opencv-python numpy cryptography ultralytics

3. Verifique se os arquivos de modelo e configuração estão presentes no diretório do projeto.

## Como executar

Execute o script principal:

   python visaoborrada.py

Durante a execução:

- a câmera será aberta em tempo real;
- a aplicação exibirá o vídeo processado com redigitação;
- pressionando a tecla `S` será gerada uma captura protegida e criptografada;
- pressionando `Q` encerra a execução.

## Observações de segurança

Este módulo foi pensado como demonstração de privacidade por design em aplicações de visão computacional. A solução é adequada para protótipos e estudos de arquitetura, mas requer revisão adicional para uso em produção, especialmente no que diz respeito a:

- armazenamento de chaves criptográficas;
- proteção de dados em trânsito e em repouso;
- validação de risco e política de retenção;
- conformidade com requisitos de privacidade e proteção de dados pessoais.

## Conclusão

O detector de óculos representa uma aplicação prática de segurança em IA e visão computacional, com foco na proteção de dados sensíveis em ambientes observados. A combinação de detecção inteligente, censura visual e criptografia reforça o princípio de que o sistema deve reduzir exposição indevida de informações antes mesmo de armazenar ou compartilhar conteúdo.
