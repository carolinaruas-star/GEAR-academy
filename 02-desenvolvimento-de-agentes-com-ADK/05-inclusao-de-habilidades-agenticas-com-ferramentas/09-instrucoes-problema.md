# 🧭 O problema: ferramentas sem orientação

<p align="center">
  <strong>De ferramentas individuais para sistemas coordenados.</strong>
</p>

<p align="center">
  <strong>Por que ferramentas poderosas precisam de instruções estratégicas.</strong>
</p>

---

## 🧭 Introdução

Ao longo do módulo, a evolução dos agentes acontece em etapas: primeiro, aprendemos os fundamentos das ferramentas; depois, utilizamos ferramentas integradas; em seguida, criamos ferramentas personalizadas.

Agora surge um novo desafio:

> **Ter ferramentas disponíveis não significa que o agente saberá utilizá-las corretamente.**

Para construir agentes capazes de atuar em cenários reais, é necessário combinar as ferramentas com **instruções estratégicas**, definindo quando, como e em que ordem cada recurso deve ser utilizado.

---

## 🚀 A jornada até aqui

A evolução apresentada no módulo pode ser representada da seguinte forma:

```text
🧩 Parte 1
Entender ferramentas
        │
        ▼
🛠️ Parte 2
Utilizar ferramentas integradas
        │
        ▼
🔧 Parte 3
Criar ferramentas personalizadas
        │
        ▼
🧠 Parte 4
Coordenar ferramentas
        │
        ▼
🤖 Agente capaz de executar
tarefas do mundo real
```

### Parte 1 — 🧩 Fundamentos

Compreensão dos conceitos fundamentais de ferramentas e criação do primeiro agente habilitado para utilizá-las.

### Parte 2 — 🔎 Ferramentas integradas

Utilização de ferramentas prontas, como:

* 🔍 Pesquisa;
* 💻 Execução de código;
* 🧰 Outros recursos integrados ao ADK.

### Parte 3 — 🔧 Ferramentas de função personalizadas

Criação de funções Python específicas para necessidades que não são atendidas pelas ferramentas genéricas.

### Parte 4 — 🧠 Coordenação de ferramentas

Combinação de diferentes ferramentas para resolver **cenários complexos do mundo real**.

---

## 🔄 A mudança de perspectiva

Até aqui, o foco estava em uma pergunta:

> **"Quais ferramentas meu agente possui?"**

Agora precisamos fazer uma pergunta diferente:

> **"Como meu agente deve utilizar essas ferramentas?"**

Essa mudança é fundamental.

```text
🛠️ FERRAMENTAS
       │
       │ fornecem capacidades
       ▼
🧠 INSTRUÇÕES ESTRATÉGICAS
       │
       │ orientam o uso
       ▼
🤖 AGENTE COORDENADO
       │
       ├── escolhe a ferramenta correta
       ├── define a ordem das ações
       ├── interpreta resultados
       ├── trata erros
       └── sabe quando pedir ajuda
```

As ferramentas fornecem as **capacidades**.

As instruções fornecem a **estratégia**.

---

## ⚠️ O problema: ferramentas sem orientação

Imagine um agente de atendimento ao cliente que possui três ferramentas:

```python
from google.adk.agents import LlmAgent


def check_order_status(order_id: str) -> dict:
    """Verifique o status de um pedido."""
    # Implementação
    pass


def process_refund(order_id: str, amount: float) -> dict:
    """Processe o reembolso de um pedido."""
    # Implementação
    pass


def lookup_customer(email: str) -> dict:
    """Consulte as informações do cliente."""
    # Implementação
    pass
```

As ferramentas existem e possuem funções bem definidas.

Porém, o agente recebe apenas uma instrução genérica:

```python
agent = LlmAgent(
    model='gemini-2.5-flash',
    instruction="Você é um agente de atendimento ao cliente.",
    tools=[
        check_order_status,
        process_refund,
        lookup_customer
    ]
)
```

