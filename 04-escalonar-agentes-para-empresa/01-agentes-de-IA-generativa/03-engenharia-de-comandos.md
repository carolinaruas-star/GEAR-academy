# 🧠 Aula 3 — Engenharia de comando em ciclos de raciocínio

## 🎯 Visão geral

A engenharia de comando pode ser utilizada para orientar o comportamento dos agentes de IA generativa durante seus **ciclos de raciocínio**.

Nesta aula, são apresentadas duas técnicas importantes:

* 🔄 **ReAct (Reasoning + Acting)** — combina raciocínio e ações externas;
* 🧠 **CoT (Chain of Thought)** — orienta o modelo a dividir o raciocínio em etapas.

O objetivo é entender como essas técnicas podem tornar os agentes mais capazes de **raciocinar, interagir com ferramentas, utilizar informações externas e tomar decisões**.

---

## 🔄 O que é o raciocínio de repetição?

O **raciocínio de repetição** é um componente fundamental de um agente de IA generativa.

Ele controla como o agente:

1. 📥 Recebe informações;
2. 🧠 Realiza o raciocínio interno;
3. ⚙️ Utiliza esse raciocínio para determinar a próxima ação ou decisão;
4. 🔁 Repete o processo até atingir seu objetivo ou interromper a execução.

De forma simplificada:

```text
Informações
     ↓
Raciocínio
     ↓
Decisão / Ação
     ↓
Novo resultado
     ↓
Raciocínio novamente
     ↓
... até atingir o objetivo
```

### Principais características

#### 🔁 Processo iterativo

O agente pode repetir o ciclo várias vezes, utilizando os resultados de cada etapa para orientar a próxima.

#### 🧠 Raciocínio interno

O agente analisa as informações disponíveis e determina o que deve fazer em seguida.

#### 🎯 Tomada de decisões

O raciocínio permite que o agente escolha ações de acordo com o objetivo que precisa alcançar.

#### 🛠️ Frameworks de raciocínio

Diferentes técnicas e frameworks podem ser utilizados para estruturar e orientar esses ciclos.

---

# 🧩 Técnicas de engenharia de comando

Entre as diversas técnicas existentes, a aula destaca duas:

| Técnica      | Foco principal                                     |
| ------------ | -------------------------------------------------- |
| 🧠 **CoT**   | Raciínio interno e resolução passo a passo         |
| 🔄 **ReAct** | Raciocínio combinado com ações e interação externa |

Embora possam ser utilizadas separadamente, as duas técnicas também podem ser combinadas.

---

# 🔄 ReAct — Reasoning + Acting

**ReAct** significa **Reasoning and Acting**, ou seja, **raciocínio e ação**.

A técnica permite que um LLM não apenas raciocine sobre um problema, mas também **realize ações para resolvê-lo**.

Um LLM tradicional pode gerar uma resposta diretamente. Com ReAct, o modelo pode interagir com ferramentas e fontes externas durante o processo.

### 💡 Exemplo

Imagine que o usuário peça:

> "Encontre um bom restaurante italiano por perto."

Com ReAct, o agente pode seguir um ciclo como:

```text
PENSAR
  ↓
AGIR
  ↓
OBSERVAR
  ↓
PENSAR NOVAMENTE
  ↓
AGIR NOVAMENTE
  ↓
RESPONDER
```

Essa repetição permite que o modelo obtenha informações do mundo externo antes de produzir sua resposta.

---

## 🔄 Principais componentes do ReAct

### 1. 🧠 Pensar

O LLM analisa o problema e determina qual deve ser o próximo passo.

Esse processo possui relação com o raciocínio utilizado na CoT.

### 2. ⚙️ Agir

O modelo escolhe uma ação que pode envolver uma ferramenta externa.

Exemplos:

* 🔎 pesquisar na Web;
* 🗄️ consultar um banco de dados;
* 🛠️ utilizar uma ferramenta específica.

O modelo também determina a entrada necessária para realizar essa ação.

### 3. 👀 Observar

O modelo recebe o resultado da ação realizada.

Por exemplo:

* resultados de uma pesquisa;
* dados retornados por um banco de dados;
* resposta de uma ferramenta.

### 4. 💬 Responder

Com base nas informações obtidas, o modelo pode:

* responder ao usuário;
* realizar outra ação;
* iniciar uma nova etapa de raciocínio.

---

## ⭐ Por que o ReAct é importante?

### 🔹 Solução dinâmica de problemas

Permite que o LLM realize tarefas complexas que exigem interação com recursos externos e adaptação a novas informações.

### 🔹 Menos alucinações

Ao fundamentar o raciocínio em informações obtidas do mundo real, o ReAct pode reduzir a geração de informações incorretas ou sem sentido.

### 🔹 Maior confiabilidade

O processo permite analisar como o modelo interage com fontes externas, tornando as respostas potencialmente mais transparentes e confiáveis.

---

## 🌎 Aplicações do ReAct

O ReAct pode ser utilizado em diferentes situações:

### ❓ Resposta a perguntas

O LLM pode consultar fontes externas para obter informações e responder com maior precisão.

### 🔎 Verificação de fatos

O modelo pode pesquisar evidências para verificar determinadas afirmações.

### 🎯 Tomada de decisões

O agente pode coletar informações e utilizá-las para tomar decisões em ambientes interativos.

---

# 🧠 CoT — Chain of Thought

**CoT (Chain of Thought)** significa **cadeia de pensamento** ou **linha de raciocínio**.

