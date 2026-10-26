# SafeCore - Desafio SENAI

Este repositório reúne duas frentes de demonstração tecnológica desenvolvidas para evidenciar como segurança, IA e operação industrial podem ser integradas em cenários críticos.

O conjunto apresenta uma solução de zero trust para acesso inteligente e uma aplicação de visão computacional focada em preservação de privacidade em ambientes com uso de realidade aumentada.

## Visão geral

O projeto é organizado em duas principais áreas:

- `petrobras-poc`: demonstração de gateway de segurança com autenticação criptográfica, autorização em blockchain e análise comportamental para bloquear requisições anômalas antes da resposta de um assistente de IA.
- `detector-oculos`: pipeline de visão computacional para detectar rostos, telas e documentos em tempo real, aplicar censura visual e produzir capturas criptografadas com foco em segurança e privacidade de dados.

## Objetivo do repositório

O objetivo é demonstrar, em escala de prova de conceito, como sistemas de IA e visão computacional podem operar com regras rigorosas de segurança, minimização de dados e validação contextual antes de permitir processamento ou armazenamento de informações sensíveis.

As soluções foram estruturadas para ilustrar cenários de:

- autenticação de hardware e identidade de dispositivo;
- controle de acesso baseado em blockchain;
- análise de risco e comportamento;
- proteção de dados pessoais e informações confidenciais;
- uso de visão computacional para reduzir a exposição de dados sensíveis.

## Estrutura do projeto

- `petrobras-poc/`
  - backend com API em FastAPI;
  - contrato inteligente em Solidity;
  - frontend para simulação de ambiente operacional;
  - dependências do projeto.

- `detector-oculos/`
  - processamento de imagem em OpenCV;
  - detecção com Deep Learning e modelos SSD e YOLO;
  - criptografia de snapshots sensíveis;
  - lógica de ocultação de elementos confidenciais em tempo real.

## Fluxo geral do ecossistema

1. O ambiente operacional emite ou processa informações sensíveis.
2. O sistema valida identidade, contexto e integridade do aparelho ou da transmissão.
3. Dados visuais são redigidos, censurados ou protegidos antes do armazenamento ou envio.
4. A decisão de liberação ou bloqueio é tomada com base em regras de segurança e análise comportamental.
5. Eventos relevantes são registrados para rastreabilidade e auditoria.

## Tecnologias principais

- Python
- FastAPI
- OpenCV
- NumPy
- scikit-learn
- Web3.py
- Solidity
- YOLO
- criptografia simétrica com Fernet
- JavaScript para a interface web

## Considerações

Este repositório foi organizado como demonstração funcional e pedagógica. Ele apresenta a lógica e a arquitetura de segurança, mas não substitui requisitos de produção, revisão de conformidade e governança digital mais exigentes.

## Execução

Para executar cada parte do projeto, siga as instruções específicas de cada subdiretório:

- `petrobras-poc/README.md`
- `detector-oculos/README.md`

## Conclusão

A combinação de inteligência artificial, visão computacional e controles de segurança torna o projeto relevante para aplicações em ambientes industriais, de campo, corporativos e regidos por requisitos de privacidade e proteção de dados. A proposta busca demonstrar uma abordagem prática de segurança por design, com foco em risco, conformidade e controle de acesso.
