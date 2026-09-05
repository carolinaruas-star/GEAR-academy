# 🛠️ O problema: ferramentas genéricas versus necessidades específicas

<p align="center">
  <strong>De recursos integrados para recursos personalizados</strong>
</p>

<p align="center">
  <strong>Adaptando agentes de IA às regras, dados e sistemas específicos de cada negócio.</strong>
</p>

---

## 🧭 Introdução

Até aqui, a jornada de ferramentas do agente passou por diferentes níveis de integração.

```text
📚 JORNADA DAS FERRAMENTAS

Parte 1
🧠 Fundamentos
     │
     ▼
🤖 Primeiro agente habilitado para ferramentas
     │
     ▼
Parte 2
🧰 Ferramentas integradas
     │
     ├── 🔎 Pesquisa Google
     └── 💻 Execução de código
     │
     ▼
Parte 3
🔗 Ferramentas MCP
     │
     ▼
Parte 4
🛠️ Ferramentas personalizadas
```

A mudança apresentada nesta etapa é importante:

> Em vez de apenas importar ferramentas prontas, podemos **escrever funções Python que o ADK converte automaticamente em ferramentas**.

---

## 🔄 A mudança de abordagem

As ferramentas integradas são excelentes quando o agente precisa realizar tarefas **genéricas e amplamente utilizadas**.

Por exemplo:

```python
from google.adk.tools import google_search

agent = LlmAgent(
    model='gemini-2.5-flash',
    tools=[google_search]
)
```

A pesquisa na web é uma necessidade comum e a ferramenta integrada consegue atendê-la sem conhecer detalhes específicos do negócio.

Mas existe outro tipo de necessidade:

```text
🌐 Necessidade genérica
        │
        ▼
🧰 Ferramenta integrada
        │
        ▼
      ✅
```

versus:

```text
🏢 Necessidade específica
        │
        ▼
🛠️ Ferramenta personalizada
        │
        ▼
      ✅
```

---

# ⚠️ O problema

## Ferramentas genéricas não conhecem o seu negócio

Imagine uma empresa que precisa de um agente capaz de realizar operações específicas.

```text
🏢 SUA EMPRESA
      │
      ├── 📦 Calcular custos de envio
      ├── 🗄️ Consultar inventário
      ├── 💰 Processar reembolsos
      ├── 🎁 Validar pontos de fidelidade
      ├── 📅 Agendar horários
      └── 🚚 Consultar status de pedidos
```

Essas tarefas dependem de **regras, dados e sistemas próprios da empresa**.

Uma ferramenta genérica não possui essas informações por padrão.

---

# 🏢 Necessidades específicas de negócio

Alguns exemplos de funcionalidades que podem exigir ferramentas personalizadas:

### 📦 Custos de envio

O cálculo pode depender de:

* Produto;
* Peso;
* Dimensões;
* Destino;
* Transportadora;
* Contratos específicos.

```text
Produto + Peso + Destino
          │
          ▼
   📦 Regra de negócio
          │
          ▼
    💰 Frete calculado
```

---

### 🗄️ Consulta de inventário

O agente pode precisar consultar o banco de dados proprietário da empresa.

```text
🤖 Agente
    │
    ▼
🛠️ Ferramenta personalizada
    │
    ▼
🗄️ Banco de dados interno
    │
    ▼
📦 Estoque atual
```

---

### 💰 Processamento de reembolsos

Um reembolso pode envolver regras internas, permissões e integrações com sistemas financeiros.

```text
👤 Cliente
    │
    ▼
🤖 Agente
    │
    ▼
🛠️ Ferramenta de reembolso
    │
    ▼
🏢 Sistema interno
    │
    ▼
💰 Reembolso processado
```

---

### 🎁 Programa de fidelidade

A ferramenta pode consultar e validar pontos de acordo com as regras específicas do programa.

