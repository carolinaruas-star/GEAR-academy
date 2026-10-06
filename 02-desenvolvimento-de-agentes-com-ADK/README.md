# 🤖 Curso 2: Desenvolvimento de Agentes com o Kit de Desenvolvimento de Agente (ADK)

[![Google Cloud - ADK Agent Development](https://img.shields.io/badge/Google%20Cloud-ADK%20Agent%20Development-4285F4?logo=googlecloud&logoColor=white)](https://www.skills.google/)


*Guia completo de arquitetura, desenvolvimento, gerenciamento de estado, integração de ferramentas (MCP) e orquestração agêntica corporativa com o Google ADK.*

---

## 🎯 Sobre o Curso

O curso **"Desenvolvimento de Agentes com o Kit de Desenvolvimento de Agente (ADK)"** aborda a transição prática e arquitetural de modelos de linguagem isolados (*LLMs puros*) para **sistemas agênticos autônomos, determinísticos, extensíveis e prontos para produção**.

Utilizando o **Google Agent Development Kit (ADK)** em Python, este repositório consolida todo o ciclo de vida de um agente: desde a criação de projetos via CLI e refinamento de instruções, até o gerenciamento avançado de **memória/estado de sessão** e a extensão de capacidades usando **ferramentas nativas, servidores MCP (*Model Context Protocol*) e `FunctionTools` personalizadas**.

Toda a jornada está ancorada na equação fundamental do ADK:

$$\text{Agente} = \text{Modelo} + \text{Ferramentas} + \text{Orquestração}$$

---

## 🚀 Módulos do Curso

| Módulo | Título | Descrição / Foco Principal | Status |
| :---: | :--- | :--- | :---: |
| **01** | **Fundamentos do ADK** | Primeiros passos na criação de agentes de IA, estrutura do SDK, CLI (`adk create`, `adk web`) e inicialização de sessões interativas com `LlmAgent`. | ✅ Concluído |
| **02** | **Laboratório: Engenharia de Agentes** | Prática *hands-on* de configuração, solução de problemas de sintaxe e ambiente, e implantação de agentes no ecossistema local e em nuvem. | ✅ Concluído |
| **03** | **Otimização do Comportamento** | Engenharia de prompts para agentes, refinamento de instruções, controle de tom, papéis, restrições e técnicas de raciocínio lógico. | ✅ Concluído |
| **04** | **Gerenciamento de Memória e Estado** | Persistência contextual via `session.state`, injeção dinâmica de variáveis (`{var}`), captura de saídas (`output_key`) e escopos/namespaces (`temp:`, sessão, `user:`, `app:`). | ✅ Concluído |
| **05** | **Habilidades Agênticas com Ferramentas** | Extensão de capacidades com grounding na web (`google_search`), matemática precisa (`BuiltInCodeExecutor`), ferramentas de função e **Model Context Protocol (MCP)**. | ✅ Concluído |
| **06** | **Laboratório: Ferramentas de Moeda via MCP** | Prática de integração de um servidor MCP em Python/FastMCP para consultar cotações de criptomoedas em tempo real via API pública da Coinbase. | ✅ Concluído |
| **07** | **Conclusão Geral do Curso** | Síntese e consolidação de toda a arquitetura de orquestração agêntica para cenários corporativos reais na Google Cloud. | ✅ Concluído |

---

## 📐 Arquitetura e Conceitos-Chave

### 🧠 1. Modelo vs. Ferramenta vs. Orquestração
- **Modelo (LLM):** Atua como o motor de raciocínio, responsável por interpretar intenções, analisar contextos e tomar decisões sobre qual ação tomar.
- **Ferramentas (Tools):** Executam ações determinísticas no mundo real (consultas a bancos de dados, chamadas de API, execução de código Python e pesquisas na web).
- **Orquestração:** O runtime do ADK gerencia o loop de raciocínio-ação-observação, mantendo o controle da sessão e encadeando múltiplos agentes ou ferramentas.

### 💾 2. Histórico da Conversa vs. Estado da Sessão (`session.state`)
- **Histórico:** Fornece contexto textual corrido para a janela de contexto do LLM.
- **Session State:** Funciona como um dicionário de dados estruturado acessível e manipulável via código Python e injeção de variáveis (`{var}`).

```text
💬 HISTÓRICO DA CONVERSA                  🧠 ESTADO DA SESSÃO
 (Texto Livre / Contexto)                 (Dados Estruturados / Código)
┌─────────────────────────┐              ┌─────────────────────────────┐
│ Usuário: "Meu nome é    │              │ session.state = {           │
│           Alex"         │ ───────────> │   "user_name": "Alex",      │
│ Agente:  "Prazer Alex!" │              │   "user_language": "pt-BR", │
└─────────────────────────┘              │   "user:theme": "dark"      │
                                         │ }                           │
                                         └─────────────────────────────┘
```

### 🔌 3. Ecossistema do Model Context Protocol (MCP)
O **MCP** padroniza a comunicação entre o agente e servidores de ferramentas externos, eliminando a necessidade de código de integração proprietário:

```text
                                  🔌 PROTOCOLO MCP
                                         │
        ┌────────────────────────────────┼────────────────────────────────┐
        ▼                                ▼                                ▼
 📁 Filesystem Server            🐙 GitHub Server                🗄️ Database Server
 (Leitura e Escrita Local)       (Issues, PRs e Commits)         (PostgreSQL, Spanner, BigQuery)
```

---

## 🛠️ Tecnologias Utilizadas

- **Linguagem Principal:** Python 3.10+
- **Framework de Agentes:** Google Agent Development Kit (ADK)
- **Modelos de Linguagem:** Gemini 2.5 Flash / Gemini Enterprise
- **Ambiente & Ferramentas:** CLI do ADK (`adk`), FastMCP, `uv`, `httpx`
- **Nuvem & Infraestrutura:** Google Cloud Platform (GCP) / Google Cloud Skills Boost

---

## 📂 Estrutura do Repositório

```text
desenvolvimento-de-agentes-com-adk/
├── 01-primeiros-passos-na-criacao-de-agentes-com-o-adk/
├── 02-laboratorio-engenharia-de-agentes-de-ia-com-o-adk/
├── 03-otimizacao-do-comportamento-de-agentes/
├── 04-gerenciamento-de-memoria-e-estado-de-agentes/
├── 05-inclusao-de-habilidades-agenticas-com-ferramentas/
├── 06-laboratorio-adicionar-ferramentas-de-moeda-a-um-agente-usando-o-mcp/
├── 07-conclusao-do-curso/
└── README.md
```

---

<div align="center">

## 👩‍💻 Autora

**Ana Carolina Pereira Ruas**  
Engenheira Florestal  
**Foco em Dados, Machine Learning, IA Generativa, LLMs, Agentes e Cloud**  

---
⭐ *Repositório desenvolvido como parte dos estudos da GEAR — Gemini Enterprise Agent Platform.*

</div>
