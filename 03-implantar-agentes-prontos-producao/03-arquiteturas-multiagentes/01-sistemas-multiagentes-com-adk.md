# 01. Criar Sistemas Multiagentes com o ADK (GENAI106)

## 📌 Visão Geral
Este laboratório aborda a orquestração de sistemas multiagentes sofisticados utilizando o **Agent Development Kit (ADK)** do Google Cloud[cite: 1]. Através da divisão de tarefas entre agentes especializados e do uso de fluxos de trabalho estruturados, é possível atingir maior confiabilidade, modularidade e facilidade de manutenção em relação a prompts únicos e complexos.

---

## 🎯 Objetivos do Laboratório
* **Hierarquias Agente Pai → Subagente:** Estruturar árvores hierárquicas para transferências de controle diretas e previsíveis.
* **Gerenciamento de Estado da Sessão (`Session State`):** Armazenar e recuperar informações entre múltiplos turnos e agentes via `ToolContext` e interpolação `{ chave? }`.
* **Agentes de Fluxo de Trabalho (Workflow Agents):** Utilizar `SequentialAgent`, `LoopAgent` e `ParallelAgent` para orquestração automática sem intervenção humana.

---

## 🏗️ Conceito: A Árvore Hierárquica de Agentes

No ADK, toda conversa se inicia no `root_agent`. Os agentes são organizados em estruturas em árvore para restringir as rotas possíveis e facilitar a delegação:

* **Subagentes:** Definidos ao passar a lista `sub_agents=[...]` na criação do agente pai.
* **Transferências Nativas:** O agente pai analisa a descrição (`description`) dos subagentes ou segue orientações explícitas de suas instruções (`instruction`) para rotear o usuário.
* **Comunicação entre Pares:** Subagentes do mesmo nível podem transferir a conversa entre si por padrão (a menos que `disallow_transfer_to_peers=True` seja ativado).

---

## 💾 Armazenamento e Recuperação de Estado (`Session State`)

A `Session` mantém o histórico e o dicionário de estado acessível por todos os agentes.

### 1. Escrita de Estado via Ferramenta Customizada
```python
def save_attractions_to_state(
    tool_context: ToolContext,
    attractions: List[str]) -> dict[str, str]:
    """Salva atrações no dicionário de estado da sessão."""
    existing_attractions = tool_context.state.get("attractions", [])
    tool_context.state["attractions"] = existing_attractions + attractions
    return {"status": "success"}