```text
👤 Cliente
    │
    ▼
🎁 Pontos de fidelidade
    │
    ▼
🛠️ Regra personalizada
    │
    ▼
✅ Pontos válidos
```

---

### 📅 Agendamento

O agente pode precisar interagir com o calendário ou sistema de agendamento da empresa.

```text
🤖 Agente
    │
    ▼
📅 Ferramenta personalizada
    │
    ▼
🗓️ Calendário da empresa
    │
    ▼
⏰ Horário agendado
```

---

### 🚚 Status do pedido

Uma ferramenta personalizada pode consultar diretamente a plataforma de e-commerce da empresa.

```text
🤖 Agente
    │
    ▼
🔎 Consulta do pedido
    │
    ▼
🛒 Plataforma de e-commerce
    │
    ▼
🚚 Status atualizado
```

---

# ❌ Limitações das soluções genéricas

As ferramentas integradas são poderosas, mas possuem limitações quando aplicadas a necessidades muito específicas.

## 01 — 🏢 Sem contexto comercial

Ferramentas genéricas não conhecem automaticamente:

* Seus produtos;
* Seus preços;
* Suas políticas;
* Seus clientes;
* Suas regras internas.

```text
🧰 Ferramenta genérica
        │
        ├── ❓ Produtos da empresa
        ├── ❓ Preços internos
        ├── ❓ Políticas
        └── ❓ Regras comerciais
```

---

## 02 — 🔒 Impossibilidade de acessar seus sistemas

Uma ferramenta integrada não possui, por padrão, acesso aos sistemas proprietários da empresa.

Isso pode incluir:

* 🗄️ Bancos de dados internos;
* 🔌 APIs privadas;
* 🏢 Sistemas corporativos;
* 🛒 Plataformas de e-commerce;
* 📊 Serviços internos.

```text
🏢 Sistemas proprietários
       │
       ├── 🗄️ Banco de dados
       ├── 🔌 API interna
       └── 🛒 Plataforma
                │
                ▼
        🛠️ Ferramenta personalizada
```

---

## 03 — 📐 Tamanho único para todos

Ferramentas genéricas são projetadas para atender necessidades amplas.

Por isso, podem não se encaixar perfeitamente nos fluxos específicos de uma organização.

```text
🧰 Ferramenta genérica
        │
        ├── Empresa A → ⚠️
        ├── Empresa B → ⚠️
        └── Empresa C → ⚠️
```

Cada empresa pode possuir processos diferentes.

---

## 04 — ⚙️ Customização limitada

Ferramentas integradas possuem comportamentos definidos pelo framework ou pelo fornecedor.

Isso limita a possibilidade de adaptar a ferramenta para regras muito específicas.

```text
🧰 Ferramenta integrada
        │
        ├── comportamento padrão
        ├── parâmetros disponíveis
        └── configurações suportadas
```

Quando o comportamento necessário não está disponível, uma alternativa é criar uma ferramenta própria.

---

# 🌳 A raiz do problema

O problema não está nas ferramentas integradas.

Elas são excelentes para **necessidades universais**.

O problema surge quando tentamos utilizá-las para representar algo que é:

```text
🏢 ESPECÍFICO DO NEGÓCIO
        │
        ├── 📋 Regras próprias
        ├── 📊 Dados próprios
        ├── 🗄️ Sistemas próprios
        ├── 🔌 APIs internas
        └── 🔄 Fluxos específicos
```

Cada negócio possui sua própria lógica.

Portanto:

> **Cada negócio possui necessidades que exigem integrações personalizadas.**

---

# 🧠 Genérico x Personalizado

| Característica          | Ferramenta genérica | Ferramenta personalizada        |
| ----------------------- | ------------------- | ------------------------------- |
| Público-alvo            | Diversos negócios   | Um negócio/caso específico      |
| Conhecimento do negócio | Limitado            | Específico                      |
| Dados internos          | ❌                   | ✅                               |
| Sistemas proprietários  | ❌                   | ✅                               |
| Regras específicas      | Limitado            | ✅                               |
| Customização            | Limitada            | Alta                            |
| Desenvolvimento         | Pronto              | Implementado pelo desenvolvedor |

