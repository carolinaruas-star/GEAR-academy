## 🧠 Google ADK — Planejamento com `BuiltInPlanner`

### A solução: planejamento com o BuiltInPlanner 

### 🎯 Objetivo

Aprender a ativar o **raciocínio em várias etapas** em agentes ADK utilizando o `BuiltInPlanner` e configurar a profundidade e visibilidade desse raciocínio por meio do `ThinkingConfig`.

A ideia é permitir que o agente trate problemas complexos de maneira mais **sistemática, estruturada e analítica**.

---

### 🧩 Ativando o planejamento

O ADK disponibiliza o parâmetro `planner` para adicionar capacidades de planejamento ao agente.

```python id="4j6x8p"
from google.adk.agents import LlmAgent
from google.adk.planners import BuiltInPlanner
from google.genai import types

planning_agent = LlmAgent(
    model="gemini-2.5-flash",
    planner=BuiltInPlanner(
        thinking_config=types.ThinkingConfig(
            include_thoughts=True,
            thinking_budget=1024
        )
    ),
    instruction="Resolva problemas complexos sistematicamente"
)
```

O `BuiltInPlanner` utiliza os **recursos de raciocínio integrados dos modelos Gemini** para realizar planejamento antes da execução da tarefa.

---

## 🧠 `ThinkingConfig`

O `ThinkingConfig` permite controlar o comportamento do raciocínio.

### `thinking_budget`

Define a quantidade de tokens disponibilizada para o processo de raciocínio.

```python id="7f3z2m"
types.ThinkingConfig(
    thinking_budget=1024
)
```

De forma geral:

```text
Budget menor → raciocínio mais rápido
Budget maior  → maior capacidade para análises complexas
```

### `include_thoughts`

Controla se os pensamentos do modelo são incluídos na resposta.

```python id="a8n5qd"
types.ThinkingConfig(
    include_thoughts=True,
    thinking_budget=1024
)
```

É especialmente útil durante **desenvolvimento e depuração**, pois permite observar como o agente estruturou sua análise.

---

## 🚗 Planejamento na prática

Considere a pergunta:

> Devo comprar ou alugar um carro para meu trajeto diário de 80 km?

### Sem planejamento

Um agente simples pode responder:

```text id="q2m7vx"
Alugar oferece pagamentos mensais menores, enquanto comprar
permite ser proprietário do veículo e dirigir sem limite de quilometragem.

Para um trajeto diário de 80 km, comprar pode ser melhor devido
às possíveis limitações de quilometragem do aluguel.
```

Embora a resposta seja plausível, ela pode não considerar:

* 💰 Custo total ao longo do tempo
* 📊 Impacto financeiro
* 🛣️ Quilometragem anual
* ⚖️ Comparação entre cenários
* ⚠️ Custos e riscos adicionais

---

### Com `BuiltInPlanner`

Com planejamento, o agente pode estruturar a análise antes de apresentar a recomendação:

```text id="r3m9ks"
Problema
   ↓
Cálculo da quilometragem
   ↓
Identificação das restrições
   ↓
Comparação de alternativas
   ↓
Análise financeira
   ↓
Avaliação de riscos
   ↓
Recomendação
```

O planejamento acrescenta:

* 🔢 Raciocínio quantificado
* ⚖️ Análise multifatorial
* 🔄 Comparação de cenários
* 💰 Avaliação de custos
* 🎯 Recomendações contextualizadas

---

## 📌 Uma observação importante sobre as instruções

O uso do `BuiltInPlanner` reduz a necessidade de colocar todo o processo de raciocínio manualmente na instrução.

Uma instrução simples como:

```python id="x1p7qc"
instruction="Ajude os usuários a tomar decisões"
```

pode ser suficiente para que o planner aplique uma abordagem mais estruturada.

O planejamento é controlado principalmente por:

```text id="s6f2qa"
BuiltInPlanner
      +
ThinkingConfig
      ↓
Raciocínio estruturado
```

Isso evita depender exclusivamente de instruções como:

> "Divida o problema em etapas, analise os prós e contras, avalie as restrições..."

---

## 🔧 Parâmetro `planner`

O parâmetro é utilizado no **singular**:

```python id="c4v8zs"
agent = LlmAgent(
    model="gemini-2.5-flash",
    planner=BuiltInPlanner(...)
)
```

### Principais características

