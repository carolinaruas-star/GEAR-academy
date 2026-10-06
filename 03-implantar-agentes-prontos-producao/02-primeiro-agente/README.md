# 🚀 Módulo 02: Implantar Seu Primeiro Agente

Bem-vindo à documentação e ao resumo prático do **2º Módulo do Curso da Academia Gemini Enterprise Agent Platform (GEAR)** promovida pelo Google Cloud. 

Este repositório consolida todo o conhecimento técnico, arquiteturas e comandos práticos para transicionar agentes de IA desenvolvidos em ambiente local (`localhost`) para infraestruturas de nuvem de alta disponibilidade, escaláveis e prontas para produção.

---

## 📌 Visão Geral do Módulo

Após construir agentes robustos com ferramentas, instruções e orquestrações complexas, surge o grande desafio da engenharia de software: **como disponibilizar esses agentes de forma global, segura e persistente?**

Neste curso, exploramos a superação da "lacuna do localhost", dominando as duas principais plataformas de implantação do Google Cloud para o **ADK (Agent Development Kit)**: **Vertex AI Agent Engine** e **Cloud Run**.

---

## 🎯 Objetivos de Aprendizagem

* **Eliminar a dependência do Localhost:** Disponibilizar agentes 24/7 com URLs HTTPS públicas e escalonamento automático.
* **Dominar o Vertex AI Agent Engine:** Realizar deploys gerenciados nativos com um único comando e sem necessidade de conhecimento prévio em DevOps/Docker.
* **Implementar a Arquitetura Completa de Memória:** Migrar o estado de sessão temporário (`InMemorySessionService`) para serviços persistentes (`VertexAiSessionService`) e conectar o **Memory Bank** para aprendizado contínuo entre sessões.
* **Explorar Implantações Flexíveis no Cloud Run:** Containerizar agentes com suporte a múltiplas linguagens e disponibilizar interfaces gráficas interativas (`--with_ui`).

---

## 📂 Estrutura dos Arquivos

```text
02-primeiro-agente/
│
├── 01-problema-agentes-em-localhost.md      # ❌ Limitações do ambiente local e a lacuna de produção
├── 02-solucao-opcoes-de-implantacao-adk.md  # 💡 Visão geral das estratégias de deploy do ADK
├── 03-problema-barreira-da-complexidade.md  # ❌ A complexidade tradicional de DevOps vs. Agentes
├── 04-solucao-vertex-ai-agent-engine.md     # 💡 Deploy nativo, gerenciado e com 1 comando
├── 05-estado-da-sessao-vs-banco-de-memoria.md # 🧠 Diferenças entre curto prazo e aprendizado contínuo
├── 06-quando-usar-banco-de-memoria.md        # 🎯 Casos de uso e escolha de arquitetura de memória
├── 07-como-implantar-no-cloud-run.md        # ☁️ Alternativa serverless flexível com interface web
├── 08-exemplo-pratico.md                    # 🛠️ Mão na massa: deploy no Cloud Run e integração via API
└── 08-badge-conclusao.md                    # 🏅 Validação de competências e encerramento

```

## ⚡ Guia Rápido de Comandos de Deploy

### 1. Vertex AI Agent Engine (Opção Padrão / 100% Gerenciada)

Ideal para agentes ADK padrão em Python. O Google Cloud gerencia automaticamente os contêineres e o estado da sessão.

```bash
adk deploy agent-engine \
  --project=$GOOGLE_CLOUD_PROJECT \
  --region=$GOOGLE_CLOUD_LOCATION \
  --staging_bucket=gs://seu-bucket-staging \
  --display_name="Meu Agente do ADK" \
  /caminho/para/o/agente

```

### 2. Cloud Run (Opção Flexível / Com Interface Web)

Ideal para quando você precisa de uma interface gráfica web pronta para teste, suporte multi-linguagem ou contêineres customizados.

```bash
adk deploy cloud_run \
  --project=$GOOGLE_CLOUD_PROJECT \
  --region=$GOOGLE_CLOUD_LOCATION \
  --service_name=meu-agente \
  --with_ui \
  /caminho/para/o/agente

```

---

## 🧠 Arquitetura de Memória: Estado vs. Memory Bank

| Recurso | Escopo | Função Principal |
| --- | --- | --- |
| **Estado da Sessão** | Conversa Ativa | Gerencia variáveis e contexto do turno atual (`VertexAiSessionService`). |
| **Memory Bank** | Todas as Conversas | Extrai e armazena preferências do usuário ao longo do tempo via busca semântica. |

---

## 🛠️ Pré-requisitos do Google Cloud

Para reproduzir os exemplos e comandos deste repositório, certifique-se de possuir:

1. **CLI `gcloud**` autenticada e configurada no projeto ativo.
2. **APIs ativadas:** `aiplatform.googleapis.com` (Vertex AI) e `run.googleapis.com` (Cloud Run).
3. **SDK da Vertex AI instalado:**
```bash
pip install --upgrade google-cloud-aiplatform[adk,agent_engines]>=1.111

```
## 🔗 Links e Recursos Recomendados

* [Documentação Oficial do ADK](https://google.github.io/adk-docs/)
* [Visão Geral do Vertex AI Agent Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview)
* [Documentação do Google Cloud Run](https://cloud.google.com/run/docs)
* [Repositório Oficial de Exemplos (google/adk-samples)](https://github.com/google/adk-samples)

---