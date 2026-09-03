# 🚀 Métodos de execução e implantação do agente

Nos módulos anteriores, o agente foi executado utilizando `adk web`, uma interface visual baseada no navegador.

Neste módulo, são apresentados **três métodos adicionais** para executar e integrar agentes:

* 🖥️ `adk run` → execução pelo terminal
* 🌐 `adk api_server` → execução como serviço de API
* 🐍 Execução programática → integração direta com aplicações Python

O mesmo agente pode ser utilizado em todos esses métodos. **O arquivo `agent.py` não precisa ser alterado**; o que muda é a forma de interação com o agente.

---

# 🖥️ 1. `adk run` — Execução pelo terminal

O `adk run` permite conversar com o agente diretamente pelo **terminal**, sem utilizar um navegador.

### ▶️ Como executar

Dentro do diretório do agente:

```bash
cd my_first_agent
adk run
```

Ou a partir do diretório pai:

```bash
adk run my_first_agent
```

O terminal se torna interativo:

```text
Você: Como eu resolvo x + 5 = 10?

Agente: Excelente pergunta! Vamos resolver esse problema juntos...
```

Para encerrar:

```text
Ctrl + C
```

### ✅ Quando utilizar

* Testes rápidos durante o desenvolvimento
* Fluxos de trabalho via linha de comando
* Servidores sem interface gráfica
* Scripts de teste
* Pipelines de CI/CD

### ❌ Não é a melhor opção para

* Apresentações para stakeholders
* Depuração de conversas complexas

---

# 🌐 2. `adk api_server` — Agente como API

O `adk api_server` executa o agente como um **serviço de API REST**, permitindo que outras aplicações se comuniquem com ele através de requisições HTTP.

### ▶️ Como executar

Dentro do projeto:

```bash
cd my_first_agent
adk api_server
```

Ou:

```bash
adk api_server my_first_agent
```

O servidor será iniciado localmente, normalmente em:

```text
http://localhost:8000
```

### 🔗 Testando com cURL

Uma aplicação ou terminal separado pode enviar uma requisição HTTP:

```bash
curl -X POST http://localhost:8000/your-endpoint \
-H "Content-Type: application/json" \
-d '{"message": "Qual é o resultado de 2x + 5 = 13?"}'
```

### ✅ Quando utilizar

* 🌐 Aplicações web
* 📱 Back-ends de aplicativos móveis
* 🧩 Arquiteturas de microsserviços
* 🧪 Testes de pré-produção
* ☁️ Desenvolvimento de APIs antes de uma implantação no Cloud Run

### ❌ Não é a melhor opção para

* Desenvolvimento interativo
* Testes rápidos no dia a dia

---

# 🐍 3. Execução programática com Python

Nesse método, o agente é executado **diretamente através de código Python**, proporcionando maior controle sobre sua execução.

É especialmente útil para:

* 📓 Jupyter Notebook e Google Colab
* 🐍 Aplicações Python personalizadas
* 🔄 Pipelines de processamento de dados
* 🧪 Pesquisas e experimentos
* ⚙️ Integrações personalizadas

### 🔧 Principais componentes

Uma execução programática utiliza elementos como:

```python
from google.adk.agents.llm_agent import Agent
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
```

O fluxo básico envolve:

```text
🤖 Definir o agente
       ↓
💾 Criar o serviço de sessão
       ↓
🏃 Criar o Runner
       ↓
💬 Preparar a mensagem
       ↓
⚡ Executar o agente
       ↓
📤 Obter a resposta
```

### ⚡ Execução assíncrona

A execução utiliza uma função assíncrona:

```python
async def run_agent():
    ...
```

Em **Jupyter/Colab**:

```python
await run_agent()
```

Em um **script Python**:

```python
asyncio.run(run_agent())
```

📌 A principal vantagem é o **controle programático da execução**, permitindo incorporar o agente diretamente em aplicações e fluxos Python.

---

# 📊 Comparando os métodos

| Método              | Principal objetivo                        | Interface     |
| ------------------- | ----------------------------------------- | ------------- |
| 🌐 `adk web`        | Desenvolvimento, depuração e demonstração | Navegador     |
| 🖥️ `adk run`       | Testes rápidos e CLI                      | Terminal      |
| 🔗 `adk api_server` | Integração e exposição como API           | HTTP/REST     |
| 🐍 Programático     | Aplicações e integrações personalizadas   | Código Python |

### 🧭 Qual escolher?

```text
Preciso desenvolver/depurar?
        ↓
   🌐 adk web

Preciso fazer um teste rápido?
        ↓
   🖥️ adk run

Preciso disponibilizar o agente como API?
        ↓
   🔗 adk api_server

Preciso integrar o agente a uma aplicação Python?
        ↓
   🐍 Execução programática
```

---

# 🧠 Ponto importante

Os diferentes métodos **não significam agentes diferentes**.

O mesmo `agent.py` pode ser executado de várias maneiras:

```text
                 🤖 AGENTE
                    │
              ┌─────┴─────┐
              │ agent.py  │
              └─────┬─────┘
                    │
       ┌────────────┼────────────┐
       ↓            ↓            ↓
  🌐 adk web    🖥️ adk run   🔗 api_server
                    │
                    └────── 🐍 Python
```

A escolha depende do **objetivo e do ambiente de execução**.

---

# 🎯 Principais aprendizados

* 🌐 **`adk web`** → desenvolvimento visual e depuração
* 🖥️ **`adk run`** → interação rápida pelo terminal
* 🔗 **`adk api_server`** → disponibilização do agente como API
* 🐍 **Execução programática** → integração com aplicações Python
* 🔄 Todos os métodos podem utilizar o **mesmo agente**
* 🧩 A escolha do método deve acompanhar o fluxo de trabalho e a necessidade da aplicação

> **O agente permanece o mesmo; o método de execução muda conforme o objetivo.**