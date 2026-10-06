# 🤖 Módulo 1 — GEAR: Introdução aos Agentes e ao Ecossistema de Agentes do Google

[![Google Cloud - Agent Fundamentals](https://img.shields.io/badge/Google%20Cloud-Agent%20Fundamentals-4285F4?logo=googlecloud&logoColor=white)](06-badge-conclusao.md)

Este repositório reúne meus estudos e anotações sobre **Agentes de IA**, cobrindo sua arquitetura, tomada de decisão autônoma, casos de uso e o ecossistema de soluções agênticas do **Google Cloud (GEAR / Gemini Enterprise Agent Platform)**.

---

## 🎯 Objetivos de Aprendizado

Compreender a evolução de **LLMs para sistemas agênticos**, identificando **quando, por que e como utilizar agentes** de forma eficiente:

- 🧠 **Fundamentos de Agentes:** Ciclos de raciocínio (*Observar → Interpretar → Planejar → Agir*) e operação autônoma.
- ⚙️ **Arquitetura Base:** Entender a equação **`Agente = Modelo + Ferramentas + Orquestração`**.
- 🛠️ **Ferramentas & Integração:** Como ampliar a capacidade de LLMs através de *Function Calling*, APIs e RAG.
- 🎯 **Tomada de Decisão:** Critérios para escolher entre automações tradicionais, chamadas de função ou sistemas de agentes.
- ☁️ **Ecossistema Google Cloud:** Visão dos 4 pilares (*Criação, Escala, Governança e Otimização*).

---

## 📚 Módulos do Curso

| Módulo | Descrição Central | Link |
| :--- | :--- | :---: |
| **01 — Introdução a Agentes** | O que são agentes, ciclo de raciocínio, capacidades e sistemas multiagentes. | [Acessar](./01-introducao-a-agentes/) |
| **02 — Abstração de Agentes** | A evolução: `LLM` ➔ `LLM + Function Calling` ➔ `Agente Autônomo`. | [Acessar](./02-abstracao-de-agentes/) |
| **03 — Como Agentes Funcionam** | Detalhamento dos 3 pilares: **Modelo** (cérebro), **Ferramentas** (mãos) e **Orquestração** (processo). | [Acessar](./03-como-os-agentes-funcionam/) |
| **04 — Agentes em Ação** | Critérios para saber quando usar agentes vs. automações tradicionais e visão do ecossistema Google Cloud. | [Acessar](./04-agentes-em-acao/) |
| **05 — Conclusão** | Modelos mentais, matriz de tomada de decisão e consolidação de arquitetura. | [Acessar](./05-conclusao/) |
| **06 — Certificado / Badge** | Registro de conclusão do selo *Google Cloud - Agent Fundamentals*. | [Acessar](./06-badge-conclusao.md) |

---

## 💡 Modelos Mentais Essenciais

### 1. Evolução da Autonomia
```text
  LLM                ➔ Responde com base no conhecimento prévio (Consultor)
  LLM + Funções      ➔ Executa ações pontuais quando ordenado (Assistente)
  Agente             ➔ Recebe um objetivo e decide autonomamente como agir (Executor)

```

### 2. Ciclo de Raciocínio Agêntico

```text
┌───────────┐     ┌────────────┐     ┌───────────┐     ┌───────────┐     ┌───────────┐
│  Observar │ ──> │ Interpretar│ ──> │  Planejar │ ──> │   Agir    │ ──> │ Verificar │
└───────────┘     └────────────┘     └───────────┘     └───────────┘     └─────┬─────┘
      ▲                                                                        │
      └────────────────────────── (Próximo Ciclo) ─────────────────────────────┘

```

### 3. Quando utilizar agentes?

> **Use Agentes** para tarefas **complexas, dinâmicas e de múltiplas etapas** que exigem raciocínio e adaptação.
> 
> 
> **Prefira Automações Tradicionais (APIs/Scripts)** para tarefas **simples, repetitivas ou determinísticas**.
> 
> 

---

## 🗂️ Estrutura do Repositório

```text
GEAR-academy/
├── README.md
├── 01-introducao-a-agentes/
├── 02-abstracao-de-agentes/
├── 03-como-os-agentes-funcionam/
├── 04-agentes-em-acao/
├── 05-conclusao/
└── 06-badge-conclusao.md
```
<div align="center">

## 👩‍💻 Autora

**Ana Carolina Pereira Ruas**  
Engenheira Florestal  
**Foco em Dados, Machine Learning, IA Generativa, LLMs, Agentes e Cloud**  

---
⭐ *Repositório desenvolvido como parte dos estudos da GEAR — Gemini Enterprise Agent Platform.*

</div>
