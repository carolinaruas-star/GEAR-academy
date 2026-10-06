# 🤖 Aula 9 — Crie seu próprio agente

## 🎯 Visão geral

Depois de conhecer modelos, engenharia de comandos, ferramentas, RAG, pesquisa e engajamento do cliente, esta aula apresenta uma aplicação prática: **criar e testar um agente de conversação**.

O processo utiliza o **Google AI Studio** para criar um chatbot contextualizado para a empresa fictícia **Cymbal Manufacturing**.

A aula apresenta dois conceitos principais:

* 📋 **Playbooks**, que definem como um agente deve agir;
* 🧠 **Instruções do sistema**, que orientam o comportamento de um LLM.

Também apresenta a técnica de **metacomando**, utilizada para gerar outros comandos.

---

# 📋 Criação de playbooks

Ao criar um agente de IA generativa com agentes de conversação, pode-se criar um **playbook** que define como o agente deve agir.

No playbook são definidos:

* 🎯 a meta do agente;
* 📌 instruções detalhadas;
* 📏 regras de comportamento;
* 🔗 ferramentas externas que o agente pode utilizar.

Entre os objetivos possíveis estão:

* oferecer suporte ao cliente;
* responder perguntas;
* gerar conteúdo;
* realizar outras tarefas específicas.

Depois de configurar o playbook, é possível **testar e interagir com o agente**.

```text id="q4n8sz"
Objetivo
   ↓
Instruções
   ↓
Regras
   ↓
Ferramentas externas
   ↓
Playbook
   ↓
Agente
   ↓
Teste e interação
```

---

# 🧪 Atividade prática: criar um agente

A atividade apresenta a empresa fictícia **Cymbal Manufacturing**, fabricante de máquinas e contêineres de armazenamento.

A empresa deseja implementar um chatbot no próprio site para:

* responder perguntas comuns;
* fornecer informações sobre produtos;
* solucionar problemas básicos.

Para isso, a atividade utiliza o **Google AI Studio**.

O objetivo é aprender a definir:

* 👤 personalidade;
* 📚 conhecimento;
* ⚙️ comportamento;
* 🚧 restrições;

por meio das **instruções do sistema**.

---

# 🧠 O que são instruções do sistema?

As **instruções do sistema** permitem fornecer contexto, perfil e restrições ao LLM **antes das entradas do usuário**.

Elas orientam o comportamento do modelo para que suas respostas estejam alinhadas ao resultado desejado.

Podemos pensar nelas como uma espécie de **manual de comportamento do agente**.

```text id="k2r5vm"
Instruções do sistema
        ↓
Contexto + Perfil + Restrições
        ↓
       LLM
        ↓
Comportamento esperado
```

---

## 🎯 Benefícios das instruções do sistema

### Consistência

Permitem manter um tom e um perfil consistentes durante as interações.

### 🎯 Acurácia

Podem fornecer conhecimento específico ao modelo e ajudar a reduzir alucinações.

### 📌 Relevância

Mantêm as respostas concentradas no domínio definido para o agente.

### 🔐 Segurança

Podem estabelecer restrições para evitar conteúdo inadequado ou respostas que não sejam úteis.

---

# ⚠️ Agentes empresariais

A atividade utiliza o Google AI Studio por ser uma ferramenta acessível para um público mais amplo.

Porém, a aula destaca que um agente de conversação **realmente preparado para uso empresarial** exige ferramentas e técnicas mais avançadas.

Para agentes de produção com recursos mais robustos, como mecanismos de defesa contra ataques, o curso recomenda conhecer melhor os **agentes conversacionais do Google Cloud**.

---

# 🛠️ Criando o chatbot da Cymbal Manufacturing

A atividade é dividida em cinco etapas.

---

## 1️⃣ Configurar o Google AI Studio

Primeiro, o ambiente é configurado para criar o chatbot.

### Passos

1. Acessar o Google AI Studio.
2. Selecionar **Chat** no menu lateral.
3. Abrir as **Configurações de execução**.
4. Selecionar o modelo atual.
5. Escolher **Gemini 2.5 Flash**.

---

# 2️⃣ Gerar as instruções do sistema

Em vez de escrever manualmente as instruções finais do chatbot, a atividade utiliza um **modelo de IA para gerar essas instruções**.

É criado um agente especializado em escrever instruções de sistema.

A ideia é fornecer ao modelo a tarefa de:

* criar uma meta específica;
* produzir instruções;
* gerar um comando que possa ser utilizado posteriormente por outro agente.

O comando é então salvo no Google AI Studio como **Agente escritor de instruções**.

---

# 3️⃣ Gerar as instruções para o chatbot

Depois de criar o agente escritor, ele recebe as informações necessárias para gerar as instruções do chatbot da Cymbal Manufacturing.

### Informações fornecidas

