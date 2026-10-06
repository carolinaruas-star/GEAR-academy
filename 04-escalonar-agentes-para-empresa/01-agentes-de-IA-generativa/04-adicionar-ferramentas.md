# 🛠️ Aula 4 — Como adicionar ferramentas aos agentes

## 🎯 Visão geral

As **ferramentas** permitem que agentes de IA generativa ultrapassem os limites do modelo e interajam com o mundo real.

Por meio delas, um agente pode:

* 📚 acessar informações;
* 🗄️ consultar bancos de dados;
* 🔎 pesquisar dados externos;
* ⚙️ executar ações;
* 📅 agendar compromissos;
* ✈️ reservar viagens;
* 🏠 controlar dispositivos;
* 🔗 interagir com diferentes sistemas e APIs.

Nesta aula, são apresentados os principais tipos de ferramentas, o funcionamento delas dentro do ciclo de raciocínio **ReAct** e alguns exemplos de serviços disponíveis no Google Cloud.

---

# 🧰 O que são ferramentas de agentes?

As ferramentas fornecem aos agentes os **recursos, conexões e capacidades** necessários para alcançar seus objetivos.

Elas permitem que o agente:

```text
        AGENTE
           ↓
   ┌───────┼────────┐
   ↓       ↓        ↓
Acessar  Realizar  Interagir
dados    ações     sistemas
   ↓       ↓        ↓
   └───────┼────────┘
           ↓
      Alcançar o
        objetivo
```

Um agente pode utilizar ferramentas para acessar sistemas que não fazem parte diretamente do modelo de IA.

---

# 🧩 Tipos de ferramentas de agentes

As ferramentas de agentes podem ser classificadas em diferentes categorias.

## 🔗 Extensões (APIs)

As **extensões** fazem a ponte entre um agente e **APIs externas**.

### O que é uma API?

API significa **Application Programming Interface** — Interface de Programação de Aplicações.

É um conjunto de regras que permite que diferentes sistemas de software se comuniquem.

As extensões fornecem uma forma padronizada para que agentes utilizem APIs, independentemente das particularidades de cada API.

### 💡 Exemplo

Imagine um agente responsável por reservar viagens.

Ele pode utilizar uma extensão conectada à API de uma empresa de viagens:

```text
Usuário
   ↓
Agente de viagens
   ↓
Extensão
   ↓
API da empresa
   ↓
Sistema de reservas
   ↓
Resultado
   ↓
Agente
   ↓
Usuário
```

A extensão cuida da comunicação com o sistema externo, permitindo que o agente se concentre na tarefa de encontrar e reservar o voo.

> 💡 **Ideia principal:** extensões facilitam a conexão entre agentes e serviços externos.

---

# 🔄 Ferramentas dentro do raciocínio ReAct

O modelo **ReAct (Reasoning + Acting)** descreve uma forma de utilização de ferramentas durante o ciclo de raciocínio do agente.

O processo pode ser dividido em quatro etapas:

```text
1. Raciocínio
      ↓
2. Ação
      ↓
3. Observação
      ↓
4. Iteração
      ↓
   Raciocínio novamente
```

---

## 1. 🧠 Raciocínio — seleção da ferramenta

Primeiro, o agente analisa a situação e determina **qual ferramenta é necessária** para realizar a tarefa.

Por exemplo:

> "Preciso encontrar um horário disponível para o serviço de jardinagem."

O agente identifica que precisa consultar uma agenda.

---

## 2. ⚙️ Ação — execução da ferramenta

Depois de selecionar a ferramenta, o agente a executa.

No exemplo do serviço de jardinagem, ele poderia utilizar um **plug-in de agendamento** conectado à agenda do profissional.

---

## 3. 👀 Observação

O agente recebe o resultado da ferramenta.

Por exemplo:

```text
Ferramenta → "Terça-feira às 14h está disponível."
```

O agente utiliza essa informação como entrada para a próxima etapa.

---

## 4. 🔁 Iteração

O agente analisa o resultado e determina se precisa realizar outra ação ou se já possui informações suficientes para concluir a tarefa.

Esse processo pode se repetir dinamicamente.

```text
Raciocínio
    ↓
Selecionar ferramenta
    ↓
Executar ferramenta
    ↓
Observar resultado
    ↓
Raciocinar novamente
    ↓
Outra ferramenta?
   ↙       ↘
 Sim       Não
 ↓          ↓
Agir      Responder
```

---

# 🌳 Exemplo: agendamento de um serviço de jardinagem

Considere o seguinte cenário:

> Um usuário quer agendar um serviço de jardinagem.

O agente precisa encontrar um horário disponível.

### Processo

**1. Raciocínio**

O agente identifica que precisa consultar a agenda do jardineiro.

**2. Ação**

Seleciona o plug-in de agendamento conectado à agenda.

**3. Observação**

Recebe os horários disponíveis.

**4. Iteração**

Com base no resultado, pode:

* apresentar os horários ao usuário;
* verificar outra data;
* realizar o agendamento;
* continuar utilizando outras ferramentas.

O exemplo demonstra como as ferramentas transformam o agente de um sistema que apenas **gera texto** em um sistema capaz de **realizar tarefas**.

---

# ☁️ Ferramentas do Google Cloud

O Google Cloud oferece diversas opções que podem ser utilizadas na construção de ferramentas para agentes.

É possível:

* criar ferramentas personalizadas;
* utilizar soluções de terceiros;
* utilizar serviços disponíveis no Google Cloud.

