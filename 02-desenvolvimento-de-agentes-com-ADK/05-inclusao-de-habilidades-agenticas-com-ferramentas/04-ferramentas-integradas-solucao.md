# 🔧 A solução: ferramentas integradas

<p align="center">
  <strong>Recursos prontos para produção</strong>
</p>

<p align="center">
  <strong>Ampliando as capacidades dos agentes sem reinventar ferramentas comuns.</strong>
</p>

---

## 💡 Introdução

Na etapa anterior, vimos que implementar recursos comuns, como **pesquisa na web** e **execução de código**, pode exigir um esforço significativo de engenharia.

O ADK oferece uma alternativa: **ferramentas integradas** (*built-in tools*).

Segundo a documentação do ADK, essas ferramentas fornecem recursos prontos para uso, como **Pesquisa Google** e **execução de código**, permitindo que os agentes tenham acesso a capacidades comuns sem que o desenvolvedor precise implementar toda a infraestrutura.

A mudança de abordagem é:

```text
❌ Implementar do zero
       │
       ├── API
       ├── Autenticação
       ├── Tratamento de erros
       ├── Formatação
       ├── Manutenção
       └── Monitoramento
              │
              ▼
        ⏳ Alto esforço


🔧 Ferramenta integrada
       │
       ▼
   Importar e usar
       │
       ▼
⚡ Recurso pronto para produção
```

---

## 🧩 Ferramentas integradas disponíveis

O ADK disponibiliza diferentes ferramentas integradas para ampliar as capacidades dos agentes:

| Ferramenta                     | Capacidade                          |
| ------------------------------ | ----------------------------------- |
| 🔎 **Pesquisa Google**         | Pesquisa na web em tempo real       |
| 🐍 **Execução de código**      | Executa código Python               |
| 📚 **Vertex AI para Pesquisa** | Pesquisa documentos empresariais    |
| 🧠 **RAG da Vertex AI**        | Recuperação aumentada de documentos |
| 🗄️ **BigQuery**               | Consulta data warehouses            |
| 💾 **Spanner**                 | Consulta bancos de dados Spanner    |
| 🗃️ **Bigtable**               | Consulta dados do Bigtable          |

Nesta etapa introdutória, o foco está em duas ferramentas:

### 🔎 Pesquisa Google

Permite obter **informações atuais da web**, sendo especialmente útil quando o agente precisa trabalhar com dados que podem ter mudado após o treinamento do modelo.

### 🐍 Execução de código

Permite realizar **cálculos, processamento de dados e operações computacionais** com maior precisão.

---

## 🗺️ Visão geral

```text
                    🔧 FERRAMENTAS INTEGRADAS
                              │
          ┌───────────────────┴───────────────────┐
          │                                       │
          ▼                                       ▼
    🔎 Pesquisa Google                    🐍 Execução de código
          │                                       │
          ▼                                       ▼
 🌐 Web em tempo real                  ⚙️ Execução em Python
          │                                       │
          └───────────────────┬───────────────────┘
                              │
              ┌───────────────┼───────────────┐
              ▼               ▼               ▼
       📚 Vertex AI       🧠 RAG          🗄️ BigQuery
       para Pesquisa      Vertex AI
              │
              ├────────── 💾 Spanner
              │
              └────────── 🗃️ Bigtable
```

---

# 1. 🔎 Ferramenta Pesquisa Google

A ferramenta `google_search` permite que o agente realize **pesquisas na web utilizando a Pesquisa Google**.

Ela é especialmente útil para perguntas que exigem informações atuais.

### O que oferece?

* 🌐 Resultados de pesquisa na web em tempo real;
* 📰 Informações atualizadas;
* 🔗 Fontes para fundamentar as respostas;
* 🎯 Sugestões de pesquisa, quando fornecidas.

---

## 🛠️ Como utilizar

Em vez de criar uma função de pesquisa manualmente, basta importar a ferramenta integrada:

```python
from google.adk.agents import LlmAgent
from google.adk.tools import google_search

search_agent = LlmAgent(
    model='gemini-2.5-flash',
    name='search_agent',
    instruction="""
    Você ajuda os usuários a encontrar informações
    usando a pesquisa na web.
    """,
    tools=[google_search]
)
```

A principal diferença é que **não precisamos implementar a função de pesquisa**.

O ADK fornece a implementação da ferramenta.

---

## 🔄 Diferenças em relação às ferramentas personalizadas

```text
🛠️ Ferramenta personalizada
        │
        ├── Definir função
        ├── Implementar lógica
        ├── Integrar API
        └── Manter integração


🔎 Ferramenta integrada
        │
        ├── Importar
        ├── Adicionar ao agente
        └── Utilizar
```

### Principais diferenças

| Aspecto           | Ferramenta integrada              | Função personalizada  |
| ----------------- | --------------------------------- | --------------------- |
| 🛠️ Implementação | Importar e usar                   | Desenvolver função    |
| 🔄 Manutenção     | ADK mantém                        | Desenvolvedor mantém  |
| 🧠 Otimização     | Pré-otimizada para LLMs           | Desenvolvedor otimiza |
| 🎯 Customização   | Limitada aos recursos disponíveis | Controle total        |
| 📌 Ideal para     | Recursos comuns                   | Lógica específica     |

---

## 🔄 Como o agente utiliza a Pesquisa Google

Quando uma consulta exige informações atualizadas, ocorre um fluxo semelhante a:

```text
👤 Usuário
    │
    ▼
💬 Pergunta
    │
    ▼
🤖 Agente
    │
    ▼
🧠 Determina que precisa pesquisar
    │
    ▼
🔎 Gera consultas de pesquisa
    │
    ▼
🌐 Pesquisa Google
    │
    ▼
📄 Resultados relevantes
    │
    ▼
🧠 Síntese das informações
    │
    ▼
📝 Resposta com fontes
```

O agente não precisa receber uma instrução explícita para cada chamada da ferramenta. Ele pode determinar **quando a pesquisa é necessária** com base na consulta e nas instruções recebidas.

---

# 🌐 Embasamento com a Pesquisa Google

## 🧠 O que é embasamento?

O **embasamento** (*grounding*) conecta as respostas do agente a fontes externas confiáveis.

Em vez de depender exclusivamente dos dados de treinamento do LLM, o agente pode utilizar informações atuais e verificáveis.

```text
🧠 LLM
  │
  │ conhecimento de treinamento
  ▼
🤖 Resposta


🔎 Pesquisa Google
  │
  ▼
🌐 Informações atuais
  │
  ▼
🔗 Fontes
  │
  ▼
🤖 Resposta fundamentada
```

---

## ✅ Benefícios do embasamento

* 🌐 Informações da web em tempo real;
* 🔗 Fontes para verificação;
* 🛡️ Redução de alucinações;
* 🔄 Informações atualizadas após o treinamento do modelo.

O embasamento não elimina completamente a possibilidade de erros, mas fornece ao agente **informações externas que podem ser verificadas**.

---

## ⚠️ Requisito da política da Pesquisa Google

Existe um requisito importante ao utilizar o embasamento da Pesquisa Google:

> **As sugestões de pesquisa (`renderedContent`) precisam ser exibidas na interface do usuário do aplicativo quando forem fornecidas.**

Isso é necessário para estar em conformidade com a política de uso da Pesquisa Google.

No código da aplicação, a resposta pode ser verificada e o conteúdo renderizado apresentado ao usuário:

```python
response = runner.run(...)

if hasattr(response, 'rendered_content') and response.rendered_content:
    display_html(response.rendered_content)
```

### ⚠️ Importante

Essa lógica deve estar na **interface/aplicação**, e não na definição do `agent.py`.

```text
🤖 Agent
    │
    ▼
🔎 Pesquisa Google
    │
    ▼
📄 Resposta + renderedContent
    │
    ▼
🖥️ Interface da aplicação
    │
    ▼
👤 Usuário
```

---

# 2. 🐍 Ferramenta de execução de código

A ferramenta de execução de código permite que o agente **execute código Python** para realizar cálculos e operações computacionais.

