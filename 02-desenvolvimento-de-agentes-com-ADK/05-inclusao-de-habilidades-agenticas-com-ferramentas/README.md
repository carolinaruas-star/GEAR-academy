# 🔧 Módulo 5 — Inclusão de Habilidades Agênticas com Ferramentas

[![Google Cloud - Add Agent Capabilities with Tools](https://img.shields.io/badge/Google%20Cloud-Add%20Capabilities%20with%20Tools-4285F4?logo=googlecloud&logoColor=white)](./12-badge-conclusao.md)

Este módulo aborda como utilizar **ferramentas (tools)** para ampliar as capacidades dos agentes de IA no **Google Agent Development Kit (ADK)**, permitindo que eles superem as limitações dos dados congelados do LLM e possam **consultar dados em tempo real, realizar cálculos exatos, interagir com APIs e executar ações no mundo real**.

Com o apoio do **Model Context Protocol (MCP)** e de **ferramentas de função personalizadas**, completamos a equação fundamental do ADK:

$$\text{Agente} = \text{Modelo} + \text{Ferramentas} + \text{Orquestração}$$

---

## 🎯 Objetivos do Módulo

- 🛠️ **Superar Limitações de LLMs:** Equipar agentes com capacidade de execução determinística, pesquisa em tempo real e acesso a sistemas proprietários.
- 🧰 **Dominar Ferramentas Integradas:** Implementar `google_search` para embasamento de dados e `BuiltInCodeExecutor` para processamento matemático preciso.
- 🔗 **Conectar ao Ecossistema MCP:** Utilizar o *Model Context Protocol* via `McpToolset` (`StdioConnectionParams` e `SseConnectionParams`) para integrar servidores externos com `tool_filter` seguro.
- ⚙️ **Desenvolver Function Tools Personalizadas:** Criar funções Python com type hints, docstrings detalhadas e dicionários estruturados com a chave `status` para inspeção automática do ADK.
- 🧠 **Design de Instruções Estratégicas:** Projetar prompts que definem sequenciamento de chamadas, regras de seleção, tratamento diferenciado de erros e suporte a `AgentTool` para delegação especializada.

---

## 📚 Conteúdo do Módulo

| Seção | Descrição / Foco Principal | Arquivos |
| :--- | :--- | :---: |
| **01 — Fundamentos de Ferramentas** | Por que LLMs puros falham em dados em tempo real, cálculos e ações, e como ferramentas estendem suas capacidades. | [Problema](./01-ferramentas-problema.md) / [Solução](./02-ferramentas-solucao.md) |
| **02 — Ferramentas Integradas** | Uso de `google_search` para grounding na web e `BuiltInCodeExecutor` para execução de Python em sandbox. | [Problema](./03-ferramentas-integradas-problema.md) / [Solução](./04-ferramentas-integradas-solucao.md) |
| **03 — Model Context Protocol (MCP)** | Conexão de agentes a servidores externos padronizados via `McpToolset` e aplicação de `tool_filter`. | [Problema](./05-mcp-problema.md) / [Solução](./06-mcp-solucao.md) |
| **04 — Function Tools Personalizadas** | Transformação de funções Python com type hints e docstrings em ferramentas agênticas de negócio. | [Problema](./07-function-tools-problema.md) / [Solução](./08-function-tools-solucao.md) |
| **05 — Instruções Estratégicas** | Design de prompts para orientar fluxos sequenciais, tratamento de exceções e uso do padrão `AgentTool`. | [Problema](./09-instrucoes-problema.md) / [Solução](./10-instrucoes-solucao.md) |
| **06 — Conclusão do Módulo** | Síntese sobre a orquestração de ferramentas, boas práticas e mapas de decisão. | [Acessar](./11-conclusao.md) |
| **07 — Badge de Conclusão** | Registro da conquista da credencial oficial *Add Agent Capabilities with Tools*. | [Acessar](./12-badge-conclusao.md) |

---

## ⚙️ A Escolha Certa da Ferramenta

```text
                        ❓ Qual ferramenta utilizar?
                                     │
           ┌─────────────────────────┼─────────────────────────┐
           ▼                         ▼                         ▼
   🔧 FERRAMENTAS INTEGRADAS    🔗 SERVIDORES MCP         🛠️ FUNCTION TOOLS
   (Pesquisa & Código)          (Ecossistema Existente)   (Lógica de Negócio)
           │                         │                         │
           ├─ google_search          ├─ Filesystem, Slack      ├─ Banco de Dados Interno
           └─ Code Execution         └─ GitHub, PostgreSQL     └─ Cálculos de Frete/Regras

```

---

## ⚖️ Comparativo de Abordagens

| Tipo de Ferramenta | Mantenedor | Configuração | Casos de Uso Recomendados |
| --- | --- | --- | --- |
| **🔧 Integradas (`tools` / `code_executor`)** | Equipe do ADK | Importar e declarar | Pesquisa Google em tempo real e execução de código Python.|
| **🔗 MCP (`McpToolset`)** | Comunidade / Fornecedores | `Stdio` / `SseConnection` | Conexão com sistemas de arquivos, GitHub, Slack e bancos de dados.|
| **⚙️ Função Personalizada (`FunctionTool`)** | Desenvolvedor | Função Python + Metadados | Regras de negócio proprietárias, chamadas de APIs privadas e consultas internas.|
| **🤖 Agente como Ferramenta (`AgentTool`)** | Desenvolvedor | Encapsulamento de `LlmAgent` | Delegação de subtarefas complexas que exigem raciocínio especializado.|

---

## 🗂️ Estrutura da Pasta

```text
05-inclusao-de-habilidades-agenticas-com-ferramentas/
├── README.md
├── 01-ferramentas-problema.md
├── 02-ferramentas-solucao.md
├── 03-ferramentas-integradas-problema.md
├── 04-ferramentas-integradas-solucao.md
├── 05-mcp-problema.md
├── 06-mcp-solucao.md
├── 07-function-tools-problema.md
├── 08-function-tools-solucao.md
├── 09-instrucoes-problema.md
├── 10-instrucoes-solucao.md
├── 11-conclusao.md
└── 12-badge-conclusao.md
```
<div align="center">

## 👩‍💻 Autora

**Ana Carolina Pereira Ruas**  
Engenheira Florestal  
**Foco em Dados, Machine Learning, IA Generativa, LLMs, Agentes e Cloud**  

---
⭐ *Repositório desenvolvido como parte dos estudos da GEAR — Gemini Enterprise Agent Platform.*
</div>