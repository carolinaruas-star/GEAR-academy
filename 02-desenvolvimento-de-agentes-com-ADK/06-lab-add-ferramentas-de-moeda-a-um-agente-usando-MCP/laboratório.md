## 🧪 Laboratório — Adicionar ferramentas de moeda a um agente usando o MCP

### 🎯 Objetivo

Modificar um agente desenvolvido com o **Google Agent Development Kit (ADK)** para utilizar ferramentas externas por meio do **Model Context Protocol (MCP)**, permitindo que o agente acesse informações que não estavam disponíveis em seu comportamento inicial.

### 🛠️ Tecnologias e conceitos

* 🤖 **Google Agent Development Kit (ADK)**
* 🔌 **Model Context Protocol (MCP)**
* 🔗 **A2A (Agent2Agent)**
* 🐍 **Python**
* ⚡ **uv**
* 🌐 **API pública da Coinbase**
* 💱 Dados de moedas fiduciárias e criptomoedas

### 🔬 Prática realizada

O laboratório foi desenvolvido em duas etapas principais:

**Antes:** o agente de moeda conseguia consultar taxas de câmbio entre moedas fiduciárias, como USD/EUR e USD/CNY, mas não possuía uma ferramenta para consultar o preço atual de criptomoedas.

**Depois:** foi criada a ferramenta `get_crypto_price` no servidor MCP, utilizando a API pública da Coinbase. Após reiniciar os servidores MCP e A2A, o agente passou a conseguir utilizar essa ferramenta para consultar o preço atual do Bitcoin.

### 💡 Principal aprendizado

> O **MCP funciona como uma ponte padronizada entre agentes de IA e ferramentas ou serviços externos**, permitindo ampliar as capacidades do agente sem precisar incorporar diretamente toda a lógica ou integração ao próprio agente.

Na prática, o laboratório demonstrou como um agente pode deixar de depender exclusivamente de seu conhecimento interno e passar a **consultar dados externos e atualizados por meio de ferramentas**.

### 🚀 Resultado

Ao final do laboratório, o agente foi modificado com sucesso para utilizar uma nova ferramenta disponibilizada pelo servidor MCP, permitindo consultas sobre **criptomoedas em tempo real**.

**Status:** ✅ Concluído
**Dificuldade:** Introdutório
**Duração:** 20 minutos
**Créditos:** 1
