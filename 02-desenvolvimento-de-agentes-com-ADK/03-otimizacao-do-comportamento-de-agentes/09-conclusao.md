# 🤖 Google ADK — Conclusão: Construção de Agentes de IA Profissionais

## 📚 Visão geral

Ao longo deste módulo, a construção de agentes evoluiu de uma abordagem simples e reativa para uma arquitetura mais **estruturada, previsível, segura e otimizada**.

Foram trabalhados quatro pilares fundamentais do desenvolvimento de agentes com o **Google Agent Development Kit (ADK)**:

* 🧠 Instruções avançadas
* 📦 Saídas estruturadas
* ⚙️ Seleção e configuração de modelos
* 🔍 Planejamento para tarefas complexas

O resultado é uma base para desenvolver agentes capazes de **seguir comportamentos bem definidos, gerar dados compatíveis com sistemas, utilizar modelos de forma estratégica e resolver problemas complexos de maneira estruturada**.

---

## 🧠 Módulo 1 — Instruções avançadas

### O que foi aprendido

* Utilização de cinco padrões reutilizáveis:

  * **Identidade**
  * **Missão**
  * **Metodologia**
  * **Limites**
  * **Few-shot**
* Criação de instruções genéricas utilizando **placeholders**.
* Aplicação dos padrões em diferentes domínios, como:

  * E-commerce
  * Educação
  * Finanças
  * Saúde
* Organização das instruções utilizando **Markdown**.

### 💡 Insight principal

> Instruções não são apenas comandos: elas funcionam como uma **especificação do comportamento do agente**.

Uma boa instrução define claramente **quem é o agente, qual sua missão, como deve trabalhar, quais são seus limites e como deve responder**.

---

## 📦 Módulo 2 — Saída estruturada

### O que foi aprendido

* Criação de esquemas utilizando **Pydantic `BaseModel`**.
* Utilização de `Field(description=...)` para descrever os campos.
* Configuração de `output_schema` para produzir dados estruturados.
* Utilização de `output_key` para armazenar e transmitir informações entre etapas.
* Aplicação de saída estruturada em agentes raiz e subagentes.
* Tratamento de campos opcionais e valores padrão.
* Importância da validação antes da utilização dos dados em produção.

### 💡 Insight principal

> A saída estruturada funciona como um **contrato entre o agente e o sistema**.

Enquanto o texto livre é adequado para interação com pessoas, estruturas como JSON permitem que os resultados sejam utilizados por **APIs, bancos de dados, pipelines e outros agentes**.

### Exemplo

```python
from pydantic import BaseModel, Field

class ProductInfo(BaseModel):
    product_name: str = Field(description="Nome do produto")
    price: float = Field(description="Preço")
    storage: str = Field(description="Armazenamento")

agent = LlmAgent(
    model="gemini-2.5-flash",
    output_schema=ProductInfo,
    output_key="product"
)
```

---

## ⚙️ Módulo 3 — Seleção e configuração de modelos

### Estratégia de seleção

A escolha do modelo deve considerar **qualidade, complexidade, velocidade e custo**.

| Etapa           | Modelo           | Uso                               |
| --------------- | ---------------- | --------------------------------- |
| 🧪 Prototipagem | Gemini 2.5 Pro   | Qualidade e benchmark inicial     |
| 🚀 Produção     | Gemini 2.5 Flash | Velocidade e otimização de custos |
| 🔎 Validação    | Pro → Flash      | Análise de lacunas de qualidade   |

### 🌡️ Temperatura

A temperatura deve ser definida de acordo com o comportamento esperado:

| Temperatura | Perfil         | Exemplos                            |
| ----------- | -------------- | ----------------------------------- |
| `0.0 – 0.3` | Determinístico | Fatos, extração, classificação      |
| `0.4 – 0.7` | Equilibrado    | Suporte, orientação, conversação    |
| `0.8 – 1.0` | Criativo       | Ideias, marketing, escrita criativa |

### 🔐 Segurança

Também foi estudada a configuração de filtros utilizando `SafetySetting` e diferentes níveis de bloqueio:

