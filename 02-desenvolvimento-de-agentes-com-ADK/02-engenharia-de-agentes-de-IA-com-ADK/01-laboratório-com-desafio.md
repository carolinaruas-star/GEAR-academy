## 🤖 Google Cloud — Engenharia de Agentes de IA com ADK: Laboratório com Desafio

<p align="center">
  <img src="https://cdn.qwiklabs.com/qOlrcccT7tpWjoRm26%2FwivZVzpaqvKP%2B0wCvnFY7Yj8%3D" width="180"/>
</p>

### 📚 Informações

**Laboratório:** Engenharia de agentes de IA com o Kit de Desenvolvimento de Agente (ADK): laboratório com desafio
**Plataforma:** Google Cloud Skills Boost
**ID:** GSP540
**Nível:** Intermediário
**Duração:** 1h30min
**Créditos:** 5
**Status:** ✅ Concluído

---

### 🎯 Objetivo

Desenvolver e corrigir agentes de IA utilizando o **Agent Development Kit (ADK)**, trabalhando com ferramentas de pesquisa, geração de respostas estruturadas e fluxos multiagente.

O desafio utiliza o cenário da **Cymbal Travel**, no qual diferentes agentes são responsáveis por pesquisar informações de viagens, validar dados de destinos e auditar conteúdos de marketing.

---

### 🧠 Conceitos e tecnologias praticados

* 🤖 **Google Agent Development Kit (ADK)**
* 🔎 **Google Search Tool**
* 🌐 **Agent Platform**
* 🧩 **Agentes multiagente**
* 🔄 **Sequential Agents**
* 📋 **Structured Output**
* 📦 **Pydantic**
* 🗂️ **JSON Schema**
* 💻 **ADK Web**
* ⌨️ **ADK CLI**
* ☁️ **Google Cloud**
* 🔐 **Google Cloud Authentication**
* 🛠️ **Configuração de agentes**
* 🧪 **Teste e validação de agentes**

---

### 🛠️ Desafios realizados

#### 🔎 1. Buscador de Viagens

Configuração do agente `my_google_search_agent` para utilização da ferramenta **Google Search**, permitindo que o agente pesquise informações atualizadas na web e utilize os resultados como base para suas respostas.

#### 📋 2. Verificador de Destino

Implementação de respostas estruturadas no agente `geo_validator`, utilizando um modelo **Pydantic** para garantir que a saída siga um formato JSON definido.

Também foram configuradas restrições de transferência entre agentes e definido o modelo Gemini apropriado.

#### 🔄 3. Auditor de Conteúdo

Correção do pipeline multiagente `llm_auditor`, restaurando o **Agente Revisor** e sua participação no fluxo sequencial.

O pipeline passou a executar:

**Agente Crítico → Agente Revisor**

permitindo verificar informações na web e posteriormente corrigir afirmações incorretas.

#### 💻 4. Execução e testes

Execução dos agentes por diferentes interfaces:

```bash
adk web
```

e

```bash
adk run my_google_search_agent
```

Além da execução programática do agente estruturado.

---

### 💡 Aprendizados

> Este laboratório reforçou conceitos fundamentais para a construção de sistemas de agentes mais confiáveis, destacando a importância de **ferramentas externas, saídas estruturadas e orquestração multiagente**.

A prática também demonstrou como o ADK pode ser utilizado para transformar agentes individuais em **fluxos de trabalho completos**, nos quais diferentes agentes desempenham funções específicas dentro de um mesmo processo.

---

### 🔗 Documentação

* [Google Agent Development Kit (ADK)](https://google.github.io/adk-docs/)
* [Google Search para ADK](https://google.github.io/adk-docs/tools/gemini-api/google-search/)
* [Structured Data com ADK](https://google.github.io/adk-docs/agents/llm-agents/#structuring-data-input_schema-output_schema-output_key)
* [Sequential Agents](https://google.github.io/adk-docs/agents/workflow-agents/sequential-agents/)
* [Google Cloud Skills Boost](https://www.skills.google/)

---

### 🏆 Resultado

**Laboratório concluído com sucesso.**

Prática realizada na construção, configuração, teste e correção de agentes de IA utilizando o **Google ADK**, incluindo integração com pesquisa na web, respostas estruturadas e arquitetura multiagente sequencial.
