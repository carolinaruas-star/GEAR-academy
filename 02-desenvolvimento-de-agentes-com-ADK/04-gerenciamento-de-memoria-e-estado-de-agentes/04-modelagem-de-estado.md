# 🧠 Gerenciamento de Memória e Estado de Agentes — Modelagem de estado com `{var}`

## 📚 Contexto

No capítulo anterior, vimos que o `session.state` permite armazenar informações, mas ainda faltava uma forma de **utilizar esses valores diretamente nas instruções do agente**.

A solução apresentada pelo ADK é a **modelagem de estado**, utilizando a sintaxe `{var}`.

---

## 💡 A solução: modelagem de estado

O ADK permite inserir uma chave do estado diretamente na instrução:

```python
instruction="Olá, {user_name}, como posso te ajudar?"
```

Antes de enviar a instrução ao LLM, o framework:

1. identifica `{user_name}`;
2. consulta `session.state["user_name"]`;
3. substitui o marcador pelo valor atual;
4. envia a instrução resolvida ao LLM.

### 🔄 Exemplo

```python
session.state["user_name"] = "Alex"

agent = LlmAgent(
    instruction="Olá, {user_name}, como posso te ajudar hoje?"
)
```

O LLM recebe:

```text
Olá, Alex, como posso te ajudar hoje?
```

Assim, **a mesma instrução pode se adaptar a diferentes sessões e usuários sem alterar o código do agente**.

---

## 🔑 Sintaxe `{var}`

A sintaxe básica é:

```text
{key}
```

Exemplo:

```python
session.state["topic"] = "quantum computing"

agent = LlmAgent(
    instruction="Forneça uma visão geral de {topic}"
)
```

A instrução será resolvida para:

```text
Forneça uma visão geral de quantum computing
```

### 📌 Características

* A substituição ocorre antes de cada invocação do agente.
* O valor utilizado é o valor **atual** armazenado no estado.
* Pode ser utilizada qualquer chave de estado.
* A correspondência é **sensível a maiúsculas e minúsculas**:

  * `{name}` ≠ `{Name}`

---

## 🛡️ Modelagem opcional

Quando uma variável pode não existir no estado, é possível utilizar `?`.

### `{var?}` — valor vazio

```python
instruction="Olá, {user_name?}"
```

Se `user_name` não existir, o marcador será resolvido como uma string vazia.

### `{var?default}` — valor padrão

```python
instruction="Olá, {user_name?Convidado}"
```

Se `user_name` não existir:

```text
Olá, Convidado
```

### `{var?texto}` — conteúdo condicional

Também é possível utilizar a variável para inserir um bloco de texto somente quando ela estiver disponível:

```text
{premium_user?Você tem acesso aos recursos premium.}
```

Isso permite criar instruções que se adaptam ao estado disponível.

---

## ⚙️ Fluxo de execução

```text
┌──────────────────────────┐
│      session.state       │
│                          │
│ user_name = "Alex"       │
│ topic = "Computação..."  │
└────────────┬─────────────┘
             ↓
┌──────────────────────────┐
│   Instrução do agente    │
│                          │
│ Olá, {user_name}.        │
│ Vamos falar sobre        │
│ {topic}.                 │
└────────────┬─────────────┘
             ↓
       ADK resolve {var}
             ↓
┌──────────────────────────┐
│    Instrução resolvida   │
│                          │
│ Olá, Alex. Vamos falar   │
│ sobre Computação...     │
└────────────┬─────────────┘
             ↓
            LLM
```

### 🎯 Insight principal

A modelagem transforma instruções estáticas em **instruções dinâmicas baseadas no estado**, sem necessidade de alterar o código do agente.

---

## 🛠️ Aplicação prática — Personalized Greeter

O projeto demonstra um agente que personaliza sua resposta utilizando informações armazenadas no estado.

### Criar o projeto

```bash
adk create personalized_greeter
cd personalized_greeter
```

### Agente

```python
from google.adk.agents import LlmAgent

root_agent = LlmAgent(
    model="gemini-2.5-flash",
    name="personalized_greeter",
    instruction="""
Você é um assistente amigável.

Informações do usuário:
- Nome: {user_name?there}
- Idioma preferido: {user_language?English}
- Assinatura: {membership_tier?free}

{membership_tier?Seu nível de assinatura é: {membership_tier}}

Cumprimente o usuário cordialmente e ofereça ajuda.
Responda em {user_language?English}.
"""
)
```

### 🧩 O que acontece

| Variável                  | Função                             |
| ------------------------- | ---------------------------------- |
| `{user_name?there}`       | Usa `there` caso o nome não exista |
| `{user_language?English}` | Usa inglês como padrão             |
| `{membership_tier?free}`  | Define um nível padrão             |
| `{membership_tier?Texto}` | Permite inserir texto condicional  |

A instrução pode, portanto, funcionar com **nenhum, parte ou todos os dados disponíveis no estado**.

---

## 🧪 Testes

O comportamento pode ser validado utilizando diferentes estados.

### Teste 1 — Sem estado

Nenhuma informação foi definida.

**Resultado esperado:** utilização dos valores padrão.

```text
Olá, tudo bem? Estou aqui para te ajudar...
```

### Teste 2 — Estado parcial

```python
session.state["user_name"] = "Alex"
```

**Resultado esperado:**

```text
Olá, Alex! Que bom te ver de novo...
```

Os demais valores continuam utilizando seus padrões.

### Teste 3 — Estado completo

```python
session.state["user_name"] = "Alex"
session.state["user_language"] = "espanhol"
session.state["membership_tier"] = "premium"
```

**Resultado esperado:**

```text
¡Hola Alex! Tu nivel de membresía es: premium.
¿En qué puedo ayudarte hoy?
```

### Estado final

```python
{
    "user_name": "Alex",
    "user_language": "Spanish",
    "membership_tier": "premium"
}
```

---

## 🔑 Conceitos-chave

| Conceito         | Função                                      |
| ---------------- | ------------------------------------------- |
| `{var}`          | Injeta um valor do estado na instrução      |
| `{var?}`         | Variável opcional, vazia quando ausente     |
| `{var?default}`  | Utiliza um valor padrão                     |
| `{var?texto}`    | Permite conteúdo condicional                |
| `session.state`  | Fonte dos valores utilizados pela modelagem |
| State templating | Torna as instruções dinâmicas e contextuais |

---

## 💡 Principal aprendizado

> **A modelagem de estado conecta o `session.state` às instruções do agente, permitindo que o comportamento seja personalizado dinamicamente com base nos dados disponíveis na sessão.**

O agente deixa de depender de instruções totalmente estáticas e passa a utilizar **contexto real da aplicação**.

---

## 📌 Quando usar

A modelagem com `{var}` é especialmente útil quando:

* 👤 o agente precisa personalizar respostas;
* 🌎 o comportamento depende de preferências do usuário;
* 📊 valores exatos da aplicação precisam ser inseridos na instrução;
* 🔄 as instruções precisam mudar conforme o estado;
* 🧠 o agente precisa ser sensível ao contexto da sessão.

### 🔗 Relação com os capítulos anteriores

```text
session.state
     ↓
Armazena informações
     ↓
{var}
     ↓
Injeta informações nas instruções
     ↓
Agente contextualizado
```

**Próxima etapa:** aprender sobre **namespaces de estado (`temp:`, `user:`, `app:`)** e como eles controlam o escopo e a persistência das informações armazenadas.