* `BLOCK_LOW_AND_ABOVE` → maior rigor
* `BLOCK_MEDIUM_AND_ABOVE` → uso geral
* `BLOCK_ONLY_HIGH` → configuração mais flexível

### 💡 Insight principal

> A configuração do modelo deve ser **estratégica e orientada à tarefa**, e não simplesmente baseada no modelo mais poderoso disponível.

---

## 🧠 Módulo 4 — Planejamento para tarefas complexas

### O que foi aprendido

* Ativação de planejamento com `BuiltInPlanner`.
* Configuração de `ThinkingConfig`.
* Utilização de `thinking_budget`.
* Diferença entre **planejamento** e **arquitetura multiagente**.
* Uso do `PlanReActPlanner` para modelos que não possuem o mesmo mecanismo nativo de raciocínio.
* Identificação de situações em que o planejamento agrega valor.

### Quando utilizar planejamento?

O planejamento é especialmente útil para:

* Problemas com várias etapas;
* Análise de alternativas;
* Tomada de decisão;
* Diagnóstico e debugging;
* Planejamento estratégico;
* Problemas com dependências entre etapas.

Para tarefas simples, como responder uma informação factual direta, o planejamento pode ser desnecessário.

### Exemplo

```python
from google.adk.planners import BuiltInPlanner
from google.genai import types

planner = BuiltInPlanner(
    thinking_config=types.ThinkingConfig(
        include_thoughts=True,
        thinking_budget=1024
    )
)
```

### 💡 Insight principal

> O planejamento transforma um agente reativo em um agente capaz de **estruturar abordagens para problemas mais complexos**.

---

# 🛠️ Aplicações práticas

Os conhecimentos adquiridos podem ser combinados para construir diferentes tipos de sistemas.

### 🎧 Atendimento ao cliente

Combinação de:

* Persona e limites;
* Planejamento;
* Saída estruturada;
* Configurações de segurança.

```python
class TicketOutput(BaseModel):
    ticket: dict
    priority: str

customer_agent = LlmAgent(
    model="gemini-2.5-flash",
    instruction="[Persona + regras de atendimento]",
    planner=BuiltInPlanner(...),
    output_schema=TicketOutput
)
```

---

### 📊 Pipeline de análise de dados

Agentes podem transformar informações não estruturadas em resultados organizados:

```python
class AnalysisOutput(BaseModel):
    insights: list[str]
    metrics: dict

analysis_agent = LlmAgent(
    model="gemini-2.5-pro",
    instruction="[Framework de análise]",
    output_schema=AnalysisOutput
)
```

---

### 🔄 Automação de workflows

O `output_key` pode ser utilizado para transmitir resultados entre diferentes etapas:

```python
automation_agent = LlmAgent(
    model="gemini-2.5-flash",
    instruction="[Regras do processo]",
    output_key="aprovado",
    generate_content_config=types.GenerateContentConfig(
        temperature=0.2
    )
)
```

---

### 🎓 Assistentes educacionais

Podem combinar metodologia pedagógica, planejamento e controle de criatividade:

```python
education_agent = LlmAgent(
    model="gemini-2.5-pro",
    instruction="[Metodologia de ensino]",
    planner=BuiltInPlanner(...),
    generate_content_config=types.GenerateContentConfig(
        temperature=0.5
    )
)
```

---

# ✅ Checklist de boas práticas

## 🧠 Instruções

* [x] Definir identidade e persona.
* [x] Estabelecer uma missão clara.
* [x] Definir uma metodologia de trabalho.
* [x] Estabelecer limites utilizando regras **Nunca/Sempre**.
* [x] Utilizar exemplos `few-shot`.
* [x] Utilizar Markdown para organizar instruções.
* [x] Criar templates reutilizáveis.

## ⚙️ Modelo

* [x] Começar com um modelo adequado para estabelecer um benchmark.
* [x] Avaliar a possibilidade de utilizar um modelo mais rápido e econômico.
* [x] Realizar análise de lacunas antes da substituição.
* [x] Configurar temperatura de acordo com a tarefa.
* [x] Definir políticas de segurança adequadas ao público.

## 🧠 Planejamento

