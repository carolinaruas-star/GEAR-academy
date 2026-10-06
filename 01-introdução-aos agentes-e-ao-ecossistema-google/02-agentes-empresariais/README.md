# 🤖 Módulo 2 — Agentes Empresariais e Ecossistema Google

[![Google Cloud - Enterprise Agents and Use Cases](https://img.shields.io/badge/Google%20Cloud-Enterprise%20Agents-4285F4?logo=googlecloud&logoColor=white)](./05-badge-conclusao.md)

Este módulo apresenta como os **Agentes de IA são aplicados no contexto corporativo** para gerar resultados de negócio mensuráveis e como o ecossistema **Google Cloud (Gemini Enterprise, ADK e Agent Platform)** oferece a infraestrutura necessária para criar, implantar, governar e otimizar essas soluções.

---

## 🎯 Objetivo do Módulo

Compreender a aplicação prática de agentes em empresas, conectando **problemas de negócio a KPIs mensuráveis** e identificando a plataforma de desenvolvimento ideal (desde abordagens *no-code* até *code-first*).

---

## 📚 Conteúdo do Módulo

| Seção | Foco Principal | Arquivo |
| :--- | :--- | :---: |
| **01 — Casos de Uso Corporativo** | As 6 categorias de agentes de negócios, valor empresarial e KPIs. | [Acessar](./01-casos-de-uso-corporativo.md) |
| **02 — Desenvolvimento Google Cloud** | Abordagens no-code, low-code e code-first (ADK e Agent Platform). | [Acessar](./02-desenvolvimento-com-google-cloud.md) |
| **03 — Gemini Enterprise** | Hub central que conecta pessoas, agentes, dados e sistemas da empresa. | [Acessar](./03-gemini-enterprise.md) |
| **04 — Simulação Prática** | Prática com pesquisa avançada, NotebookLM, Deep Research e estúdio. | [Acessar](./04-simulacao-pratica.md) |
| **05 — Badge / Certificado** | Registro da conquista do selo *Enterprise Agents and Use Cases*. | [Acessar](./05-badge-conclusao.md) |

---

## 🏢 1. As 6 Categorias de Agentes Empresariais

```text
  Problema de Negócio  ──>  Agente de IA  ──>  Ação em Sistema  ──>  KPI  ──>  Impacto Financeiro/Operacional

```

| Categoria | Foco e Aplicação |
| --- | --- |
| 👥 **Atendimento ao Cliente** | Suporte autônomo, resolução de chamados e personalização da experiência. |
| ⚡ **Produtividade Interna** | Auxílio aos colaboradores em processos internos e buscas corporativas. |
| 🎨 **Criação** | Apoio na geração, adaptação e produção de conteúdo corporativo. |
| 💻 **Código** | Assistência no desenvolvimento, refatoração, análise e manutenção de código. |
| 📊 **Dados** | Análise preditiva, identificação de anomalias e geração automatizada de relatórios. |
| 🔐 **Segurança** | Investigação automática de alertas, triagem de ameaças e resposta a incidentes. |

---

## ☁️ 2. Ecossistema Google Cloud para Agentes

O Google Cloud oferece uma abordagem multicamada. A regra prática de escolha é: **quanto maior a necessidade de personalização e controle, maior o uso de código.**

```text
  [ No-Code / Pronto ]          [ Low-Code / Assistido ]             [ Code-First / Profissional ]
  Gemini Enterprise        ➔    Conversational Agents / CX    ➔     Agent Development Kit (ADK)
  (Produtividade)               (Chatbot / Voz)                     (Sistemas Multiagentes em Código)

```

### 🏗️ Gemini Enterprise Agent Platform

Plataforma completa para cobrir o ciclo de vida dos agentes:

* **ADK:** Framework aberto para orquestração e código.
* **Agent Garden:** Biblioteca de conectores, ferramentas e modelos.
* **Agent Runtime:** Ambiente gerenciado (sessões, memória persistente, execução).
* **Governança e Observabilidade:** Rastreamento, segurança e métricas de qualidade.

---

## 🧩 3. Gemini Enterprise como Hub Inteligente

O Gemini Enterprise atua como a camada central de interação corporativa:

```text
                  ┌──────────────────────────────┐
                  │       Gemini Enterprise      │
                  └──────────────┬───────────────┘
                                 │
         ┌───────────────────────┼───────────────────────┐
         ▼                       ▼                       ▼
┌──────────────────┐   ┌──────────────────┐   ┌──────────────────┐
│ Agentes Google   │   │ Agentes No-Code  │   │ Agentes Terceiros│
│ (Deep Research,  │   │ (Personalizados  │   │ (Salesforce,     │
│  NotebookLM)     │   │  pela empresa)   │   │  Jira, Copilot)  │
└──────────────────┘   └──────────────────┘   └──────────────────┘

```

---

## 🔑 Principais Aprendizados

1. **A IA precisa estar atrelada a KPIs:** Não se cria um agente apenas pela tecnologia, mas sim para resolver gargalos com impacto mensurável.


2. **Autonomia proporcional ao esforço:** Soluções em código (ADK) trazem flexibilidade total, mas exigem maior controle de engenharia.


3. **Centralização de Dados:** O verdadeiro diferencial do Gemini Enterprise é unificar o conhecimento da empresa mantendo os controles de permissão existentes.



---

## 🗂️ Estrutura da Pasta

```text
02-agentes-empresariais/
├── README.md
├── 01-casos-de-uso-corporativo.md
├── 02-desenvolvimento-com-google-cloud.md
├── 03-gemini-enterprise.md
├── 04-simulacao-pratica.md
└── 05-badge-conclusao.md

```
<div align="center">

## 👩‍💻 Autora

**Ana Carolina Pereira Ruas**  
Engenheira Florestal  
**Foco em Dados, Machine Learning, IA Generativa, LLMs, Agentes e Cloud**  

---
⭐ *Repositório desenvolvido como parte dos estudos da GEAR — Gemini Enterprise Agent Platform.*

</div>