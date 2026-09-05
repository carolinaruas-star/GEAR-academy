# 🧠 Gerenciamento de Memória e Estado de Agentes — Estado da Sessão

## 📚 Contexto

O histórico de conversas permite que o LLM compreenda informações mencionadas anteriormente, mas ele não oferece ao código da aplicação uma estrutura adequada para realizar **verificações, comparações e decisões programáticas**.

Para resolver essa limitação, o Google ADK disponibiliza o **estado da sessão (`session.state`)**.

> O estado da sessão funciona como uma coleção de pares **chave-valor** que pode ser lida e escrita programaticamente pelo código.

---

## 💡 A solução: Session State

O `session.state` é um **dicionário Python** associado à sessão do agente.

Ele permite armazenar informações que precisam ser acompanhadas durante a interação.

Alguns exemplos de utilização:

```text
"user_preference_theme": "dark"
"booking_step": "confirm_payment"
"shopping_cart_items": ["book", "pen"]
"user_is_authenticated": True
```

Dessa forma, informações importantes deixam de existir apenas como texto no histórico e passam a estar disponíveis como **dados estruturados para a aplicação**.

---

## 🧠 O que o estado permite?

### 💻 Acesso programático

O código pode acessar valores específicos diretamente:

```python
session.state.get("user_name")
```

### 💾 Salvamento automático

O parâmetro `output_key` permite salvar automaticamente a resposta final do agente no estado:

```python
output_key="user_name"
```

O resultado será armazenado como:

```python
session.state["user_name"]
```

### 🔀 Tomada de decisão

O código pode verificar valores e executar regras:

```python
if session.state.get("user_name"):
    print("O usuário forneceu o nome!")
```

### 🔄 Persistência durante a sessão

Os valores armazenados permanecem disponíveis nos diferentes turnos da **mesma sessão**.

---

# 🔎 Estado da sessão × Histórico de conversas

Os dois mecanismos possuem funções diferentes e complementares.

| Recurso                         | Histórico de conversas | Estado da sessão              |
| ------------------------------- | ---------------------- | ----------------------------- |
| Estrutura                       | Mensagens de texto     | Pares chave-valor             |
| LLM pode utilizar               | ✅ Sim                  | ✅ Sim                         |
| Código pode acessar diretamente | ❌ Não                  | ✅ Sim                         |
| Acesso programático             | ❌                      | `session.state`               |
| Principal finalidade            | Contexto da conversa   | Controle e dados estruturados |
| Uso em decisões programáticas   | ❌                      | ✅                             |

### Comparação conceitual

```text
💬 HISTÓRICO DE CONVERSAS
        │
        ├── Mensagens do usuário
        ├── Mensagens do agente
        │
        └── 🧠 LLM utiliza como contexto


🧠 ESTADO DA SESSÃO
        │
        ├── user_name → "Alex"
        ├── booking_step → "payment"
        ├── authenticated → True
        │
        └── 💻 Código pode acessar e verificar
```

### 💡 Insight

> **Histórico fornece contexto ao LLM; estado fornece dados controláveis para o código.**

---

# 💻 Acessando `session.state`

O estado pode ser acessado utilizando o atributo `state` da sessão.

```python
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.genai.types import Content, Part

session_service = InMemorySessionService()

session = session_service.create_session(
    app_name="app",
    user_id="user1"
)

runner = Runner(
    agent=my_agent,
    app_name="app",
    session_service=session_service
)

result = runner.run(
    user_id="user1",
    session_id=session.id,
    new_message=Content(
        parts=[Part(text="Olá")]
    )
)

name = session.state.get(
    "user_name",
    "Guest"
)

count = session.state.get(
    "count",
    0
)
```

## 🔐 Leitura segura com `.get()`

Uma prática importante é utilizar:

```python
session.state.get("chave", valor_padrao)
```

Por exemplo:

```python
name = session.state.get("user_name", "Guest")
count = session.state.get("count", 0)
```

Se a chave não existir, o valor padrão será retornado.

---

# 🔑 Salvando respostas com `output_key`

O `output_key` permite salvar automaticamente a resposta final do agente no estado.

```python
from google.adk.agents import LlmAgent

agent = LlmAgent(
    model="gemini-2.5-flash",
    instruction="Extraia o tópico principal. Retorne SOMENTE o tópico.",
    output_key="topic"
)
```

Após a execução:

```python
session.state.get("topic")
```

poderá retornar:

```text
quantum computing
```

### 🔄 Fluxo

```text
👤 Usuário
    │
    ▼
🤖 Agente
    │
    │ gera resposta
    ▼
🔑 output_key="topic"
    │
    ▼
🧠 session.state["topic"]
    │
    ▼
💻 Código pode acessar o valor
```

### 💡 Vantagem

Não é necessário escrever código adicional para copiar manualmente a resposta do agente para o estado.

---

# 🛠️ Aplicação prática — Name Extractor

O exercício prático consiste em criar um agente capaz de:

1. 👤 Receber uma mensagem com o nome do usuário;
2. 🔎 Extrair o nome;
3. 💾 Armazená-lo no estado;
4. 💻 Permitir que o código consulte o valor;
5. 🔄 Demonstrar que o estado continua disponível em um segundo turno.

