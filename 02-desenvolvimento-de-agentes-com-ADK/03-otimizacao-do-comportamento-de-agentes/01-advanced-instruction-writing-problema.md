## 🧠 Google Cloud — Instruções Profissionais para Agentes de IA com ADK

### O Problema: instruções vagas criam comportamentos imprevissíveis

### 📚 Contexto

No módulo, um agente orientador de matemática criado anteriormente com o **Agent Development Kit (ADK)** é utilizado como ponto de partida para demonstrar a diferença entre uma instrução básica e uma instrução estruturada para uso em produção.

O agente inicial utilizava uma instrução simples:

```python
math_tutor_agent = LlmAgent(
    model="gemini-2.5-flash",
    name="math_tutor_agent",
    description="Orienta os estudantes em matemática",
    instruction="Você é um orientador de matemática cordial. Ajude os estudantes a entender os conceitos de matemática."
)
```

Embora funcional para testes simples, essa abordagem não define claramente como o agente deve se comportar em diferentes situações.

---

### ⚠️ Problema: instruções vagas

Instruções genéricas podem gerar comportamentos **imprevisíveis e inconsistentes**, especialmente quando o agente recebe solicitações fora do objetivo para o qual foi desenvolvido.

Uma instrução como:

```python
instruction="Seja prestativo"
```

não estabelece:

* 🎯 Quais tarefas estão dentro ou fora do escopo
* 🔄 Como lidar com situações inesperadas
* 💬 Qual tom e estilo utilizar
* 🚫 Quando uma solicitação deve ser recusada
* 📋 Como estruturar as respostas

---

### 🛠️ Evolução para instruções profissionais

O módulo apresenta práticas recomendadas para transformar instruções simples em **sistemas de orientação mais robustos**, estabelecendo um framework comportamental para o agente.

A estrutura de uma boa instrução deve considerar:

**Escopo → Metodologia → Exemplos → Casos extremos → Restrições → Comportamento esperado**

---

### 🧠 Principais aprendizados

* Estruturar instruções para agentes de IA
* Definir claramente o **escopo de atuação**
* Estabelecer metodologias de interação
* Utilizar exemplos para orientar o comportamento do LLM
* Definir respostas para solicitações fora do escopo
* Criar limites e restrições para o agente
* Melhorar consistência e previsibilidade das respostas
* Preparar agentes para cenários mais próximos de **produção**

---

### 💡 Conceito-chave

> **Instruções não são apenas comandos para o LLM; são um framework que define como o agente deve pensar, agir e responder dentro de um determinado contexto.**

---

### 🔗 Documentação relacionada

* [Google Agent Development Kit (ADK)](https://google.github.io/adk-docs/)
* [LlmAgent — ADK](https://google.github.io/adk-docs/agents/llm-agents/)
