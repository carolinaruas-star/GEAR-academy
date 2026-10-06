# 🤖 Módulo 1 — Sistemas Multiagentes e Implantação em Produção com ADK

[![Google Cloud - Criar e Implantar Agentes em Produção](https://img.shields.io/badge/Google%20Cloud-Create%20and%20Deploy%20Agents-4285F4?logo=googlecloud&logoColor=white)](./03-badge-conclusao.md)
--
*Arquiteturas multiagentes, orquestração de workflows determinísticos e estratégias corporativas de implantação em produção.*

---

## 🎯 Objetivos do Módulo

- 🌳 **Arquiteturas Hierárquicas Multiagentes:** Estruturar árvores de agentes (pai/mãe, subagentes e peers) para garantir transferências previsíveis e escopos controlados[cite: 38].
- ⚙️ **Agentes de Fluxo de Trabalho (Workflow Agents):** Implementar orquestração determinística usando `SequentialAgent`, `LoopAgent`, `ParallelAgent` e workflows personalizados[cite: 38].
- ☁️ **Opções de Implantação na Google Cloud:** Selecionar a infraestrutura adequada entre Vertex AI Agent Engine, Cloud Run, GKE, App Engine e Compute Engine[cite: 39].
- 🔐 **Segurança e Observabilidade Corporativa:** Aplicar o princípio do menor privilégio via IAM, proteger perímetros com VPC Service Controls e monitorar via Cloud Logging, Cloud Trace e Cloud Monitoring[cite: 39].
- 🔄 **Ciclo de Vida e MLOps:** Controlar versionamento, gestão de ambientes (*Dev ➔ Hml ➔ Prod*) e estratégias de reversão (*rollback*)[cite: 39].

---

## 📚 Conteúdo do Módulo

| Seção | Descrição / Foco Principal | Arquivo |
| :--- | :--- | :---: |
| **01 — Sistemas Multiagentes com ADK** | Hierarquia de agentes e orquestradores de fluxo (`Sequential`, `Loop`, `Parallel` e Personalizado)[cite: 38]. | [Acessar](./01-sistemas-multiagentes-com-adk.md) |
| **02 — Agentes de IA em Produção** | Infraestrutura de implantação no GCP, segurança, observabilidade e governança de ciclo de vida[cite: 39]. | [Acessar](./02-agentes-de-IA-em-producao.md) |
| **03 — Badge de Conclusão** | Registro da conquista da credencial oficial *Criar e implantar agentes em produção*[cite: 40]. | [Acessar](./03-badge-conclusao.md) |

---

## 🧩 Orquestração Multiagente vs. Agentes de Workflow

```text
                        🤖 SISTEMA MULTIAGENTE
                                   │
         ┌─────────────────────────┴─────────────────────────┐
         ▼                                                   ▼
  🧠 AGENTES LLM                                  ⚙️ WORKFLOW AGENTS
  (Raciocínio Autónomo)                           (Orquestração Determinística)
  ├── Tomam decisões contextuais                  ├── Executam lógicas sequenciais (`SequentialAgent`)
  ├── Interagem com ferramentas                   ├── Executam repetições iterativas (`LoopAgent`)
  └── Respondem a comandos em linguagem natural   └── Executam tarefas simultâneas (`ParallelAgent`)

```

---

## ☁️ Matriz de Opções de Implantação na Google Cloud

| Serviço GCP | Nível de Gerenciamento | Casos de Uso Recomendados |
| --- | --- | --- |
| **Vertex AI Agent Engine** | Fully Managed | Implantação simplificada de agentes ADK com gestão nativa de sessões e A2A. |
| **Cloud Run** | Serverless / Containers | Agentes empacotados em contêineres com tráfego variável e custo reduzido a zero. |
| **Google Kubernetes Engine (GKE)** | Kubernetes / Infra | Cargas de trabalho de IA complexas, distribuídas, de alto desempenho e com hardware dedicado. |
| **App Engine** | PaaS Serverless | Backend web escalável e integração com agentes conversacionais/webhooks. |
| **Compute Engine** | IaaS / VMs | Sistemas legados, controle total do S.O., kernel e serviços persistentes sem desligamento. |

---

## 📊 Governança, Segurança e Observabilidade

* 🔑 **IAM & Menor Privilégio:** Permissões estritas por contas de serviço para o agente e suas ferramentas externas.


* 🛡️ **VPC Service Controls:** Perímetros de segurança de rede para prevenção contra exfiltração de dados sensíveis.


* 🔎 **Observabilidade Tripla:**
* **Cloud Logging:** Registro auditável de interações e exceções de ferramentas.


* **Cloud Trace:** Análise de latência por etapas (chamada do LLM, execução de *tools*, RAG).


* **Cloud Monitoring:** Acompanhamento operático de QPS, taxas de erro e falhas do agente.





---

## 🗂️ Estrutura da Pasta

```text
01-sistemas-multiagentes-e-producao/
├── README.md
├── 01-sistemas-multiagentes-com-adk.md
├── 02-agentes-de-IA-em-producao.md
└── 03-badge-conclusao.md

```
<div align="center">

## 👩‍💻 Autora

**Ana Carolina Pereira Ruas**  
Engenheira Florestal  
**Foco em Dados, Machine Learning, IA Generativa, LLMs, Agentes e Cloud**  

---
⭐ *Repositório desenvolvido como parte dos estudos da GEAR — Gemini Enterprise Agent Platform.*

</div>