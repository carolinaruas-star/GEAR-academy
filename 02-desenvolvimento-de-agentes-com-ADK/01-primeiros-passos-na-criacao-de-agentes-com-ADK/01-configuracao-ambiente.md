# ⚙️ Configuração do ambiente — Google ADK

O **Agent Development Kit (ADK)** é um framework para desenvolvimento de agentes de IA. O curso utiliza **Python**, mas o ADK também possui suporte a Java.

## 🐍 Pré-requisitos

Para acompanhar o curso com Python, é necessário:

* **Python 3.11+**
* **pip**
* Terminal ou prompt de comando
* Acesso para instalar pacotes
* Conexão com a internet

O ADK é compatível com **Windows 10/11, macOS e Linux**.

---

## 🛠️ Configurando o ambiente

### 1️⃣ Verificar o Python

```bash
python --version
```

ou

```bash
python3 --version
```

A versão deve ser **3.11 ou superior**.

### 2️⃣ Criar o diretório do projeto

```bash
mkdir adk-workspace
cd adk-workspace
```

O diretório centraliza os projetos desenvolvidos com o ADK.

### 3️⃣ Criar e ativar um ambiente virtual

O ambiente virtual permite **isolar as dependências** do projeto e evitar conflitos com outras aplicações Python.

```bash
python -m venv .venv
```

**Windows PowerShell:**

```bash
.venv\Scripts\Activate.ps1
```

**Windows CMD:**

```bash
.venv\Scripts\activate.bat
```

**Mac/Linux:**

```bash
source .venv/bin/activate
```

Quando estiver ativo, `(.venv)` aparecerá no início do terminal.

### 4️⃣ Instalar o ADK

Com o ambiente virtual ativado:

```bash
pip install google-adk
```

Depois, verifique a instalação:

```bash
adk --version
```

O pacote fornece as abstrações de agentes, ferramentas de CLI e dependências para trabalhar com modelos Gemini.

---

## 🔑 Configuração do modelo

O agente precisa de acesso a um **LLM**. Neste curso, é utilizado o **Gemini**.

Existem duas opções:

### 🟢 Google AI Studio

Recomendado para **aprendizado e desenvolvimento inicial**.

A configuração utiliza uma chave de API:

```env
GOOGLE_GENAI_USE_VERTEXAI=0
GOOGLE_API_KEY=sua-chave
```

É a opção mais simples e possui uma modalidade sem custo financeiro.

### ☁️ Vertex AI

Indicada para **ambientes de produção e recursos empresariais**.

```env
GOOGLE_GENAI_USE_VERTEXAI=1
GOOGLE_CLOUD_PROJECT=seu-projeto
GOOGLE_CLOUD_LOCATION=us-central1
```

Oferece recursos empresariais, maior capacidade de escala e recursos de segurança para produção.

---

## 🤖 Criando o primeiro agente

O ADK fornece um comando para criar automaticamente a estrutura inicial:

```bash
adk create my_first_agent
```

Estrutura gerada:

```text
my_first_agent/
├── agent.py
├── __init__.py
└── .env
```

### 📄 `agent.py`

É o arquivo principal do agente, onde são definidos **modelo, identidade, comportamento e posteriormente ferramentas**.

Exemplo:

```python
from google.adk.agents.llm_agent import Agent

root_agent = Agent(
    model="gemini-2.5-flash",
    name="root_agent",
    description="Um agente assistente colaborativo.",
    instruction="Você é um assistente colaborativo."
)
```

O `root_agent` é o agente principal que o ADK procura.

### 📄 `.env`

Armazena informações sensíveis, como chaves de API, mantendo essas credenciais fora do código.

⚠️ **Nunca faça commit do `.env` no Git.**

Inclua o arquivo no `.gitignore`:

```gitignore
.env
```

As chaves de API devem ser tratadas como credenciais sensíveis.

### 📄 `__init__.py`

Inicializa o pacote Python e permite que o ADK descubra o agente.

---

## 🌐 Testando o agente

Para iniciar a interface web do ADK:

```bash
adk web
```

O servidor será executado localmente, normalmente em:

```text
http://localhost:8000
```

A interface permite interagir visualmente com o agente e verificar se a configuração está funcionando corretamente.

---

## 🧠 Conceito central

Um agente pode ser entendido como:

> **Agente = Modelo + Ferramentas + Orquestração**

### 🧠 Modelo

É o **LLM**, responsável por compreender informações, raciocinar e tomar decisões.

### 🛠️ Ferramentas

São funções que permitem ao agente **realizar ações**, como pesquisar na web, ler arquivos ou enviar e-mails.

### 🔄 Orquestração

É o processo responsável por executar o ciclo do agente:

**Percepção → Raciocínio → Ação → Verificação → Repetição**

O ADK fornece essa orquestração.

---

## 🔁 Fluxo de desenvolvimento

O fluxo básico apresentado no material é:

```text
✏️ Editar agent.py
       ↓
🌐 Executar adk web
       ↓
🧪 Testar o agente
       ↓
🔄 Fazer alterações
       ↓
🧪 Testar novamente
```

O ADK também disponibiliza outras formas de execução, como:

```bash
adk run
```

para interação pelo terminal, e:

```bash
adk api_server
```

para execução como serviço de API.

## 🎯 Principais aprendizados

* 🐍 Configuração de um ambiente Python para o ADK
* 📦 Instalação do `google-adk`
* 🔐 Uso de variáveis de ambiente para credenciais
* 🤖 Criação de um agente com `root_agent`
* 🧠 Integração com modelos Gemini
* 🌐 Execução e teste através do `adk web`
* 🔄 Compreensão do ciclo de desenvolvimento de agentes
* 🧩 Relação entre **modelo, ferramentas e orquestração**