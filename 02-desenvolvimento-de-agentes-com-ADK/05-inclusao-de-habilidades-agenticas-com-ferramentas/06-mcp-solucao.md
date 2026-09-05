# 🔗 A solução: Protocolo de Contexto de Modelo (MCP)

<p align="center">
  <strong>Um adaptador universal para ferramentas de IA</strong>
</p>

<p align="center">
  <strong>Conectando agentes do ADK a um ecossistema de ferramentas externas por meio de um protocolo padronizado.</strong>
</p>

---

## 🧭 Introdução

Depois de compreender o problema de depender apenas das ferramentas integradas ao framework, surge uma questão fundamental:

> **Como conectar agentes do ADK a ferramentas externas que já existem no ecossistema?**

A solução apresentada neste módulo é o **MCP — Model Context Protocol (Protocolo de Contexto de Modelo)**.

O MCP funciona como um **padrão aberto de comunicação** que permite conectar agentes de IA a servidores de ferramentas externas de maneira padronizada.

A ideia pode ser comparada a um **USB para ferramentas de IA**:

```text
                 🔌 MCP
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
   🤖 Gemini     🤖 GPT      🤖 Claude
        │           │           │
        └───────────┼───────────┘
                    │
              🌐 Servidores MCP
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
     📁 Files     🐙 GitHub    🗄️ Database
```

Qualquer cliente compatível com MCP pode se comunicar com servidores compatíveis, independentemente do framework de IA utilizado.

---

## 🧠 O que é o MCP?

O **MCP (Model Context Protocol)** é um padrão aberto criado pela Anthropic e posteriormente hospedado pela **The Linux Foundation**.

Seu objetivo é estabelecer uma forma padronizada para que agentes de IA possam:

* 🔌 Conectar-se a ferramentas externas;
* 🔍 Descobrir ferramentas disponíveis;
* ⚙️ Invocar ferramentas;
* 📥 Receber resultados;
* 🌐 Interagir com diferentes serviços e sistemas.

A documentação do ADK destaca que o framework permite **usar e consumir ferramentas MCP dentro dos agentes**, oferecendo integração com servidores MCP externos.

---

## 🔄 Dois padrões de integração com o ADK

O ADK oferece suporte a **dois padrões principais de integração com MCP**.

### 01 — 🤖 ADK como cliente MCP

O agente do ADK atua como um **cliente MCP**, conectando-se a servidores externos e consumindo suas ferramentas.

```text
🤖 Agente ADK
      │
      ▼
  🔌 McpToolset
      │
      ▼
🌐 Servidor MCP
      │
      ├── 📁 list_directory
      ├── 📄 read_file
      └── 🔎 outras ferramentas
```

Este é o padrão abordado neste módulo.

---

### 02 — 🌐 ADK como servidor MCP

O segundo padrão funciona no sentido contrário.

As ferramentas criadas com ADK podem ser encapsuladas em um **servidor MCP**, tornando-as acessíveis para qualquer cliente compatível com o protocolo.

```text
🛠️ Ferramentas ADK
        │
        ▼
🌐 Servidor MCP
        │
   ┌────┼────┐
   ▼    ▼    ▼
 Claude GPT  Gemini
```

Esse cenário é mais avançado e permite compartilhar ferramentas criadas no ADK com outros frameworks de IA.

---

## 🎯 Foco deste módulo

Neste módulo, o foco está no **Padrão 1**:

> **Conectar agentes do ADK a servidores MCP pré-existentes para ampliar suas capacidades.**

Isso permite aproveitar ferramentas que já foram desenvolvidas e mantidas por comunidades, fornecedores e especialistas.

---

# 🌍 Por que o MCP é importante?

O principal benefício do MCP é a **padronização da integração entre agentes e ferramentas**.

## ❌ Sem MCP

Cada ferramenta pode exigir uma integração específica.

