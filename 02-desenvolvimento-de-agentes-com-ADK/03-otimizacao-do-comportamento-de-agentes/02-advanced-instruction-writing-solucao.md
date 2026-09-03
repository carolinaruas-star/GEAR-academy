## 🧩 Instruções Estruturadas para Agentes de IA

### A solução: instruções estruturadas

### 🎯 A solução

O parâmetro `instruction` é um dos principais elementos para definir o comportamento de um `LlmAgent`. Para criar agentes mais previsíveis e adequados a ambientes de produção, as instruções devem estabelecer:

1. **Tarefa ou meta principal** — o que o agente deve realizar
2. **Personalidade/Persona** — como o agente deve se apresentar
3. **Restrições de comportamento** — o que o agente não deve fazer
4. **Formato de saída** — como as respostas devem ser estruturadas

As instruções podem ser definidas como uma **string**, utilizar variáveis de estado com a sintaxe `{var}` ou, em cenários avançados, utilizar funções que retornam instruções dinamicamente.

---

### 🧠 Cinco padrões para instruções profissionais

O ADK recomenda estruturar as instruções utilizando **Markdown**, organizando o comportamento do agente em cinco padrões principais:

#### 1. 👤 Identidade

Define **quem é o agente**, seu papel e sua especialização.

```text
# Sua identidade

Você é [nome], um(a) [papel/cargo] com [experiência/especialização].
```

**Objetivo:** estabelecer uma persona consistente e orientar o tom e a perspectiva do agente.

---

#### 2. 🎯 Missão

Define **qual é o objetivo principal** do agente e quais princípios devem ser mantidos durante sua execução.

```text
# Sua missão

[Meta principal] e [manter qualidade/restrições].
```

**Objetivo:** manter o agente focado na tarefa e reduzir desvios de escopo.

---

#### 3. 🔄 Metodologia

Estabelece um **fluxo de trabalho estruturado**, dividindo tarefas complexas em etapas.

```text
# Como você trabalha

1. **[Etapa 1]** — [descrição]
2. **[Etapa 2]** — [descrição]
3. **[Etapa 3]** — [descrição]
4. **[Etapa 4]** — [descrição]
```

Um fluxo de 3 a 5 etapas costuma ser suficiente para tornar o comportamento mais consistente e previsível.

**Exemplo:**

**Reconhecer → Esclarecer → Resolver → Verificar**

---

#### 4. 🛡️ Limites

Define explicitamente **o que o agente nunca deve fazer**, funcionando como uma camada adicional de controle específica ao papel do agente.

Os limites podem ser divididos em:

* **Escopo:** atividades fora da função do agente
* **Qualidade:** prevenção de informações inventadas e alucinações
* **Privacidade e segurança:** proteção de dados e informações sensíveis

Exemplos:

```text
## O que você nunca deve fazer

- Nunca invente informações.
- Nunca compartilhe dados protegidos.
- Nunca faça promessas que não pode cumprir.

## Como você mantém a qualidade

- Sempre utilize informações disponíveis e confiáveis.
- Se não souber algo, admita a limitação.
- Nunca adivinhe uma resposta.
```

Os limites definidos nas instruções **complementam as configurações de segurança do modelo**, permitindo estabelecer regras específicas para o papel desempenhado pelo agente.

---

#### 5. 💬 Exemplos Few-Shot

Apresenta exemplos completos de **entrada do usuário → resposta esperada**, permitindo demonstrar ao LLM o comportamento desejado.

Os exemplos devem contemplar:

* Situações comuns
* Casos extremos
* Perguntas fora do escopo
* Informações insuficientes
* Situações que exigem recusa

**Objetivo:** orientar o tom, a estrutura, a formulação das respostas e o comportamento esperado em situações específicas.

---

### 📋 Boas práticas do ADK

As instruções profissionais devem ser:

| Prática                                  | Objetivo                                          |
| ---------------------------------------- | ------------------------------------------------- |
| 🎯 **Claras e específicas**              | Reduzir ambiguidades                              |
| 📝 **Formatadas em Markdown**            | Melhorar organização e compreensão                |
| 💬 **Com exemplos Few-Shot**             | Demonstrar comportamentos esperados               |
| 🛠️ **Orientadas ao uso de ferramentas** | Definir quando e por que utilizar cada ferramenta |
| 🔒 **Com limites explícitos**            | Controlar escopo, qualidade e segurança           |

O ADK também oferece recursos avançados, como:

* Modelagem de estado com `{var}`
* `InstructionProvider` para instruções dinâmicas
* Instruções globais para sistemas multiagente

---

### 🛠️ Exemplo prático — Agente de Suporte

Como aplicação dos cinco padrões, foi desenvolvido um agente de suporte técnico utilizando `LlmAgent` e `gemini-2.5-flash`.

**Persona:** Alex Chen, especialista sênior em suporte técnico.

**Missão:** ajudar clientes a resolver problemas técnicos com eficiência e profissionalismo.

**Metodologia:**

```text
Reconhecer → Esclarecer → Resolver → Verificar
```

**Limites definidos:**

* Não fornecer senhas ou acesso a contas
* Não compartilhar informações de outros clientes
* Não inventar informações técnicas
* Não fornecer aconselhamento jurídico, financeiro ou médico
* Encaminhar solicitações específicas para as equipes responsáveis

**Comportamento esperado:** manter uma comunicação profissional, amigável, clara, paciente e objetiva.

---

### 🧪 Testes realizados

O agente pode ser validado utilizando diferentes cenários:

| Cenário                                 | Comportamento esperado                       |
| --------------------------------------- | -------------------------------------------- |
| 🔐 Problema de login                    | Fazer perguntas para diagnosticar o problema |
| 🔒 Solicitação de dados de terceiros    | Recusar de forma profissional                |
| 🚀 Pergunta sobre lançamento de recurso | Encaminhar para a equipe de produtos         |
| ❓ Informação insuficiente               | Solicitar esclarecimentos                    |

Esses testes demonstram como os cinco padrões trabalham em conjunto para produzir um agente **mais consistente, previsível e alinhado ao seu propósito**.

---

### 💡 Principais aprendizados

> **Uma boa instrução transforma um LLM genérico em um agente com comportamento definido.**

Os cinco padrões formam uma estrutura reutilizável:

**👤 Identidade → 🎯 Missão → 🔄 Metodologia → 🛡️ Limites → 💬 Exemplos**

A combinação desses elementos permite criar agentes com **escopo bem definido, comportamento consistente, maior controle sobre respostas e melhor preparação para ambientes de produção**.

---

### 🔗 Documentação

* [Google Agent Development Kit (ADK)](https://google.github.io/adk-docs/)
* [LlmAgent — ADK](https://google.github.io/adk-docs/agents/llm-agents/)
* [Modelagem de estado — ADK](https://google.github.io/adk-docs/agents/llm-agents/#structuring-data-input_schema-output_schema-output_key)
