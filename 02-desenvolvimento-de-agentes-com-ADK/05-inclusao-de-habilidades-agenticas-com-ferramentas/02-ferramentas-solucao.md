# 🛠️ A solução: ferramentas

## 📚 Como estender as capacidades do agente

No módulo anterior, vimos que um agente baseado apenas em um **LLM** possui limitações para acessar informações atualizadas, realizar cálculos, consultar sistemas externos e executar ações.

A solução apresentada neste módulo é o uso de **ferramentas (tools)**.

No contexto do **Google Agent Development Kit (ADK)**:

> Uma ferramenta representa uma capacidade específica fornecida a um agente de IA para que ele execute ações e interaja com o mundo além de suas habilidades básicas de geração de texto e raciocínio.

Assim, as ferramentas completam a equação fundamental apresentada anteriormente:

```text
🤖 Agente = 🧠 Modelo + 🛠️ Ferramentas + 🔄 Orquestração
```

---

## 🛠️ O que as ferramentas permitem

As ferramentas ampliam as capacidades do agente, permitindo:

* 🌐 **Acessar informações em tempo real:** pesquisa na web, APIs de previsão do tempo e cotações;
* 🧮 **Realizar cálculos:** execução de código, modelos financeiros e processamento de dados;
* 🗄️ **Consultar bancos de dados:** pedidos de clientes, estoque e perfis de usuários;
* 🔌 **Interagir com sistemas externos:** envio de e-mails, agendamento e processamento de pagamentos;
* ⚙️ **Executar ações:** atualização de registros, acionamento de workflows e controle de dispositivos.

```text
                 🤖 AGENTE
                     │
            ┌────────┴────────┐
            │                 │
         🧠 LLM          🛠️ Ferramentas
                              │
              ┌───────────────┼───────────────┐
              │               │               │
             🌐              🧮              🗄️
          Informações      Cálculos        Dados
              │               │               │
              └───────────────┼───────────────┘
                              │
                              ▼
                       ⚙️ Ações externas
```

---

## 🧩 O que é uma ferramenta?

Tecnicamente, uma ferramenta costuma ser um **componente de código modular**, como uma função Python, um método de classe ou até mesmo outro agente especializado, criado para executar uma tarefa específica e predefinida.

### Principais características

#### 🎯 Orientadas à ação

As ferramentas executam ações específicas para o agente, como:

* 🔎 Pesquisar informações;
* 🌐 Chamar uma API;
* 🧮 Realizar cálculos;
* 🗄️ Consultar dados;
* ⚙️ Executar operações.

#### 🚀 Ampliam as capacidades do agente

Elas permitem que o agente tenha acesso a informações e recursos que não fazem parte do conhecimento original do LLM.

#### ⚙️ Executam lógica predefinida

A ferramenta executa uma lógica definida pelo desenvolvedor.

Diferentemente do LLM, ela **não possui raciocínio independente**.

```text
🧠 LLM
 │
 ├── Analisa a solicitação
 ├── Decide qual ferramenta utilizar
 ├── Define os argumentos
 │
 ▼
🛠️ Ferramenta
 │
 └── Executa a lógica definida
```

O **LLM decide o que fazer**, enquanto a ferramenta **executa a tarefa**.

---

## 💻 Exemplo de ferramenta simples

Uma função Python pode ser utilizada como uma ferramenta:

```python
def get_capital_city(country: str) -> str:
    """Recupera a capital de um determinado país."""
    
    capitals = {
        "França": "Paris",
        "Japão": "Tóquio",
        "Canadá": "Ottawa"
    }

    return capitals.get(
        country.lower(),
        f"Desculpe, não sei a capital de {country}."
    )
```

### O que torna essa função uma ferramenta?

```text
🐍 Função Python
      │
      ├── 🎯 Executa uma tarefa específica
      │
      ├── ⚙️ Possui lógica predefinida
      │
      └── 🚀 Amplia as capacidades do agente
```

A função:

* É um componente de código modular;
* Executa uma tarefa específica;
* Possui lógica predefinida;
* Disponibiliza dados estruturados ao agente.

---

## 🔄 Como os agentes usam ferramentas

O uso de ferramentas acontece por meio de um processo de **cinco etapas**.

```text
👤 Solicitação do usuário
          │
          ▼
① 🧠 Raciocínio
          │
          ▼
② 🎯 Seleção
          │
          ▼
③ ⚙️ Invocação
          │
          ▼
④ 👁️ Observação
          │
          ▼
⑤ 🏁 Finalização
          │
          ▼
🤖 Resposta do agente
```