Ela é especialmente útil quando a precisão matemática é importante.

### O que oferece?

* 🧮 Cálculos precisos;
* 📊 Processamento e análise de dados;
* ⚙️ Execução de algoritmos;
* 🔄 Transformação de dados;
* 📈 Geração de visualizações.

---

## 🛠️ Como utilizar

A execução de código possui uma diferença importante em relação à `google_search`.

Ela utiliza o parâmetro **`code_executor`**, e não a lista `tools`.

```python
from google.adk.agents import LlmAgent
from google.adk.code_executors import BuiltInCodeExecutor

code_agent = LlmAgent(
    model='gemini-2.5-flash',
    name='code_agent',
    instruction="""
    Você ajuda os usuários com cálculos
    e processamento de dados.
    """,
    code_executor=BuiltInCodeExecutor()
)
```

### 🔎 Diferença importante

```text
🔎 Pesquisa Google
        │
        ▼
tools=[google_search]


🐍 Execução de código
        │
        ▼
code_executor=BuiltInCodeExecutor()
```

A execução de código **não é adicionada à lista `tools`** nesse formato.

---

## 🧮 Exemplo: juros compostos

Imagine que o usuário solicite:

> "Calcule os juros compostos sobre US$ 10.000 a uma taxa anual de 5% por 10 anos."

O agente pode gerar e executar código Python:

```python
principal = 10000
rate = 0.05
time = 10

amount = principal * (1 + rate) ** time
interest = amount - principal
```

O resultado pode então ser utilizado pelo agente para formular a resposta.

```text
👤 Pergunta
    │
    ▼
🧠 Agente identifica necessidade de cálculo
    │
    ▼
🐍 Gera código Python
    │
    ▼
⚙️ Executa código
    │
    ▼
📊 Obtém resultado
    │
    ▼
📝 Explica o cálculo
```

---

## ✅ Vantagens da execução de código

### 🎯 Precisão

Os cálculos são executados em vez de simplesmente estimados pelo LLM.

### ⚙️ Operações complexas

É possível realizar operações que envolvem várias etapas.

### 🔍 Verificação

O código executado pode ser analisado para verificar como o resultado foi obtido.

### 🔄 Reprodutibilidade

O mesmo código, com as mesmas entradas, produz o mesmo resultado.

---

# 3. 🧠 Ferramentas integradas + estado da sessão

As ferramentas integradas também podem trabalhar em conjunto com o **estado da sessão** estudado no módulo anterior.

Isso permite criar agentes mais **contextualizados e personalizados**.

```text
🧠 Session State
      │
      ├── Preferências
      ├── Configurações
      └── Contexto do usuário
              │
              ▼
        🔧 Ferramenta
              │
              ▼
      🎯 Comportamento
       personalizado
```

### Exemplos de utilização

* 🔎 Pesquisa adaptada ao idioma ou localização do usuário;
* 🧮 Resultados de cálculos armazenados no estado;
* 🎯 Consultas personalizadas;
* 🔄 Continuidade entre diferentes etapas de uma tarefa.

Por exemplo:

```python
state["user:preferred_units"] = "metric"
```

A instrução pode utilizar esse valor:

```python
instruction = """
Ao realizar cálculos, utilize as unidades
{user:preferred_units?imperial}.

Utilize a execução de código para
fazer cálculos precisos.
"""
```

> A integração completa entre estado e ferramentas será aprofundada posteriormente no curso.

---

# 4. ⚖️ Quando utilizar ferramentas integradas?

A escolha depende principalmente da **finalidade da ferramenta**.

| Aspecto      | 🔧 Integrada    | 🛠️ Personalizada      |
| ------------ | --------------- | ---------------------- |
| Configuração | Importar e usar | Escrever implementação |
| Manutenção   | ADK mantém      | Você mantém            |
| Otimização   | Pré-otimizada   | Você otimiza           |
| Customização | Limitada        | Controle total         |
| Exemplo      | Pesquisa Google | `get_capital_city`     |
| Melhor uso   | Recursos comuns | Lógica de negócio      |

