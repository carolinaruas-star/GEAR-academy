# 🤖 Módulo 2 — Engenharia de Agentes de IA com ADK (Laboratório com Desafio)

[![Google Cloud - Engineer AI Agents with ADK](https://img.shields.io/badge/Google%20Cloud-Engineer%20AI%20Agents-4285F4?logo=googlecloud&logoColor=white)](./02-badge-conclusao.md)

Este módulo consolida o aprendizado prático por meio de um **laboratório com desafio (GSP540)** no cenário fictício da *Cymbal Travel*. Ele aborda a construção, correção e orquestração avançada de agentes de IA utilizando o **Google Agent Development Kit (ADK)**, incluindo integração com ferramentas de pesquisa na web, respostas estruturadas com Pydantic e pipelines multiagentes sequenciais[cite: 22].

---

## 🎯 Objetivos do Módulo

- 🔎 **Pesquisa Externa:** Integrar o agente `my_google_search_agent` à ferramenta **Google Search Tool** para consultas web em tempo real[cite: 22].
- 📋 **Saídas Estruturadas:** Implementar validação de esquemas JSON no agente `geo_validator` utilizando modelos **Pydantic**[cite: 22].
- 🔄 **Orquestração Multiagente:** Corrigir e executar o pipeline sequencial `llm_auditor` (*Agente Crítico ➔ Agente Revisor*)[cite: 22].
- 🧪 **Execução Multi-interface:** Testar e validar o comportamento dos agentes via **ADK Web**, **ADK CLI** e scripts de execução programática[cite: 22].

---

## 📚 Conteúdo do Módulo

| Seção | Descrição / Foco Principal | Arquivo |
| :--- | :--- | :---: |
| **01 — Laboratório com Desafio** | Resolução dos desafios práticos com o cenário Cymbal Travel (GSP540). | [Acessar](./01-laboratório-com-desafio.md) |
| **02 — Badge de Conclusão** | Registro da conquista da Skill Badge oficial no Google Cloud. | [Acessar](./02-badge-conclusao.md) |

---

## 🛠️ 1. Desafios Práticos do Laboratório

```text
 ┌────────────────────────┐      ┌────────────────────────┐      ┌────────────────────────┐
 │ 1. Buscador de Viagens │ ───> │ 2. Verificador Geográfico│ ───>│ 3. Auditor de Conteúdo │
 │ (Google Search Tool)   │      │ (Pydantic / Structured)│      │ (Pipeline Sequencial)  │
 └────────────────────────┘      └────────────────────────┘      └────────────────────────┘

```

### 🔍 1. Buscador de Viagens (`my_google_search_agent`)

Habilitação da ferramenta `Google Search` para consulta de dados em tempo real na web, fundamentando as respostas do agente em fontes atualizadas.

### 📋 2. Verificador de Destino (`geo_validator`)

Garantia de **Structured Output** utilizando **Pydantic / JSON Schema**, forçando o modelo Gemini a retornar respostas padronizadas e validadas programaticamente.

### 🔄 3. Pipeline Auditor de Conteúdo (`llm_auditor`)

Restauração da arquitetura **Sequential Agents** para auditoria de materiais de marketing:

```text
  Solicitação ──> [ Agente Crítico ] ──> [ Agente Revisor ] ──> Saída Corrigida

```

---

## ⚙️ 2. Tecnologias e Conceitos Aplicados

* **ADK & Agent Platform:** Gestão de ciclo de vida e orquestração de agentes.


* **Google Search Tool:** Conexão do LLM com mecanismos de busca.


* **Pydantic & JSON Schema:** Tipagem forte e estruturação de dados de saída.


* **Sequential Workflows:** Encadeamento ordenado de agentes especializados.


* **Interfaces ADK:** Execução por terminal (`adk run`), navegador (`adk web`) e código Python.



---

## 🗂️ Estrutura da Pasta

```text
02-laboratorio-desafio-adk/
├── README.md
├── 01-laboratório-com-desafio.md
└── 02-badge-conclusao.md
```

<div align="center">

## 👩‍💻 Autora

**Ana Carolina Pereira Ruas**  
Engenheira Florestal  
**Foco em Dados, Machine Learning, IA Generativa, LLMs, Agentes e Cloud**  

---
⭐ *Repositório desenvolvido como parte dos estudos da GEAR — Gemini Enterprise Agent Platform.*

</div>