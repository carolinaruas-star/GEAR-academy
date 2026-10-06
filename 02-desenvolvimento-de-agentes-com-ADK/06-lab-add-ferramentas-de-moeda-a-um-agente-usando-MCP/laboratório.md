# 🧪 Módulo 6 — Laboratório: Adicionar Ferramentas de Moeda a um Agente Usando o MCP

[![Google Cloud - Add Agent Capabilities with Tools](https://img.shields.io/badge/Google%20Cloud-Lab%20Currency%20Tools%20MCP-4285F4?logo=googlecloud&logoColor=white)](../05-inclusao-de-habilidades-agenticas-com-ferramentas/12-badge-conclusao.md)

---

## 🎯 Objetivo do Laboratório

Modificar um agente de conversão financeira desenvolvido com o **Google Agent Development Kit (ADK)** para integrar novas ferramentas externas através do **Model Context Protocol (MCP)**. 

A prática demonstra como estender as capacidades de um agente que lidava apenas com moedas fiduciárias, habilitando consultas em tempo real ao preço de criptomoedas via integração com API externa no servidor MCP.

---

## 🛠️ Tecnologias e Conceitos Aplicados

- 🤖 **Google Agent Development Kit (ADK):** Framework para orquestração e execução do agente raiz.
- 🔌 **Model Context Protocol (MCP):** Protocolo padronizado para conexão entre o agente e ferramentas externas[cite: 58].
- 🔗 **A2A (Agent2Agent):** Protocolo de comunicação e delegação entre agentes do ADK.
- ⚡ **FastMCP & uv:** Gerenciamento de ambiente Python de alta performance para execução do servidor MCP.
- 🌐 **Coinbase Spot Price API:** Endpoint público de dados financeiros em tempo real.

---

## 🔬 Evolução da Prática (Antes vs. Depois)

```text
 ❌ ANTES (Agente Limitado)
 ┌───────────────┐        ┌────────────────────────┐
 │  Usuário:     │ ─────> │ Agente de Moedas (ADK) │ ─────> ❌ Sem suporte a criptomoedas
 │ "Preço do BTC"│        │ (Apenas USD/EUR/CNY)   │        (Ferramenta ausente)
 └───────────────┘        └────────────────────────┘

 -----------------------------------------------------------------------------------------

 ✅ DEPOIS (Habilitado via MCP)
 ┌───────────────┐        ┌────────────────────────┐        ┌────────────────────────┐
 │  Usuário:     │ ─────> │ Agente de Moedas (ADK) │ ─────> │ Servidor MCP (FastMCP) │
 │ "Preço do BTC"│        │ (Orquestração ADK/A2A) │        │ get_crypto_price()     │
 └───────────────┘        └────────────────────────┘        └───────────┬────────────┘
                                                                        │
                                                                        ▼
                                                            🌐 Coinbase Public API

```

1. **Antes:** O agente de moedas atendia a consultas de taxas de câmbio entre moedas fiduciárias tradicionais (ex: USD/EUR, USD/CNY), mas falhava ao solicitar preços de criptomoedas por falta de ferramentas e dados no modelo.


2. **Depois:** Foi desenvolvida e registrada a função `@mcp.tool()` denominada `get_crypto_price` no servidor MCP em Python/FastMCP, consultando a API da Coinbase em tempo real. Após o restart dos serviços MCP e A2A, o agente passou a orquestrar e responder cotações atualizadas do Bitcoin (BTC-USD).



---

## 💻 Implementação da Tool no Servidor MCP

```python
import httpx
from mcp.server.fastmcp import FastMCP

mcp = FastMCP("Currency Service")

@mcp.tool()
def get_crypto_price(currency_pair: str = "BTC-USD") -> dict:
    """Obtém o preço atual de um par de criptomoedas via API da Coinbase."""
    url = f"[https://api.coinbase.com/v2/prices/](https://api.coinbase.com/v2/prices/){currency_pair}/spot"
    response = httpx.get(url)
    return response.json()["data"]

```

---

## 💡 Principal Aprendizado

> O **Model Context Protocol (MCP)** atua como um adaptador universal entre o ecossistema de agentes e serviços externos. Ele permite expandir dinamicamente o conjunto de habilidades (*skills*) de um agente sem a necessidade de reescrever a arquitetura interna do modelo ou alterar seu pipeline principal de orquestração.
> 
> 

---

## 📊 Ficha Técnica do Laboratório

| Item | Detalhe |
| --- | --- |
| **Status** | ✅ Concluído |
| **Dificuldade** | Introdutório |
| **Duração** | 20 minutos |
| **Créditos** | 1 |

---

<div align="center">

## 👩‍💻 Autora

**Ana Carolina Pereira Ruas**  
Engenheira Florestal  
**Foco em Dados, Machine Learning, IA Generativa, LLMs, Agentes e Cloud**  

---
⭐ *Repositório desenvolvido como parte dos estudos da GEAR — Gemini Enterprise Agent Platform.*
</div>