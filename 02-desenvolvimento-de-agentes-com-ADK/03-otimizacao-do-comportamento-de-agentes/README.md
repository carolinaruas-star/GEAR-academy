# 🤖 Módulo 3: Otimização do Comportamento de Agentes

## 📚 Sobre o módulo

Este módulo apresenta técnicas para **otimizar o comportamento de agentes de IA**, evoluindo de agentes básicos para agentes mais **estruturados, previsíveis, seguros e eficientes**.

Durante os estudos, foram explorados recursos do **Google Agent Development Kit (ADK)** para controlar como os agentes recebem instruções, estruturam suas respostas, utilizam modelos e lidam com problemas complexos.

---

## 🎯 Objetivos

Ao longo do módulo, foram trabalhados os seguintes objetivos:

* 🧠 Criar instruções avançadas e reutilizáveis;
* 📦 Produzir saídas estruturadas utilizando esquemas Pydantic;
* ⚙️ Configurar modelos de acordo com diferentes tipos de tarefas;
* 🔐 Ajustar parâmetros de segurança e geração;
* 🔍 Utilizar planejamento para problemas complexos;
* 🛠️ Desenvolver agentes mais consistentes e preparados para aplicações reais.

---

## 🗂️ Conteúdos do módulo

### ✍️ 01 — Advanced Instruction Writing

Exploração de técnicas para criar instruções mais completas e controlar o comportamento dos agentes.

**Conteúdos:**

* Identidade e persona;
* Missão;
* Metodologia;
* Limites;
* Exemplos `few-shot`;
* Templates reutilizáveis;
* Organização das instruções com Markdown.

📄 **Arquivos:**

* [`01-advanced-instruction-writing-problema.md`](./01-advanced-instruction-writing-problema.md)
* [`02-advanced-instruction-writing-solucao.md`](./02-advanced-instruction-writing-solucao.md)

---

### 📦 02 — Structured Output

Estudo da utilização de **saídas estruturadas** para transformar respostas de linguagem natural em dados previsíveis e integráveis com sistemas.

**Conteúdos:**

* `output_schema`;
* Pydantic `BaseModel`;
* `Field`;
* `output_key`;
* JSON estruturado;
* Validação de dados;
* Fluxo de informações entre agentes.

📄 **Arquivos:**

* [`03-structured-output-problema.md`](./03-structured-output-problema.md)
* [`04-structured-output-solucao.md`](./04-structured-output-solucao.md)

---

### ⚙️ 03 — Escolhendo e Configurando Modelos

Estudo da seleção estratégica de modelos e dos parâmetros que controlam seu comportamento.

**Conteúdos:**

* Gemini 2.5 Pro;
* Gemini 2.5 Flash;
* `GenerateContentConfig`;
* `temperature`;
* `top_p`;
* `top_k`;
* `max_output_tokens`;
* `SafetySetting`;
* Otimização de custo e desempenho.

📄 **Arquivos:**

* [`05-escolhendo-e-config-modelos-problema.md`](./05-escolhendo-e-config-modelos-problema.md)
* [`06-escolhendo-e-config-modelos-solucao.md`](./06-escolhendo-e-config-modelos-solucao.md)

---

### 🧠 04 — Planning for Complex Tasks

Estudo do planejamento para agentes que precisam lidar com **problemas complexos e múltiplas etapas**.

**Conteúdos:**

* `BuiltInPlanner`;
* `PlanReActPlanner`;
* `ThinkingConfig`;
* `thinking_budget`;
* `include_thoughts`;
* Planejamento estruturado;
* Diferença entre planejamento e sistemas multiagentes.

📄 **Arquivos:**

* [`07-planning-for-complex-tasks-problem.md`](./07-planning-for-complex-tasks-problem.md)
* [`08-planning-for-complex-tasks-solution.md`](./08-planning-for-complex-tasks-solution.md)

---

## 🧩 Principais conceitos