* [x] Utilizar `BuiltInPlanner` em tarefas complexas com modelos Gemini.
* [x] Utilizar `PlanReActPlanner` quando apropriado para outros modelos.
* [x] Configurar `ThinkingConfig`.
* [x] Definir um `thinking_budget` adequado.
* [x] Evitar planejamento desnecessário em tarefas simples.

## 📦 Saída estruturada

* [x] Utilizar `Pydantic BaseModel`.
* [x] Definir todos os campos necessários.
* [x] Utilizar `Field(description=...)`.
* [x] Utilizar `output_key` em fluxos de trabalho.
* [x] Tratar campos opcionais.
* [x] Validar os dados antes da utilização em produção.

---

# ⚠️ Armadilhas comuns

### Instruções

❌ Personas vagas
❌ Ausência de limites
❌ Falta de exemplos few-shot
❌ Instruções excessivamente complexas
❌ Falta de metodologia definida
❌ Criação de instruções específicas demais para um único domínio

### Configuração

❌ Utilizar modelos mais caros sem necessidade
❌ Utilizar temperatura alta em tarefas factuais
❌ Configurar segurança inadequadamente
❌ Alterar o modelo sem avaliar a perda de qualidade

### Planejamento

❌ Utilizar planner em tarefas simples
❌ Escolher o planner inadequado
❌ Não definir restrições realistas
❌ Utilizar um `thinking_budget` inadequado
❌ Tornar o processo mais complexo sem necessidade

### Saída estruturada

❌ Utilizar dicionários no lugar de `BaseModel`
❌ Não definir todos os campos necessários
❌ Não utilizar descrições nos campos
❌ Ignorar dados opcionais
❌ Não validar a saída antes da integração

---

# 🔑 Ficha de referência rápida

| Recurso                 | Função                                         |
| ----------------------- | ---------------------------------------------- |
| `instruction`           | Define o comportamento do agente               |
| `output_schema`         | Define o formato estruturado da saída          |
| `output_key`            | Armazena/transmite resultados                  |
| `GenerateContentConfig` | Configura o comportamento do modelo            |
| `temperature`           | Controla o grau de variação                    |
| `SafetySetting`         | Define filtros de segurança                    |
| `BuiltInPlanner`        | Planejamento para modelos Gemini               |
| `PlanReActPlanner`      | Planejamento estruturado para outros modelos   |
| `ThinkingConfig`        | Configura recursos de pensamento               |
| `thinking_budget`       | Define orçamento para o processo de raciocínio |

---

# 🧩 Os quatro pilares

```text
              🤖 AGENTE PROFISSIONAL
                       │
        ┌──────────────┼──────────────┐
        │              │              │
        ▼              ▼              ▼
   🧠 INSTRUÇÃO    📦 ESTRUTURA    ⚙️ CONFIGURAÇÃO
        │              │              │
   Comportamento      Dados         Modelo
        │              │              │
        └──────────────┼──────────────┘
                       │
                       ▼
                🧠 PLANEJAMENTO
                       │
                       ▼
              🎯 SOLUÇÃO COMPLETA
```

---

# 🎯 Conclusão

Este módulo consolidou a evolução da construção de agentes de IA, passando de agentes simples e reativos para sistemas mais **estruturados, previsíveis, eficientes e preparados para aplicações reais**.

Ao final, os agentes são capazes de:

* 🧠 Seguir instruções profissionais com personalidade, metodologia e limites;
* 📦 Produzir dados estruturados para integração com sistemas;
* ⚙️ Utilizar modelos e parâmetros de forma estratégica;
* 🔐 Operar com configurações de segurança adequadas;
* 🔍 Planejar soluções para problemas complexos;
* 🔄 Participar de workflows e pipelines automatizados.

> **Insight final:** construir um bom agente não significa apenas escolher um modelo poderoso. É necessário combinar **instruções bem projetadas, estrutura de dados, configuração adequada e planejamento**, de acordo com o objetivo da aplicação.

### 🚀 Resultado

A base foi estabelecida para avançar da criação de agentes individuais para a construção de **sistemas agentivos mais robustos e preparados para produção com Google ADK**.
