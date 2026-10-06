# 🤖 Curso 3: Sistemas Multiagentes e Implantação com ADK

[![Google Cloud - Deploying Production-Ready Agents](https://img.shields.io/badge/Google%20Cloud-Deploying%20Production--Ready%20Agents-4285F4?logo=googlecloud&logoColor=white)](https://www.skills.google/)

---
*Guia completo de arquiteturas multiagentes, orquestração de workflows determinísticos e estratégias de implantação em produção com o Vertex AI Agent Engine e Cloud Run.*

---

## 🎯 Sobre o Curso

O curso **"Sistemas Multiagentes e Implantação com ADK"** aborda a construção e a governança de ecossistemas de IA avançados, transicionando da orquestração de um único agente para **sistemas multiagentes distribuídos, escaláveis, seguros e prontos para produção**.

Utilizando o **Google Agent Development Kit (ADK)** no Google Cloud, este repositório consolida desde a estruturação de árvores hierárquicas (agentes pai e subagentes) e *Workflow Agents* (`SequentialAgent`, `LoopAgent`, `ParallelAgent`), até a comunicação entre agentes remotos via protocolo **Agent2Agent (A2A)**, a integração de ferramentas via **Model Context Protocol (MCP)** e as estratégias de infraestrutura (Vertex AI Agent Engine, Cloud Run, GKE) com segurança e observabilidade de nível corporativo.

Toda a arquitetura multiagente está ancorada na evolução da equação de orquestração:

$$\text{Sistema Multiagente} = \text{Agentes LLM (Raciocínio)} + \text{Workflow Agents (Orquestração)} + \text{Protocolo A2A / MCP}$$

---

## 📚 Módulos do Curso

| Módulo | Título | Descrição / Foco Principal | Status |
| :---: | :--- | :--- | :---: |
| **01** | **Criar e Implantar Agentes em Produção** | Arquiteturas hierárquicas, *Workflow Agents* e a matriz de infraestrutura e governança (IAM, VPC Service Controls, Cloud Logging/Trace/Monitoring) no GCP. | ✅ Concluído |
| **02** | **Implantar Seu Primeiro Agente** | Eliminação do gargalo do `localhost`, deploys gerenciados no Vertex AI Agent Engine e Cloud Run (`--with_ui`), e estado de sessão vs. Memory Bank. | ✅ Concluído |
| **03** | **Arquiteturas Multiagentes (Prática)** | Comunicação distribuída via protocolo Agent2Agent (A2A), padrão `AgentTool` para evitar bugs de RAG e Challenge Lab com deploy no Agent Engine. | ✅ Concluído |
| **04** | **Conclusão do Curso** | Síntese do programa, consolidação dos pilares de produção e encerramento da trilha GEAR. | ✅ Concluído |

---

## 📐 Arquitetura e Conceitos-Chave

### 🌳 1. Hierarquia e Agentes de Fluxo (Workflow Agents)
- **Agentes LLM (Cérebro):** Responsáveis por compreender a linguagem natural, tomar decisões contextuais e acionar ferramentas.
- **Workflow Agents (Orquestradores):** Determinísticos e focados no controle do fluxo sem tomar decisões autônomas.
  - **`SequentialAgent`:** Executa etapas em ordem fixa pré-definida.
  - **`LoopAgent`:** Repete ciclos de execução até que uma condição de parada seja atingida.
  - **`ParallelAgent`:** Executa múltiplos subagentes simultaneamente para tarefas independentes.

### 🌐 2. Protocolo Agent2Agent (A2A) vs. Subagentes Nativos
- **Subagentes Nativos:** Agentes executados dentro do mesmo processo local ou contêiner.
- **Agentes Remotos A2A:** Comunicação entre agentes em servidores distintos via **JSON-RPC 2.0 sobre HTTP(S)**, descobertos dinamicamente por manifestos `agent.json` (*Agent Cards*).

### 🛡️ 3. Governança, Segurança e Observabilidade em Produção
- **IAM & Menor Privilégio:** Escopo de acesso estrito para os agentes e suas ferramentas.
- **VPC Service Controls:** Perímetros de segurança para proteção contra exfiltração de dados.
- **Observabilidade Tripla:** **Cloud Logging** (auditabilidade), **Cloud Trace** (análise de latência) e **Cloud Monitoring** (métricas operacionais/QPS).

---

## 🛠️ Tecnologias Utilizadas

- **Framework de Agentes:** Google Agent Development Kit (ADK)
- **Modelos de Linguagem:** Gemini 2.5 Flash / Gemini Enterprise
- **Protocolos & Padrões:** Agent2Agent (A2A) e Model Context Protocol (MCP)
- **Infraestrutura Cloud:** Vertex AI Agent Engine, Cloud Run, GKE e Vertex AI Search (RAG)
- **Front-end & Testes:** Chainlit UI, ADK CLI (`adk web`), Python SDK e cURL

---

## 📂 Estrutura do Repositório

```text
GEAR-academy/
└── 03-implantar-agentes-prontos-producao/
    ├── 01-criacao-e-implantacao/
    │   ├── 01-sistemas-multiagentes-com-adk.md
    │   ├── 02-agentes-de-IA-em-producao.md
    │   └── 03-badge-conclusao.md
    ├── 02-primeiro-agente/
    │   ├── 01-problema-agentes-em-localhost.md
    │   ├── ...
    │   └── 10-badge-conclusao_2.md
    ├── 03-arquiteturas-multiagentes/
    │   ├── 01-sistemas-multiagentes-com-adk_2.md
    │   ├── ...
    │   └── 05-badge-conclusao.md
    ├── 04-implantar-agentes-prontos/
    │   └── README.md
    └── README.md
```
---
## 🔗 Links e Recursos Oficiais

* [🎥 Criar sistemas multiagentes com o ADK](https://www.skills.google/paths/3802/course_sessions/45241014/video/637477)
* [📖 Como implantar e gerenciar agentes de IA em produção](https://www.skills.google/paths/3802/course_sessions/45241014/documents/637478)

---

<div align="center">

## 👩‍💻 Autora

**Ana Carolina Pereira Ruas**  
Engenheira Florestal  
**Foco em Dados, Machine Learning, IA Generativa, LLMs, Agentes e Cloud**  

---
⭐ *Repositório desenvolvido como parte dos estudos da GEAR — Gemini Enterprise Agent Platform.*

</div>