```text
🤖 Framework de IA
       │
       ├── código personalizado → 📁 Filesystem
       ├── código personalizado → 🐙 GitHub
       ├── código personalizado → 💬 Slack
       └── código personalizado → 🗄️ Database
```

Isso gera:

* Mais código;
* Mais manutenção;
* Mais complexidade;
* Maior dependência de frameworks específicos;
* Maior esforço para integrar novas ferramentas.

---

## ✅ Com MCP

Um único padrão pode ser utilizado para conectar diferentes ferramentas.

```text
                 🔌 MCP
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
     📁 Files     🐙 GitHub    🗄️ DB
        │           │           │
        └───────────┼───────────┘
                    │
              🤖 Agentes de IA
```

Com isso:

* 🔗 A integração é padronizada;
* 🌐 As ferramentas podem ser utilizadas por diferentes frameworks;
* 🛠️ A manutenção pode ficar com os responsáveis pela ferramenta;
* 🌱 O agente pode aproveitar um ecossistema crescente de servidores.

---

# 🏭 Adoção pelo setor

O MCP ganhou adoção entre grandes participantes do ecossistema de IA.

Entre os marcos apresentados no curso estão:

* 🟣 **Anthropic** — criação do protocolo em novembro de 2024;
* 🔵 **OpenAI** — adoção oficial do MCP em março de 2025;
* 🔴 **Google ADK** — suporte nativo ao MCP por meio do `McpToolset`;
* 🌐 **The Linux Foundation** — hospedagem do MCP como padrão aberto.

Isso reforça a importância do MCP como uma camada de interoperabilidade entre agentes e ferramentas.

---

# 🚀 O que o MCP significa na prática?

A padronização proporciona quatro vantagens principais.

### ✍️ Escreva uma vez, use em qualquer lugar

Uma ferramenta compatível com MCP pode ser utilizada por diferentes clientes compatíveis com o protocolo.

### 🌱 Aproveite o ecossistema

É possível utilizar ferramentas criadas por especialistas para:

* Bancos de dados;
* APIs;
* Sistemas de arquivos;
* Serviços em nuvem;
* Plataformas de colaboração;
* Repositórios de código.

### 🔄 Fique em dia

À medida que novos servidores MCP são disponibilizados, agentes compatíveis podem aproveitar essas novas capacidades sem que toda a integração precise ser construída do zero.

### 🧩 Separe responsabilidades

O desenvolvedor pode se concentrar na **lógica e orquestração do agente**, enquanto os responsáveis pelos servidores cuidam da implementação e manutenção das ferramentas.

---

# 🌐 Como encontrar servidores MCP

Antes de desenvolver uma ferramenta personalizada, é importante verificar se já existe um **servidor MCP** capaz de atender à necessidade.

## 📚 Recursos importantes

| Recurso                        | Descrição                              |
| ------------------------------ | -------------------------------------- |
| **Registro de Servidores MCP** | Catálogo pesquisável de servidores MCP |
| **Servidores de referência**   | Servidores mantidos pelo projeto MCP   |
| **Documentação do MCP**        | Especificação e guias oficiais         |

### 🔎 Registro

```text
registry.modelcontextprotocol.io
```

A recomendação é:

> **Pesquise primeiro no Registro MCP antes de criar uma ferramenta personalizada.**

A funcionalidade necessária pode já existir.

---

## 🧰 Exemplos de servidores MCP

O ecossistema disponibiliza servidores para diferentes tipos de tarefas:

| Servidor               | Possibilidade                        |
| ---------------------- | ------------------------------------ |
| 📁 Sistema de arquivos | Ler e gravar arquivos e diretórios   |
| 🐙 GitHub              | Repositórios, issues e pull requests |
| 💬 Slack               | Enviar mensagens e acessar canais    |
| 🗄️ PostgreSQL/MySQL   | Consultar bancos de dados            |
| 📝 Notion              | Acessar documentos e bancos de dados |
| ☁️ Google Drive        | Acessar arquivos armazenados         |