* **Empresa:** Cymbal Manufacturing
* **Atividade:** fabricação de contêineres de armazenamento
* **Serviço adicional:** usinagem personalizada mediante solicitação
* **Regra:** solicitações de usinagem personalizada devem ser direcionadas à empresa por telefone
* **Produtos:** geralmente azuis ou verdes, podendo ocasionalmente ser vermelhos
* **Comportamento:** responder dentro do escopo da fabricação de contêineres
* **Restrição:** não inventar informações
* **Tom:** respeitoso
* **Transparência:** admitir quando não souber uma resposta

O modelo gera então o comando do sistema que será utilizado no chatbot final.

---

# 4️⃣ Criar o chatbot da Cymbal Manufacturing

Com as instruções geradas, é criado um novo chat.

As instruções do sistema produzidas anteriormente são copiadas para o chatbot.

O agente recebe o nome:

**Chatbot da Cymbal Manufacturing**

A partir desse momento, o chatbot passa a utilizar as instruções definidas para orientar suas respostas.

```text id="u6m3px"
Agente escritor
      ↓
Gera instruções
      ↓
Instruções do sistema
      ↓
Chatbot da Cymbal Manufacturing
      ↓
Respostas orientadas pelo contexto
```

---

# 5️⃣ Testar o agente

Depois de criado, o chatbot deve ser testado com diferentes tipos de solicitações.

### Exemplos

**👋 Saudação**

> Oi.

**📦 Pergunta sobre produto**

> Qual é a cor dos contêineres?

**📏 Pergunta sobre características**

> Quais são os tamanhos disponíveis?

**🏭 Fabricação personalizada**

> Vocês fazem usinagem personalizada?

**🌦️ Pergunta fora do escopo**

> Como está a previsão do tempo?

Esses testes permitem observar se o agente:

* segue suas instruções;
* permanece dentro do domínio definido;
* reconhece quando não possui uma informação;
* respeita suas restrições;
* mantém o comportamento esperado.

---

# 🧪 O que o teste demonstra?

A atividade mostra que **criar um agente não significa apenas conectar um modelo a uma interface de chat**.

É necessário definir seu comportamento.

```text id="c7v2ha"
Modelo
  +
Contexto
  +
Instruções
  +
Restrições
  +
Conhecimento
  ↓
Agente especializado
```

---

# 🧩 Metacomando

Um dos principais conceitos apresentados nesta aula é o **metacomando**.

Um metacomando é um comando utilizado para orientar a IA a:

* gerar outros comandos;
* modificar comandos;
* interpretar comandos.

Na atividade, isso acontece quando a IA é utilizada para **criar as próprias instruções do sistema** que serão utilizadas pelo chatbot.

```text id="w8n4yr"
Usuário
   ↓
Metacomando
   ↓
IA
   ↓
Instruções do sistema
   ↓
Agente final
```

---

## 💡 Por que usar metacomandos?

Os metacomandos podem tornar o processo de criação de prompts mais:

* 🔄 dinâmico;
* 🧩 flexível;
* ⚙️ adaptável;
* 🚀 eficiente.

Eles permitem utilizar um LLM para ajudar a criar, modificar ou interpretar comandos destinados a outros usos.

---

# 🔗 Playbook × instruções do sistema

Os conceitos apresentados possuem funções relacionadas, mas não são exatamente a mesma coisa.

| Conceito                 | Função                                                  |
| ------------------------ | ------------------------------------------------------- |
| 📋 Playbook              | Define como o agente deve agir                          |
| 🧠 Instruções do sistema | Orientam o comportamento do LLM                         |
| 🔗 Ferramentas           | Permitem acesso a recursos externos                     |
| 🪄 Metacomando           | Orienta a IA a criar, modificar ou interpretar comandos |

No contexto dos agentes de conversação, o playbook pode reunir instruções, regras e ferramentas necessárias para alcançar o objetivo do agente.

---

# 🧠 Principais aprendizados

* 🤖 Agentes de conversação podem ser configurados por meio de **playbooks**.
* 📋 Um playbook pode definir metas, instruções, regras e ferramentas externas.
* 🧠 As **instruções do sistema** orientam o LLM antes das entradas do usuário.
* 🎯 Instruções bem definidas ajudam a melhorar consistência, acurácia, relevância e segurança.
* 🧪 O Google AI Studio pode ser utilizado para criar e testar agentes de conversação básicos.
* 🔄 Um agente pode ser utilizado para gerar as instruções de outro agente.
* 🪄 Essa técnica é chamada de **metacomando**.
* 🏢 Agentes empresariais de produção exigem recursos e técnicas mais avançados.
* 🔗 Agentes de conversação podem ser conectados a ferramentas e repositórios de dados.

> 🎯 **Conclusão:** Criar um agente envolve muito mais do que escolher um modelo. É necessário definir seu objetivo, contexto, comportamento, regras e, quando necessário, suas ferramentas. Os playbooks e as instruções do sistema ajudam a orientar esse comportamento, enquanto os metacomandos permitem utilizar a própria IA para criar e aperfeiçoar comandos. A atividade com a Cymbal Manufacturing demonstra esse processo de forma prática, desde a geração das instruções até o teste do agente.