* 🐍 Disponível para Python
* 🧠 Utiliza os recursos de raciocínio do modelo
* 🔢 Adequado para problemas de múltiplas etapas
* 🎛️ Permite controlar a profundidade do raciocínio

---

# 🔀 Tipos de Planner

O ADK apresenta diferentes abordagens de planejamento.

## 🟢 `BuiltInPlanner`

É indicado principalmente para modelos **Gemini com recursos nativos de raciocínio**.

```python id="v5j2na"
from google.adk.planners import BuiltInPlanner
from google.genai import types

agent = LlmAgent(
    model="gemini-2.5-flash",
    planner=BuiltInPlanner(
        thinking_config=types.ThinkingConfig(
            include_thoughts=True,
            thinking_budget=1024
        )
    )
)
```

### Características

* 🧠 Utiliza o raciocínio nativo do Gemini
* 🎛️ Permite controlar o `thinking_budget`
* 🔎 Permite visualizar o raciocínio com `include_thoughts=True`
* ⚡ Adequado para problemas complexos

---

## 🟠 `PlanReActPlanner`

É uma alternativa principalmente para modelos que **não possuem recursos nativos de raciocínio**.

```python id="e8w4kc"
from google.adk.planners import PlanReActPlanner

agent = LlmAgent(
    model="your-model",
    planner=PlanReActPlanner()
)
```

Ele utiliza uma estrutura explícita:

```text id="y6k9tp"
PLANNING
    ↓
ACTION
    ↓
REASONING
    ↓
FINAL_ANSWER
```

Essa abordagem é especialmente útil para:

* Modelos que não possuem raciocínio integrado
* Workflows com uso intensivo de ferramentas
* Processos que exigem fases explícitas
* Necessidade de uma estrutura de saída previsível

---

## 📊 `BuiltInPlanner` x `PlanReActPlanner`

| Característica      | `BuiltInPlanner`     | `PlanReActPlanner`     |
| ------------------- | -------------------- | ---------------------- |
| Principal uso       | Modelos Gemini       | Outros modelos         |
| Raciocínio nativo   | ✅                    | ❌                      |
| Estrutura explícita | Não necessariamente  | ✅                      |
| `thinking_budget`   | ✅                    | —                      |
| `include_thoughts`  | ✅                    | —                      |
| Uso com ferramentas | ✅                    | ✅                      |
| Foco                | Raciocínio integrado | Planejamento explícito |

📌 **Neste curso, o foco está no `BuiltInPlanner`**, pois os exemplos utilizam modelos Gemini.

---

## 🎯 Quando utilizar planejamento?

### ✅ Use planejamento para:

* Problemas de múltiplas etapas
* Tomada de decisões complexas
* Análise de prós e contras
* Estratégias de negócios
* Solução de problemas
* Depuração do comportamento do agente

### ❌ Evite planejamento para:

* Perguntas simples
* Consultas factuais rápidas
* Tarefas de uma única etapa
* Respostas que precisam ser extremamente rápidas

Exemplo adequado:

```python id="m8x4qd"
strategic_agent = LlmAgent(
    model="gemini-2.5-flash",
    planner=BuiltInPlanner(
        thinking_config=types.ThinkingConfig(
            include_thoughts=True,
            thinking_budget=2048
        )
    ),
    instruction="Analise estratégias de negócios e apresente recomendações"
)
```

Exemplo em que o planner é desnecessário:

```python id="u7k3wp"
simple_agent = LlmAgent(
    model="gemini-2.5-flash",
    instruction="Cumprimente os usuários de modo afetuoso"
)
```

---

## 🐛 Raciocínio visível para depuração

Durante o desenvolvimento, `include_thoughts=True` pode ser utilizado para observar o processo de raciocínio disponibilizado pelo modelo:

```python id="n4z6vc"
debug_agent = LlmAgent(
    model="gemini-2.5-flash",
    planner=BuiltInPlanner(
        thinking_config=types.ThinkingConfig(
            include_thoughts=True,
            thinking_budget=1024
        )
    ),
    instruction="Ajude os usuários a depurar problemas sistematicamente"
)
```

Isso pode ajudar a identificar:

* Como o problema foi dividido
* Quais fatores foram considerados
* Onde uma análise pode estar falhando
* Como a recomendação final foi construída

---

## 🛠️ Exemplo prático — Strategic Problem Solver