---

# 🔗 Como o MCP funciona no ADK

A integração do ADK com MCP utiliza o **`McpToolset`**.

```text
🤖 Agente do ADK
       │
       ▼
🔌 McpToolset
       │
       ▼
🌐 Servidor MCP
       │
       ├── 📁 list_directory
       ├── 📄 read_file
       └── 🔎 outras ferramentas
       │
       ▼
📤 Resultado
       │
       ▼
🤖 Agente
```

## ⚙️ Fluxo de integração

1. 🌐 O servidor MCP expõe ferramentas por meio do protocolo padronizado;
2. 🔌 O agente do ADK utiliza `McpToolset` para estabelecer a conexão;
3. 🔍 As ferramentas disponíveis são descobertas automaticamente;
4. 🧠 O agente pode utilizar essas ferramentas como parte de sua execução;
5. 📥 Os resultados retornam ao agente por meio do protocolo MCP.

A principal vantagem é que **não é necessário cadastrar manualmente cada ferramenta fornecida pelo servidor**.

---

# 🧩 Principais conceitos

## 01 — 🔌 `McpToolset`

O `McpToolset` é a principal classe utilizada pelo ADK para conectar agentes a servidores MCP.

Ele pode ser adicionado diretamente à lista `tools` do agente:

```python
from google.adk.agents import LlmAgent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters

agent = LlmAgent(
    model='gemini-2.5-flash',
    name='my_agent',
    instruction="Use as ferramentas disponíveis para ajudar os usuários.",
    tools=[
        McpToolset(
            connection_params=StdioConnectionParams(
                server_params=StdioServerParameters(
                    command='npx',
                    args=['-y', '@some/mcp-server'],
                ),
            ),
        )
    ],
)
```

### O que o `McpToolset` faz?

```text
🔌 McpToolset
      │
      ├── 1. Conecta ao servidor MCP
      │
      ├── 2. Descobre as ferramentas
      │
      ├── 3. Disponibiliza as ferramentas ao agente
      │
      └── 4. Retorna os resultados
```

### Pontos importantes

* `McpToolset` entra na lista `tools`;
* Os parâmetros de conexão indicam como acessar o servidor;
* As ferramentas são descobertas automaticamente;
* O agente utiliza essas ferramentas como parte de sua capacidade.

---

# 🔌 Tipos de conexão

O ADK oferece diferentes formas de estabelecer conexão com servidores MCP.

## 01 — 💻 `StdioConnectionParams`

Utilizado para **servidores locais**.

O servidor MCP é iniciado como um subprocesso na máquina local.

```python
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters

connection = StdioConnectionParams(
    server_params=StdioServerParameters(
        command='npx',
        args=[
            '-y',
            '@modelcontextprotocol/server-filesystem',
            '/path'
        ],
    ),
)
```

### Quando utilizar?

* Desenvolvimento;
* Testes;
* Experimentação;
* Cenários de usuário único.

---

## 02 — 🌐 `SseConnectionParams`

Utilizado para **servidores remotos**.

A conexão ocorre com um servidor MCP hospedado remotamente.

```python
from google.adk.tools.mcp_tool.mcp_session_manager import SseConnectionParams

connection = SseConnectionParams(
    url="https://your-mcp-server.example.com/sse",
    headers={
        'Authorization': 'Bearer YOUR_TOKEN'
    },
)
```

### Quando utilizar?

* Produção;
* Servidores hospedados na nuvem;
* Ambientes com múltiplos usuários;
* Infraestruturas distribuídas.

---

## 📊 Comparação

| Aspecto        | `StdioConnectionParams`  | `SseConnectionParams` |
| -------------- | ------------------------ | --------------------- |
| Localização    | Local                    | Remota                |
| Comunicação    | Subprocesso              | HTTP                  |
| Configuração   | Mais simples             | Requer infraestrutura |
| Ideal para     | Desenvolvimento e testes | Produção e nuvem      |
| Escalabilidade | Usuário único            | Múltiplos usuários    |