---

## 🔧 Utilize ferramentas integradas quando:

* ✅ Precisar de recursos comuns;
* ✅ Quiser uma solução pronta para produção;
* ✅ Não quiser implementar integrações complexas;
* ✅ Precisar de otimização para interação com LLMs;
* ✅ Buscar confiabilidade de nível empresarial.

### Exemplos

```text
🌐 Pesquisa na web
🐍 Execução de código
🗄️ Consultas a dados
📚 Recuperação de documentos
```

---

## 🛠️ Utilize ferramentas personalizadas quando:

* ✅ Precisar de lógica específica do negócio;
* ✅ Precisar integrar sistemas proprietários;
* ✅ Implementar algoritmos exclusivos;
* ✅ Criar tarefas específicas da aplicação;
* ✅ Precisar de controle total da implementação.

### Exemplos

```text
🏢 Sistema interno
   │
   ▼
🛠️ consultar_inventario()

💳 Sistema financeiro
   │
   ▼
🛠️ calcular_limite_cliente()

📦 Sistema de pedidos
   │
   ▼
🛠️ consultar_pedido()
```

---

## 🧭 Exemplos de decisão

### 🌐 Pesquisa na web

**Tarefa:**

> "Adicionar pesquisa na web ao agente."

**Decisão:**

```text
🔎 google_search
```

**Motivo:**

É um recurso comum, complexo de implementar e já mantido pelo ADK.

---

### 🏢 Consulta ao inventário

**Tarefa:**

> "Consultar o inventário no nosso banco de dados."

**Decisão:**

```text
🛠️ Ferramenta personalizada
```

**Motivo:**

Trata-se de uma lógica específica do negócio e de um sistema proprietário.

---

# 5. ⚠️ Limitação das ferramentas integradas

Existe uma limitação importante na utilização das ferramentas integradas:

> **Atualmente, um agente raiz ou agente único suporta apenas uma ferramenta integrada.**

Isso significa que não é possível simplesmente combinar várias ferramentas integradas ou misturar uma ferramenta integrada com uma ferramenta personalizada no mesmo agente.

### ❌ Não compatível

```python
root_agent = LlmAgent(
    model='gemini-2.5-flash',
    tools=[google_search, my_custom_function]
)
```

Também não é possível combinar diretamente:

```python
root_agent = LlmAgent(
    model='gemini-2.5-flash',
    tools=[google_search],
    code_executor=BuiltInCodeExecutor()
)
```

A limitação pode ser representada assim:

```text
🤖 Agente
   │
   ├── 🔎 Pesquisa Google
   │
   └── ❌ Outra ferramenta integrada
```

ou:

```text
🤖 Agente
   │
   ├── 🔎 Pesquisa Google
   │
   └── ❌ Ferramenta personalizada
```

---

## 🧩 Como lidar com essa limitação?

Uma estratégia é utilizar **arquiteturas multiagentes**, nas quais diferentes agentes especializados ficam responsáveis por diferentes ferramentas.

```text
                 🤖 Agente principal
                        │
             ┌──────────┴──────────┐
             │                     │
             ▼                     ▼
      🔎 Agente pesquisa      🧮 Agente cálculo
             │                     │
             ▼                     ▼
      Google Search          Code Execution
```

A coordenação entre agentes especializados será abordada posteriormente no curso.

> O ADK também possui mecanismos avançados para contornar essa limitação em algumas ferramentas no Python, mas esse recurso está fora do escopo desta aula introdutória.

---

# 🧪 Exemplo prático

## 🔎 Assistente de pesquisa com Pesquisa Google

### Etapa 1 — Criar o projeto

```bash
adk create research_assistant
cd research_assistant
```

### Etapa 2 — Criar o agente