### ① 🧠 Raciocínio

O LLM analisa:

* As instruções do agente;
* O histórico da conversa;
* A solicitação do usuário;
* As ferramentas disponíveis.

---

### ② 🎯 Seleção

O LLM decide **se uma ferramenta é necessária** e qual ferramenta atende melhor à solicitação.

---

### ③ ⚙️ Invocação

O LLM gera os argumentos necessários e realiza a chamada da ferramenta.

Exemplo:

```python
get_weather(city="Paris")
```

---

### ④ 👁️ Observação

O agente recebe o resultado retornado pela ferramenta.

```python
{
    "status": "success",
    "report": "Paris está ensolarada, 20 °C"
}
```

---

### ⑤ 🏁 Finalização

O agente utiliza o resultado obtido para formular sua resposta ou decidir qual será a próxima etapa.

---

## 🌤️ Exemplo completo

Considere a pergunta:

> **"Como está o tempo em Paris?"**

O processo ocorre da seguinte maneira:

```text
👤 Usuário
"Como está o tempo em Paris?"
        │
        ▼
① 🧠 Raciocínio
"Preciso de dados meteorológicos atuais."
        │
        ▼
② 🎯 Seleção
"get_weather atende à solicitação."
        │
        ▼
③ ⚙️ Invocação
get_weather(city="Paris")
        │
        ▼
④ 👁️ Observação
"Paris está ensolarada, 20 °C"
        │
        ▼
⑤ 🏁 Finalização
"O tempo atual em Paris é ensolarado,
com temperatura de 20 °C."
```

### 💡 Principal insight

> O **LLM é responsável pelo raciocínio e pela tomada de decisão**, enquanto a **ferramenta executa a ação ou recupera os dados**.

Essa separação permite construir agentes mais capazes e flexíveis.

---

## 🧰 Tipos de ferramentas no ADK

O ADK oferece diferentes formas de equipar um agente com ferramentas.

### 01 — ⚙️ Ferramentas de função

São funções criadas pelo desenvolvedor para atender às necessidades específicas da aplicação.

**Exemplos:**

```text
calculate_shipping_cost()
lookup_order_status()
get_customer_profile()
```

São indicadas quando existe uma **lógica de negócio personalizada**.

---

### 02 — 🔧 Ferramentas integradas

São ferramentas disponibilizadas pelo framework para funcionalidades comuns.

**Exemplos:**

* 🔎 Pesquisa Google;
* 💻 Execução de código;
* 📚 Geração aumentada por recuperação (RAG).

São indicadas quando a aplicação precisa de funcionalidades já disponíveis.

---

### 03 — 🤖 Agente como ferramenta

Um agente especializado pode ser utilizado como uma ferramenta por outro agente.

```text
🤖 Agente principal
       │
       ▼
🛠️ AgentTool
       │
       ▼
🤖 Agente especializado
       │
       ▼
🎯 Subtarefa
```

Essa abordagem permite **delegação de tarefas e raciocínio especializado**.

---

## 📊 Comparação dos tipos

| Tipo                      | Complexidade | Configuração               | Utilização                      |
| ------------------------- | ------------ | -------------------------- | ------------------------------- |
| 🔧 Integrada              | Baixa        | Importar e utilizar        | Funcionalidades comuns          |
| ⚙️ Função                 | Média        | Criar função Python        | Lógica de negócio personalizada |
| 🤖 Agente como ferramenta | Média/alta   | Criar agente especializado | Raciocínio especializado        |

---

## 🧩 O parâmetro `tools`

O `LlmAgent` disponibiliza o parâmetro `tools` para informar quais ferramentas o agente pode utilizar.

```python
from google.adk.agents import LlmAgent

def get_capital_city(country: str) -> str:
    """Recupera a capital de um determinado país."""
    
    capitals = {
        "França": "Paris",
        "Japão": "Tóquio",
        "Canadá": "Ottawa"
    }

    return capitals.get(
        country.lower(),
        f"Desculpe, não sei a capital de {country}."
    )

capital_agent = LlmAgent(
    model="gemini-2.5-flash",
    name="capital_agent",
    description="Responde a perguntas sobre capitais.",
    instruction="Você é um agente que fornece a capital de um país.",
    tools=[get_capital_city]
)
```

### 🔍 Como o LLM entende a ferramenta

O LLM utiliza os metadados da ferramenta para decidir quando e como utilizá-la:

```text
🛠️ get_capital_city
       │
       ├── 📝 Nome da função
       ├── 📖 Docstring
       ├── 📋 Parâmetros
       └── ↩️ Retorno
              │
              ▼
        🧠 LLM decide
        quando utilizar
```

