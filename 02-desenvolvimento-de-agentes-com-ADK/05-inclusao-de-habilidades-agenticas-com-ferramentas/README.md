# 🔧 Módulo 5: Inclusão de Habilidades Agênticas com Ferramentas

<p align="center">
  <strong>Google Cloud Skills Boost • Google Agent Development Kit (ADK)</strong>
</p>

<p align="center">
  <strong>Equipando agentes de IA com ferramentas para interagir com o mundo real.</strong>
</p>

---

## 📚 Sobre o módulo

Este módulo apresenta como utilizar **ferramentas** para ampliar as capacidades dos agentes de IA, permitindo que eles ultrapassem as limitações de seus dados de treinamento e possam **consultar informações, executar tarefas, acessar sistemas externos e realizar ações específicas**.

Um agente baseado apenas em um modelo de linguagem possui limitações importantes: seus conhecimentos podem estar desatualizados e ele não consegue, por conta própria, interagir diretamente com sistemas externos.

A utilização de **tools** permite conectar os agentes a recursos capazes de executar operações específicas, tornando-os mais úteis, dinâmicos e capazes de participar de workflows reais.

O módulo também apresenta o **Model Context Protocol (MCP)**, um padrão aberto que facilita a integração entre agentes, modelos de linguagem e ferramentas ou serviços externos.

---

## 🎯 Objetivos de aprendizagem

Ao longo do módulo, os principais objetivos são:

* 🛠️ Compreender como **ferramentas** ampliam as habilidades dos agentes;
* 🔎 Utilizar ferramentas para acessar informações e executar tarefas;
* 🧩 Conhecer ferramentas integradas para funcionalidades comuns;
* 🔗 Compreender o **Model Context Protocol (MCP)**;
* 🌐 Conectar agentes a ferramentas e serviços externos;
* ⚙️ Criar e utilizar **ferramentas de função personalizadas**;
* 🧠 Desenvolver instruções estratégicas para orientar o uso das ferramentas;
* 🤖 Criar agentes capazes de executar tarefas além da geração de texto.

---

## 🧩 Conteúdos do módulo

### 01 — 🛠️ Ferramentas e habilidades agênticas

Primeiro contato com o problema de agentes limitados aos conhecimentos disponíveis em seus modelos de linguagem.

**Principais conceitos:**

* Limitações dos dados de treinamento;
* Ferramentas agênticas;
* Extensão das capacidades dos agentes;
* Acesso a informações externas;
* Execução de tarefas.

As ferramentas permitem que o agente deixe de apenas **processar informações** e passe a utilizar recursos capazes de realizar operações específicas.

---

### 02 — 🔧 Ferramentas integradas

Estudo das ferramentas já disponibilizadas para determinadas funcionalidades e tarefas comuns.

**Principais conceitos:**

* Ferramentas integradas;
* Execução de ações;
* Pesquisa de informações;
* Consulta de dados;
* Automação de tarefas.

Essas ferramentas permitem adicionar capacidades aos agentes sem a necessidade de implementar cada funcionalidade do zero.

---

### 03 — 🔗 Model Context Protocol (MCP)

Introdução ao **Model Context Protocol**, um padrão aberto utilizado para conectar modelos de linguagem e agentes a ferramentas, dados e serviços externos.

**Principais conceitos:**

* Model Context Protocol;
* Servidores MCP;
* Ferramentas externas;
* Integração entre agentes e serviços;
* Comunicação com recursos externos.

O MCP fornece uma forma padronizada de disponibilizar ferramentas para que os agentes possam utilizá-las durante suas execuções.

---

### 04 — ⚙️ Ferramentas de função personalizadas

Estudo da criação de ferramentas específicas para atender às necessidades de uma aplicação.

**Principais conceitos:**

* Custom Function Tools;
* Funções personalizadas;
* Parâmetros de entrada;
* Retorno de informações;
* Integração com agentes.

As ferramentas personalizadas permitem adaptar o agente a **necessidades específicas do negócio ou da aplicação**.

---

### 05 — 🧠 Design de instruções estratégicas

Estudo de como orientar o agente sobre **quando, por que e como utilizar determinada ferramenta**.

**Principais conceitos:**

* Instruções estratégicas;
* Seleção de ferramentas;
* Orientação do comportamento;
* Uso adequado das ferramentas;
* Controle das ações do agente.

Uma ferramenta por si só não garante um comportamento adequado. As instruções precisam orientar o agente sobre como utilizá-la de maneira eficiente.

---

