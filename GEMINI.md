# --- REGRAS DE OURO DO PROJETO AIDO ---

## Arquitetura e Estrutura
- A lógica de negócio principal reside na pasta `core/`.
- As classes de serviço (TranscriptionService, VisionService, etc.) estão no arquivo `core/services.py`.
- A API web é construída com FastAPI e está localizada em `app/main.py`.
- Os prompts de IA são arquivos de texto e ficam na pasta `plugins/`.

## Bibliotecas e Tecnologias
- Para modelos de IA locais, a biblioteca principal é a `transformers` da Hugging Face, com otimização 4-bit via `bitsandbytes`.
- A transcrição de áudio deve ser feita com a biblioteca `faster-whisper`.
- A geração de documentos `.docx` é feita com a biblioteca `docxtpl`.

## Estilo de Código e Qualidade
- Use `ruff` para toda a verificação de qualidade (linting) e formatação de código. Antes de finalizar uma tarefa, sempre rode `ruff format .` e `ruff check .`.
- Todas as funções, métodos e classes públicas devem ter docstrings no estilo Google, incluindo as seções `Args:` e `Returns:`.
- Todo o código Python deve usar `type hints` para todos os argumentos e retornos.

## Suas Regras Adicionais

- PRD: "Com certeza, Pedro. Entendido.

Nossa meta é criar o blueprint de engenharia definitivo para o AIDO. Um documento tão completo e claro que possa ser entregue diretamente a uma IA como a Gemini CLI para orquestrar a construção do projeto do início ao fim.

Preparei este PRD Masterizado em Markdown (.md), consolidando nossa visão final. Você pode salvá-lo como o "manual do projeto" e copiar e colar seu conteúdo como contexto para guiar o Gemini em cada etapa.

PRD Masterizado: AIDO
A Fábrica de Conhecimento Automatizada

Autor: Pedro Gonçalves
Versão: Final (Local-First)
Data: 27 de Setembro de 2025

1. A Visão: Transformando Ação em Conhecimento Escalável
Em toda grande corporação, o conhecimento mais valioso reside na experiência prática de seus colaboradores – um conhecimento tácito, difícil de documentar e escalar. O AIDO ataca este problema fundamental. Ele não é um simples gravador de tela ou um editor de texto. O AIDO é uma fábrica de engenharia de conhecimento, projetada para observar uma ação (um especialista executando um processo em vídeo) e transformá-la em um ativo de conhecimento explícito, estruturado e reutilizável (um manual técnico perfeito).

Nossa missão é eliminar o gargalo entre o "saber fazer" e o "saber ensinar".

2. As Personas
A Especialista (Ana): Uma analista sênior na Bosch, expert em um processo complexo de Power BI. Ela precisa treinar novos membros da equipe, mas não tem tempo para escrever um manual detalhado. Ela grava sua tela executando o processo uma única vez.

O Novato (Bruno): Um novo membro da equipe. Ele precisa aprender o processo da Ana. Assistir a um vídeo de 30 minutos é ineficiente; ele precisa de um documento passo a passo, consultável, para seguir e aprender no seu próprio ritmo.

3. O Problema: O Conhecimento que se Evapora
Conhecimento Tácito é Inescalável: A expertise de colaboradores como a Ana fica presa em suas cabeças ou em formatos de difícil consulta, como vídeos.

Documentação é um Gargalo: A criação manual de documentação de alta qualidade é um processo lento, caro e que especialistas raramente têm tempo para executar.

Vídeos são Ineficientes para Aprendizado: Vídeos são ótimos para demonstrações, mas péssimos como referência. É impossível pesquisar texto, copiar comandos ou seguir um passo a passo complexo a partir de um vídeo.

4. A Solução: Uma Pipeline de IA Multimodal
O AIDO resolve o problema de Ana e Bruno. Ele ingere o vídeo de Ana e, de forma autônoma, gera o manual que Bruno precisa.

Princípios do Produto:

Automatizado: Do vídeo ao documento final, sem intervenção manual.

Multimodal: A IA entende o que foi dito (áudio) e o que foi mostrado (visual).

Estruturado: O resultado não é um texto corrido, mas um documento com seções claras, tabelas e um passo a passo lógico.

Local-First: Todo o processamento de IA e dados ocorre na máquina do usuário, garantindo 100% de privacidade e segurança.

5. Requisitos Funcionais (MVP)
EP-01: Ingestão de Vídeo: O sistema aceita um arquivo de vídeo (.mp4) como input principal.

EP-02: Análise de Áudio (Serviço de Transcrição): Utiliza faster-whisper para gerar uma transcrição completa do áudio, com timestamps precisos para cada segmento de fala.

EP-03: Análise Visual (Serviço de Visão):

Utiliza opencv-python para extrair frames do vídeo em intervalos regulares (ex: a cada 5 segundos).

Utiliza um modelo de IA da Hugging Face (Salesforce/blip-image-captioning-base) para gerar uma descrição textual para cada frame, associando-a a um timestamp.

EP-04: Log Enriquecido: Os dados da transcrição e da análise visual são fundidos e ordenados cronologicamente em um único arquivo de texto, o "Log de Eventos", que serve como a fonte da verdade completa do processo.

EP-05: Geração de Conteúdo (Agente de Geração):

Utiliza um poderoso LLM local (meta-llama/Llama-3-8B-Instruct) para analisar o Log de Eventos.

Guiado por um prompt detalhado (ManualAgent), a IA gera um único e completo objeto JSON que contém todo o conteúdo textual do manual (título, resumo, introdução, passo a passo detalhado, etc.).

EP-06: Criação do Documento Final: O sistema utiliza docxtpl para renderizar o objeto JSON em um template .docx pré-formatado, salvando o manual final.

6. Arquitetura Técnica (Local-First com Hugging Face)
Linguagem: Python 3.10+

Estrutura: Projeto modular com pastas core (lógica), app (API), plugins (prompts) e data.

Modelos de IA:

Gerenciamento: Ecossistema Hugging Face (transformers, accelerate).

Otimização: bitsandbytes para carregar modelos em 4-bit (quantização), reduzindo drasticamente o uso de memória.

Framework: PyTorch.

API (Opcional, para expansão): FastAPI para expor a funcionalidade como um serviço.

Conectores: Nenhum conector externo é necessário para o MVP, tudo é processado localmente.

7. Fluxo de Dados
Vídeo (.mp4) → [Transcrição + Análise Visual] → Log Enriquecido (.txt) → [Agente de Geração com LLM Local] → Conteúdo Estruturado (.json) → [Renderizador docxtpl] → Manual Final (.docx)

8. Métricas de Sucesso (MVP)
Redução de Tempo: O tempo para criar um manual de processo de alta qualidade é reduzido em mais de 95% (de horas/dias para minutos).

Qualidade do Output: Feedback qualitativo de usuários "Bruno" indica que os manuais gerados são claros, fáceis de seguir e mais úteis que o vídeo original como material de referência.

Viabilidade Técnica: O sistema completo roda com sucesso em uma máquina local com hardware de consumidor (com GPU dedicada).

9. Visão de Futuro (Roadmap)
Editor Interativo: Criar uma interface web (com Streamlit ou FastAPI+React) onde o usuário "Ana" possa revisar e editar o manual gerado pela IA antes de salvá-lo.

Geração de Múltiplos Formatos: Exportar o manual não apenas como .docx, mas também como .pdf ou uma página da Confluence/SharePoint.

"Agente de Otimização": Um segundo fluxo que lê um manual já gerado e sugere melhorias e automações para o processo documentado."
