# 🤖 Módulo 01 — Agentes de IA Generativa: Transforme sua Organização

[![Google Cloud - Generative AI Leader](https://img.shields.io/badge/Google%20Cloud-Generative%20AI%20Leader-4285F4?logo=googlecloud&logoColor=white)](./12-badge-conclusao_2.md)
---

*Fundamentos, arquiteturas híbridas, engenharia de prompts (ReAct/CoT), RAG, ecossistema GCP e estratégias empresariais com o Gemini Enterprise.* 

---

## 📌 Visão Geral do Módulo

O módulo **"Agentes de IA generativa: transforme sua organização"** é o quinto e último curso do programa **Líder em IA generativa do Google Cloud**. Ele apresenta como as organizações podem criar e implantar **agentes de IA generativa personalizados** para resolver problemas específicos de negócio e automatizar processos complexos.

Ao longo das aulas, são explorados desde a evolução histórica (de sistemas determinísticos a agentes generativos e híbridos), até técnicas de raciocínio (ReAct/Chain of Thought), integração com APIs e ferramentas[cite: 26], RAG com busca vetorial, a plataforma **Vertex AI Search**, atendimento ao cliente (CCaaS), criação prática com metacomandos no Google AI Studio e a plataforma corporativa **Gemini Enterprise**.

---

## 🎯 Objetivos de Aprendizagem

- 🧠 **Compreender a Evolução Agêntica:** Analisar a transição de fluxos determinísticos (regras) para agentes generativos e sistemas híbridos de alta previsibilidade.
- ⚙️ **Ajustar Parâmetros de Amostragem:** Dominar o impacto de Tokens, Temperatura, Top-K, Top-P e limites nas APIs Gemini e plataformas AI Studio / Vertex AI Studio.
- 🔄 **Engenharia de Comandos e Raciocínio Iterativo:** Aplicar as técnicas **Chain of Thought (CoT)** para raciocínio lógico interno e **ReAct (Reasoning + Acting)** para ações e chamadas de ferramentas externas.
- 🛠️ **Extensão de Capacidades com Ferramentas & RAG:** Integrar APIs, extensões, bancos de dados vetoriais (embeddings) e repositórios não estruturados (PDF, HTML) via Retrieval-Augmented Generation.
- 🏢 **Escala Corporativa e Governança:** Implementar agentes de pesquisa com a **Vertex AI Search**, soluções para Centrais de Atendimento (CCaaS / Agent Assist) e o **Gemini Enterprise** com o NotebookLM Enterprise.

---

## 📚 Conteúdo do Módulo

| Seção | Descrição / Foco Principal | Arquivo |
| :--- | :--- | :---: |
| **01 — Introdução e Evolução dos Agentes** | A transição de agentes determinísticos para generativos, RAG e arquiteturas híbridas. | [Acessar](./01-introducao-e-evolucao-dos-agentes.md) |
| **02 — Como Usar Modelos** | Parâmetros de amostragem (Temperatura, Top-K, Top-P), APIs e comparativo AI Studio vs. Vertex AI Studio. | [Acessar](./02-como-usar-modelos.md) |
| **03 — Engenharia de Comandos** | Raciocínio de repetição, técnicas Chain of Thought (CoT), ReAct e escolha por caso de uso. | [Acessar](./03-engenharia-de-comandos.md) |
| **04 — Adicionar Ferramentas** | Extensões de APIs, ciclo ReAct no mundo real e serviços GCP (Cloud Storage, Cloud Run, Document AI, Maps). | [Acessar](./04-adicionar-ferramentas.md) |
| **05 — Criar Apps com Agentes** | Integração via API Gemini, desenvolvimento low-code/no-code (Apps Script, AppSheet) e arquiteturas multiagentes.| [Acessar](./05-criar-app-com-agentes.md) |
| **06 — RAG e Ferramentas** | Geração Aumentada por Recuperação, bancos vetoriais, embeddings, dados estruturados e não estruturados. | [Acessar](./06-RAG-e-ferramentas.md) |
| **07 — Agentes de Pesquisa** | Vertex AI Search, mecanismos de recomendação de mídia/varejo, resumos automáticos e respostas embasadas. | [Acessar](./07-agentes-de-pesquisa.md) |
| **08 — Engajamento do Cliente** | Pacote de Atendimento, agentes conversacionais, Agent Assist, Insights de Conversação e infraestrutura CCaaS. | [Acessar](./08-engajamento-do-cliente.md) |
| **09 — Crie Seu Próprio Agente** | Construção prática do chatbot Cymbal Manufacturing no AI Studio, playbooks, instruções de sistema e metacomandos. | [Acessar](./09-crie-seu-agente.md) |
| **10 — Gemini Enterprise** | Plataforma corporativa unificada, integração com NotebookLM Enterprise e agentes para produtividade interna. | [Acessar](./10-gemini-enterprise.md) |
| **11 — Estratégia e Planejamento** | Governança, priorização de ROI, gestão da mudança, liderança em IA e preparação para o exame Generative AI Leader. | [Acessar](./11-planejamento-antecipado.md) |
| **12 — Badge de Conclusão** | Registro da conquista do selo oficial *Agentes de IA generativa: transforme sua organização*. | [Acessar](./12-badge-conclusao_2.md) |

---

## 🏗️ Evolução Histórica dos Agentes de IA

```text
 1. DETERMINÍSTICOS             2. GENERATIVOS               3. GENERATIVOS + RAG              4. HÍBRIDOS
┌───────────────────────┐      ┌────────────────────┐       ┌─────────────────────────┐       ┌────────────────────────┐
│ Regras & Regressão    │ ───> │ LLM + Intenção +   │ ────> │ LLM + Ferramentas +     │ ────> │ Previsibilidade das    │
│ (Se Pressionar 1...)  │      │ Respostas Livres   │       │ Dados Externos (Vector) │       │ Regras + Flexibilidade │
└───────────────────────┘      └────────────────────┘       └─────────────────────────┘       └────────────────────────┘
```

---

## ⚖️ ReAct (Reasoning + Acting) vs. Chain of Thought (CoT)

| Técnica | Foco Principal | Uso de Ferramentas Externas | Caso de Uso Ideal |
| :--- | :--- | :---: | :--- |
| **Chain of Thought (CoT)** | Raciocínio lógico interno passo a passo. | ❌ Não exige. | Problemas matemáticos, lógica complexa e explicações estruturadas. |
| **ReAct (Reasoning + Acting)** | Loop iterativo de Raciocínio, Ação e Observação. | ✅ Sim (APIs, Banco de Dados, Web). | Consultas em tempo real, agendamentos, busca de dados e ações no mundo real. |
| **CoT + ReAct (Combinados)** | Estruturação lógica interna com execução externa. | ✅ Sim. | Tarefas complexas corporativas e agentes autônomos robustos. |

---

## 📊 Matriz de Ferramentas de Experimentação Google

| Plataforma | Público Alvo | Acesso | Foco de Aplicação |
| :--- | :--- | :--- | :--- |
| **Google AI Studio** | Iniciantes e Prototipadores. | Conta Google simples. | Experimentação rápida de prompts, parâmetros e testes com chaves de API. |
| **Vertex AI Studio** | Desenvolvedores e Empresas. | Google Cloud Project. | Soluções profissionais escaláveis, com governança, segurança IAM e cotas dedicadas. |

---

## 🔗 Links e Recursos Recomendados

* [Google Cloud Skills Boost — Formação Generative AI Leader](https://www.skills.google/)
* [Documentação da API Gemini & Google AI Studio](https://ai.google.dev/)
* [Documentação da Vertex AI Search & Conversation](https://cloud.google.com/vertex-ai/generative-ai/docs/search-overview)

---

<div align="center">

## 👩‍💻 Autora

**Ana Carolina Pereira Ruas**  
Engenheira Florestal  
**Foco em Dados, Machine Learning, IA Generativa, LLMs, Agentes e Cloud**  

---
⭐ *Repositório desenvolvido como parte dos estudos da GEAR — Gemini Enterprise Agent Platform.*

</div>
