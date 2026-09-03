# ⚙️ Duas maneiras de definir agentes no ADK

O **Google ADK (Agent Development Kit)** oferece duas formas principais de definir agentes:

* 🐍 **Código Python**
* 📄 **Configuração YAML (Agent Config)**

As duas abordagens podem produzir agentes com o **mesmo comportamento**, mas cada uma é mais adequada para diferentes situações.

---

## 🐍 1. Definição com código Python

Nos módulos anteriores, os agentes foram criados diretamente no arquivo `agent.py`:

```python
from google.adk.agents.llm_agent import Agent

root_agent = Agent(
    model='gemini-2.5-flash',
    name='math_tutor_agent',
    description='Ajuda estudantes a aprender álgebra',
    instruction='Você é um orientador de matemática paciente...'
)
```

Esse método oferece maior flexibilidade e é especialmente importante para agentes que precisam de:

* lógica personalizada;
* ferramentas próprias;
* callbacks;
* integração com outras bibliotecas;
* arquiteturas multiagente;
* controle programático.

### Estrutura do projeto

Criado com:

```bash
adk create my_agent
```

Gera:

```text
my_agent/
├── agent.py
├── __init__.py
└── .env
```

---

# 📄 2. Definição com YAML — Agent Config

O **Agent Config** permite definir um agente usando um arquivo de configuração no formato **YAML**, reduzindo a necessidade de escrever código.

Criado com:

```bash
adk create --type=config my_agent
```

Gera:

```text
my_agent/
├── root_agent.yaml
└── .env
```

O arquivo `root_agent.yaml` contém diretamente as configurações do agente:

```yaml
name: assistant_agent
model: gemini-2.5-flash
description: Um assistente colaborativo
instruction: Você é um assistente colaborativo.
```

Em vez de importações, classes e parênteses, temos simplesmente **pares de chave e valor**.

---

## 🧩 Os quatro parâmetros principais

O YAML utiliza os mesmos conceitos aprendidos nos módulos anteriores:

| Parâmetro     | Função                                 |
| ------------- | -------------------------------------- |
| `name`        | Identificador exclusivo do agente      |
| `model`       | LLM utilizado pelo agente              |
| `description` | Explica o que o agente faz             |
| `instruction` | Define como o agente deve se comportar |

---

# ✏️ 3. Instruções com múltiplas linhas

O YAML permite utilizar `|` para representar um texto com várias linhas:

```yaml
instruction: |
  Você é um orientador de álgebra paciente e motivador.

  Seu método de ensino:
  1. Entenda a dificuldade do estudante
  2. Divida o problema em etapas menores
  3. Oriente o estudante até a resposta
  4. Incentive o raciocínio
  5. Use linguagem simples
```

### 💡 Por que usar `|`?

É especialmente útil para **instruções longas e detalhadas**, pois permite escrever o conteúdo de maneira natural e organizada.

---

# 🧮 4. Exemplo: agente tutor de matemática

O mesmo agente criado anteriormente em Python pode ser configurado em YAML:

```yaml
name: math_tutor_agent
model: gemini-2.5-flash

description: Ajuda estudantes a aprender álgebra com orientação pelas etapas de solução de problemas.

instruction: |
  Você é um orientador de álgebra paciente e motivador.

  Seu método de ensino:
  1. Quando um estudante faz uma pergunta, primeiro entenda a dificuldade dele
  2. Divida o problema em etapas menores e viáveis
  3. Oriente-o a encontrar a resposta em vez de responder diretamente
  4. Incentive o trabalho de raciocínio e conquista
  5. Use linguagem simples e evite jargões

  Sempre mantenha um tom calmo e apoiador.
```

---

# 🚀 5. Executando um agente YAML

A execução é praticamente igual à de um agente criado em Python.

No diretório pai do projeto:

```bash
adk web my_config_agent
```

O ADK:

1. 📂 Localiza o projeto;
2. 📄 Carrega o `root_agent.yaml`;
3. 🤖 Cria o agente com base na configuração;
4. 🌐 Inicia a interface web.

O agente pode ser utilizado normalmente.

### Exemplo de teste

```text
Como resolvo 2x + 5 = 13?
```

O agente deve orientar o estudante pelas etapas da resolução, seguindo as instruções definidas no YAML.

---

# ⚖️ YAML × Python

Embora produzam agentes equivalentes, os dois métodos possuem características diferentes.

