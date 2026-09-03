## ⚙️ Google ADK — Configuração e Otimização de Modelos

### O problema: não existe uma abordagem única que sirva para todos os casos

### 📚 Contexto

Nos primeiros módulos, os agentes foram criados utilizando apenas as configurações básicas do modelo:

```python
agent = LlmAgent(
    model="gemini-2.5-flash",
    instruction="..."
)
```

Essa configuração funciona, porém utiliza os **valores padrão do modelo** para diferentes aspectos de geração e segurança.

À medida que os agentes se tornam mais complexos, é necessário ajustar essas configurações de acordo com o objetivo de cada tarefa.

---

### ⚠️ Limitações das configurações padrão

Utilizar sempre as configurações padrão pode resultar em:

* ❌ Falta de controle entre criatividade e consistência
* ❌ Ausência de configurações de segurança específicas
* ❌ Falta de controle sobre limites de tokens
* ❌ Uso das mesmas configurações para tarefas com necessidades diferentes
* ❌ Maior custo quando um modelo mais poderoso é utilizado sem necessidade

A principal ideia do módulo é:

> **Não existe uma configuração única que seja ideal para todos os tipos de agentes.**

Uma tarefa de escrita criativa, por exemplo, possui requisitos diferentes de uma tarefa de extração de dados ou classificação.

---

### 💰 Problema 1 — Modelo inadequado para a tarefa

Utilizar um modelo mais poderoso em uma tarefa simples pode gerar custos desnecessários.

```python
greeting_agent = LlmAgent(
    model="gemini-2.5-pro",
    instruction="Cumprimente o usuário de modo afetuoso"
)
```

Para uma tarefa simples como uma saudação, utilizar um modelo mais avançado pode ser um **excesso de capacidade em relação à necessidade da tarefa**.

A escolha do modelo deve considerar:

```text
Complexidade da tarefa
        ↓
Qualidade necessária
        ↓
Custo e desempenho
        ↓
Modelo adequado
```

---

### 🌡️ Problema 2 — Temperatura inadequada

A **temperatura** influencia o grau de aleatoriedade e criatividade das respostas do modelo.

Para tarefas factuais, como extração de informações, uma temperatura mais baixa tende a favorecer respostas mais consistentes.

Exemplo:

```python
factual_agent = LlmAgent(
    model="gemini-2.5-flash",
    instruction="Extraia as datas exatas dos documentos"
)
```

Para uma tarefa de extração precisa, utilizar uma configuração mais criativa pode aumentar a variabilidade desnecessariamente.

### 🔎 Comparação

| Tipo de tarefa       | Comportamento desejado |
| -------------------- | ---------------------- |
| 📝 Escrita criativa  | Maior criatividade     |
| 💬 Brainstorming     | Maior diversidade      |
| 📊 Extração de dados | Maior consistência     |
| 🔢 Tarefas factuais  | Maior previsibilidade  |
| 🧾 Classificação     | Respostas consistentes |

A temperatura deve, portanto, ser escolhida de acordo com o **comportamento esperado do agente**.

---

### 🛡️ Problema 3 — Configurações de segurança

Os agentes também podem exigir configurações de segurança específicas para determinados contextos.

```python
public_agent = LlmAgent(
    model="gemini-2.5-flash",
    instruction="Responda às perguntas dos clientes"
)
```

As configurações padrão podem não ser suficientes para aplicações que possuem requisitos específicos de:

* 🛡️ Segurança
* 🔐 Compliance
* 📋 Políticas internas
* 👥 Atendimento ao público
* 🚫 Controle de conteúdo

Por isso, o agente pode precisar de configurações personalizadas de segurança.

---

### 🎛️ `generate_content_config`

O ADK permite controlar parâmetros de geração utilizando o:

```python
generate_content_config
```

Esse recurso permite adaptar o comportamento do modelo às necessidades específicas de cada agente.

A ideia geral é:

```text
              Agente
                 │
                 ▼
        generate_content_config
                 │
       ┌─────────┼─────────┐
       ▼         ▼         ▼
  Criatividade  Tokens  Segurança
       │         │         │
       └─────────┼─────────┘
                 ▼
          Resposta otimizada
```

---

### 🎯 Configuração baseada na tarefa

Em vez de utilizar as mesmas configurações para todos os agentes, cada aplicação deve considerar seus próprios requisitos.

| Cenário                    | Prioridade                 |
| -------------------------- | -------------------------- |
| 🎨 Conteúdo criativo       | Diversidade e criatividade |
| 📊 Extração de dados       | Precisão e consistência    |
| 🔎 Análise factual         | Previsibilidade            |
| 💬 Atendimento             | Segurança e qualidade      |
| 💰 Tarefas simples         | Eficiência e custo         |
| 🏢 Aplicações corporativas | Segurança + compliance     |

---

### 💡 Principal aprendizado

A configuração de um agente não deve ser tratada como algo fixo.

A escolha do **modelo** e dos parâmetros de geração deve considerar:

**Tarefa → Qualidade → Consistência → Segurança → Custo**

O `generate_content_config` permite transformar uma configuração genérica em uma configuração **otimizada para o contexto específico do agente**.

### 🔑 Conceitos-chave

`LlmAgent` · `generate_content_config` · `temperature` · `max_output_tokens` · `Safety Settings` · `Model Selection` · `Criatividade` · `Consistência` · `Segurança` · `Custo`