---

# 🛡️ Filtragem de ferramentas

Um servidor MCP pode disponibilizar muitas ferramentas.

Entretanto, **o agente não precisa necessariamente ter acesso a todas elas**.

O parâmetro `tool_filter` permite selecionar quais ferramentas estarão disponíveis.

```python
McpToolset(
    connection_params=StdioConnectionParams(...),
    tool_filter=[
        'list_directory',
        'read_file'
    ],
)
```

## 🎯 Por que filtrar?

### 🔐 Segurança

Limitar ferramentas pode impedir operações potencialmente perigosas.

### 🧩 Simplicidade

O agente recebe apenas as ferramentas necessárias.

### 🎯 Foco

Menos opções podem facilitar a tomada de decisão do agente.

---

## ✅ Exemplo seguro

```python
McpToolset(
    connection_params=StdioConnectionParams(
        server_params=StdioServerParameters(
            command='npx',
            args=[
                '-y',
                '@modelcontextprotocol/server-filesystem',
                '/allowed/path'
            ],
        ),
    ),
    tool_filter=[
        'list_directory',
        'read_file'
    ],
)
```

Nesse exemplo, o agente possui apenas ferramentas de **leitura**.

---

## ⚠️ Exposição excessiva

Sem `tool_filter`, o agente pode receber acesso a um conjunto muito maior de ferramentas, incluindo operações de escrita ou exclusão.

```text
❌ Sem filtro
      │
      ├── list_directory
      ├── read_file
      ├── write_file
      ├── delete_file
      └── outras operações
```

### 💡 Boa prática

> **Em produção, exponha apenas as ferramentas realmente necessárias para o agente.**

Sempre que possível, prefira operações de **somente leitura**.

---

# 🧭 Como escolher o tipo de ferramenta?

Nem todo problema exige MCP.

A escolha depende da funcionalidade necessária e da existência de uma solução pronta.

```text
             🎯 Você precisa dessa funcionalidade?
                         │
             ┌───────────┴───────────┐
             ▼                       ▼
      🔎 Google Search        💻 Execução de código
             │                       │
             └───────────┬───────────┘
                         ▼
                🧰 Ferramentas integradas
                         │
                         ▼
              Já existe servidor MCP?
                    │           │
                   SIM         NÃO
                    │           │
                    ▼           ▼
              🔗 Ferramenta   Sua lógica é
                  MCP         específica?
                                │
                               SIM
                                │
                                ▼
                     🛠️ Função personalizada
```

---

## 📊 Comparação das abordagens

| Aspecto       | Ferramentas do MCP      | Ferramentas integradas | Funções personalizadas |
| ------------- | ----------------------- | ---------------------- | ---------------------- |
| Quem mantém   | Comunidade/fornecedores | Equipe do ADK          | Você                   |
| Configuração  | Conectar e configurar   | Importar               | Escrever código        |
| Portabilidade | Alta                    | ADK                    | ADK                    |
| Customização  | Limitada ao servidor    | Limitada               | Controle total         |
| Implementação | Minutos                 | Minutos                | Horas a dias           |

---

## 🔎 Quando usar cada uma?

### 🔗 Ferramentas do MCP

Ideais quando:

* A funcionalidade é comum;
* Já existe um servidor MCP;
* Você quer aproveitar uma implementação existente;
* Deseja maior portabilidade entre frameworks.

### 🧰 Ferramentas integradas

Ideais quando:

* A funcionalidade já é fornecida pelo ADK;
* Você precisa de recursos como pesquisa ou execução de código;
* Uma ferramenta oficial já atende ao problema.

### 🛠️ Funções personalizadas

Ideais quando:

* A lógica é específica do negócio;
* O sistema é proprietário;
* É necessário controle total;
* Não existe um servidor MCP adequado.

---

# 🌎 Exemplos de decisão