### Pontos importantes

* 🧰 `tools=[...]` é uma **lista**, permitindo adicionar várias ferramentas;
* 🐍 Funções Python podem ser passadas diretamente;
* 🤖 O ADK encapsula automaticamente a função como `FunctionTool`;
* 📝 O nome, a docstring e os parâmetros ajudam o LLM a compreender a ferramenta;
* ⚙️ Não é necessário realizar o encapsulamento manualmente.

---

## 🧠 Ferramentas e estado da sessão

As ferramentas também podem trabalhar em conjunto com o **Session State**, apresentado no Módulo 4.

Essa integração permite criar agentes capazes de utilizar informações armazenadas anteriormente para oferecer experiências mais **contextualizadas e personalizadas**.

```text
🧠 Session State
       │
       ▼
🛠️ Ferramenta
       │
       ├── 📖 Lê informações
       ├── 💾 Salva informações
       └── 🔄 Atualiza estado
              │
              ▼
       🤖 Agente contextualizado
```

### Exemplo

Uma ferramenta pode salvar uma preferência do usuário:

```python
def save_user_preference(
    preference_key: str,
    preference_value: str,
    ctx
) -> dict:
    """Salva uma preferência do usuário no estado da sessão."""

    ctx.session.state[
        f"user:{preference_key}"
    ] = preference_value

    return {
        "status": "success",
        "message": f"Salvo {preference_key} = {preference_value}"
    }
```

Isso permite:

* 👤 Personalizar respostas;
* 🧠 Utilizar contexto anterior;
* 🔄 Manter resultados intermediários;
* 💾 Persistir preferências entre sessões utilizando `user:`.

> A integração avançada entre ferramentas e estado será aprofundada em aulas futuras, especialmente com o uso de `tool_context`.

---

# 🧪 Exemplo prático

## 🌎 Criando um agente de geografia com ferramentas

O objetivo é criar um assistente capaz de responder perguntas sobre **capitais do mundo** utilizando uma ferramenta personalizada.

---

### ① Criar o projeto

```bash
adk create geography_assistant
cd geography_assistant
```

Esse comando cria:

* 📁 O diretório do projeto;
* 🧩 A estrutura básica do agente;
* 📄 O arquivo `agent.py`.

---

### ② Criar a ferramenta

```python
def get_capital_city(country: str) -> str:
    """Recupera a capital de um país específico."""

    capitals = {
        "França": "Paris",
        "Japão": "Tóquio",
        "Canadá": "Ottawa",
        "Alemanha": "Berlim",
        "Brasil": "Brasília",
        "Austrália": "Canberra",
        "Índia": "Nova Délhi",
        "México": "Cidade do México"
    }

    return capitals.get(
        country.lower(),
        f"Desculpe, não tenho informações sobre a capital de {country}."
    )
```

A função utiliza um pequeno banco de dados simulado para recuperar a capital correspondente ao país informado.

---

### ③ Criar o agente

```python
from google.adk.agents import LlmAgent

root_agent = LlmAgent(
    model="gemini-2.5-flash",
    name="geography_assistant",
    description="Ajuda os usuários a aprender sobre geografia mundial.",
    instruction="""
    Você é um assistente de geografia que ajuda os usuários
    a aprender sobre as capitais do mundo.

    Quando um usuário perguntar sobre uma capital:
    1. Use a ferramenta get_capital_city para encontrar a resposta.
    2. Apresente as informações de forma amigável e didática.
    3. Você pode adicionar fatos interessantes, se conhecer algum.

    Se a ferramenta retornar uma mensagem de erro,
    diga educadamente ao usuário que você não possui essa informação.
    """,
    tools=[get_capital_city]
)
```

A principal alteração em relação a um agente sem ferramentas é a inclusão de:

```python
tools=[get_capital_city]
```

---

## 🧪 Testando o agente

Execute:

```bash
adk web
```

Depois, acesse:

```text
http://localhost:8000
```

---

### 🧪 Teste 1 — Consulta básica

**Usuário:**

```text
Qual é a capital do Japão?
```

**Fluxo esperado:**

```text
👤 Usuário
     │
     ▼
🤖 Agente
     │
     ▼
🛠️ get_capital_city("Japão")
     │
     ▼
"Tóquio"
     │
     ▼
🤖 "A capital do Japão é Tóquio."
```

O agente:

* Seleciona automaticamente a ferramenta;
* Extrai o país corretamente;
* Utiliza o resultado para formular a resposta.

---

### 🧪 Teste 2 — Múltiplas capitais