```python
from google.adk.agents import LlmAgent
from google.adk.tools import google_search

root_agent = LlmAgent(
    model='gemini-2.5-flash',
    name='research_assistant',
    description='Ajuda os usuários a pesquisar tópicos usando a Pesquisa Google.',
    instruction="""
    Você é um assistente de pesquisa que ajuda os usuários
    a encontrar informações precisas e atualizadas.

    Sua abordagem:

    1. Quando os usuários fizerem perguntas que exigirem
       informações atualizadas, use a Pesquisa Google.

    2. Baseie suas respostas nos resultados da pesquisa.

    3. Ao fornecer informações, cite as fontes.

    4. Se os resultados forem insuficientes,
       reconheça as limitações.

    Priorize sempre a acurácia em detrimento da especulação.
    Se não tiver certeza, diga isso.
    """,
    tools=[google_search]
)
```

### Etapa 3 — Executar

```bash
adk web
```

A aplicação pode ser acessada localmente pelo navegador.

---

## 🧪 Testes

### Teste 1 — Atualidades

```text
👤 Quais são os últimos desenvolvimentos
   em energia renovável?
```

**Comportamento esperado:**

* 🔎 O agente utiliza a Pesquisa Google;
* 📰 Recupera informações recentes;
* 🔗 Apresenta fontes;
* 🎯 Baseia a resposta em dados atuais.

---

### Teste 2 — Pesquisa factual

```text
👤 Quem é o atual CEO da Microsoft?
```

**Comportamento esperado:**

* 🔎 Pesquisa informações atualizadas;
* 🎯 Retorna uma resposta atual;
* 🔗 Apresenta a fonte.

---

### Teste 3 — Pesquisa complexa

```text
👤 Compare veículos elétricos e veículos
   com célula de combustível de hidrogênio.
```

**Comportamento esperado:**

* 🔎 Realiza pesquisa;
* 📚 Considera múltiplas perspectivas;
* 🧠 Sintetiza os resultados;
* 🔗 Apresenta fontes.

---

## ⚠️ Política de sugestões de pesquisa

Quando a resposta da Pesquisa Google incluir `renderedContent`, as sugestões de pesquisa precisam ser **exibidas na interface da aplicação**.

```text
🔎 Pesquisa Google
       │
       ▼
📄 renderedContent
       │
       ▼
🖥️ Interface
       │
       ▼
👤 Usuário
```

Essa etapa é obrigatória para conformidade com a política de uso da Pesquisa Google.

---

# 🧮 Assistente de matemática com execução de código

### Etapa 1 — Criar o projeto

```bash
adk create math_assistant
cd math_assistant
```

### Etapa 2 — Criar o agente

```python
from google.adk.agents import LlmAgent
from google.adk.code_executors import BuiltInCodeExecutor

root_agent = LlmAgent(
    model='gemini-2.5-flash',
    name='math_assistant',
    description='Auxilia os usuários com cálculos e análises matemáticas.',
    instruction="""
    Você é um assistente de matemática.

    Suas capacidades:

    1. Utilize a execução de código para cálculos.
    2. Explique os passos do processo.
    3. Verifique os resultados executando o código.
    4. Realize operações matemáticas complexas.

    Para garantir a acurácia dos cálculos numéricos,
    utilize sempre a execução de código.
    """,
    code_executor=BuiltInCodeExecutor()
)
```

### Etapa 3 — Executar

```bash
adk web
```

---

## 🧪 Testes

### Teste 1 — Cálculo simples

```text
👤 Calcule a gorjeta de 15% em uma conta
   de US$ 87,50.
```

**Comportamento esperado:**

```text
87,50 × 0,15 = 13,125
```

Resultado aproximado:

**US$ 13,13**

---

### Teste 2 — Cálculo complexo

```text
👤 Qual é o juro composto sobre um investimento
   de US$ 5.000 a uma taxa anual de 6% durante
   8 anos, com capitalização mensal?
```

O agente deve:

* 🧠 Identificar a necessidade de cálculo;
* 🐍 Gerar código Python;
* ⚙️ Executar o código;
* 📊 Retornar o resultado;
* 📝 Explicar o cálculo.

---

### Teste 3 — Processamento de dados

```text
👤 Calcule a média, a mediana e o desvio padrão
   destes números:

   12, 15, 18, 20, 22, 25, 28, 30
```