| Necessidade                            | Abordagem            | Justificativa                        |
| -------------------------------------- | -------------------- | ------------------------------------ |
| 📁 Ler arquivos                        | MCP                  | Existe servidor MCP para filesystem  |
| 🗄️ Consultar PostgreSQL               | MCP                  | Banco de dados possui servidores MCP |
| 💰 Calcular custo de frete             | Função personalizada | Lógica específica do negócio         |
| 👥 Acessar API interna de funcionários | Função personalizada | Sistema proprietário                 |

---

# 🧪 Exemplo prático

## 📁 Assistente de leitura de arquivos com MCP

O objetivo é criar um agente capaz de:

* 📂 Listar arquivos;
* 📄 Ler arquivos;
* 🤖 Utilizar ferramentas MCP automaticamente;
* 🔐 Trabalhar apenas dentro de uma pasta permitida.

---

## 01 — Criar o projeto

```bash
adk create file_reader_assistant
cd file_reader_assistant
```

Isso cria a estrutura inicial do projeto ADK.

---

## 02 — Criar arquivos de teste

```bash
mkdir -p my_files

echo "Olá, este é um arquivo de teste." > my_files/hello.txt

echo "Este é outro arquivo com conteúdo diferente." > my_files/notes.txt
```

Estrutura esperada:

```text
file_reader_assistant/
│
├── agent.py
│
└── my_files/
    ├── hello.txt
    └── notes.txt
```

---

## 03 — Criar o agente

```python
import os

from google.adk.agents import LlmAgent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters


# Pasta permitida para acesso
ALLOWED_PATH = os.path.abspath("./my_files")

# Criar a pasta caso ela não exista
os.makedirs(ALLOWED_PATH, exist_ok=True)


root_agent = LlmAgent(
    model='gemini-2.5-flash',
    name='file_reader_assistant',

    description=(
        'Permite que os usuários leiam e descubram arquivos '
        'usando as ferramentas do MCP.'
    ),

    instruction="""
    Você é um assistente de leitura de arquivos que ajuda
    os usuários a analisar arquivos.

    Suas capacidades:
    - Listar arquivos usando list_directory
    - Ler arquivos usando read_file

    Ao ajudar os usuários:
    1. Use list_directory para exibir os arquivos disponíveis.
    2. Use read_file quando o conteúdo de um arquivo for solicitado.
    3. Descreva o que você encontrou de forma útil.

    Sempre deixe claro com qual pasta você está trabalhando.
    """,

    tools=[
        McpToolset(
            connection_params=StdioConnectionParams(
                server_params=StdioServerParameters(
                    command='npx',
                    args=[
                        '-y',
                        '@modelcontextprotocol/server-filesystem',
                        ALLOWED_PATH,
                    ],
                ),
            ),

            # Expor somente ferramentas de leitura
            tool_filter=[
                'list_directory',
                'read_file'
            ],
        )
    ],
)
```

---

## 🔍 Entendendo o código

### Configuração

```python
from google.adk.tools.mcp_tool import McpToolset
```

Importa o componente responsável pela integração com servidores MCP.

```python
ALLOWED_PATH = os.path.abspath("./my_files")
```

Define o caminho absoluto da pasta que poderá ser acessada pelo servidor.

---

### Conexão

```python
McpToolset(
    connection_params=StdioConnectionParams(
        server_params=StdioServerParameters(
            command='npx',
            args=[
                '-y',
                '@modelcontextprotocol/server-filesystem',
                ALLOWED_PATH,
            ],
        ),
    ),
)
```

Aqui acontece a integração:

```text
🤖 Agente
   │
   ▼
🔌 McpToolset
   │
   ▼
💻 StdioConnectionParams
   │
   ▼
📦 Servidor filesystem
   │
   ▼
📁 my_files
```

---

### Filtragem

```python
tool_filter=[
    'list_directory',
    'read_file'
]
```

O agente recebe apenas duas ferramentas:

```text
📁 list_directory → listar arquivos
📄 read_file      → ler arquivos
```

Isso reduz a superfície de acesso e evita disponibilizar operações desnecessárias.

---

# ▶️ Executando o agente

Execute:

```bash
adk web
```

Depois, acesse:

```text
http://localhost:8000
```

---

# 🧪 Testando o agente

## Teste 01 — 📂 Listar arquivos

**Usuário:**

```text
Quais arquivos estão na pasta?
```

### Comportamento esperado

```text
👤 Usuário
    │
    ▼
🤖 Agente
    │
    ▼
🔧 list_directory
    │
    ▼
📁 my_files
    │
    ▼
📋 Lista de arquivos
```

O agente deve identificar e apresentar os arquivos disponíveis.

### 💡 Observação

O agente descobriu e utilizou a ferramenta MCP automaticamente.

Não foi necessário implementar uma função personalizada para listar os arquivos.

---

## Teste 02 — 📄 Ler um arquivo

**Usuário:**

```text
Mostre o conteúdo de hello.txt
```

### Comportamento esperado

```text
🤖 Agente
    │
    ▼
🔧 read_file
    │
    ▼
📄 hello.txt
    │
    ▼
📝 Conteúdo
```

O agente deve utilizar `read_file` e retornar o conteúdo do arquivo.

---

## Teste 03 — 🔄 Múltiplas operações

**Usuário:**

```text
Liste os arquivos e depois leia o arquivo notes.txt.
```

### Comportamento esperado

```text
🤖 Agente
    │
    ├── 🔧 list_directory
    │
    └── 🔧 read_file
            │
            ▼
       📄 notes.txt
```

O agente deve:

1. Listar os arquivos;
2. Identificar `notes.txt`;
3. Ler seu conteúdo;
4. Apresentar os resultados.

### 🧠 Insight

O agente consegue **orquestrar múltiplas chamadas de ferramentas MCP**, utilizando os mesmos princípios de seleção e execução de ferramentas estudados anteriormente.

---

# 🧠 Principais aprendizados

## 🔗 Sobre o MCP

* É um padrão aberto para conectar agentes a ferramentas externas;
* Permite interoperabilidade entre diferentes frameworks;
* Reduz a necessidade de integrações personalizadas;
* Permite aproveitar um ecossistema crescente de ferramentas.

## 🤖 MCP no ADK

* `McpToolset` conecta o agente aos servidores MCP;
* As ferramentas são descobertas automaticamente;
* As ferramentas MCP podem ser utilizadas como parte do agente;
* O agente pode orquestrar múltiplas chamadas.

## 🔌 Conexões

* `StdioConnectionParams` → servidores locais;
* `SseConnectionParams` → servidores remotos.

## 🛡️ Segurança

* `tool_filter` controla quais ferramentas ficam disponíveis;
* Menos ferramentas reduzem decisões desnecessárias;
* Ferramentas somente leitura são preferíveis quando possível.

---

# 🧭 Quando usar MCP?

```text
                 🎯 Necessidade
                      │
       ┌──────────────┼──────────────┐
       ▼              ▼              ▼
  🔎 Google       🌐 Servidor      🏢 Lógica
     Search           MCP          específica
       │              │              │
       ▼              ▼              ▼
 🧰 Integrada      🔗 MCP       🛠️ Personalizada
```

| Cenário                            | Abordagem         | Por quê?                       |
| ---------------------------------- | ----------------- | ------------------------------ |
| Funcionalidade já existente no ADK | 🧰 Integrada      | Mantida pela equipe do ADK     |
| Arquivos, bancos, APIs comuns      | 🔗 MCP            | Comunidade/fornecedores mantêm |
| Lógica específica do negócio       | 🛠️ Personalizada | Apenas você conhece a regra    |

---

# 🌐 Além deste módulo

O MCP oferece possibilidades mais avançadas que vão além do consumo de servidores existentes.