A técnica permite orientar o modelo por meio de **etapas intermediárias de raciocínio**, ajudando-o a abordar problemas de maneira mais estruturada.

Em vez de simplesmente solicitar uma resposta, o processo pode orientar o modelo a dividir um problema complexo em etapas menores.

```text
Problema
   ↓
Etapa 1
   ↓
Etapa 2
   ↓
Etapa 3
   ↓
Conclusão
```

A ideia é semelhante a ensinar alguém a resolver um problema passo a passo.

---

## ⭐ Por que a CoT é importante?

### 🧠 Raciocínio aprimorado

Pode ajudar LLMs a resolver problemas complexos que exigem raciocínio lógico.

### 🎯 Maior precisão

Ao dividir problemas em etapas menores, o modelo pode chegar a resultados mais precisos.

### 🔍 Explicabilidade aprimorada

O processo estruturado facilita a compreensão de como uma solução foi construída, contribuindo para confiança e transparência.

---

# 🧩 Técnicas relacionadas à CoT

Existem diferentes formas de implementar ou aprimorar o uso da CoT.

### 🔄 Autoconsistência

O LLM pode gerar diferentes soluções e selecionar aquela que apresenta maior consistência.

### 💬 Comandos ativos

Permitem que o LLM faça perguntas para esclarecer informações ou solicitar dados adicionais.

### 🖼️ CoT multimodal

Combina texto com outros tipos de dados, como:

* imagens;
* vídeos;
* outros formatos de informação.

Isso pode contribuir para o raciocínio em situações que envolvem diferentes modalidades.

---

## 🌎 Aplicações da CoT

### 🧩 Tarefas de raciocínio complexo

Pode ajudar a dividir problemas complexos em etapas menores, como:

* problemas matemáticos;
* quebra-cabeças;
* problemas de lógica.

### 📖 Geração de explicações

Pode ser utilizada para estruturar explicações e tornar uma solução mais compreensível.

### 📋 Planejamento em várias etapas

Pode auxiliar no planejamento de tarefas complexas, como:

* escrever uma história;
* planejar uma viagem;
* depurar código.

---

# ⚖️ ReAct × CoT

As duas técnicas possuem objetivos relacionados, mas seus focos são diferentes.

| Característica       | 🔄 ReAct                                    | 🧠 CoT                                                           |
| -------------------- | ------------------------------------------- | ---------------------------------------------------------------- |
| Nome                 | Reasoning + Acting                          | Chain of Thought                                                 |
| Foco                 | Interação externa                           | Raciocínio interno                                               |
| Ferramentas          | Pode utilizar ferramentas externas          | Não depende de ferramentas externas                              |
| Informações externas | Pode coletar informações durante o processo | Trabalha principalmente com as informações disponíveis ao modelo |
| Ações                | O modelo pode executar ações                | O foco está no raciocínio                                        |
| Principal objetivo   | Raciocinar e agir                           | Estruturar o raciocínio                                          |

### 🎯 Regra prática

```text
Precisa raciocinar sobre o problema?
        ↓
      CoT 🧠

Precisa raciocinar + interagir com o mundo externo?
        ↓
     ReAct 🔄
```

---

# 🤝 ReAct + CoT

ReAct e CoT **não precisam ser utilizados de forma isolada**.

As duas técnicas podem ser combinadas para criar agentes capazes de:

* 🧠 realizar raciocínio mais estruturado;
* 🔎 buscar informações externas;
* 🛠️ utilizar ferramentas;
* 🔄 adaptar suas ações aos resultados obtidos;
* 🎯 resolver tarefas mais complexas.

De forma simplificada:

```text
             AGENTE
                │
       ┌────────┴────────┐
       ↓                 ↓
     CoT 🧠           ReAct 🔄
       │                 │
Raciocínio interno   Ação externa
       │                 │
       └────────┬────────┘
                ↓
        Decisão mais completa
```

---

# 📝 Como escolher a técnica?

A escolha deve considerar o **caso de uso**.

### Use CoT quando:

* o problema exige raciocínio lógico;
* é necessário dividir uma tarefa em etapas;
* o foco está no raciocínio interno;
* a tarefa não depende necessariamente de informações externas.

### Use ReAct quando:

* o agente precisa utilizar ferramentas;
* é necessário consultar fontes externas;
* o agente precisa adaptar suas ações com base em novos resultados;
* a tarefa exige interação com o ambiente.

### Use ambas quando:

A tarefa exige **raciocínio estruturado e interação externa**.

---

# 🧠 Principais aprendizados

* 🔄 O **raciocínio de repetição** permite que agentes recebam informações, raciocinem e tomem decisões de maneira iterativa.
* 🧠 A **CoT** estrutura o raciocínio em etapas.
* 🔄 O **ReAct** combina raciocínio com ações externas.
* 🛠️ O ReAct permite que o agente utilize ferramentas e consulte informações.
* 🎯 A CoT pode ajudar na resolução de problemas complexos.
* 🔎 O ReAct pode melhorar a fundamentação das respostas ao utilizar informações externas.
* 🤝 ReAct e CoT podem ser combinados.
* ⚙️ A melhor técnica depende do caso de uso e das necessidades do agente.

> 🎯 **Conclusão:** A engenharia de comando pode orientar os ciclos de raciocínio dos agentes de IA generativa. Enquanto a CoT concentra-se no raciocínio interno, o ReAct combina raciocínio e ação, permitindo que o agente interaja com ferramentas e informações externas. Compreender essas técnicas ajuda a desenvolver agentes mais capazes, precisos e adaptáveis.
