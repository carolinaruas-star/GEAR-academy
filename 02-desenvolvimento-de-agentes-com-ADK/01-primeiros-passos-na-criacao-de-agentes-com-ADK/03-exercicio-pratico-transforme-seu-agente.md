# 🧪 Exercício prático — Transformando o agente

Neste exercício, o agente genérico criado no módulo 1 será personalizado para atuar como um **orientador especializado em matemática e álgebra**.

A prática demonstra como `name`, `description` e principalmente `instruction` influenciam a identidade e o comportamento do agente.

---

## 🔹 1. Agente inicial

O agente criado no módulo 1 possuía uma configuração genérica:

```python
from google.adk.agents.llm_agent import Agent

root_agent = Agent(
    model="gemini-2.5-flash",
    name="root_agent",
    description="Um agente assistente colaborativo.",
    instruction="Você é um assistente colaborativo."
)
```

O objetivo agora é transformá-lo em um agente especializado.

---

## 🏷️ 2. Atualizando o nome

Primeiro, o `name` é alterado para representar melhor a finalidade do agente:

```python
name="math_tutor_agent"
```

O nome interno passa a identificar claramente que o agente é especializado em orientação matemática.

---

## 📝 3. Definindo a descrição

Em seguida, o `description` é especificado:

```python
description="Ajuda estudantes a aprender álgebra com orientação pelas etapas de solução de problemas."
```

Agora outros agentes, em uma arquitetura multiagente, conseguem entender que este agente é especializado em **álgebra e orientação de estudantes**.

---

## 🎯 4. Definindo o comportamento

Por fim, a `instruction` é personalizada:

```python
instruction="Você é um orientador de matemática paciente. Ajude os estudantes a resolver problemas de álgebra."
```

Essa instrução define:

* 🎓 **Papel:** orientador de matemática
* 😊 **Personalidade:** paciente
* ➗ **Tarefa:** ajudar com problemas de álgebra

---

## 🤖 Agente final

A configuração completa fica:

```python
from google.adk.agents.llm_agent import Agent

root_agent = Agent(
    model="gemini-2.5-flash",
    name="math_tutor_agent",
    description="Ajuda estudantes a aprender álgebra com orientação pelas etapas de solução de problemas.",
    instruction="Você é um orientador de matemática paciente. Ajude os estudantes a resolver problemas de álgebra."
)
```

📌 O código deve ser salvo no arquivo `agent.py` dentro do diretório `my_first_agent`.

---

# 🌐 Testando o agente personalizado

Depois de salvar as alterações, o agente pode ser testado através da interface web do ADK.

### ▶️ Iniciar o servidor

No diretório `my_first_agent` ou em seu diretório pai:

```bash
adk web
```

O ADK iniciará um servidor local, normalmente em:

```text
http://localhost:8000
```

A interface web permite selecionar o agente e conversar com ele.

---

## 💬 Testes sugeridos

### Teste 1 — Problema de álgebra

**Pergunta:**

```text
Qual é o resultado de 2x + 5 = 13?
```

Espera-se que o agente:

* ➗ Ajude a resolver o problema
* 🎓 Atue como orientador de matemática
* 😊 Mantenha uma postura paciente

### Teste 2 — Dificuldade com álgebra

**Pergunta:**

```text
Não entendo nada de álgebra.
```

Espera-se que o agente:

* 😊 Responda de maneira paciente
* 📚 Explique conceitos de álgebra
* 💪 Mantenha uma postura motivadora

---

# 🔄 Comparando os agentes

A principal diferença está na instrução utilizada.

### 🤖 Agente genérico

```python
instruction="Você é um assistente colaborativo."
```

Características:

* Respostas genéricas
* Nenhuma especialização de domínio
* Comportamento pouco direcionado

### 🧮 Agente personalizado

```python
instruction="Você é um orientador de matemática paciente. Ajude os estudantes a resolver problemas de álgebra."
```

Características:

* 🎓 Foco em matemática
* 😊 Postura paciente
* ➗ Especialização em álgebra
* 📚 Orientação voltada ao ensino

💡 **Conclusão:** instruções simples, claras e direcionadas já podem modificar significativamente o comportamento do agente.

---

## 🛠️ Solução de problemas

### ❌ O agente não aparece na interface

Verifique se o comando foi executado no diretório correto.

Uma alternativa é especificar diretamente o projeto:

```bash
adk web my_first_agent
```

### ❌ O agente continua respondendo de forma genérica

Verifique se:

1. 💾 As alterações foram salvas no `agent.py`
2. 🛑 O servidor foi interrompido com `Ctrl+C`
3. 🔄 O `adk web` foi iniciado novamente

É necessário reiniciar o servidor para que as alterações no código sejam detectadas.

---

# 🎯 Principais aprendizados

### Parâmetros

* 🧠 `model` → modelo responsável pelo raciocínio
* 🏷️ `name` → identifica o agente
* 📝 `description` → informa sua finalidade
* 🎯 `instruction` → orienta seu comportamento

### Boas práticas

✅ Criar instruções simples e direcionadas
✅ Definir claramente o papel e a tarefa
✅ Especificar o que o agente faz
✅ Incluir características de personalidade para orientar o tom
✅ Testar as mudanças utilizando `adk web`

### ⚠️ Erros comuns

❌ Usar instruções vagas, como `"seja colaborativo"`
❌ Confundir `description` com `instruction`
❌ Esquecer de atribuir o agente à variável `root_agent`
❌ Utilizar nomes genéricos ou pouco claros

---