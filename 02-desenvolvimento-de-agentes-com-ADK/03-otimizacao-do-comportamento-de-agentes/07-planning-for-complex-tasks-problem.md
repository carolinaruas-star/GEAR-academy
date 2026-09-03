## 🧠 Google ADK — Planejamento e Raciocínio Estruturado

### O problema: tarefas complexas exigem raciocínio estruturado

### 📚 Contexto

Nos módulos anteriores, os agentes eram configurados para responder diretamente às solicitações dos usuários:

```python id="7k4n2p"
agent = LlmAgent(
    model="gemini-2.5-flash",
    instruction="Resolver problemas para os usuários"
)
```

Essa abordagem funciona bem para tarefas simples, mas problemas mais complexos podem exigir **planejamento, análise de alternativas e raciocínio em múltiplas etapas**.

Neste módulo, o ADK apresenta o **`BuiltInPlanner`**, permitindo adicionar uma etapa de planejamento ao comportamento de um agente.

---

### ⚡ Agentes reativos

Um agente reativo recebe uma solicitação e tenta produzir imediatamente uma resposta:

```text id="4y2j1m"
Usuário
   ↓
Solicitação
   ↓
Agente
   ↓
Resposta
```

Essa abordagem é adequada quando o problema possui baixa complexidade.

Porém, em tarefas mais elaboradas, o agente pode:

* ❌ Não decompor o problema adequadamente
* ❌ Ignorar alternativas
* ❌ Apresentar soluções superficiais
* ❌ Tirar conclusões precipitadas
* ❌ Não considerar todas as restrições envolvidas

---

## 🧩 O que caracteriza um problema complexo?

Problemas complexos normalmente envolvem:

* 🔢 Múltiplas etapas
* ⚖️ Análise de prós e contras
* 🔄 Dependências entre decisões
* 🎯 Várias restrições
* 🧠 Necessidade de planejamento antes da resposta

### 💼 Estratégia de negócios

> Como reduzir os custos da nuvem em 30% sem afetar o desempenho?

O agente precisa considerar fatores como:

```text
Custos atuais
     ↓
Identificação de desperdícios
     ↓
Requisitos de desempenho
     ↓
Alternativas
     ↓
Prós e contras
     ↓
Plano de implementação
```

### 🏗️ Decisão técnica

> Microsserviços ou arquitetura monolítica para o MVP?

É necessário avaliar:

* Velocidade de desenvolvimento
* Escalabilidade
* Tamanho da equipe
* Complexidade operacional
* Crescimento futuro

### ✈️ Planejamento de viagem

> Planejar duas semanas no Japão para uma família de quatro pessoas com orçamento de US$ 5.000.

O problema envolve a coordenação de:

* ✈️ Voos
* 🏨 Hospedagem
* 🚆 Transporte
* 🎎 Atividades
* 🍜 Alimentação
* 💰 Orçamento

---

## 🟢 Problemas que não precisam de planejamento

Nem toda solicitação exige raciocínio em múltiplas etapas.

Exemplos:

| Tipo                | Exemplo                                  |
| ------------------- | ---------------------------------------- |
| 📚 Pergunta factual | "Qual é a capital da França?"            |
| 🔢 Cálculo simples  | "Converter 100 USD em EUR"               |
| 💬 Tarefa simples   | "Cumprimente o usuário de modo afetuoso" |

Nesses casos, adicionar planejamento pode representar **complexidade desnecessária**.

---

## 🧠 Planejamento x Multiagente

É importante diferenciar as duas abordagens.

### 🔹 Planejamento

Utilizado quando **um único agente** precisa lidar com:

* Problemas com várias etapas
* Análise de alternativas
* Prós e contras
* Sequência lógica de decisões

```text
Problema complexo
       ↓
     Agente
       ↓
   Planejamento
       ↓
   Raciocínio
       ↓
    Resposta
```

### 🔹 Multiagente

Utilizado quando o problema exige **habilidades especializadas distintas**, que podem ser distribuídas entre diferentes agentes.

```text
                 Problema
                    ↓
        ┌───────────┼───────────┐
        ↓           ↓           ↓
     Agente A   Agente B    Agente C
     Pesquisa    Análise     Execução
```

📌 **Neste módulo, o foco está no planejamento de um único agente.**

---

## ⚠️ Problema: ausência de planejamento

Considere um agente configurado apenas para resolver problemas:

```python id="m4s7xk"
problem_solver = LlmAgent(
    model="gemini-2.5-flash",
    instruction="Ajudar os usuários a resolver problemas complexos"
)
```

Diante da pergunta:

> Como posso reduzir os custos com a nuvem da minha empresa em 30% sem afetar o desempenho?

O agente pode responder rapidamente sem considerar todos os fatores necessários.

Isso pode resultar em:

```text id="0j5y2v"
Problema
   ↓
Resposta imediata
   ↓
Sugestões superficiais
   ↓
Possíveis decisões incompletas
```

---

## 🧭 Solução: planejamento estruturado

Problemas complexos se beneficiam de uma abordagem que permita ao agente:

1. **Dividir o problema**
2. **Identificar os fatores relevantes**
3. **Considerar diferentes alternativas**
4. **Avaliar as opções**
5. **Planejar uma abordagem**
6. **Produzir a resposta final**

O ADK fornece o **`BuiltInPlanner`** para adicionar esse comportamento de planejamento ao agente.

```text id="z9w3q1"
Problema complexo
       ↓
   Decomposição
       ↓
    Análise
       ↓
  Alternativas
       ↓
    Avaliação
       ↓
   Planejamento
       ↓
 Resposta final
```

---

### 🎯 Quando utilizar planejamento?

O planejamento é especialmente útil quando:

* A tarefa possui várias etapas.
* Existem restrições que precisam ser consideradas.
* É necessário comparar alternativas.
* Uma decisão depende de outras decisões.
* A qualidade da solução depende de uma análise mais cuidadosa.

Por outro lado, para perguntas simples e diretas, um agente sem planejamento pode ser mais eficiente.

---

### 💡 Principais aprendizados

1. Agentes reativos respondem diretamente às solicitações.
2. Problemas complexos podem exigir **raciocínio estruturado** antes da resposta.
3. Planejamento ajuda a decompor problemas e avaliar alternativas.
4. Nem toda tarefa precisa de planejamento.
5. **Planejamento** é diferente de **arquitetura multiagente**.
6. O planejamento é adequado quando um único agente precisa lidar com múltiplas etapas dentro de seu domínio.
7. O **`BuiltInPlanner`** do ADK permite adicionar capacidades de planejamento aos agentes.
8. A escolha entre resposta direta e planejamento deve considerar a **complexidade da tarefa**.

### 🔑 Conceitos-chave

`BuiltInPlanner` · `Planning` · `Reasoning` · `LlmAgent` · `Problem Decomposition` · `Multi-Step Reasoning` · `Alternative Evaluation` · `Multi-Agent Systems`