| Aspecto                        | 📄 YAML        | 🐍 Python             |
| ------------------------------ | -------------- | --------------------- |
| Facilidade de edição           | ✅ Muito fácil  | ⚠️ Requer programação |
| Prototipagem rápida            | ✅ Excelente    | ✅                     |
| Não programadores              | ✅ Podem editar | ❌ Mais difícil        |
| Controle programático          | ⚠️ Limitado    | ✅ Completo            |
| Lógica personalizada           | ⚠️ Limitada    | ✅                     |
| Ferramentas personalizadas     | ⚠️ Limitado    | ✅                     |
| Callbacks                      | ⚠️ Limitado    | ✅                     |
| Sistemas multiagente complexos | ⚠️ Limitado    | ✅                     |
| Separação configuração/código  | ✅ Excelente    | ⚠️ Menos direta       |

---

# 📄 Quando escolher YAML?

O **YAML** é uma boa escolha quando você precisa de:

### 👥 Colaboração entre equipes

Pessoas que não programam podem alterar configurações do agente sem precisar modificar código Python.

### ⚡ Experimentos rápidos

É possível testar rapidamente:

* diferentes instruções;
* diferentes modelos;
* diferentes configurações.

Basta editar o YAML e reiniciar o agente.

### 🧹 Simplicidade

Para agentes simples, o arquivo YAML pode ser muito mais fácil de ler e manter.

### 🔀 Separação entre configuração e código

A configuração do agente fica separada da lógica de programação, facilitando diferentes configurações para desenvolvimento, teste e produção.

---

# 🐍 Quando escolher Python?

O **Python** se torna mais adequado quando o agente precisa de funcionalidades avançadas.

### 🤖 Sistemas multiagente

Arquiteturas envolvendo:

* delegação;
* agentes de fluxo de trabalho;
* orquestração personalizada.

### 🔧 Ferramentas personalizadas

Quando o agente precisa executar ferramentas desenvolvidas especificamente para a aplicação.

### 🔄 Callbacks

Recursos avançados de controle do comportamento do agente exigem código Python.

### 🧠 Controle programático

Python permite gerar configurações dinamicamente, alterar comportamentos de acordo com condições do ambiente e integrar o agente com outras bibliotecas.

---

# 🔍 Comparação lado a lado

O mesmo agente pode ser definido das duas maneiras.

### Python — `agent.py`

```python
from google.adk.agents.llm_agent import Agent

root_agent = Agent(
    model='gemini-2.5-flash',
    name='greeting_agent',
    description='Um agente de saudação amigável',
    instruction='Cumprimente os usuários de modo afetuoso e profissional.'
)
```

### YAML — `root_agent.yaml`

```yaml
name: greeting_agent
model: gemini-2.5-flash
description: Um agente de saudação amigável
instruction: Cumprimente os usuários de modo afetuoso e profissional.
```

### Resultado

Os dois representam o **mesmo agente**, com:

* mesmo modelo;
* mesmo nome;
* mesma descrição;
* mesma instrução;
* mesmo comportamento.

A principal diferença está na **forma como o agente é definido**.

---

# 🧠 Uma forma simples de lembrar

```text
              DEFINIR UM AGENTE
                     │
          ┌──────────┴──────────┐
          │                     │
      🐍 PYTHON              📄 YAML
          │                     │
    Mais flexibilidade     Mais simplicidade
          │                     │
    Lógica personalizada    Configuração
    Ferramentas             Prototipagem
    Callbacks               Colaboração
    Multiagentes            Edição rápida
          │                     │
          └──────────┬──────────┘
                     │
               🤖 AGENTE ADK
```

---

# 🌐 Compatibilidade de linguagens

O ADK possui suporte a diferentes linguagens, mas existe uma diferença importante:

* 🐍 **Python:** suporte ao código Python **e** ao Agent Config com YAML.
* ☕ **Java:** compatível com agentes baseados em código Python, conforme a documentação apresentada no curso.
* 📄 **Agent Config/YAML:** neste módulo, o recurso é apresentado como **exclusivo para Python**.

> ⚠️ O Agent Config é apresentado como um recurso experimental, com algumas limitações conhecidas.

---

# 🏆 Principais aprendizados

* O ADK oferece **duas maneiras de definir agentes**: Python e YAML.
* O **Python** oferece maior controle e flexibilidade.
* O **YAML** simplifica a configuração de agentes.
* Os dois métodos podem produzir **agentes equivalentes**.
* `adk create --type=config` cria um agente baseado em `root_agent.yaml`.
* `adk web`, `adk run` e `adk api_server` podem ser utilizados com as duas abordagens.
* YAML é especialmente útil para **agentes simples, prototipagem e colaboração**.
* Python é essencial para **ferramentas personalizadas, callbacks e sistemas multiagente complexos**.
* É possível **começar com YAML e migrar para Python** quando o projeto exigir mais recursos.
* O **Agent Config/YAML é apresentado como recurso disponível para Python**.

---

## 🎯 Regra prática

> **YAML para simplicidade. Python para flexibilidade.**

Não existe uma opção universalmente melhor. A escolha depende da complexidade e das necessidades do agente.
