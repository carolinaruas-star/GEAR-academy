# 🚀 Módulo 03 — Arquiteturas Multiagentes e Protocolo Agent2Agent (A2A)

[![Google Cloud - Deploy Multi-Agent Architectures](https://img.shields.io/badge/Google%20Cloud-Deploy%20Multi--Agent%20Architectures-4285F4?logo=googlecloud&logoColor=white)](./05-badge-conclusao.md)

---
*Desenvolvimento, orquestração distribuída com A2A, integração via MCP e implantação de ecossistemas multiagentes no Vertex AI Agent Engine.*

---

## 📌 Visão Geral do Módulo

Em aplicações corporativas complexas, utilizar um único agente e um prompt monolítico torna o sistema frágil e imprevisível[cite: 30]. Este módulo aborda a construção de **sistemas multiagentes modulares e distribuídos** com o **Agent Development Kit (ADK)**.

Ao longo do módulo, exploramos a orquestração através de árvores hierárquicas (agente pai → subagentes)[cite: 30], a comunicação entre agentes remotos via protocolo **Agent2Agent (A2A)**[cite: 31, 34], a integração de ferramentas via **Model Context Protocol (MCP)** e a resolução de desafios de engenharia (*Challenge Lab*) para colocar ecossistemas completos em produção no **Vertex AI Agent Engine** com interface gráfica web.

---

## 🎯 Objetivos de Aprendizagem

- 🌳 **Arquiteturas Hierárquicas:** Estruturar árvores de agentes para restringir rotas de conversa e delegar tarefas com precisão.
- 🌐 **Comunicação Distribuída (A2A):** Conectar agentes remotos hospedados em serviços/nuvens distintas utilizando o protocolo Agent2Agent, *Agent Cards* (`agent.json`) e a classe `RemoteA2aAgent`.
- 🛠️ **Integração de Ferramentas e Resolução de Erros:** Isolar subagentes e ferramentas de busca (RAG/Vertex AI Agent Search) utilizando **`AgentTool`** para evitar conflitos de sintaxe no LLM.
- 💾 **Persistência de Estado Avançada (`ToolContext`):** Armazenar e recuperar variáveis da sessão dinamicamente via ferramentas personalizadas e modelos de chaves `{ VARIABLE? }`.
- 🎯 **Challenge Lab de Produção:** Depurar, implementar e implantar em nuvem o *Paint Agent* da varejista fictícia Cymbal Shops no Vertex AI Agent Engine, integrando com um front-end Chainlit.

---

## 📂 Estrutura dos Arquivos

| Seção | Descrição / Foco Principal | Arquivos |
| :--- | :--- | :---: |
| **01 — Sistemas Multiagentes com ADK** | Hierarquias de agentes, `Session State` com `ToolContext` e agentes de fluxo (`Sequential`, `Loop`, `Parallel`)[cite: 30]. | [Acessar](./01-sistemas-multiagentes-com-adk_2.md) |
| **02 — Conexão de Agentes Remotos (A2A)** | Comunicação distribuída entre agentes via protocolo Agent2Agent, *Agent Cards* (`agent.json`) e `RemoteA2aAgent`[cite: 31]. | [Acessar](./02-conexao-agentes-remotos.md) |
| **03 — Ferramentas MCP com ADK** | *(Laboratório em Manutenção)* Integração de clientes e servidores Model Context Protocol[cite: 33, 34]. | *(Em Manutenção)* |
| **04 — Desafio de Implantação Multiagente** | Challenge Lab: depuração, resolução de conflitos de ferramentas com `AgentTool`, RAG e deploy no Agent Engine[cite: 32]. | [Acessar](./04-desafio-implantacao-multiagente.md) |
| **05 — Badge de Conclusão** | Registro da conquista da credencial oficial *Deploy Multi-Agent Architectures*[cite: 33]. | [Acessar](./05-badge-conclusao.md) |

---

## 🏗️ Protocolo Agent2Agent (A2A) vs. Subagentes Nativos

```text
 🏠 SUBAGENTES NATIVOS (Mesmo Processo)
 ┌────────────────────────────────────────────────────────┐
 │ root_agent (LlmAgent)                                  │
 │   └── sub_agents = [search_agent, calculator_agent]    │
 └────────────────────────────────────────────────────────┘

 ----------------------------------------------------------------------------------

 🌐 AGENTES REMOTOS A2A (Serviços Distribuídos)
 ┌─────────────────────────┐   HTTP / JSON-RPC 2.0   ┌─────────────────────────┐
 │ slide_content_agent     │ ──────────────────────> │ illustration-agent      │
 │ (Agente Local)          │ <────────────────────── │ (Cloud Run / A2A)       │
 │   └── RemoteA2aAgent    │   Agent Card (JSON)     │   └── A2aAgentExecutor  │
 └─────────────────────────┘                         └─────────────────────────┘

```

---

## 🛠️ Resolução do Bug de Ferramentas: O Padrão `AgentTool`

Ao combinar ferramentas convencionais com subagentes de pesquisa (Vertex AI Search / RAG), o ADK exige o isolamento do agente de busca através de um **`AgentTool`** no `root_agent` para evitar erros de validação no LLM:

```python
from google.adk.agents import LlmAgent
from google.adk.tools import AgentTool

# Encapsula o agente de busca para permitir coexistência com outras ferramentas
search_agent_tool = AgentTool(
    agent=search_agent,
    skip_summarization=False
)

# Configuração do agente principal
root_agent = LlmAgent(
    name="paint_agent",
    tools=[search_agent_tool, set_session_value]
)
```

---

## 🔗 Links e Recursos Recomendados

* [Documentação Oficial do ADK](https://google.github.io/adk-docs/)
* [Visão Geral do Protocolo Agent2Agent (A2A)](https://www.google.com/search?q=https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/a2a)
* [Vertex AI Agent Search & RAG Docs](https://www.google.com/search?q=https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/agent-search)

---

<div align="center">

## 👩‍💻 Autora

**Ana Carolina Pereira Ruas**  
Engenheira Florestal  
**Foco em Dados, Machine Learning, IA Generativa, LLMs, Agentes e Cloud**  

---
⭐ *Repositório desenvolvido como parte dos estudos da GEAR — Gemini Enterprise Agent Platform.*

</div>