O agente pode gerar código Python para calcular as métricas solicitadas e retornar os resultados.

---

# 📊 Ferramentas integradas × ferramentas personalizadas

```text
                    🤖 AGENTE
                       │
          ┌────────────┴────────────┐
          │                         │
          ▼                         ▼
   🔧 Integradas              🛠️ Personalizadas
          │                         │
          ▼                         ▼
   Recursos comuns            Lógica específica
          │                         │
          ├── Pesquisa              ├── Negócio
          ├── Código                ├── Sistemas próprios
          ├── RAG                   └── Algoritmos exclusivos
          └── Dados
```

| Aspecto       | 🔧 Ferramentas integradas | 🛠️ Personalizadas |
| ------------- | ------------------------- | ------------------ |
| Implementação | Importar e usar           | Desenvolver        |
| Manutenção    | ADK                       | Desenvolvedor      |
| Otimização    | Pré-otimizada             | Desenvolvedor      |
| Customização  | Limitada                  | Total              |
| Melhor uso    | Recursos comuns           | Lógica de negócio  |

---

## 🧠 Principais aprendizados

### 🔧 Ferramentas integradas reduzem complexidade

Recursos comuns não precisam necessariamente ser implementados do zero.

### 🚀 São preparadas para uso

O ADK fornece ferramentas mantidas e otimizadas para integração com agentes.

### 🔎 Pesquisa Google adiciona informações atuais

O agente pode pesquisar a web e fundamentar suas respostas em fontes externas.

### 🐍 Execução de código aumenta a precisão

Cálculos e operações computacionais podem ser executados em Python em vez de serem apenas estimados pelo LLM.

### 🧠 Ferramentas podem trabalhar com estado

A combinação entre ferramentas e estado permite experiências mais contextualizadas e personalizadas.

### ⚖️ A escolha depende do problema

```text
Recurso comum?
      │
      ├── SIM ──► 🔧 Ferramenta integrada
      │
      └── NÃO
           │
           ▼
    Lógica específica?
           │
           ▼
    🛠️ Personalizada
```

---

## ⚠️ Pontos de atenção

* 🔎 A Pesquisa Google requer modelos Gemini compatíveis;
* 📜 `renderedContent` precisa ser exibido quando fornecido;
* 🐍 A execução de código utiliza `code_executor`;
* 🔧 A execução de código não é adicionada à lista `tools`;
* ⚠️ Há uma limitação de uma ferramenta integrada por agente;
* 🤖 Arquiteturas multiagentes podem ser utilizadas para coordenar diferentes capacidades;
* 🎯 Ferramentas integradas são melhores para recursos comuns;
* 🛠️ Ferramentas personalizadas são melhores para necessidades específicas.

---

## 🗂️ Organização dos estudos

```text
01 ── ⚠️ Ferramentas: o problema
 │
 ├── Agentes limitados
 ├── Dados de treinamento
 └── Necessidade de ferramentas
        │
        ▼
02 ── 🔧 Ferramentas: solução
 │
 ├── Ferramentas personalizadas
 ├── Function Tools
 └── Uso de ferramentas
        │
        ▼
03 ── ⚠️ Ferramentas integradas: o problema
 │
 ├── Reinventar recursos comuns
 ├── Complexidade
 └── Manutenção
        │
        ▼
04 ── 🚀 Ferramentas integradas: solução
 │
 ├── Pesquisa Google
 ├── Execução de código
 ├── Estado
 └── Escolha da ferramenta
        │
        ▼
🧪 Teste do módulo
```

---

## 🚀 Próxima etapa

Depois de aprender a utilizar ferramentas integradas, o próximo desafio é lidar com capacidades que **não estão disponíveis diretamente no conjunto de ferramentas fornecido pelo ADK**.

Isso leva ao próximo conceito:

> **🔗 Model Context Protocol (MCP)** — uma forma padronizada de conectar agentes a ferramentas e recursos externos.

---

<p align="center">
  <strong>🔧 Google Agent Development Kit (ADK)</strong><br>
  De ferramentas personalizadas para recursos integrados prontos para produção.
</p>