| Conceito                   | Função                                     |
| -------------------------- | ------------------------------------------ |
| 🧠 `instruction`           | Define o comportamento do agente           |
| 📦 `output_schema`         | Define a estrutura da saída                |
| 🔑 `output_key`            | Armazena e transmite resultados            |
| ⚙️ `GenerateContentConfig` | Configura a geração do modelo              |
| 🌡️ `temperature`          | Controla a variação das respostas          |
| 🔐 `SafetySetting`         | Define filtros de segurança                |
| 🔍 `BuiltInPlanner`        | Permite planejamento com modelos Gemini    |
| 🧠 `ThinkingConfig`        | Configura recursos de pensamento           |
| 🎯 `thinking_budget`       | Define o orçamento destinado ao pensamento |

---

## 🧠 Evolução do agente

O módulo apresenta uma evolução progressiva:

```text
🤖 Agente básico
      │
      ▼
🧠 Instruções avançadas
      │
      ▼
📦 Saída estruturada
      │
      ▼
⚙️ Configuração estratégica
      │
      ▼
🔍 Planejamento
      │
      ▼
🚀 Agente mais robusto
```

Cada etapa adiciona uma camada de controle ao agente, permitindo maior **previsibilidade, consistência e adequação ao objetivo da aplicação**.

---

## 💡 Principais aprendizados

### 🧠 Instruções

Uma instrução bem construída funciona como uma **especificação de comportamento**, definindo identidade, missão, metodologia, limites e exemplos.

### 📦 Estrutura de dados

O `output_schema` estabelece um **contrato para a saída do agente**, facilitando a integração com aplicações, APIs, bancos de dados e outros agentes.

### ⚙️ Configuração

A escolha do modelo e dos parâmetros deve considerar o equilíbrio entre **qualidade, custo, velocidade e segurança**.

### 🔍 Planejamento

O planejamento é especialmente útil para tarefas que exigem **múltiplas etapas, análise de alternativas e tomada de decisão estruturada**.

---

## 🏁 Conclusão

Ao concluir este módulo, os conhecimentos adquiridos permitem desenvolver agentes de IA com maior controle sobre:

* 🧠 **Comportamento**
* 📦 **Estrutura das respostas**
* ⚙️ **Configuração dos modelos**
* 🔐 **Segurança**
* 🔍 **Planejamento**

O resultado é uma evolução de agentes simplesmente reativos para sistemas mais **estruturados, eficientes e preparados para cenários reais de aplicação**.

📄 Para consultar a conclusão completa:

➡️ [`09-conclusao.md`](./09-conclusao.md)

---

## 🎓 Certificação

O módulo foi concluído com sucesso na plataforma **Google Cloud Skills Boost**.

📄 Registro da conclusão:

➡️ [`10-badge-conclusao.md`](./10-badge-conclusao.md)

---

## 📌 Estrutura do módulo

```text
03-otimizacao-do-comportamento-de-agentes/
│
├── 01-advanced-instruction-writing-problema.md
├── 02-advanced-instruction-writing-solucao.md
├── 03-structured-output-problema.md
├── 04-structured-output-solucao.md
├── 05-escolhendo-e-config-modelos-problema.md
├── 06-escolhendo-e-config-modelos-solucao.md
├── 07-planning-for-complex-tasks-problem.md
├── 08-planning-for-complex-tasks-solution.md
├── 09-conclusao.md
├── 10-badge-conclusao.md
│
└── README.md
```

---

## 🚀 Próxima etapa

Com os fundamentos de **otimização do comportamento dos agentes** concluídos, o próximo passo da trilha é avançar para recursos que permitem aos agentes **utilizar ferramentas, acessar informações externas e executar tarefas**, aproximando-os de aplicações agentivas mais completas.

---

<p align="center">
  <strong>🤖 Google Agent Development Kit (ADK)</strong><br>
  Construindo agentes mais inteligentes, estruturados e eficientes.
</p>