### 1. Criando o projeto

```bash id="r9h2kf"
adk create problem_solver
cd problem_solver
```

### 2. Criando o agente

```python id="z3q8wm"
from google.adk.agents import LlmAgent
from google.adk.planners import BuiltInPlanner
from google.genai import types

root_agent = LlmAgent(
    model="gemini-2.5-flash",
    name="strategic_problem_solver",
    description="Resolve problemas complexos utilizando planejamento",
    instruction="""
Você é um solucionador de problemas estratégicos.

Para problemas complexos:
1. Entenda e divida o problema em componentes.
2. Analise diferentes abordagens e seus prós e contras.
3. Desenvolva uma estratégia de solução.
4. Apresente recomendações claras e práticas.

Considere:
- Implicações de curto e longo prazo.
- Casos extremos.
- Possíveis riscos.
- Estratégias de mitigação.

Seja detalhista, analítico e sistemático.
""",
    planner=BuiltInPlanner(
        thinking_config=types.ThinkingConfig(
            include_thoughts=True,
            thinking_budget=2048
        )
    )
)
```

### 3. Executando

```bash id="c6y5zr"
adk web
```

---

## 🧪 Testes realizados

### Teste 1 — Problema complexo

**Entrada:**

```text
Como devo me preparar para uma transição de carreira
de engenharia de software para gestão de produtos
nos próximos 12 meses?
```

Com planejamento, o agente deve:

* Analisar a lacuna de competências
* Identificar habilidades transferíveis
* Definir prioridades
* Considerar diferentes estratégias
* Organizar a transição em fases
* Produzir um roteiro estruturado

Exemplo de estrutura:

```text
1–3 meses → Fundamentos de Product Management
4–6 meses → Desenvolvimento de habilidades
7–9 meses → Experiência e visibilidade
10–12 meses → Busca ativa de oportunidades
```

---

### Teste 2 — Pergunta simples

**Entrada:**

```text
Qual é a capital da França?
```

Mesmo utilizando planejamento, perguntas simples devem continuar recebendo **respostas diretas**, sem necessidade de uma análise extensa.

📌 O agente deve adaptar o esforço à complexidade da tarefa.

---

### Teste 3 — Análise de alternativas

**Entrada:**

```text
Devo alugar ou comprar uma casa em São Francisco
se meus planos são morar lá por 3–5 anos?
```

O planejamento permite analisar:

* 💰 Custos financeiros
* 🏠 Entrada e pagamentos
* 📈 Formação de patrimônio
* 🔄 Custo de oportunidade
* 📊 Condições do mercado
* ⏳ Horizonte de 3–5 anos
* ⚖️ Cenários de compra e aluguel

---

## 📈 Impacto do planejamento

```text
                 Sem Planner
                    │
                    ▼
             Resposta imediata
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
    Análise superficial   Fatores ignorados


                 Com Planner
                    │
                    ▼
             Decomposição
                    ↓
                Análise
                    ↓
             Alternativas
                    ↓
               Avaliação
                    ↓
             Planejamento
                    ↓
             Recomendação
```

---

### 💡 Principais aprendizados

1. O parâmetro **`planner`** habilita o planejamento em múltiplas etapas.
2. O **`BuiltInPlanner`** aproveita os recursos de raciocínio integrados dos modelos Gemini.
3. `ThinkingConfig` controla o comportamento do raciocínio.
4. `thinking_budget` define o orçamento de tokens destinado ao raciocínio.
5. `include_thoughts=True` permite visualizar o raciocínio disponibilizado pelo modelo para fins de desenvolvimento e depuração.
6. Problemas complexos se beneficiam de planejamento estruturado.
7. Perguntas simples não precisam necessariamente de planejamento.
8. `BuiltInPlanner` é especialmente indicado para modelos Gemini com suporte a raciocínio integrado.
9. `PlanReActPlanner` utiliza uma estrutura explícita de planejamento e ação, sendo útil principalmente para modelos sem raciocínio nativo.
10. O planejamento deve ser aplicado de acordo com a **complexidade e os requisitos da tarefa**.

### 🔑 Conceitos-chave

`BuiltInPlanner` · `PlanReActPlanner` · `ThinkingConfig` · `thinking_budget` · `include_thoughts` · `planner` · `Reasoning` · `Planning` · `Problem Decomposition` · `Multi-Step Reasoning` · `Gemini`