Esses recursos podem ser utilizados mesmo quando a lógica principal do agente é desenvolvida fora do Google Cloud.

---

# 🛠️ Principais serviços do Google Cloud para agentes

Entre os serviços que podem ser utilizados como ferramentas estão:

### 📦 Cloud Storage

Serviço de armazenamento que pode fornecer acesso a arquivos e dados para os agentes.

### 🗄️ Bancos de dados

Entre as opções citadas estão:

* **Cloud SQL**
* **Cloud Spanner**
* **Firestore**

Esses serviços podem fornecer acesso a dados estruturados utilizados pelo agente.

### ⚙️ Cloud Run functions

Permite executar funções que podem ser utilizadas como parte das capacidades de um agente.

### ☁️ Cloud Run

Pode ser utilizado para executar aplicações e serviços que participam da arquitetura de agentes.

### 🤖 Vertex AI

Oferece recursos relacionados à inteligência artificial e pode fazer parte da infraestrutura utilizada pelos agentes.

---

# 🧠 APIs de IA pré-criadas

Além dos serviços de infraestrutura, o Google Cloud oferece APIs pré-criadas que fornecem funcionalidades específicas de IA.

Elas podem ser utilizadas como ferramentas pelos agentes.

| API                             | Possível função                           |
| ------------------------------- | ----------------------------------------- |
| 🎙️ **Speech-to-Text**          | Conversão de fala em texto                |
| 🔊 **Text-to-Speech**           | Conversão de texto em fala                |
| 🌎 **Translation**              | Tradução de textos                        |
| 📄 **Document Translation**     | Tradução de documentos                    |
| 📑 **Document AI**              | Processamento e compreensão de documentos |
| 👁️ **Cloud Vision**            | Análise de imagens                        |
| 🎥 **Cloud Video Intelligence** | Análise de vídeos                         |
| 📝 **Natural Language**         | Processamento de linguagem natural        |

Essas APIs permitem adicionar capacidades específicas aos agentes sem precisar desenvolver cada funcionalidade do zero.

---

# 🔗 Outras APIs

O Google Cloud também oferece APIs relacionadas a outros produtos e serviços do Google.

Entre os exemplos citados estão:

* 🗺️ Google Maps;
* 📧 Google Workspace;
* ▶️ YouTube;
* 📷 Google Fotos.

Isso amplia as possibilidades de integração dos agentes com diferentes serviços.

---

# 📍 Exemplo: planejador de local de reunião

Um exemplo apresentado na aula envolve um agente que precisa sugerir o **local mais conveniente para uma reunião**.

### Cenário

O usuário envia um documento contendo informações como:

* convite para uma reunião;
* lista de possíveis locais;
* endereços dos participantes.

O agente precisa analisar essas informações e sugerir uma localização adequada.

---

## 🔄 Combinação de ferramentas

Nesse cenário, diferentes ferramentas podem trabalhar em conjunto:

```text
Documento enviado
       ↓
Document AI
       ↓
Extração dos endereços
       ↓
Google Maps
       ↓
Análise dos locais
       ↓
Agente
       ↓
Sugestão de local
```

### 📄 Document AI

O agente utiliza a **Document AI** para processar o documento enviado e identificar os endereços presentes nele.

### 🗺️ Google Maps

Depois, a API do Google Maps pode ser utilizada para analisar os locais e ajudar o agente a determinar uma opção conveniente.

### 🤖 Resultado

O agente combina as informações obtidas pelas ferramentas para gerar uma recomendação.

> 💡 **Ideia principal:** agentes podem combinar várias ferramentas para resolver tarefas que seriam difíceis de executar utilizando apenas o modelo de IA.

---

# 🔄 Ferramentas + raciocínio

A principal relação entre esta aula e a anterior está no uso do **ReAct**.

Na Aula 4:

```text
ReAct = Pensar → Agir → Observar → Responder
```

Nesta aula, vemos que a etapa **Agir** pode envolver a utilização de ferramentas:

```text
Pensar
  ↓
Escolher ferramenta
  ↓
Executar ferramenta
  ↓
Observar resultado
  ↓
Raciocinar novamente
  ↓
Escolher próxima ação
```

Assim, as ferramentas dão ao agente a capacidade de **interagir com sistemas e informações externas**.

---

# 🧠 Principais aprendizados

* 🛠️ **Ferramentas** ampliam as capacidades dos agentes de IA.
* 🔗 **Extensões** permitem conectar agentes a APIs externas.
* 🔄 O **ReAct** estrutura o uso de ferramentas dentro de um ciclo de raciocínio.
* 🧠 O agente pode selecionar uma ferramenta com base na tarefa que precisa realizar.
* 👀 Os resultados das ferramentas são utilizados para orientar as próximas decisões.
* ☁️ O Google Cloud oferece diversos serviços que podem funcionar como ferramentas para agentes.
* 🤖 APIs pré-criadas permitem adicionar capacidades de IA sem desenvolver tudo do zero.
* 🔗 Diferentes ferramentas podem ser combinadas para resolver tarefas complexas.
* 🌎 As ferramentas permitem que agentes interajam com o mundo real, em vez de apenas gerar respostas.

> 🎯 **Conclusão:** As ferramentas dão aos agentes de IA generativa as capacidades necessárias para acessar informações, executar ações e interagir com diferentes sistemas. Quando combinadas com ciclos de raciocínio como o ReAct, elas permitem que os agentes realizem tarefas complexas de maneira dinâmica e interativa.