**Usuário:**

```text
Diga as capitais da França, Alemanha e Brasil.
```

O agente deve chamar a ferramenta três vezes:

```text
get_capital_city("França")
        ↓
      Paris

get_capital_city("Alemanha")
        ↓
      Berlim

get_capital_city("Brasil")
        ↓
      Brasília
```

Depois, o agente sintetiza os resultados em uma única resposta.

---

### 🧪 Teste 3 — Capital desconhecida

**Usuário:**

```text
Qual é a capital da Islândia?
```

A ferramenta retorna uma mensagem indicando que não possui a informação.

O agente deve transmitir essa limitação de forma adequada, **sem inventar uma resposta**.

```text
🛠️ Ferramenta
      │
      ▼
❌ Informação não disponível
      │
      ▼
🤖 Resposta transparente
```

---

### 🧪 Teste 4 — Nenhuma ferramenta necessária

**Usuário:**

```text
Fale sobre geografia.
```

Nesse caso, nenhuma ferramenta precisa ser utilizada.

```text
👤 Usuário
      │
      ▼
🤖 Agente
      │
      ├── 🧠 Raciocínio
      │
      └── ❌ Nenhuma ferramenta necessária
                  │
                  ▼
             💬 Resposta
```

Isso demonstra que **as ferramentas são opcionais**.

O agente decide quando utilizá-las com base no contexto e nas instruções.

---

## 💡 Principais aprendizados

### 🛠️ Ferramentas ampliam as capacidades do agente

Elas permitem que o agente vá além do conhecimento disponível no LLM, acessando dados e executando ações práticas.

### 🔄 O uso de ferramentas segue cinco etapas

```text
🧠 Raciocínio
      ↓
🎯 Seleção
      ↓
⚙️ Invocação
      ↓
👁️ Observação
      ↓
🏁 Finalização
```

### 🧰 Existem diferentes tipos de ferramentas

* 🔧 Ferramentas integradas;
* ⚙️ Ferramentas de função personalizadas;
* 🤖 Agente como ferramenta.

### 🧠 O LLM decide quando utilizar uma ferramenta

A decisão considera:

* Nome da função;
* Docstring;
* Esquema de parâmetros;
* Contexto da conversa;
* Instruções do agente.

### ⚙️ O ADK simplifica a criação

Funções Python podem ser adicionadas diretamente ao parâmetro `tools`, sendo encapsuladas automaticamente pelo ADK.

---

## ✅ Práticas recomendadas

Ao criar ferramentas, é importante utilizar:

* 📝 **Nomes descritivos:** prefira `get_capital_city` em vez de `lookup`;
* 📖 **Docstrings objetivas:** explique claramente o propósito da ferramenta;
* 🏷️ **Dicas de tipo:** utilize `str`, `int`, `float` etc.;
* ↩️ **Retornos simples:** comece com tipos básicos;
* ⚠️ **Mensagens de erro claras:** facilite o tratamento de falhas pelo agente.

---

## 🚀 Comportamento dos agentes com ferramentas

As ferramentas proporcionam maior flexibilidade ao agente:

```text
                 🤖 AGENTE
                    │
          ┌─────────┴─────────┐
          │                   │
     🛠️ Ferramentas       🧠 Raciocínio
          │                   │
          │                   ├── Quando usar?
          │                   ├── Qual usar?
          │                   └── Quais argumentos?
          │
          ▼
      ⚙️ Execução
          │
          ▼
      📊 Resultado
          │
          └──────────► 🤖 Resposta
```

O agente pode:

* 🔄 Utilizar uma ferramenta várias vezes;
* 🧰 Utilizar diferentes ferramentas;
* ❌ Não utilizar nenhuma ferramenta quando ela não for necessária;
* 🧩 Incorporar os resultados das ferramentas à resposta;
* ⚠️ Tratar mensagens de erro de maneira adequada.

---

## 🏁 Conclusão

A introdução de ferramentas transforma o agente de um sistema limitado à **geração de texto** em um sistema capaz de **interagir com dados, serviços e recursos externos**.

A principal divisão de responsabilidades é:

```text
🧠 LLM
Raciocínio + Decisão
        │
        ▼
🛠️ Ferramenta
Ação + Execução
        │
        ▼
📊 Resultado
        │
        ▼
🤖 Agente
Resposta contextualizada
```

> **O LLM pensa sobre o que precisa ser feito; a ferramenta executa a tarefa.**

Essa combinação é fundamental para transformar agentes de IA em sistemas capazes de **agir, consultar informações e executar workflows do mundo real**.