---

# 🔄 Evolução da estratégia

A evolução das ferramentas pode ser representada assim:

```text
             🤖 AGENTE
                 │
                 ▼
       🧰 Ferramentas integradas
                 │
        Necessidades genéricas
                 │
                 ▼
          🔗 Ferramentas MCP
                 │
       Recursos já existentes
                 │
                 ▼
      🛠️ Ferramentas personalizadas
                 │
       Lógica específica do negócio
                 │
                 ▼
        🏢 Sistemas proprietários
```

A estratégia não é substituir uma abordagem pela outra.

É **escolher a ferramenta adequada para cada problema**.

---

# 🎯 Insight principal

Podemos resumir a decisão da seguinte maneira:

```text
🔎 A funcionalidade já existe no ADK?
        │
       SIM
        ▼
🧰 Use ferramenta integrada


        NÃO
        │
        ▼
🔎 Existe um servidor MCP?
        │
       SIM
        ▼
🔗 Use ferramenta MCP


        NÃO
        │
        ▼
🏢 A lógica é específica do negócio?
        │
       SIM
        ▼
🛠️ Crie uma ferramenta personalizada
```

Essa lógica evita tanto o **desenvolvimento desnecessário** quanto a tentativa de adaptar ferramentas inadequadas.

---

# 🧠 Principais aprendizados

* 🧰 Ferramentas integradas são excelentes para tarefas genéricas;
* 🏢 Cada empresa possui regras e sistemas próprios;
* 🗄️ Dados e APIs proprietárias podem exigir integração personalizada;
* 📐 Soluções genéricas nem sempre atendem fluxos específicos;
* ⚙️ Ferramentas integradas possuem limites de customização;
* 🛠️ Funções Python podem ser transformadas em ferramentas personalizadas pelo ADK;
* 🎯 A escolha da ferramenta deve considerar a necessidade real do negócio.

---

# 🗂️ Organização dos estudos

Esta etapa corresponde à introdução às **ferramentas de função personalizadas**.

```text
📚 Módulo 5
│
├── 01 — O problema: agentes limitados pelos dados de treinamento
│
├── 02 — A solução: ferramentas integradas
│
├── 03 — Teste do módulo
│
├── 04 — O problema: reproduzir habilidades comuns
│
├── 05 — A solução: ferramentas integradas
│
├── 06 — A solução: Protocolo de Contexto de Modelo (MCP)
│
├── 07 — Teste do módulo
│
├── 08 — 🛠️ O problema: ferramentas genéricas
│
└── ...
```

### 📌 Conceitos-chave

```text
🛠️ Ferramentas personalizadas
│
├── 🏢 Lógica de negócio
├── 🗄️ Dados internos
├── 🔌 APIs proprietárias
├── 📋 Regras específicas
├── ⚙️ Alta customização
└── 🐍 Funções Python
```

---

# 🚀 Próxima etapa

Depois de identificar a limitação das ferramentas genéricas, o próximo passo é conhecer a solução:

> **Criar funções Python personalizadas que o ADK pode transformar automaticamente em ferramentas para o agente.**

A jornada continua:

```text
🧰 Ferramentas integradas
          │
          ▼
🔗 Ferramentas MCP
          │
          ▼
🛠️ Funções personalizadas
          │
          ▼
🏢 Lógica específica do negócio
```

O objetivo será transformar **código Python próprio em capacidades agênticas**, permitindo que o agente interaja com regras, dados e sistemas específicos.

---

<p align="center">
  <strong>🛠️ Ferramentas personalizadas conectam agentes à lógica real do negócio.</strong>
</p>

<p align="center">
  <strong>Do recurso genérico para a capacidade específica.</strong>
</p>