## 🤖 Agentes sem ferramentas x agentes com ferramentas

Um dos principais conceitos apresentados no módulo é a diferença entre um agente limitado ao conhecimento do modelo e um agente capaz de **interagir com recursos externos**.

```text
🤖 AGENTE SEM FERRAMENTAS
        │
        │ conhecimento do modelo
        ▼
   📚 Dados de treinamento
        │
        ▼
   💬 Resposta
```

Com ferramentas:

```text
🤖 AGENTE
    │
    ├── 🧠 Modelo de linguagem
    │
    ├── 🔎 Pesquisa
    │
    ├── 💾 Banco de dados
    │
    ├── ⚙️ Funções personalizadas
    │
    └── 🔗 Servidor MCP
            │
            ▼
      🌐 Recursos externos
            │
            ▼
      🎯 Resultado da tarefa
```

As ferramentas adicionam uma camada de **ação e integração** ao agente, permitindo que ele obtenha informações atuais e execute operações que não seriam possíveis apenas com o conhecimento do modelo.

---

## 🔄 Fluxo conceitual

```text
👤 Usuário
    │
    ▼
💬 Solicitação
    │
    ▼
🤖 Agente
    │
    ▼
🧠 Analisa a tarefa
    │
    ├── Responde diretamente
    │
    └── 🛠️ Utiliza uma ferramenta
            │
            ▼
       🔗 Serviço externo
            │
            ▼
       📊 Resultado
            │
            ▼
       🤖 Agente
            │
            ▼
      🎯 Resposta final
```

O agente pode decidir quando uma ferramenta é necessária para obter informações ou executar uma determinada ação.

---

## 🛠️ Conceitos fundamentais

| Conceito                      | Função                                                             |
| ----------------------------- | ------------------------------------------------------------------ |
| 🛠️ **Tools**                 | Ampliam as capacidades dos agentes                                 |
| 🔧 **Ferramentas integradas** | Fornecem funcionalidades prontas para tarefas comuns               |
| 🔗 **MCP**                    | Padroniza a conexão entre agentes e recursos externos              |
| ⚙️ **Function Tools**         | Permitem criar funcionalidades específicas para o agente           |
| 🧠 **Instructions**           | Orientam o agente sobre como utilizar as ferramentas               |
| 🌐 **Serviços externos**      | Disponibilizam dados e funcionalidades fora do modelo              |
| 🎯 **Ações**                  | Permitem que o agente execute tarefas em vez de apenas gerar texto |

---

## 💡 Principais aprendizados

### 🧠 Modelos possuem limitações

Um modelo de linguagem possui conhecimento limitado ao seu treinamento e não consegue, sozinho, acessar informações que estejam fora desse contexto.

As ferramentas permitem superar parte dessas limitações.

### 🛠️ Ferramentas ampliam as habilidades dos agentes

Ao conectar ferramentas aos agentes, é possível adicionar capacidades como:

* 🔎 Pesquisa na web;
* 💻 Execução de código;
* 💾 Consulta a bancos de dados;
* 📊 Processamento de informações;
* ⚙️ Execução de funções;
* 🌐 Interação com serviços externos.

### 🔗 MCP facilita integrações

O **Model Context Protocol** fornece uma maneira padronizada de disponibilizar ferramentas e recursos externos para agentes e modelos de linguagem.

### ⚙️ Ferramentas personalizadas tornam os agentes mais especializados

Quando as ferramentas integradas não atendem às necessidades da aplicação, é possível criar **funções personalizadas** para fornecer exatamente a capacidade necessária.

### 🧠 Instruções orientam o uso das ferramentas

O agente precisa receber orientações claras para identificar **qual ferramenta utilizar, em qual situação e com qual objetivo**.

---

## 🧪 Laboratório prático

### 💰 Adicionar ferramentas de moeda a um agente usando o MCP

Neste laboratório, um agente desenvolvido com o **Google ADK** foi modificado para utilizar um **servidor MCP**, permitindo que ele acessasse uma ferramenta externa para consultar informações atuais sobre criptomoedas.

### 🔹 Antes

Inicialmente, o agente conseguia responder consultas relacionadas a moedas fiduciárias, como:

```text
💵 USD → EUR
💵 USD → CNY
```

Porém, ao solicitar o preço atual do Bitcoin, o agente não possuía uma ferramenta capaz de consultar essa informação externamente.

---

### 🔹 Implementação

Foi adicionada ao servidor MCP uma ferramenta personalizada:

```python
@mcp.tool()
def get_crypto_price(currency_pair: str = "BTC-USD") -> dict:
    """Get the current price of a cryptocurrency pair."""
    url = f"https://api.coinbase.com/v2/prices/{currency_pair}/spot"
    response = httpx.get(url)
    return response.json()["data"]
```

A função utiliza um endpoint público para obter o preço atual do par de criptomoedas solicitado.

---

### 🔹 Depois

Após a integração, o agente passou a utilizar a ferramenta:

```text
👤 Usuário
    │
    ▼
🤖 Agente ADK
    │
    ▼
🔗 Servidor MCP
    │
    ▼
🛠️ get_crypto_price
    │
    ▼
🌐 Coinbase API
    │
    ▼
💰 Preço atual do Bitcoin
    │
    ▼
🤖 Resposta do agente
```

O agente passou a ser capaz de consultar o **preço atual do Bitcoin** utilizando a ferramenta `get_crypto_price`.

---

## 🚀 Competências desenvolvidas

* 🛠️ Integração de **ferramentas** em agentes de IA;
* 🔗 Utilização do **Model Context Protocol (MCP)**;
* 🌐 Conexão de agentes com **serviços externos**;
* ⚙️ Criação de **ferramentas de função personalizadas**;
* 🧠 Desenvolvimento de instruções para orientar o uso das ferramentas;
* 🤖 Construção de agentes capazes de **executar tarefas além da geração de texto**;
* 💰 Integração de uma ferramenta de consulta de preços de criptomoedas.

---

## ⚠️ Pontos de atenção

Ao trabalhar com ferramentas e integrações externas, é importante considerar:

* 🔐 Segurança das credenciais e informações utilizadas;
* 🎯 Quando uma ferramenta realmente é necessária;
* 🧠 Clareza das instruções fornecidas ao agente;
* ⚙️ Validação dos parâmetros enviados às ferramentas;
* 🌐 Disponibilidade dos serviços externos;
* 🛡️ Tratamento de erros e respostas inesperadas;
* 🔄 Atualização e manutenção das integrações.

> Ferramentas aumentam significativamente as capacidades dos agentes, mas precisam ser utilizadas de forma **controlada, segura e orientada por instruções claras**.

---

## 🗂️ Organização dos estudos

Os conteúdos do módulo seguem uma progressão baseada no problema → solução → verificação:

```text
01 ── 🛠️ Ferramentas agênticas
 │
 ├── Problema
 ├── Solução
 └── Teste
        │
        ▼
02 ── 🔧 Ferramentas integradas
 │
 ├── Problema
 ├── Solução
 └── Teste
        │
        ▼
03 ── 🔗 Model Context Protocol
 │
 ├── Problema
 ├── Solução
 └── Teste
        │
        ▼
04 ── ⚙️ Ferramentas de função personalizadas
 │
 ├── Problema
 ├── Solução
 └── Teste
        │
        ▼
05 ── 🧠 Design de instruções estratégicas
 │
 ├── Problema
 ├── Solução
 └── Teste
        │
        ▼
📖 Lista de leitura
        │
        ▼
🏁 Conclusão
```

---

## 📌 Estrutura do módulo

```text
05-inclusao-de-habilidades-agenticas-com-ferramentas/
│
├── 01-ferramentas-problema.md
├── 02-ferramentas-solucao.md
├── 03-ferramentas-integradas-problema.md
├── 04-ferramentas-integradas-solucao.md
├── 05-mcp-problema.md
├── 06-mcp-solucao.md
├── 07-function-tools-problema.md
├── 08-function-tools-solucao.md
├── 09-instrucoes-problema.md
├── 10-instrucoes-solucao.md
├── 11-conclusao.md
├── 12-badge-conclusao.md
├── 17-
├── 18-
│
└── README.md
```

> Os nomes dos arquivos podem ser ajustados para acompanhar exatamente a nomenclatura utilizada no repositório.

---

## 🚀 Próxima etapa

Após aprender a ampliar as capacidades dos agentes por meio de **ferramentas, MCP e funções personalizadas**, o próximo passo é avançar para a construção de agentes capazes de **combinar diferentes capacidades, executar workflows e lidar com tarefas cada vez mais complexas**.

Isso permite evoluir de agentes que apenas respondem a solicitações para sistemas capazes de **raciocinar, utilizar recursos externos e executar ações de forma mais autônoma**.

---

<p align="center">
  <strong>🔧 Google Agent Development Kit (ADK)</strong><br>
  Equipando agentes de IA com ferramentas e habilidades do mundo real.
</p>