O problema está justamente na instrução:

```text
"Você é um agente de atendimento ao cliente."
```

Ela informa **quem é o agente**, mas não explica **como ele deve trabalhar**.

---

## ❌ O que pode dar errado?

Quando o agente possui várias ferramentas, mas não recebe orientações claras, diferentes problemas podem ocorrer.

### 1. ❌ Seleção incorreta da ferramenta

O agente pode escolher uma ferramenta inadequada para determinada situação.

Por exemplo:

```text
Cliente solicita reembolso
        │
        ▼
🤖 Agente
        │
        ├── process_refund() ❌
        │
        ▼
Pedido nem sequer foi verificado
```

O agente poderia tentar processar o reembolso **antes de verificar se o pedido existe ou se é elegível**.

---

### 2. ❌ Tratamento inadequado de erros

Uma ferramenta pode retornar:

```python
{
    "status": "error",
    "error_message": "Pedido não encontrado."
}
```

Sem instruções específicas, o agente pode não saber qual deve ser sua próxima ação.

Ele precisa saber, por exemplo:

```text
Ferramenta retorna erro
        │
        ▼
🤖 Interpretar o erro
        │
        ├── Informar o cliente
        ├── Solicitar informação adicional
        └── Encaminhar para supervisor
```

---

### 3. ❌ Ordem incorreta das ferramentas

Algumas operações possuem **dependências entre si**.

Um fluxo de atendimento pode exigir:

```text
1️⃣ Consultar cliente
       ↓
2️⃣ Verificar pedido
       ↓
3️⃣ Validar elegibilidade
       ↓
4️⃣ Processar reembolso
```

Sem uma instrução clara, o agente pode tentar executar essas ações em uma ordem inadequada.

---

### 4. ❌ Resultados ignorados

As ferramentas retornam informações que devem ser utilizadas pelo agente.

Por exemplo:

```python
{
    "status": "success",
    "order_id": "ORD12345",
    "order_status": "delivered"
}
```

O agente precisa interpretar esse resultado e utilizá-lo para decidir a próxima ação ou construir a resposta ao cliente.

```text
Ferramenta
    │
    ▼
Resultado
    │
    ▼
🤖 Agente interpreta
    │
    ├── Decide próxima ação
    └── Constrói resposta
```

Se o resultado for ignorado, a ferramenta perde grande parte de sua utilidade.

---

### 5. ❌ Ausência de encaminhamento

Nem todos os problemas podem ser resolvidos pelas ferramentas disponíveis.

Um agente de atendimento precisa saber quando uma situação:

* ultrapassa suas capacidades;
* exige intervenção humana;
* envolve uma exceção;
* não pode ser resolvida com segurança.

Nesse caso, deve existir um **canal de encaminhamento para um supervisor**.

```text
                    ┌─────────────────────┐
                    │      🤖 AGENTE       │
                    └──────────┬──────────┘
                               │
                     problema do cliente
                               │
              ┌────────────────┴────────────────┐
              │                                 │
       Pode resolver?                    Não pode resolver?
              │                                 │
             SIM                                ▼
              │                         👤 Supervisor
              ▼
      🛠️ Utiliza ferramentas
```

---

## 🧠 A raiz do problema

O problema não está necessariamente nas ferramentas.

As ferramentas podem ser perfeitamente funcionais.

O problema é a **ausência de uma estratégia de utilização**.

```text
🛠️ Ferramentas
     │
     │ sem orientação
     ▼
🤖 Agente
     │
     ├── ferramenta errada
     ├── sequência errada
     ├── erros mal tratados
     ├── resultados ignorados
     └── situações sem encaminhamento
```

Portanto:

> **Ferramentas precisam de instruções estratégicas para orientar quando, como e em que ordem devem ser utilizadas.**

---

## 🎯 O que as instruções precisam definir?

