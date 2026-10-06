# 04. Laboratório com Desafio: Implantação de um Agente com o ADK (GENAI129)

## 📌 Visão Geral
Este laboratório de desafio prático (*Challenge Lab*) consolida as habilidades avançadas na construção, depuração, gerenciamento de estado e deploy de ecossistemas multiagente no **Vertex AI Agent Engine** (Agent Runtime), além de sua integração a uma interface de usuário externa (*Chainlit*).

No cenário do desafio, assume-se a engenharia de ML da empresa varejista fictícia **Cymbal Shops** para depurar e colocar em produção o **Paint Agent** (Agente de Pintura) — um sistema que auxilia clientes na escolha de tintas, cálculo de cobertura de área por cômodo e orçamento.

---

## 🎯 Objetivos Validados

1. **Agent Search / RAG:** Criação de app de pesquisa no Vertex AI Agent Search e indexação de fichas técnicas em PDF do Cloud Storage (`Cymbal_Shops_Paint_Datasheets.pdf`).
2. **Depuração de Conflitos de Ferramentas:** Resolução do erro `400 INVALID_ARGUMENT` ao combinar ferramentas de busca com outras ferramentas Python via **`AgentTool`**.
3. **Persistência de Estado Personalizada (`ToolContext`):** Atualização da ferramenta `set_session_value` e carregamento de modelos de chaves no dicionário de estado (`{ SELECTED_PAINT? }` e `{ COVERAGE_RATE? }`).
4. **Deploy no Agent Engine (Agent Runtime):** Implantação serverless em nuvem via CLI `adk deploy agent_engine`.
5. **Integração com Front-end Web (Chainlit):** Conexão da UI remota ao recurso ativo no Agent Engine via SDK.

---

## 🔧 Pontos Críticos de Engenharia e Resolução de Bugs

### 1. Resolução do Erro de Múltiplas Ferramentas (Bug no `root_agent`)
O ADK não permite misturar ferramentas de busca (`VertexAiSearchTool`) com ferramentas convencionais no mesmo agente direto. Para resolver:

* **Estratégia:** Isola-se o subagente de busca (`search_agent`) encapsulando-o com um **`AgentTool`** no `root_agent`:
```python
from google.adk.tools import AgentTool

# Encapsula o agente de busca para permitir convivência com outras ferramentas
search_agent_tool = AgentTool(
    agent=search_agent,
    skip_summarization=False
)

# Atualização no root_agent
root_agent = LlmAgent(
    name="paint_agent",
    tools=[search_agent_tool, set_session_value],
    # O subagente de busca é removido de sub_agents ao virar AgentTool
)
```

### 2. Implementação do `ToolContext.state`
A ferramenta personalizada `set_session_value` armazena dados de forma dinâmica na sessão do usuário:

```python
def set_session_value(tool_context: ToolContext, key: str, value: str) -> str:
    """Atualiza o dicionário de estado da sessão com pares chave-valor."""
    tool_context.state[key] = value
    return f"stored '{value}' in '{key}'"
```

 Nas instruções dos agentes downstream (como o `coverage_calculator_agent`), os valores são recuperados via modelo de chave opcional:
```python
instruction="""
Calcule a quantidade necessária de tinta considerando o produto { SELECTED_PAINT? }
e a taxa de cobertura { COVERAGE_RATE? }.
"""
```

---

## 💻 Comandos e Fluxo de Implantação

### 1. Execução e Testes Locais
```bash
# Execução no terminal para validação de lógica
adk run paint_agent

# Interface Web para teste de fluxo e validação do dicionário de estado
adk web --allow_origins "regex:https://.*\.cloudshell\.dev"
```

### 2. Deploy no Agent Engine
```bash
cd ~/adk_challenge_lab

adk deploy agent_engine \
  --display_name "Paint Agent" \
  .
```

### 3. Integração no Front-end (Chainlit App)
No arquivo `chainlit_ui/app.py`, conecta-se o cliente ao nome do recurso gerado no deploy:

```python
agent = client.agent_engines.get(name='projects/PROJECT_ID/locations/us-central1/reasoningEngines/RESOURCE_ID')
```

```bash
# Inicialização da interface interativa
cd ~/adk_challenge_lab/chainlit_ui
chainlit run app.py
```

---

## 🏗️ Arquitetura do Sistema Final

```text
[ Front-end / Chainlit UI ]
            │
            ▼ (SDK Agent Engine)
[ Paint Agent (root_agent) ]
    ├── AgentTool ──> [ search_agent ] ──> Vertex AI Search (RAG nos PDFs de tintas)
    ├── Tool ───────> [ set_session_value ] ──> Grava 'SELECTED_PAINT', 'COVERAGE_RATE' no State
    └── sub_agents
          └── [ room_planner ]
                └── [ coverage_calculator_agent ] ──> Lê { SELECTED_PAINT? } do State
```
```