---

## 1️⃣ Criar o projeto

```bash
adk create name_extractor
cd name_extractor
```

---

## 2️⃣ Criar o agente

```python
from google.adk.agents import LlmAgent

root_agent = LlmAgent(
    model="gemini-2.5-flash",
    name="name_extractor",
    instruction=(
        "Extract the person's name from the message. "
        "Retorna SOMENTE o nome, nada mais."
    ),
    output_key="user_name"
)
```

O ponto principal é:

```python
output_key="user_name"
```

Essa configuração faz com que a resposta do agente seja armazenada automaticamente em:

```python
state["user_name"]
```

---

# 🧪 Testando com o Runner

Para visualizar diretamente o estado, o exercício utiliza o `Runner` em vez do `adk web`.

```python
from agent import root_agent
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.genai.types import Content, Part

session_service = InMemorySessionService()

session = session_service.create_session(
    app_name="name_extractor_app",
    user_id="test_user",
    session_id="test_session"
)

runner = Runner(
    agent=root_agent,
    app_name="name_extractor_app",
    session_service=session_service
)

user_message = Content(
    parts=[
        Part(text="Olá, meu nome é Alex Johnson")
    ]
)

result = runner.run(
    user_id="test_user",
    session_id="test_session",
    new_message=user_message
)

for event in result:
    if event.is_final_response():
        print(
            f"\nAgent response: "
            f"{event.content.parts[0].text}"
        )

print("\n=== State after execution ===")
print(f"Full state: {session.state}")
print(
    f"Extracted name: "
    f"{session.state.get('user_name')}"
)

if session.state.get("user_name"):
    print("O nome foi extraído e armazenado com sucesso!")
else:
    print("Falha na extração do nome")
```

---

# 📊 Resultado esperado

Após executar:

```bash
python test_state.py
```

O resultado esperado é semelhante a:

```text
=== Running agent ===

Agent response: Alex Johnson

=== State after execution ===
Full state: {'user_name': 'Alex Johnson'}
Extracted name: Alex Johnson

O nome foi extraído e armazenado com sucesso!
```

---

# 🔄 Persistência entre turnos

O exercício também demonstra que o valor permanece disponível no segundo turno da mesma sessão.

```python
result2 = runner.run(
    user_id="test_user",
    session_id="test_session",
    new_message=Content(
        parts=[
            Part(text="Qual é o meu nome?")
        ]
    )
)

print(
    session.state.get("user_name")
)
```

Resultado:

```text
Seu nome é Alex Johnson

State still contains: Alex Johnson
```

Isso demonstra que o estado continua disponível durante os diferentes turnos da sessão.

---

# 🧩 Padrão de utilização

Um padrão comum para trabalhar com estado no ADK é:

```python
# 1. Agente salva o resultado
agent = LlmAgent(
    output_key="result"
)

# 2. Agente é executado
runner.run(...)

# 3. Código acessa o estado
if session.state.get("result"):
    # Tomar decisão programática
    pass
```

Esse padrão conecta diretamente o **resultado produzido pelo agente** à **lógica da aplicação**.

---

# 🔑 Conceitos-chave

| Conceito                     | Função                                            |
| ---------------------------- | ------------------------------------------------- |
| `session.state`              | Dicionário de estado da sessão                    |
| `output_key`                 | Salva automaticamente a resposta do agente        |
| `.get()`                     | Permite leitura segura do estado                  |
| `Runner`                     | Executa o agente e gerencia a interação           |
| `InMemorySessionService`     | Serviço de sessão utilizado no exemplo            |
| Session State                | Armazena informações acessíveis programaticamente |
| Estado persistente na sessão | Mantém valores entre diferentes turnos            |

---

# 💡 Principais aprendizados

* 🧠 O **histórico de conversas** é utilizado principalmente como contexto para o LLM.
* 💻 O **estado da sessão** permite que o código trabalhe diretamente com valores estruturados.
* 🔑 `output_key` simplifica o armazenamento automático das respostas.
* 🔎 `session.state.get()` permite consultar valores específicos.
* 🔄 O estado permanece disponível entre os turnos da mesma sessão.
* 🔀 Valores armazenados no estado podem ser utilizados em decisões programáticas.
* 🎯 O estado é especialmente útil quando a aplicação precisa **acompanhar informações, progresso ou dados extraídos da conversa**.

---

## 📌 Quando utilizar Session State?

### ✅ Utilize quando:

* O código precisa verificar valores exatos;
* É necessário tomar decisões programáticas;
* O agente precisa acompanhar o progresso de uma tarefa;
* Informações extraídas precisam ser utilizadas posteriormente;
* Preferências ou dados do usuário precisam ser mantidos durante a sessão.

### ❌ Não utilize apenas para:

* Fornecer contexto conversacional básico ao LLM.

Nesse caso, o próprio histórico da conversa já cumpre essa função.

---

## 🚀 Próxima etapa

Agora que o agente consegue **armazenar informações no estado**, o próximo passo é aprender como utilizar esses valores diretamente nas instruções.

A modelagem com **`{var}`** permitirá injetar valores do estado nas instruções do agente, criando um comportamento mais **dinâmico e personalizado**.
