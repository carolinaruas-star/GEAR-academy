# 🤖 Curso 1: Introdução aos Agentes e ao Ecossistema de Agentes do Google

[![Google Cloud - Agent Fundamentals](https://img.shields.io/badge/Google%20Cloud-Agent%20Fundamentals-4285F4?logo=googlecloud&logoColor=white)](./01-fundamentos-de-agentes/06-badge-conclusao.md)[![Google Cloud - Enterprise Agents](https://img.shields.io/badge/Enterprise%20Agents-34A853?logo=googlecloud&logoColor=white)](./02-agentes-empresariais/05-badge-conclusao.md)

---
*Guia completo dos princípios fundamentais de agentes de IA, ecossistema do Google ADK e construção de primeiros assistentes inteligentes.*

---

Este repositório reúne meus estudos e anotações do programa **GEAR — Gemini Enterprise Agent Platform**, cobrindo desde os conceitos fundamentais de **Agentes de IA** até a sua aplicação prática no ambiente corporativo utilizando o ecossistema do **Google Cloud**.

O conteúdo acompanha a evolução tecnológica dos modelos de linguagem: **da geração passiva de texto (LLM) para a execução autônoma de tarefas orientadas a objetivos (Agentes)**.

---

## 🎯 Objetivos de Aprendizado

- 🧠 **Fundamentos Agênticos:** Entender a arquitetura `Modelo + Ferramentas + Orquestração` e o ciclo contínuo `Observar → Interpretar → Planejar → Agir → Verificar`.
- 🏢 **Casos de Uso Empresariais:** Conectar o desenvolvimento de agentes a KPIs de negócio (produtividade, custo, qualidade e velocidade) nas 6 grandes categorias corporativas.
- ⚙️ **Matriz de Decisão:** Saber diferir quando usar automações tradicionais/APIs (*determinísticas*), chamadas de função (*assistidas*) ou agentes autônomos (*dinâmicos/complexos*).
- ☁️ **Ecossistema Google Cloud:** Explorar as plataformas e ferramentas da Google (Gemini Enterprise, ADK, Conversational Agents, NotebookLM e Agent Runtime).

---

## 📚 Módulos do Curso

### 📁 Módulo 1 — Fundamentos de Agentes de IA
Apresenta a base teórica e conceitual dos agentes, sua arquitetura central e critérios de quando aplicar ou evitar essa tecnologia.

| Seção | Tópico Principal | Link |
| :--- | :--- | :---: |
| **01 — Introdução a Agentes** | O que são agentes, capacidades e sistemas multiagentes. | [Acessar](./01-fundamentos-de-agentes/01-introducao-a-agentes.md) |
| **02 — Abstração de Agentes** | Evolução: `LLM` ➔ `Function Calling` ➔ `Agente Autônomo`. | [Acessar](./01-fundamentos-de-agentes/02-abstracao-de-agentes.md) |
| **03 — Como Agentes Funcionam** | Detalhamento dos 3 pilares: **Modelo, Ferramentas e Orquestração**. | [Acessar](./01-fundamentos-de-agentes/03-como-os-agentes-funcionam.md) |
| **04 — Agentes em Ação** | Quando usar ou não usar agentes e introdução ao Google Cloud. | [Acessar](./01-fundamentos-de-agentes/04-agentes-em-acao.md) |
| **05 — Conclusão** | Modelos mentais essenciais para arquitetura de software agêntico. | [Acessar](./01-fundamentos-de-agentes/05-conclusao.md) |
| **06 — Badge / Certificado** | Conquista do selo *Google Cloud — Agent Fundamentals*. | [Acessar](./01-fundamentos-de-agentes/06-badge-conclusao.md) |

---

### 📁 Módulo 2 — Agentes Empresariais e Ecossistema Google
Aprofunda na aplicação de agentes para problemas corporativos e no uso da infraestrutura gerenciada do Google Cloud.

| Seção | Tópico Principal | Link |
| :--- | :--- | :---: |
| **01 — Casos de Uso Corporativos** | As 6 categorias de agentes de negócios e alinhamento a KPIs. | [Acessar](./02-agentes-empresariais/01-casos-de-uso-corporativo.md) |
| **02 — Desenvolvimento no GCP** | Abordagens *No-Code*, *Low-Code* e *Code-First* (ADK e Agent Platform). | [Acessar](./02-agentes-empresariais/02-desenvolvimento-com-google-cloud.md) |
| **03 — Gemini Enterprise** | O Hub inteligente que unifica pessoas, agentes, dados e sistemas. | [Acessar](./02-agentes-empresariais/03-gemini-enterprise.md) |
| **04 — Simulação Prática** | Prática com busca avançada, Deep Research, NotebookLM e Studio. | [Acessar](./02-agentes-empresariais/04-simulacao-pratica.md) |
| **05 — Badge / Certificado** | Conquista do selo *Google Cloud — Enterprise Agents and Use Cases*. | [Acessar](./02-agentes-empresariais/05-badge-conclusao.md) |

---

## 🧠 Modelos Mentais e Sínteses

### 1. Evolução da Capacidade e Autonomia
```text
  LLM                ➔ Responde com base no conhecimento (Consultor)
  LLM + Funções      ➔ Executa ações pontuais quando ordenado (Assistente)
  Agente Autônomo    ➔ Recebe um objetivo e decide como alcançá-lo (Executor)

```

### 2. O Ciclo Agêntico Fundamental

```text
┌───────────┐     ┌────────────┐     ┌───────────┐     ┌───────────┐     ┌───────────┐
│  Observar │ ──> │ Interpretar│ ──> │  Planejar │ ──> │   Agir    │ ──> │ Verificar │
└───────────┘     └────────────┘     └───────────┘     └───────────┘     └─────┬─────┘
      ▲                                                                        │
      └────────────────────────── (Próximo Ciclo) ─────────────────────────────┘

```

### 3. As 4 Camadas da Gemini Enterprise Agent Platform

```text
  CRIAR       ➔ ADK, Agent Studio, Agent Garden, Model Garden, RAG
  ESCALAR     ➔ Agent Runtime, Sessões, Memória Persistente, Execução de Código
  GOVERNAR    ➔ Registros, Identidade, Gateways, Políticas de Segurança
  OTIMIZAR    ➔ Avaliação, Simulação, Observabilidade, Otimização de Prompts

```

---

## 🗂️ Estrutura do Repositório

```text
GEAR-academy/
├── README.md
│
├── 01-fundamentos-de-agentes/
│   ├── 01-introducao-a-agentes.md
│   ├── 02-abstracao-de-agentes.md
│   ├── 03-como-os-agentes-funcionam.md
│   ├── 04-agentes-em-acao.md
│   ├── 05-conclusao.md
│   └── 06-badge-conclusao.md
│
└── 02-agentes-empresariais/
    ├── 01-casos-de-uso-corporativo.md
    ├── 02-desenvolvimento-com-google-cloud.md
    ├── 03-gemini-enterprise.md
    ├── 04-simulacao-pratica.md
    └── 05-badge-conclusao.md

```

---

## 🛠️ Tecnologias e Conceitos Explorados

* **IA Generativa & LLMs:** Gemini API, Vertex AI, Prompt Engineering.
* **Arquitetura de Agentes:** Function Calling, ReAct, RAG, Memória Persistente, Sistemas Multiagentes.
* **Plataformas e Ferramentas Google:** Gemini Enterprise, Agent Development Kit (ADK), Agent Runtime, NotebookLM, Conversational Agents.
* **Engenharia de Software & Cloud:** APIs REST, Cloud Storage, Observabilidade, Governança e Métricas (KPIs).

---

## 💡 Ideia Central

> **Entender agentes é o primeiro passo. Saber quando e como utilizá-los é o que transforma conhecimento em engenharia.** 🚀

---

<div align="center">

## 👩‍💻 Autora

**Ana Carolina Pereira Ruas**  
Engenheira Florestal  
**Foco em Dados, Machine Learning, IA Generativa, LLMs, Agentes e Cloud**  

---
⭐ *Repositório desenvolvido como parte dos estudos da GEAR — Gemini Enterprise Agent Platform.*

</div>