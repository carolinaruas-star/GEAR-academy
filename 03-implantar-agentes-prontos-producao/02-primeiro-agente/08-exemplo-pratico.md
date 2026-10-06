# 08. Exemplo Prático: Deploy no Cloud Run & Acesso aos Agentes

## 🛠️ Passo a Passo Prático de Implantação

### Etapa 1: Estruturação do Agente
Crie o diretório do agente e adicione os arquivos base[cite: 1]:

```bash
mkdir weather_agent_cloud_run
cd weather_agent_cloud_run

```

* **`agent.py`:**
```python
from google.adk.agents import LlmAgent

root_agent = LlmAgent(
    model='gemini-2.5-flash',
    name='weather_agent',
    description='Weather agent on Cloud Run',
    instruction='''
    Você é um assistente de clima prestativo.
    Forneça informações meteorológicas para cidades do mundo todo.
    '''
)

```


* **`__init__.py`:**
```python
from .agent import root_agent

```



---

### Etapa 2: Deploy no Cloud Run

Defina as variáveis de ambiente e execute o comando do ADK com a flag `--with_ui`:

```bash
export GOOGLE_CLOUD_PROJECT="seu-project-id"
export GOOGLE_CLOUD_LOCATION="us-central1"

adk deploy cloud_run \
  --project=$GOOGLE_CLOUD_PROJECT \
  --region=$GOOGLE_CLOUD_LOCATION \
  --service_name=weather-agent \
  --with_ui \
  weather_agent_cloud_run/

```

**Saída esperada:**

```text
Criando contêiner…
Implantando no Cloud Run…
✓ Serviço implantado
URL do serviço: [https://weather-agent-xyz123.us-central1.run.app](https://weather-agent-xyz123.us-central1.run.app)

```

---

## 🌐 Formas de Acessar o Agente Implantado

### 1. Interface Web (Com a flag `--with_ui`)

* Acesse a URL pública gerada diretamente no navegador: `https://weather-agent-xyz123.us-central1.run.app`

* Permite utilizar uma interface gráfica de chat interativa pronta para compartilhamento com a equipe ou usuários finais.



### 2. Requisições cURL (API REST)

```bash
SERVICE_URL="[https://weather-agent-xyz123.us-central1.run.app](https://weather-agent-xyz123.us-central1.run.app)"

curl -X POST $SERVICE_URL/api/query \
  -H "Content-Type: application/json" \
  -d '{"input": "Como está o tempo em Seattle?"}'

```

### 3. Integração via Python (`requests`)

```python
import requests

SERVICE_URL = "[https://weather-agent-xyz123.us-central1.run.app](https://weather-agent-xyz123.us-central1.run.app)"

response = requests.post(
    f"{SERVICE_URL}/api/query",
    json={"input": "Como está o tempo em Londres?"}
)

print(response.json())

```

---

## ⚠️ Ponto Crítico: Gestão do Estado da Sessão

> **Atenção:** Ao contrário do Agent Engine, o **Cloud Run NÃO configura o serviço de sessão automaticamente**.
> 
> 
> Para garantir a persistência das conversas em produção, você deve instanciar explicitamente o `VertexAiSessionService` dentro do seu agente:
> 
> 

```python
import os
from google.adk.sessions import VertexAiSessionService

session_service = VertexAiSessionService(
    project=os.environ.get('GOOGLE_CLOUD_PROJECT'),
    location=os.environ.get('GOOGLE_CLOUD_LOCATION')
)

```

---

## ⚖️ Resumo Comparativo Final

| Plataforma | Configuração do Servicio de Sessão | Quando Escolher |
| --- | --- | ---|
| **Vertex AI Agent Engine** | **Automático** (`VertexAiSessionService`) | Opção mais simples para agentes ADK padrão em Python.|
| **Cloud Run** | **Manual** (Requer código explícito) | Requer UI Web nativa (`--with_ui`), contêineres customizados ou multi-linguagem.
 |

> **Observação:** O código do agente do ADK é idêntico em ambas as plataformas. A escolha entre Agent Engine e Cloud Run muda apenas o comando de deploy e as opções de infraestrutura utilizadas.
> 
> 
---