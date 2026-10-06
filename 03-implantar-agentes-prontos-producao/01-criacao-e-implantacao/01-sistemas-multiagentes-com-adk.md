# Sistemas Multiagentes com ADK

Sistemas multiagentes permitem dividir uma aplicação em diferentes agentes, cada um especializado em uma determinada tarefa. No **Agent Development Kit (ADK)**, esses agentes podem ser organizados em uma estrutura hierárquica e coordenados por diferentes tipos de agentes de fluxo de trabalho.

---

## 🌳 Estrutura de agentes

No ADK, os agentes podem ser organizados em uma **árvore hierárquica**, formada por agentes pai/mãe e seus subagentes.

Os agentes podem transferir a conversa para:

* **Subagentes:** agentes que estão abaixo dele na hierarquia;
* **Agente pai/mãe:** agente responsável por sua execução;
* **Agentes peer:** outros agentes que compartilham o mesmo agente pai/mãe.

Também é possível **desativar a transferência para agentes peer individualmente**.

Essa estrutura em árvore ajuda a tornar o comportamento do sistema mais **previsível e confiável**, pois limita quais agentes podem assumir determinada parte da conversa.

### Por que utilizar uma estrutura hierárquica?

Imagine um sistema em que qualquer agente pudesse transferir uma conversa para qualquer outro agente. Se existissem vários agentes especializados em pesquisas diferentes, poderia ser difícil garantir que a solicitação chegasse ao agente correto.

Com a hierarquia, a transferência fica mais controlada e o sistema consegue direcionar a conversa para os agentes relacionados àquela parte do fluxo.

---

# 🧠 Agentes baseados em LLM

Os agentes baseados em **Large Language Models (LLMs)** funcionam como o "cérebro" da aplicação.

Eles utilizam modelos de linguagem para:

* compreender linguagem natural;
* responder às solicitações dos usuários;
* tomar decisões;
* utilizar ferramentas;
* adaptar seu comportamento de acordo com o contexto.

Normalmente, esses agentes trabalham alternando turnos de conversa com o usuário.

Quando é necessário executar vários agentes automaticamente, sem depender de um turno de conversa entre cada um, podemos utilizar **agentes de fluxo de trabalho**.

---

# ⚙️ Agentes de fluxo de trabalho

Os **agentes de fluxo de trabalho (workflow agents)** são responsáveis por **orquestrar a execução de outros agentes**.

Diferentemente dos agentes baseados em LLM, eles não possuem necessariamente um modelo de linguagem associado e **não tomam decisões de forma autônoma**.

Seu papel é determinar:

* quais agentes serão executados;
* em qual ordem;
* em quais condições;
* como o contexto será encaminhado entre eles.

Por isso, seus fluxos geralmente são **determinísticos**.

> Para uma determinada entrada e configuração, a sequência de execução tende a ser a mesma.

Essa previsibilidade é especialmente útil em processos estruturados nos quais consistência e confiabilidade são importantes.

---

# 🔢 SequentialAgent

O `SequentialAgent` executa uma lista de agentes **um após o outro**, seguindo uma ordem predefinida.

### Exemplo

Um fluxo para **processar um novo pedido** poderia ser:

```text
Agente de validação
        ↓
Agente de estoque
        ↓
Agente de pagamento
        ↓
Agente de confirmação
```

Cada agente executa sua tarefa antes que o próximo seja acionado.

### Quando utilizar?

É adequado quando existe uma **dependência ou sequência lógica** entre as etapas de um processo.

---

# 🔄 LoopAgent

O `LoopAgent` executa repetidamente um conjunto de agentes até que uma determinada condição seja atingida.

É útil para processos que exigem:

* refinamento iterativo;
* monitoramento contínuo;
* tarefas cíclicas;
* negociação simulada;
* tentativa e melhoria de resultados.

### Exemplo

Um sistema de pesquisa poderia seguir o fluxo:

```text
Pesquisar dados
      ↓
Analisar dados
      ↓
A resposta é suficiente?
   ↙          ↘
 Não           Sim
 ↓              ↓
Pesquisar     Finalizar
novamente
```

Enquanto o resultado não for considerado satisfatório, o fluxo pode continuar sendo executado.

---

# ⚡ ParallelAgent

O `ParallelAgent` permite executar vários agentes **simultaneamente**.

Isso pode melhorar o desempenho quando uma tarefa pode ser dividida em subtarefas independentes.

### Exemplo

Um sistema de geração de relatórios pode executar simultaneamente:

```text
              ┌─ Relatório Região A
              │
Solicitação ──┼─ Relatório Região B
              │
              └─ Relatório Região C
```

Em vez de esperar uma região terminar para iniciar a próxima, os agentes trabalham em paralelo.

### Quando utilizar?

É especialmente útil para:

* buscar dados em diferentes fontes;
* executar cálculos independentes;
* gerar relatórios simultaneamente;
* dividir tarefas pesadas em subtarefas.

> A execução paralela não pressupõe que os agentes precisem compartilhar estado ou trocar informações diretamente entre si.

---

# 🛠️ Agentes de fluxo de trabalho personalizados

Além dos agentes `SequentialAgent`, `LoopAgent` e `ParallelAgent`, o ADK permite criar **agentes de fluxo de trabalho personalizados**.

Eles possibilitam definir uma lógica de orquestração específica para necessidades que não se encaixam nos padrões predefinidos.

Podem ser utilizados para implementar:

* fluxos complexos;
* regras de negócio específicas;
* interações que dependem de estado;
* combinações personalizadas de diferentes agentes;
* lógicas próprias de orquestração.

Isso oferece maior flexibilidade para construir sistemas multiagentes mais complexos.

---

# 📌 Comparando os agentes de fluxo de trabalho

| Agente            | Funcionamento                   | Principal utilização                   |
| ----------------- | ------------------------------- | -------------------------------------- |
| `SequentialAgent` | Executa agentes em sequência    | Processos com etapas ordenadas         |
| `LoopAgent`       | Repete agentes até uma condição | Refinamento e processos iterativos     |
| `ParallelAgent`   | Executa agentes simultaneamente | Tarefas independentes e paralelizáveis |
| Personalizado     | Define uma lógica própria       | Fluxos complexos e regras específicas  |

---

# 💡 Conceito principal

Um sistema multiagente no ADK pode combinar **agentes inteligentes baseados em LLM** com **agentes de fluxo de trabalho responsáveis pela orquestração**.

De forma simplificada:

```text
                 Sistema Multiagente
                        │
          ┌─────────────┴─────────────┐
          │                           │
    Agentes LLM              Workflow Agents
          │                           │
   Tomam decisões              Controlam o fluxo
   Usam ferramentas             Determinam a ordem
   Entendem linguagem           Coordenam agentes
          │                           │
          └─────────────┬─────────────┘
                        │
                Aplicação multiagente
```

A combinação desses componentes permite criar sistemas em que cada agente possui uma responsabilidade específica, enquanto a estrutura de agentes e os workflows determinam **como essas responsabilidades são coordenadas**.

## ✨ Resumindo

* Sistemas multiagentes podem ser organizados em uma **estrutura hierárquica de agentes**.
* A hierarquia restringe as possibilidades de transferência e aumenta a previsibilidade do sistema.
* **Agentes baseados em LLM** são responsáveis por compreensão, decisões e uso de ferramentas.
* **Agentes de fluxo de trabalho** controlam a execução de outros agentes.
* `SequentialAgent` executa agentes em sequência.
* `LoopAgent` repete agentes até uma condição ser atendida.
* `ParallelAgent` executa agentes simultaneamente.
* Agentes de fluxo de trabalho personalizados permitem implementar **lógicas de orquestração específicas**.
