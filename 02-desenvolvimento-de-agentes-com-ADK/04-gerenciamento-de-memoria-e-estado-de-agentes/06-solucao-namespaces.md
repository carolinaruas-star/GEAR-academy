# 🧠 Gerenciamento de Memória e Estado de Agentes — Namespaces de estado

## 📚 Contexto

Até aqui, aprendemos que:

* `session.state` permite armazenar informações;
* `output_key` salva automaticamente respostas no estado;
* `{var}` permite utilizar valores do estado nas instruções.

Agora surge uma questão fundamental:

> **Por quanto tempo cada informação deve permanecer disponível?**

A solução do ADK é utilizar **namespaces de estado**, que definem o escopo e o ciclo de vida das informações.

---

## 💡 A solução: namespaces de estado

O ADK oferece quatro escopos principais:

| Namespace    | Prefixo    | Persistência             | Escopo            |
| ------------ | ---------- | ------------------------ | ----------------- |
| ⚡ Temporário | `temp:`    | Apenas a invocação atual | Turno atual       |
| 💬 Sessão    | *(nenhum)* | Durante a sessão         | Conversa atual    |
| 👤 Usuário   | `user:`    | Entre sessões            | Mesmo usuário     |
| 🌐 App       | `app:`     | Global                   | Todos os usuários |

### 📌 Sintaxe

```python id="g2m5wv"
state["temp:var"]   # Temporário
state["var"]        # Sessão
state["user:var"]   # Usuário
state["app:var"]    # Aplicação
```

---

## ⚡ 1. Estado temporário — `temp:`

O namespace `temp:` armazena informações **somente durante a invocação atual**.

Uma invocação corresponde ao processamento completo de uma entrada do usuário até a resposta final do agente.

```text id="9kjm4f"
Usuário envia mensagem
        ↓
[ INVOCATION START ]
        ↓
Agente processa
        ↓
Agente responde
        ↓
[ INVOCATION END ]
        ↓
temp: é descartado
```

### Exemplo

```python id="0qpx3e"
agent = LlmAgent(
    instruction="Process request. Store step: {temp:current_step?starting}",
    output_key="temp:processing_result"
)
```

Após o término do turno:

```python id="0s3v8r"
session.state.get("temp:current_step")
```

retorna `None`, pois o valor foi descartado.

### ✅ Quando usar

* etapas intermediárias de processamento;
* flags temporárias;
* cálculos intermediários;
* dados compartilhados entre ferramentas durante uma única invocação.

### ❌ Não utilizar para

Informações necessárias em vários turnos.

---

## 💬 2. Estado da sessão — sem prefixo

O estado sem prefixo pertence à **sessão atual**.

```python id="v2n5lq"
session.state["conversation_topic"] = "refunds"
```

O valor permanece disponível enquanto a sessão estiver ativa:

```text id="x3c8q1"
Sessão
│
├── Turno 1 → topic = refunds
├── Turno 2 → topic = refunds
├── Turno 3 → topic = refunds
│
└── Sessão encerrada → estado descartado
```

### Exemplo

```python id="w1gq8k"
agent = LlmAgent(
    instruction="Current topic: {conversation_topic?none}",
    output_key="conversation_topic"
)
```

### ✅ Quando usar

* 💬 tópico da conversa;
* 🔢 contador de turnos;
* 🛒 carrinho da sessão;
* 📋 progresso de uma tarefa;
* 🚦 flags específicas da conversa.

### ❌ Não utilizar para

Informações que precisam estar disponíveis em várias conversas do mesmo usuário.

> **Observação:** a persistência entre reinicializações depende do `SessionService`. Com serviços persistentes, o estado da sessão pode ser mantido de forma persistente.

---

## 👤 3. Estado do usuário — `user:`

O namespace `user:` está associado ao `user_id` e pode ser compartilhado entre diferentes sessões do mesmo usuário dentro do mesmo aplicativo.

```python id="x4d9ps"
session.state["user:language"] = "Spanish"
session.state["user:theme"] = "dark"
```

O comportamento esperado é:

```text id="z8r5km"
Usuário
│
├── Sessão 1
│   ├── user:language = Spanish
│   └── user:theme = dark
│
├── Sessão termina
│
└── Sessão 2
    ├── user:language = Spanish
    └── user:theme = dark
```

### Exemplo

```python id="n4kq7x"
agent = LlmAgent(
    instruction="""
    Preferências do usuário:
    - Idioma: {user:language?English}
    - Tema: {user:theme?light}

    Responda em {user:language?English}.
    """
)
```

### ✅ Quando usar

* 🌎 preferência de idioma;
* 🎨 tema da interface;
* ⭐ nível de assinatura;
* 👤 informações do perfil;
* ⚙️ preferências pessoais.

### ❌ Não utilizar para

Dados específicos da conversa atual.

> **Observação:** a persistência entre sessões e reinicializações depende do serviço de sessão utilizado. Serviços persistentes, como Database ou Vertex AI, permitem persistência durável.

---

## 🌐 4. Estado do app — `app:`

O namespace `app:` representa informações compartilhadas pelo aplicativo.

```python id="m8tq2v"
session.state["app:version"] = "2.0"
session.state["app:api_url"] = "https://api.example.com"
```

