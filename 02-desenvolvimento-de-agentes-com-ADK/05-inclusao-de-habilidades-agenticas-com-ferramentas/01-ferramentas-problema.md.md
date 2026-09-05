# 🛠️ O problema: agentes limitados por dados de treinamento

## 📚 Introdução

No curso anterior, foi apresentada a **equação fundamental de um agente**:

```text
🤖 Agente = 🧠 Modelo + 🛠️ Ferramentas + 🔄 Orquestração
```

Até então, os agentes foram construídos principalmente com base no **modelo de linguagem (LLM)** e em mecanismos de orquestração.

Este módulo completa essa equação ao apresentar as **ferramentas**, recursos que transformam agentes capazes de gerar respostas em **assistentes capazes de executar tarefas e interagir com sistemas externos**.

---

## 🤖 Agente sofisticado sem ferramentas

No Curso 3, foi desenvolvido um agente utilizando o `LlmAgent`:

```python
from google.adk.agents import LlmAgent

agent = LlmAgent(
    model='gemini-2.5-flash',
    instruction="""
    Você é um assistente prestativo que fornece informações atualizadas aos usuários.
    Seja sempre preciso e mantenha suas respostas atualizadas.
    """,
)
```

Apesar de possuir instruções e um modelo avançado, esse agente continua limitado às capacidades disponíveis no próprio **LLM**.

---

## ⚠️ O problema

Considere algumas solicitações que um usuário poderia fazer:

```text
👤 Usuário:
"Qual é a previsão do tempo em Tóquio neste momento?"

👤 Usuário:
"Calcule o custo de envio de um pacote de 5 kg para o Canadá"

👤 Usuário:
"Consulte o pedido nº ORD12345 no nosso sistema"
```

O agente pode compreender as solicitações, mas não possui os recursos necessários para **obter os dados ou executar as ações solicitadas**.

---

## 🚧 Limitações fundamentais

### ❌ Dados de treinamento

O LLM possui conhecimento baseado em seus **dados de treinamento**.

Isso significa que as informações disponíveis podem estar congeladas em determinado momento e o modelo não consegue, sozinho, acessar informações em tempo real.

```text
🧠 LLM
  │
  └── 📚 Dados de treinamento
           │
           ▼
      Conhecimento
      disponível
```

Por exemplo, o agente não consegue consultar sozinho a **previsão do tempo atual em Tóquio**.

---

### ❌ Cálculos precisos

Embora os LLMs consigam raciocinar sobre problemas matemáticos, eles não são, por si só, mecanismos confiáveis para realizar **cálculos precisos e determinísticos**.

```text
👤 Solicitação
      │
      ▼
"Calcule o custo de envio"
      │
      ▼
🧠 LLM
      │
      ✖
Sem ferramenta de cálculo
```

Para operações que exigem precisão, o agente pode utilizar uma ferramenta especializada.

---

### ❌ Acesso a sistemas externos

Um LLM não possui acesso automático a bancos de dados, APIs ou sistemas corporativos.

```text
🤖 Agente
    │
    ✖
    │
    ├── 🗄️ Banco de dados
    ├── 🌐 APIs
    └── 🖥️ Sistemas externos
```

Sem uma ferramenta apropriada, o agente não consegue consultar diretamente informações armazenadas nesses sistemas.

---

### ❌ Execução de ações

Um LLM gera **texto**. Ele não executa, por conta própria, operações no mundo real.

Por exemplo:

```text
👤 "Consulte meu pedido ORD12345"

        │
        ▼

🤖 LLM
        │
        ✖
Não consegue acessar
o sistema de pedidos
```

Para realizar essa operação, o agente precisa de uma ferramenta capaz de executar a consulta.

---

## 🧠 A raiz do problema

Todas essas limitações possuem uma origem comum:

> **O agente está limitado ao que o LLM conhece e consegue fazer por meio de seus próprios recursos.**

O modelo pode compreender a solicitação e gerar uma resposta, mas não possui automaticamente acesso a:

```text
🌐 Informações em tempo real
🗄️ Bancos de dados
🔌 APIs
🧮 Calculadoras
⚙️ Sistemas externos
🚀 Ações no mundo real
```

---

## 🔑 A solução

Para superar essas limitações, o agente precisa ser equipado com **ferramentas**.

```text
              🤖 AGENTE
                  │
        ┌─────────┴─────────┐
        │                   │
   🧠 Modelo          🛠️ Ferramentas
        │                   │
        │             ┌─────┼─────┐
        │             │     │     │
        │            🌐    🗄️    ⚙️
        │           APIs  Dados  Ações
        │
        └─────────┬─────────┘
                  │
             🔄 Orquestração
                  │
                  ▼
          🎯 Tarefa executada
```

As ferramentas permitem que o agente **acesse informações externas, execute cálculos, consulte sistemas e realize ações específicas**.

---

## 💡 Principal aprendizado

> Um LLM pode compreender e gerar respostas, mas suas capacidades são limitadas sem acesso a recursos externos. **As ferramentas ampliam o que o agente consegue fazer**, permitindo transformar conhecimento em ações concretas.

---

## ➡️ Próxima etapa

Depois de compreender as limitações dos agentes sem ferramentas, o próximo passo é conhecer **como as ferramentas ampliam as habilidades agênticas** e permitem que os agentes executem tarefas além da simples geração de texto.
