# 🏁 Conclusão do Curso — Desenvolvimento de Agentes com o ADK

[![Google Cloud - ADK Agent Development](https://img.shields.io/badge/Google%20Cloud-ADK%20Agent%20Development-4285F4?logo=googlecloud&logoColor=white)](https://www.skills.google/)

---

## 🎓 Encerramento da Jornada

O programa **"Desenvolvimento de agentes com o Kit de Desenvolvimento de Agente (ADK)"** marcou a transição completa de **modelos de linguagem isolados** para **sistemas agênticos autônomos, seguros e prontos para produção**.

Ao longo do programa, foi consolidada a equação fundamental do framework:

$$\text{Agente} = \text{Modelo} + \text{Ferramentas} + \text{Orquestração}$$

---

## 📋 Trilha de Aprendizado Consolidada

| Módulo | Foco de Domínio | Competências Chave |
| :--- | :--- | :--- |
| **01 — Fundamentos do ADK** | Primeiros passos na criação de agentes | Estrutura de projetos com a CLI do ADK (`adk create`, `adk web`), arquitetura básica com `LlmAgent` e inicialização de sessões interativas. |
| **02 — Laboratório Prático** | Engenharia de Agentes com ADK | Prática de configuração, solução de problemas de sintaxe/ambiente e implantação de agentes no ecossistema local e nuvem. |
| **03 — Otimização de Comportamento** | Engenharia de Prompts e Raciocínio | Transformação de um LLM genérico em um assistente sofisticado, definindo papéis, restrições, tom de voz e estratégias de instrução. |
| **04 — Memória e Estado** | Gerenciamento de Memória e Estado | Uso do `session.state`, persistência via `output_key`, injeção dinâmica de variáveis (`{var}`) e namespaces de ciclo de vida (`temp:`, sessão, `user:`, `app:`). |
| **05 — Habilidades com Ferramentas** | Extensão de Capacidades com Tools | Embasamento com `google_search`, precisão determinística com `BuiltInCodeExecutor`, ecossistema externo via **MCP** (`McpToolset`) e `FunctionTools` personalizadas. |
| **06 — Laboratório Prático MCP** | Ferramentas de Moeda via MCP | Extensão prática de um agente ADK com servidor MCP customizado em Python/FastMCP para consultar cotações de criptomoedas via API pública em tempo real. |
| **07 — Conclusão Geral** | Síntese do Programa | Visão holística da orquestração de IA Generativa pronta para cenários corporativos reais na Google Cloud. |

---

## 💡 Principais Conceitos Consolidados

* 🧠 **Raciocínio vs. Execução:** O LLM é responsável por analisar contextos e tomar decisões, enquanto as **ferramentas** executam chamadas deterministicamente.
* 💾 **Estado vs. Histórico Conversacional:** O histórico serve de contexto textual para o modelo, enquanto o **Session State** armazena dados estruturados acessíveis e manipuláveis por código.
* 🔌 **Interoperabilidade com MCP:** O *Model Context Protocol* elimina código de integração proprietário, permitindo que o ADK consuma servidores locais (`Stdio`) ou remotos (`Sse`) do ecossistema.
* 🎯 **Instruções Estratégicas:** Prompts estruturados orientam a seleção de ferramentas, sequenciamento de passos, degradação suave perante falhas e delegação via `AgentTool`.

---

<p align="center">
  <strong>🏅 Programa Concluído — Do primeiro agente ao domínio completo de Memória, Ferramentas e MCP na Google Cloud! 🚀</strong>
</p>

---
<div align="center">

## 👩‍💻 Autora

**Ana Carolina Pereira Ruas**  
Engenheira Florestal  
**Foco em Dados, Machine Learning, IA Generativa, LLMs, Agentes e Cloud**  

---
⭐ *Repositório desenvolvido como parte dos estudos da GEAR — Gemini Enterprise Agent Platform.*
</div>