# 🧠 Gerenciamento de Memória e Estado de Agentes — O desafio: usar o estado nas instruções

## 📚 Contexto

No capítulo anterior, foi introduzido o **estado da sessão**, permitindo que o agente armazene informações importantes em `session.state`.

Agora surge uma nova necessidade: **como fazer o agente utilizar esses valores armazenados para adaptar suas respostas?**

### 📌 O que já é possível fazer

O estado pode armazenar informações extraídas pelo agente:

```python
from google.adk.agents import LlmAgent

agent = LlmAgent(
    instruction="Extract the user's name",
    output_key="user_name"
)
```

Após a execução:

```python
session.state["user_name"]
```

pode conter:

```text
Alex
```

Também é possível acessar o valor programaticamente:

```python
session.state.get("user_name")
```

---

## ❌ O problema

Salvar informações no estado não é suficiente. O agente também precisa **utilizar esses valores em suas instruções**.

Imagine que o estado contenha:

```python
session.state["user_name"] = "Alex"
session.state["user_language"] = "Espanhol"
```

Uma instrução genérica como:

```python
agent = LlmAgent(
    instruction="Responder ao usuário"
)
```

não informa ao agente que ele deve:

* utilizar o nome armazenado;
* responder no idioma armazenado;
* adaptar seu comportamento com base no contexto da sessão.

### 🔴 O desafio

Queremos que a instrução seja **dinâmica**, utilizando automaticamente os valores presentes no estado, sem precisar codificar diretamente:

```text
Responder a Alex em espanhol
```

Isso seria inadequado porque os valores podem mudar a cada sessão ou usuário.

---

## 💡 O que precisamos

É necessária uma forma de **injetar valores do `session.state` diretamente nas instruções do agente**.

A ideia é permitir que a instrução utilize referências como:

```text
user_name
user_language
```

e que, durante a execução, esses valores sejam substituídos pelos dados existentes no estado.

Assim, o mesmo agente pode adaptar seu comportamento para diferentes usuários e contextos.

### 🔄 Conceito

```text
session.state
      ↓
Valores armazenados
      ↓
Instrução dinâmica
      ↓
Agente adapta sua resposta
```

---

## 🔑 Principal aprendizado

> **O estado da sessão armazena o contexto, mas o agente precisa de uma forma de acessar esse contexto dentro das próprias instruções para agir de maneira dinâmica.**

O próximo capítulo apresenta a solução para esse problema: **modelagem de estado com `{var}`**.
