# 🤖 Módulo 3 — Otimização do Comportamento de Agentes de IA com ADK

[![Google Cloud - Optimize Agent Behavior](https://img.shields.io/badge/Google%20Cloud-Optimize%20Agent%20Behavior-4285F4?logo=googlecloud&logoColor=white)](./10-badge-conclusao.md)

Este módulo aborda as técnicas avançadas de **engenharia e otimização do comportamento de Agentes de IA** utilizando o **Google Agent Development Kit (ADK)**. O conteúdo foca na evolução de agentes reativos simples para o desenvolvimento de sistemas profissionais **previsíveis, estruturados, seguros e otimizados para produção**.

---

## 🎯 Objetivos do Módulo

- 🧠 **Instruções Estruturadas:** Substituir prompts vagos por um framework de 5 pilares (*Identidade, Missão, Metodologia, Limites e Few-Shot*) em Markdown.
- 📦 **Saídas Estruturadas (`output_schema`):** Garantir respostas determinísticas através de objetos **Pydantic `BaseModel`** e persistir estados com `output_key`.
- ⚙️ **Configuração Estratégica de Modelos:** Ajustar a **temperatura**, **limites de tokens** e **Safety Settings** via `GenerateContentConfig` para equilibrar qualidade, consistência, segurança e custo.
- 🔍 **Raciocínio e Planejamento em Múltiplas Etapas:** Capacitar os agentes a resolver problemas complexos com o **`BuiltInPlanner`** e **`ThinkingConfig`**.

---

## 📚 Conteúdo do Módulo

| Seção | Descrição / Foco Principal | Arquivos |
| :--- | :--- | :---: |
| **01 — Instruções Profissionais** | Como estruturar comportamentos previsíveis usando os 5 padrões (Identidade, Missão, Metodologia, Limites e Few-shot). | [Problema](./01-advanced-instruction-writing-problema.md) / [Solução](./02-advanced-instruction-writing-solucao.md) |
| **02 — Saídas Estruturadas** | Uso do `output_schema` com Pydantic `BaseModel` e `output_key` para integração com sistemas e workflows. | [Problema](./03-structured-output-problema.md) / [Solução](./04-structured-output-solucao.md) |
| **03 — Seleção e Configuração de Modelos** | Otimização estratégica usando Gemini 2.5 Pro/Flash, `GenerateContentConfig`, temperatura e segurança. | [Problema](./05-escolhendo-e-config-modelos-problema.md) / [Solução](./06-escolhendo-e-config-modelos-solucao.md) |
| **04 — Planejamento Estruturado** | Decomposição de tarefas complexas e raciocínio em múltiplas etapas com `BuiltInPlanner` e `ThinkingConfig`. | [Problema](./07-planning-for-complex-tasks-problem.md) / [Solução](./08-planning-for-complex-tasks-solution.md) |
| **05 — Conclusão do Módulo** | Síntese dos 4 pilares, checklists de boas práticas e tabela de referência rápida. | [Acessar](./09-conclusao.md) |
| **06 — Badge de Conclusão** | Registro da conquista do selo oficial *Optimize Agent Behavior*. | [Acessar](./10-badge-conclusao.md) |

---

## 🧩 Os 4 Pilares da Otimização de Agentes

```text
              🤖 AGENTE PROFISSIONAL DE IA
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
   🧠 INSTRUÇÃO    📦 ESTRUTURA    ⚙️ CONFIGURAÇÃO
  (Comportamento)   (Dados JSON)      (Modelo/LLM)
        │              │              │
        └──────────────┼──────────────┘
                       │
                       ▼
                🧠 PLANEJAMENTO
              (Múltiplas Etapas)
                       │
                       ▼
              🎯 SOLUÇÃO COMPLETA

```

---

### 1. 🧠 Instruções Estruturadas (Framework de 5 Padrões)

As instruções profissionais superam comandos genéricos ao definir explicitamente:

1. **👤 Identidade:** Persona, nome e especialização do agente.


2. **🎯 Missão:** Objetivo principal e diretrizes centrais.


3. **🔄 Metodologia:** Passos estruturados de execução (*Reconhecer ➔ Esclarecer ➔ Resolver ➔ Verificar*).


4. **🛡️ Limites:** Regras explícitas do que o agente **NUNCA** deve fazer.


5. **💬 Exemplos Few-Shot:** Pares de entrada/saída orientando tom e formato.



---

### 2. 📦 Saída Estruturada (`output_schema` + Pydantic)

Transforma texto livre em um **contrato de dados previsível** para sistemas externos:

```python
from google.adk.agents import LlmAgent
from pydantic import BaseModel, Field

class ProductInfo(BaseModel):
    product_name: str = Field(description="Nome do produto")
    price: float = Field(description="Preço em USD")
    storage: str = Field(description="Capacidade de armazenamento")

root_agent = LlmAgent(
    model="gemini-2.5-flash",
    instruction="Extrair informações de produto.",
    output_schema=ProductInfo,      # Contrato Pydantic
    output_key="extracted_product"  # Salva no estado da sessão
)

```

---

### 3. ⚙️ Configuração Estratégica (`GenerateContentConfig`)

Ajusta os parâmetros de amostragem de acordo com o objetivo da tarefa:

| Perfil | Modelo | Temperatura | Casos de Uso |
| --- | --- | --- | --- |
| **Factual / Determinístico** | Gemini 2.5 Flash | `0.0 – 0.3` | Extração de dados, JSON, classificações e finanças.|
| **Equilibrado** | Gemini 2.5 Flash / Pro | `0.4 – 0.7` | Atendimento ao cliente, suporte técnico e chats gerais.|
| **Criativo** | Gemini 2.5 Pro | `0.8 – 1.0` | Brainstorming, marketing e geração de ideias.|

---

### 4. 🔍 Planejamento Estruturado (`BuiltInPlanner`)

Habilita a capacidade de raciocínio prévio em várias etapas para problemas complexos:

```python
from google.adk.agents import LlmAgent
from google.adk.planners import BuiltInPlanner
from google.genai import types

planning_agent = LlmAgent(
    model="gemini-2.5-flash",
    instruction="Analise problemas estratégicos de negócios.",
    planner=BuiltInPlanner(
        thinking_config=types.ThinkingConfig(
            include_thoughts=True, # Raciocínio visível para debug
            thinking_budget=2048   # Orçamento de tokens para pensamento
        )
    )
)

```

---

## 🗂️ Estrutura da Pasta

```text
03-otimizacao-do-comportamento-de-agentes/
├── README.md
├── 01-advanced-instruction-writing-problema.md
├── 02-advanced-instruction-writing-solucao.md
├── 03-structured-output-problema.md
├── 04-structured-output-solucao.md
├── 05-escolhendo-e-config-modelos-problema.md
├── 06-escolhendo-e-config-modelos-solucao.md
├── 07-planning-for-complex-tasks-problem.md
├── 08-planning-for-complex-tasks-solution.md
├── 09-conclusao.md
└── 10-badge-conclusao.md

```
<div align="center">

## 👩‍💻 Autora

**Ana Carolina Pereira Ruas**  
Engenheira Florestal  
**Foco em Dados, Machine Learning, IA Generativa, LLMs, Agentes e Cloud**  

---
⭐ *Repositório desenvolvido como parte dos estudos da GEAR — Gemini Enterprise Agent Platform.*

</div>