| Capacidade                          | Descrição                                                  |
| ----------------------------------- | ---------------------------------------------------------- |
| 🛠️ Criar servidor MCP próprio      | Transformar ferramentas personalizadas em um servidor MCP  |
| 🔄 Expor ferramentas do ADK via MCP | Disponibilizar ferramentas para outros clientes            |
| 🌐 Conectar múltiplos servidores    | Utilizar ferramentas de diferentes servidores em um agente |
| ☁️ Implantar no Cloud Run           | Hospedar servidores MCP para produção                      |

---

# 🚀 Segundo padrão de integração

O segundo padrão apresentado pelo ADK permite **expor ferramentas do ADK por meio de um servidor MCP**.

Isso possibilita:

```text
🛠️ Ferramentas criadas no ADK
             │
             ▼
      🌐 Servidor MCP
             │
       ┌─────┼─────┐
       ▼     ▼     ▼
    Claude  GPT  Gemini
```

Dessa maneira, ferramentas desenvolvidas com ADK podem ser disponibilizadas para outros clientes compatíveis com MCP.

### 🎯 Benefício

Você deixa de pensar apenas em:

> **"Como meu agente usa ferramentas externas?"**

e passa a considerar também:

> **"Como minhas ferramentas podem ser utilizadas por diferentes agentes e frameworks?"**

Essa é uma das principais ideias por trás da interoperabilidade promovida pelo MCP.

---

# 🧠 Insight principal

O MCP transforma a relação entre agentes e ferramentas.

```text
ANTES

🤖 Agente
   │
   ├── integração própria → 📁 Arquivos
   ├── integração própria → 🗄️ Banco
   └── integração própria → 🌐 API


COM MCP

🤖 Agente
   │
   ▼
🔌 Protocolo MCP
   │
   ├── 📁 Arquivos
   ├── 🗄️ Banco
   ├── 🐙 GitHub
   ├── 💬 Slack
   └── 🌐 APIs
```

O agente passa a depender menos de implementações específicas e mais de um **padrão comum de comunicação**.

---

# 🗂️ Organização dos estudos

Este conteúdo corresponde à **Parte 3 — Protocolo de Contexto de Modelo (MCP)** do módulo sobre ferramentas.

```text
📚 Módulo 5
│
├── 01 — O problema: agentes limitados pelos dados de treinamento
│
├── 02 — A solução: ferramentas integradas
│
├── 03 — Teste do módulo
│
├── 04 — O problema: reproduzir habilidades comuns
│
├── 05 — A solução: ferramentas integradas
│
├── 06 — 🔗 A solução: Protocolo de Contexto de Modelo (MCP)
│
├── 07 — Teste do módulo
│
└── ...
```

### 📌 Conceitos-chave

```text
MCP
│
├── 🔌 Protocolo padronizado
├── 🌐 Servidores externos
├── 🤖 McpToolset
├── 🔍 Descoberta automática
├── 💻 StdioConnectionParams
├── 🌐 SseConnectionParams
├── 🛡️ tool_filter
└── 🔄 Interoperabilidade
```

---

# 🚀 Próxima etapa

Depois de aprender a utilizar servidores MCP existentes, o próximo passo é avaliar **como lidar com funcionalidades que não estão disponíveis por meio de ferramentas prontas**.

A jornada continua avançando de:

```text
🧠 Modelo
   │
   ▼
🧰 Ferramentas integradas
   │
   ▼
🔗 Servidores MCP
   │
   ▼
🛠️ Ferramentas de função personalizadas
```

O objetivo é aprender a escolher a abordagem mais adequada para cada necessidade, equilibrando **reutilização, segurança, portabilidade e controle**.

---

<p align="center">
  <strong>🔗 MCP conecta agentes de IA a um ecossistema aberto de ferramentas.</strong>
</p>

<p align="center">
  <strong>Do agente isolado para agentes capazes de interagir com o mundo.</strong>
</p>