Essas informações podem ser utilizadas por diferentes usuários e sessões dentro do mesmo `app_name`.

```text id="p6w2zq"
Aplicação
│
├── Usuário A → app:version = 2.0
├── Usuário B → app:version = 2.0
└── Usuário C → app:version = 2.0
```

### Exemplo

```python id="c9v5nk"
agent = LlmAgent(
    instruction="""
    Você está usando a versão {app:version?1.0}.
    Endpoint: {app:api_url?not set}
    Features: {app:features?basic}
    """
)
```

### ✅ Quando usar

* 🌐 endpoints de API;
* 🚩 feature flags;
* ⚙️ configurações globais;
* 📦 versão do aplicativo;
* 🤖 modelos ou configurações compartilhadas.

### ❌ Não utilizar para

Dados específicos de usuários ou de uma sessão.

---

## 🧪 Aplicação prática — Namespace Demo

O projeto demonstra os quatro namespaces em um único agente.

### Criar o projeto

```bash id="r7p3kx"
adk create namespace_demo
cd namespace_demo
```

### Configurando os estados

```python id="f5n8qm"
session.state["app:name"] = "Namespace Demo"
session.state["app:version"] = "2.0"

session.state["user:theme"] = "dark"

session.state["topic"] = "state management"

session.state["temp:step"] = "initialization"
```

O agente pode acessar todos eles utilizando modelagem:

```python id="u2c7vd"
instruction="""
App: {app:name?Namespace Demo}
Versão: {app:version?1.0}

Tema do usuário: {user:theme?not set}

Tópico: {topic?not set}

Etapa atual: {temp:step?not set}
"""
```

---

## 🧪 Testes de persistência

### Teste 1 — Primeiro turno

Antes da execução:

```text
temp:step → initialization
topic → state management
user:theme → dark
app:version → 2.0
```

Após o turno:

```text
temp:step → None ❌
topic → state management ✅
user:theme → dark ✅
app:version → 2.0 ✅
```

### Teste 2 — Segundo turno na mesma sessão

```text
temp:step → None ❌
topic → state management ✅
user:theme → dark ✅
app:version → 2.0 ✅
```

O estado da sessão continua disponível, enquanto o estado temporário já foi descartado.

### Teste 3 — Nova sessão do mesmo usuário

```text
topic → None ❌
user:theme → dark ✅
app:version → 2.0 ✅
```

Isso demonstra a diferença entre os escopos:

* `topic` pertence à sessão anterior;
* `user:theme` pertence ao usuário;
* `app:version` pertence à aplicação.

---

## 🌳 Árvore de decisão

A principal regra para escolher o namespace é:

```text id="w9x4jc"
Quanto tempo os dados precisam persistir?
│
├── ⚡ Apenas AGORA / turno atual?
│      └── temp:
│          Ex.: temp:processing_step
│
├── 💬 Apenas nesta CONVERSA?
│      └── Estado da sessão
│          Ex.: conversation_topic
│
├── 👤 Em TODAS as conversas deste USUÁRIO?
│      └── user:
│          Ex.: user:language
│
└── 🌐 Para TODOS os usuários?
       └── app:
           Ex.: app:api_url
```

---

## 🎯 Prática recomendada

> **Use sempre o escopo mais restrito possível.**

Isso significa:

```text id="a6m2vk"
temp:   → processamento temporário
session → contexto da conversa
user:   → preferências do usuário
app:    → configurações globais
```

Dessa forma, os dados permanecem disponíveis **somente pelo tempo e no contexto em que são realmente necessários**.

---

## 🔄 Namespaces + modelagem

Todos os namespaces podem ser utilizados com `{var}`:

```python id="k7q4nb"
instruction="""
App: {app:name?MyApp}
Usuário: {user:language?English}
Tópico: {topic?none}
Etapa: {temp:step?start}
"""
```

O agente consegue combinar informações de diferentes escopos em uma única instrução dinâmica.

---

## 🔑 Conceitos-chave

| Conceito        | Função                                   |
| --------------- | ---------------------------------------- |
| `temp:`         | Estado temporário da invocação           |
| *(sem prefixo)* | Estado da sessão                         |
| `user:`         | Estado compartilhado pelo usuário        |
| `app:`          | Estado global da aplicação               |
| `{var}`         | Injeta valores do estado nas instruções  |
| Escopo          | Define onde o dado está disponível       |
| Persistência    | Define por quanto tempo o dado é mantido |

---

## 💡 Principal aprendizado

> **Namespaces permitem controlar o ciclo de vida do estado, garantindo que cada informação seja armazenada no escopo adequado.**

O objetivo não é simplesmente **guardar mais dados**, mas armazená-los de forma organizada, segura e coerente com sua finalidade.

### 📌 Regra de ouro

**Quanto mais amplo o escopo, maior deve ser a justificativa para utilizá-lo.**

```text
temp: → turno
   ↓
session → conversa
   ↓
user: → usuário
   ↓
app: → aplicação
```

Essa estrutura permite construir agentes mais **contextuais, eficientes e previsíveis**, evitando persistência desnecessária ou mistura de informações entre diferentes contextos.
