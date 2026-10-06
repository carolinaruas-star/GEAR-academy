# 🤖 Módulo 1 — Primeiros Passos na Criação de Agentes com o ADK

[![Google Cloud - ADK Fundamentals](https://img.shields.io/badge/Google%20Cloud-ADK%20Fundamentals-4285F4?logo=googlecloud&logoColor=white)](./07-badge-conclusao.md)

Este módulo aborda a prática de desenvolvimento e configuração de **Agentes de IA** utilizando o **Google Agent Development Kit (ADK)**. Ele cobre desde a preparação do ambiente virtual Python e variáveis de ambiente até a definição de identidades de agentes e múltiplos métodos de execução (*Web, Terminal, API e Programático*).

---

## 🎯 Objetivos do Módulo

- ⚙️ **Configuração de Ambiente:** Instalar o `google-adk`, configurar o ambiente virtual Python 3.11+ e gerenciar chaves de API (Google AI Studio / Vertex AI).
- 🏷️ **Identidade do Agente:** Dominar os 4 parâmetros essenciais: `model`, `name`, `description` e `instruction`.
- 🚀 **Métodos de Execução:** Saber quando e como utilizar `adk web`, `adk run`, `adk api_server` e execução programática assíncrona.
- 📄 **YAML vs. Python:** Comparar o uso do **Agent Config (`root_agent.yaml`)** para prototipagem rápida com a flexibilidade de desenvolvimento em código Python (`agent.py`).

---

## 📚 Conteúdo do Módulo

| Seção | Descrição / Foco Principal | Arquivo |
| :--- | :--- | :---: |
| **01 — Configuração do Ambiente** | Pré-requisitos, ambiente virtual e instalação do pacote `google-adk`. | [Acessar](./01-configuracao-ambiente.md) |
| **02 — Identidade do Agente** | Os 4 parâmetros (`model`, `name`, `description`, `instruction`) e o `root_agent`. | [Acessar](./02-identidade-agente.md) |
| **03 — Exercício Prático** | Personalização de um tutor de matemática e testes via interface. | [Acessar](./03-exercicio-pratico-transforme-seu-agente.md) |
| **04 — Métodos de Execução** | Execução via Web CLI, Terminal, API REST e scripts assíncronos. | [Acessar](./04-metodos-de-implantacao.md) |
| **05 — Formas de Definição** | Comparativo detalhado entre definição via **Código Python** e **YAML**. | [Acessar](./05-maneiras-definir-agentes.md) |
| **06 — Conclusão** | Síntese do fluxo de desenvolvimento e guia rápido de comandos. | [Acessar](./06-conclusao.md) |
| **07 — Badge / Certificado** | Registro de conclusão do selo oficial do Google Cloud. | [Acessar](./07-badge-conclusao.md) |

---

## 🧠 1. Os 4 Parâmetros Fundamentais do Agente

Todo agente construído no ADK baseia-se em quatro pilares principais:

```text
               🤖 AGENTE ADK
                  │
     ┌────────────┼────────────┬────────────┐
     ▼            ▼            ▼            ▼
  🧠 model     🏷️ name      📝 descr     📋 instruct
 (LLM/Cérebro) (ID Interno)  (O que faz?) (Como age?)

```

| Parâmetro | Função | Exemplo |
| --- | --- | --- |
| `model` | Define o LLM de raciocínio. | `gemini-2.5-flash` |
| `name` | Identificador interno e de roteamento multiagente. | `math_tutor_agent` |
| `description` | Explica a finalidade para outros agentes (Multiagente). | *"Ajuda estudantes com álgebra."* |
| `instruction` | Prompt do sistema orientando postura e regras do agente. | *"Você é um orientador paciente..."* |

> ⚠️ **Convenção ADK:** A variável de entrada principal do projeto sempre deve se chamar `root_agent`.

---

## 🚀 2. Matriz de Métodos de Execução

O mesmo arquivo `agent.py` pode ser executado e consumido de 4 formas diferentes:

```text
                  ┌────────────────────────┐
                  │        agent.py        │
                  └───────────┬────────────┘
                              │
     ┌────────────────────────┼────────────────────────┐
     ▼                        ▼                        ▼
🌐 adk web                🖥️ adk run              🔗 adk api_server
(Interface Web para       (Interação direta       (Exposição como API
 desenvolvimento e debug)  pelo terminal)          REST para integrações)
     │
     └───────────────► 🐍 Execução Programática
                       (Python assíncrono via Runner e Sessions)

```

---

## 📄 3. Python (`agent.py`) vs. YAML (`root_agent.yaml`)

```text
📄 YAML   ➔ Ideal para simplicidade, prototipagem rápida e não-programadores.
🐍 PYTHON ➔ Essencial para lógica avançada, ferramentas customizadas, callbacks e multiagentes.

```

### Exemplo Lado a Lado:

**Python (`agent.py`)**

```python
from google.adk.agents.llm_agent import Agent

root_agent = Agent(
    model='gemini-2.5-flash',
    name='math_tutor_agent',
    description='Ajuda estudantes a aprender álgebra',
    instruction='Você é um orientador de matemática paciente.'
)

```

**YAML (`root_agent.yaml`)**

```yaml
name: math_tutor_agent
model: gemini-2.5-flash
description: Ajuda estudantes a aprender álgebra
instruction: |
  Você é um orientador de matemática paciente.

```

---

## 🗂️ Estrutura da Pasta

```text
01-primeiros-passos-adk/
├── README.md
├── 01-configuracao-ambiente.md
├── 02-identidade-agente.md
├── 03-exercicio-pratico-transforme-seu-agente.md
├── 04-metodos-de-implantacao.md
├── 05-maneiras-definir-agentes.md
├── 06-conclusao.md
└── 07-badge-conclusao.md
```

<div align="center">

## 👩‍💻 Autora

**Ana Carolina Pereira Ruas**  
Engenheira Florestal  
**Foco em Dados, Machine Learning, IA Generativa, LLMs, Agentes e Cloud**  

---
⭐ *Repositório desenvolvido como parte dos estudos da GEAR — Gemini Enterprise Agent Platform.*

</div>