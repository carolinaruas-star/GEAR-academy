# 02. Como Conectar Agentes Remotos com o ADK e o SDK Agent2Agent (A2A) (GENAI120)

## 📌 Visão Geral
O protocolo **Agent2Agent (A2A)** estabelece uma linguagem de comunicação padronizada para que agentes de IA generativa — criados em diferentes *frameworks* e executados em servidores ou nuvens distintas — interajam e colaborem como **agentes autônomos**, e não como meras chamadas de funções/ferramentas.

Neste laboratório, um agente gerador de ilustrações (*illustration_agent*) é empacotado e implantado no **Cloud Run** como um microsserviço A2A. Em seguida, um segundo agente (*slide_content_agent*) o consome remotamente através de um **Agent Card** em formato JSON.

---

## 🎯 Objetivos do Laboratório
* **Configuração de Servidor A2A:** Empacotar e implantar um agente ADK como servidor A2A no Google Cloud Run.
* **Definição de Agent Card (`agent.json`):** Descrever as capacidades, habilidades (*skills*) e endpoints do agente em um padrão JSON para descoberta.
* **Consumo Remoto via `RemoteA2aAgent`:** Permitir que um agente orquestrador leia o Agent Card e delegue tarefas a um agente remoto como um subagente.

---

## 🌐 Os Pilares do Protocolo Agent2Agent (A2A)

1. **Comunicação Padronizada:** Transporte estruturado via **JSON-RPC 2.0 sobre HTTP(S)**.
2. **Descoberta Dinâmica (Agent Cards):** Arquivo manifesto (`agent.json`) com metadados de capacidades, habilidades e URL do serviço.
3. **Abstração `A2aAgentExecutor`:** Camada do ADK que traduz requisições/tarefas do protocolo A2A para o sistema interno de eventos do ADK.
4. **Prontidão Empresarial:** Suporte a comunicação segura, observabilidade, autenticação e streaming (SSE).

---

## 🛠️ Passo a Passo Prático

### 1. Definição do Card do Agente (`agent.json`)
Exemplo de manifesto para expor o serviço de ilustrações da empresa fictícia *Cymbal Stadiums*:

```json
{
    "name": "illustration_agent",
    "description": "An agent designed to generate branded illustrations for Cymbal Stadiums.",
    "defaultInputModes": ["text/plain"],
    "defaultOutputModes": ["application/json"],
    "skills": [
      {
          "id": "illustrate_text",
          "name": "Illustrate Text",
          "description": "Generate an illustration to illustrate the meaning of provided text.",
          "tags": ["illustration", "image generation"]
      }
    ],
    "url": "https://illustration-agent-PROJECT_NUMBER.REGION.run.app/a2a/illustration_agent",
    "capabilities": {},
    "version": "1.0.0"
}

```

### 2. Deploy no Cloud Run com Suporte A2A

Utiliza-se a flag `--a2a` no comando `adk deploy cloud_run` para envelopar o código com o executor do protocolo A2A:

```bash
adk deploy cloud_run \
    --project YOUR_GCP_PROJECT_ID \
    --region GCP_LOCATION \
    --service_name illustration-agent \
    --a2a \
    illustration_agent \
    -- \
    --service-account=illustration-agent-sa@YOUR_GCP_PROJECT_ID.iam.gserviceaccount.com \
    --set-env-vars="GOOGLE_CLOUD_LOCATION=global"

```

### 3. Invocação do Agente Remoto (`RemoteA2aAgent`)

No agente consumidor (*slide_content_agent*), importa-se e registra-se o subagente remoto passando o caminho do arquivo de manifesto:

```python
from google.adk.agents import RemoteA2aAgent, LlmAgent

# Registra o agente A2A remoto através do seu Agent Card
illustration_agent = RemoteA2aAgent(
    name="illustration_agent",
    description="Agent that generates illustrations.",
    agent_card="illustration-agent-card.json"
)

# Adiciona o agente remoto como subagente do root_agent
root_agent = LlmAgent(
    name="slide_content_agent",
    instruction="Crie um título e texto para o slide e transfira para o illustration_agent para gerar a imagem.",
    sub_agents=[illustration_agent]
)

```

---

## 📊 Fluxo de Comunicação Distribuída

```text
[Usuário] 
    │
    ▼
[slide_content_agent] (Agente Orquestrador Local)
    │  1. Gera título e corpo do texto para o slide
    │  2. Identifica necessidade de ilustração
    │  3. Consulta 'illustration-agent-card.json'
    │
    ▼ (Requisição HTTP / JSON-RPC 2.0 A2A)
[illustration-agent no Cloud Run] (Servidor A2A Remoto)
    │  1. Recebe o texto via 'A2aAgentExecutor'
    │  2. Aplica as diretrizes de marca (Corporate Memphis, cores, etc.)
    │  3. Gera a imagem com Gemini + salva no Cloud Storage
    │
    ▼ (Resposta A2A com URL da Imagem)
[slide_content_agent] ──> Exibe resposta consolidada com o texto e a imagem
```
---