Uma boa estratégia deve orientar pelo menos quatro aspectos:

| Aspecto         | Pergunta que a instrução deve responder                    |
| --------------- | ---------------------------------------------------------- |
| 🛠️ **Quando**  | Em qual situação utilizar a ferramenta?                    |
| ⚙️ **Como**     | Quais informações devem ser fornecidas?                    |
| 🔢 **Ordem**    | Qual ferramenta deve ser chamada primeiro?                 |
| 🚨 **Exceções** | O que fazer quando ocorrer um erro ou situação inesperada? |

Também é importante definir **quando o agente deve parar de tentar resolver sozinho e encaminhar a situação para um humano**.

---

## 🧩 Ferramentas + instruções

O conceito pode ser resumido desta forma:

```text
             🛠️ FERRAMENTAS
                    │
                    │ capacidades
                    ▼
          🧠 INSTRUÇÕES ESTRATÉGICAS
                    │
        ┌───────────┼───────────┐
        │           │           │
      Quando      Como        Ordem
        │           │           │
        └───────────┼───────────┘
                    ▼
             🤖 AGENTE
                    │
                    ▼
          🎯 EXECUÇÃO EFICAZ
```

A combinação entre **capacidades** e **orientação** é o que permite transformar um conjunto de ferramentas em um sistema coordenado.

---

## 📌 Principais aprendizados

* 🛠️ Ter ferramentas disponíveis não é suficiente;
* 🧠 O agente precisa receber instruções estratégicas;
* 🎯 As instruções devem orientar a seleção das ferramentas;
* 🔢 Algumas ferramentas precisam ser utilizadas em uma ordem específica;
* 📦 Os resultados das ferramentas devem ser interpretados e utilizados;
* 🚨 Erros precisam possuir um fluxo de tratamento;
* 👤 O agente deve saber quando encaminhar uma situação para um supervisor;
* 🤖 A combinação entre ferramentas e instruções permite construir agentes mais confiáveis e coordenados.

---

## ⚠️ Ponto de atenção

Uma instrução como:

```python
instruction="Você é um agente de atendimento ao cliente."
```

define apenas o **papel geral** do agente.

Para cenários reais, é necessário definir também:

```text
Papel
  +
Objetivo
  +
Ferramentas disponíveis
  +
Regras de utilização
  +
Ordem das operações
  +
Tratamento de erros
  +
Critérios de encaminhamento
```

Essa é a base para o próximo passo do módulo: aprender a criar **instruções estratégicas capazes de coordenar o uso das ferramentas**.

---

## 🗂️ Organização dos estudos

```text
📁 Módulo 5 — Inclusão de habilidades agênticas com ferramentas
│
├── 01-ferramentas-problema.md
├── 02-ferramentas-solucao.md
├── 03-teste.md
├── 04-ferramentas-integradas-problema.md
├── 05-ferramentas-integradas-solucao.md
├── 06-teste.md
├── 07-mcp-problema.md
├── 08-mcp-solucao.md
├── 09-teste.md
├── 10-ferramentas-funcao-problema.md
├── 11-ferramentas-funcao-solucao.md
├── 12-teste.md
└── 13-ferramentas-sem-orientacao.md
```

---

## 🚀 Próxima etapa

Na próxima lição, o foco passa de **ter ferramentas** para **saber coordená-las por meio de instruções estratégicas**.

O objetivo será aprender como orientar o agente para:

```text
🧠 Interpretar a solicitação
        ↓
🛠️ Escolher a ferramenta correta
        ↓
🔢 Seguir a ordem adequada
        ↓
📦 Interpretar o resultado
        ↓
🔄 Decidir a próxima ação
        ↓
🎯 Entregar a resposta
```

Esse é o passo necessário para transformar ferramentas individuais em **sistemas agênticos coordenados**.

---

<p align="center">
  <strong>🧠 Ferramentas fornecem capacidades. Instruções fornecem direção.</strong>
</p>
