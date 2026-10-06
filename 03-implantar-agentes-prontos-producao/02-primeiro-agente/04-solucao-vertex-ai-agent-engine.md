# 04. A Solução: Vertex AI Agent Engine

## 🎯 Visão Geral
O **Vertex AI Agent Engine** é um serviço totalmente gerenciado do Google Cloud projetado para implantar, gerenciar e escalar agentes do ADK em produção sem a necessidade de gerenciar infraestruturas complexas[cite: 1].

---

## 🚀 Principais Vantagens

* **Implantação com Um Comando:** Transforma agentes locais em endpoints de produção instantaneamente[cite: 1].
* **Sem Necessidade de Docker:** Conteinerização automática gerenciada pelo ADK[cite: 1].
* **Persistência Automática de Sessão:** Substitui o `InMemorySessionService` pelo `VertexAiSessionService` sem alterações de código[cite: 1].
* **Infraestrutura Totalmente Gerenciada:** O Google Cloud cuida do escalonamento automático, atualizações, patches e alta disponibilidade 24/7[cite: 1].
* **Suporte Nativo ao ADK:** Criado sob medida para a suíte de agentes do ADK (Atualmente compatível com Python)[cite: 1].

---

## 🏗️ Arquitetura e O que é Implantado

```text
Seu Código (agent.py) 
  ↓ (adk deploy agent-engine)
Google Cloud Agent Engine
├── Contêiner (Gerado automaticamente)
├── VertexAiSessionService (Sessão persistente gerenciada)
├── Escalonamento Automático (Serverless)
└── Endpoint Público (Rest/SDK)

```

### 🧰 Conteúdo do Pacote de Deploy

* Código do agente do ADK e bibliotecas do runtime.


* Dependências listadas em `requirements.txt`.


* `VertexAiSessionService` para persistência de estado.



> **Nota:** Ferramentas de desenvolvimento local (como a interface gráfica do `adk web`) não são enviadas para produção.
> 
> 

---

## 💻 Comando de Implantação

```bash
adk deploy agent-engine \
  --project=NOME_DO_PROJETO \
  --region=us-central1 \
  --staging_bucket=gs://SEU_BUCKET \
  --display_name="Nome do Agente" \
  /caminho/para/o/agente

```

### 📋 Fluxo do Deploy (Duração: 5 a 10 min)

1. **Pacote:** O ADK agrupa o código `agent.py` e suas dependências.


2. **Upload:** Envia os artefatos para o Google Cloud Storage (GCS).


3. **Build:** O ADK constrói a imagem do contêiner automaticamente.


4. **Deploy:** Implanta o contêiner no Vertex AI Agent Engine.


5. **Endpoint:** Retorna o URI do recurso (`projects/{PROJECT}/locations/{LOCATION}/reasoningEngines/{ID}`).



---

## 🧪 Formas de Testar o Agente Implantado

### 1. SDK do Python (`google-cloud-aiplatform`)

```python
import os
from google.cloud import aiplatform

aiplatform.init(project="meu-projeto", location="us-central1")

resource_name = "projects/123/locations/us-central1/reasoningEngines/456"
remote_app = aiplatform.ReasoningEngine(resource_name)

response = remote_app.query(input="Qual a previsão do tempo?")
print(response)

```

### 2. Interface do Console do Cloud

* Acesse: `https://console.cloud.google.com/vertex-ai/agents/agent-engines`

* Teste diretamente pelo chat integrado visual e acompanhe os logs de execução do Cloud Logging.



### 3. API REST (curl)

```bash
TOKEN=$(gcloud auth print-access-token)

curl -X POST \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"input": "Qual a previsão do tempo?"}' \
  [https://REGION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/reasoningEngines/ID:query](https://REGION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/reasoningEngines/ID:query)

```

---

## 🧠 Persistência da Sessão em Produção

O `VertexAiSessionService` é ativado automaticamente, garantindo que todos os 4 namespaces do ADK funcionem sem necessidade de refatorar o código:

| Namespace | Escopo | Comportamento no Agent Engine |
| --- | --- | --- |
| `temp:` | Turno atual | Temporário (limpo ao final do turno)

 |
| `session` | Conversa ativa | **Persistente** entre reinicializações

 |
| `user:` | Usuário específico | **Persistente** entre múltiplas sessões

 |
| `app:` | Aplicação global | **Persistente** globalmente no sistema

 |

---

## 🛠️ Exemplos Práticos de Deploy

### Exemplo 1: Agente Simples (`LlmAgent`)

1. Estruture o arquivo `agent.py` definindo o `root_agent`.


2. Configure o arquivo `requirements.txt` com `google-cloud-aiplatform[adk,agent_engines]>=1.111`.


3. Crie o bucket no Cloud Storage: `gsutil mb -l us-central1 gs://meu-bucket-staging`.


4. Execute o comando `adk deploy agent-engine`.



### Exemplo 2: Fluxos Multiagentes Complexos

Sistemas complexos com orquestração dinâmica (ex: `SequentialAgent`, `ParallelAgent`, `LoopAgent` com `EventActions`) são implantados **sem nenhuma alteração de código**:

* **Execução Paralela:** `ParallelAgent` continua executando validadores simultaneamente em nuvem.


* **Encerramento Dinâmico de Loop:** Regras de `EventActions(escalate=True)` ou quebras de loop funcionam nativamente no ambiente do Agent Engine.


* **Gerenciamento de Estado:** O estado é compartilhado entre agentes downstream via `VertexAiSessionService`.
---

