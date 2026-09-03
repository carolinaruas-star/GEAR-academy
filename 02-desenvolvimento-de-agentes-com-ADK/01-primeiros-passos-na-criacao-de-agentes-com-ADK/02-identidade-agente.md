# 🤖 Definindo a identidade do agente

Neste módulo, o foco é entender como **personalizar a identidade, finalidade e comportamento de um agente no ADK**.

O agente criado no módulo anterior utiliza:

```python
from google.adk.agents.llm_agent import Agent

root_agent = Agent(
    model="gemini-2.5-flash",
    name="root_agent",
    description="Um agente assistente colaborativo.",
    instruction="Você é um assistente colaborativo."
)
```

A configuração do agente é baseada principalmente em **quatro parâmetros**: `model`, `name`, `description` e `instruction`.

---

## 🧠 Os 4 parâmetros principais

### 1️⃣ `model` — O cérebro do agente

Define o **LLM responsável pelo raciocínio e pela tomada de decisões**.

```python
model="gemini-2.5-flash"
```

O modelo influencia:

* 🧠 Capacidade e inteligência do agente
* ⚡ Velocidade das respostas
* 💰 Custo por solicitação

Exemplos apresentados:

* `gemini-2.5-flash` → rápido e eficiente para a maioria das tarefas
* `gemini-2.5-pro` → maior capacidade para tarefas e raciocínios complexos

📌 **É obrigatório**: um agente precisa de um modelo para funcionar.

---

### 2️⃣ `name` — Identidade do agente

Define um **identificador único** utilizado internamente pelo ADK.

```python
name="math_tutor_agent"
```

É importante para:

* 🔎 Identificação interna
* 🤝 Delegação em sistemas multiagente
* 📝 Registros e depuração

### ✅ Boas práticas

Use nomes:

* Em letras minúsculas
* Com `_` para separar palavras
* Descritivos

```text
customer_support_agent
data_analysis_agent
math_tutor_agent
```

Evite:

```text
user
myAgent
```

📌 **Também é obrigatório**.

---

### 3️⃣ `description` — Finalidade do agente

É uma descrição resumida sobre **o que o agente faz**.

```python
description="Ajuda estudantes a aprender álgebra."
```

Seu principal objetivo aparece em **sistemas multiagente**: outros agentes podem utilizar essa descrição para decidir se uma tarefa deve ser encaminhada para aquele agente.

Boas descrições são específicas:

```text
"Processa as consultas de faturamento dos clientes e os pagamentos."
```

Em vez de algo genérico:

```text
"Agente de faturamento"
```

📌 É **opcional**, mas especialmente útil em arquiteturas multiagente.

---

### 4️⃣ `instruction` — Comportamento do agente

Define **como o agente deve agir e responder**.

```python
instruction="""
Você é um orientador de matemática paciente.
Ajude os estudantes a resolver problemas de álgebra.
"""
```

A instrução pode definir:

* 🎭 Personalidade e estilo de comunicação
* 🎯 Objetivo principal
* 🚧 Limites e restrições
* 🛠️ Quando e como utilizar ferramentas
* 📋 Formato das respostas

Segundo o material, `instruction` é um dos elementos mais importantes para definir o comportamento do agente.

### 💡 Boas práticas

Instruções eficazes devem ser:

* **Claras e específicas**
* **Bem estruturadas**, utilizando Markdown quando necessário
* **Com exemplos (few-shot)** em tarefas mais complexas
* **Claras sobre o uso de ferramentas**

---

## 🔀 `description` × `instruction`

Essa é uma diferença fundamental:

| Parâmetro     | Quem utiliza?       | Pergunta principal                          |
| ------------- | ------------------- | ------------------------------------------- |
| `description` | 🤖 Outros agentes   | **"Devo encaminhar esta tarefa para ele?"** |
| `instruction` | 🧠 O próprio agente | **"Como devo me comportar?"**               |

### Exemplo

```python
billing_agent = Agent(
    model="gemini-2.5-flash",
    name="billing_agent",

    description="Processa as consultas de faturamento dos clientes e os pagamentos",

    instruction="""
    Você é especialista em faturamento.

    Quando ajudar os clientes:
    1. Tenha empatia e paciência
    2. Explique as cobranças com clareza
    3. Use a ferramenta billing_lookup para verificar os detalhes
    4. Nunca prometa reembolsos sem aprovação do gerente

    Mantenha sempre um tom profissional e solícito.
    """
)
```

Nesse cenário:

* `description` informa **qual é a finalidade do agente**.
* `instruction` determina **como ele deve executar sua função**.

---

## 🌳 O que é `root_agent`?

O ADK utiliza uma convenção importante: o agente principal deve estar associado a uma variável chamada:

```python
root_agent
```

Exemplo:

```python
root_agent = Agent(
    model="gemini-2.5-flash",
    name="root_agent",
    description="Um agente assistente colaborativo.",
    instruction="Você é um assistente colaborativo."
)
```

O `root_agent` funciona como o **ponto de entrada** que as ferramentas do ADK procuram para descobrir e executar o agente.

### ⚠️ `root_agent` × `name`

Os dois não são a mesma coisa.

```python
my_specialized_agent = Agent(
    model="gemini-2.5-flash",
    name="math_tutor_agent",
    description="Ajuda estudantes com álgebra",
    instruction="Você é um orientador de matemática paciente."
)

root_agent = my_specialized_agent
```

Aqui:

* `math_tutor_agent` → nome interno do agente no ADK
* `root_agent` → variável utilizada pelo ADK para localizar o agente principal

📌 **Regra:** o agente principal deve ser atribuído à variável `root_agent`.

---

## ✍️ Como criar uma boa instrução?

Para este módulo, uma instrução simples já é suficiente:

```python
instruction="""
Você é um orientador de matemática paciente.
Ajude os estudantes a resolver problemas de álgebra.
"""
```

Essa instrução define três elementos:

| Elemento         | Definição                       |
| ---------------- | ------------------------------- |
| 🎭 Papel         | Orientador de matemática        |
| 💬 Personalidade | Paciente                        |
| 🎯 Tarefa        | Ajudar com problemas de álgebra |

No curso seguinte, serão apresentadas técnicas mais avançadas, como:

* Estruturas de instrução com múltiplas seções
* Definição de persona e limites
* Exemplos *few-shot*
* Padrões de instruções para produção

---

## 🧩 Estrutura mental

Uma forma simples de memorizar:

```text
                 🤖 AGENTE
                    │
        ┌───────────┼───────────┐
        ↓           ↓           ↓
      🧠 Model    🏷️ Name    📝 Description
        │                       │
     "Pensa"              "O que faz?"
        │
        ↓
   📋 Instruction
        │
   "Como agir?"
```

### 🎯 Resumindo

* 🧠 **`model`** → define o cérebro/raciocínio
* 🏷️ **`name`** → identifica o agente
* 📝 **`description`** → explica sua finalidade para outros agentes
* 📋 **`instruction`** → define seu comportamento
* 🌳 **`root_agent`** → variável que o ADK utiliza como ponto de entrada

> **Modelo + identidade + finalidade + instruções = agente configurado para uma tarefa específica.**