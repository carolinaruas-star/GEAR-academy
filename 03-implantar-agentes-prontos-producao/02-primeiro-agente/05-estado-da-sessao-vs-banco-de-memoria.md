# 05. Estado da Sessão vs. Banco de Memória (Memory Bank)

## 📌 A Lacuna da Memória de Curto Prazo
Na implantação de agentes com persistência de sessão, o estado das variáveis fica restrito ao ciclo de vida da conversa atual. 

```python
# Sessão 1 (Segunda-feira):
Usuário: "Prefiro notificações por e-mail do que por SMS"
Agente: "Entendi!"

# Sessão 2 (Sexta-feira – Nova conversa/sessão):
Usuário: "Como devo ser notificado?"
Agente: "Não me lembro" ❌ # O estado da sessão é isolado por conversa

```

> **A Lacuna:** O Estado da Sessão persiste apenas enquanto a conversa estiver ativa. Para permitir o aprendizado e retenção de preferências do usuário em **múltiplas conversas ao longo do tempo**, é necessário utilizar o **Memory Bank**.
> 
> 

---

## ⚔️ Comparação: Estado da Sessão vs. Memory Bank

| Recurso | Estado da Sessão | Memory Bank |
| --- | --- | --- |
| **Escopo** | Conversa atual (curto prazo)| Todas as conversas (longo prazo)|
| **Persistência** | Até o fim da sessão/conversa| Indefinida / Permanente|
| **Caso de Uso** | Fluxo e contexto imediato da conversa | Aprendizado e histórico contínuo |
| **Acesso** | Direto via chave (`{variable}`) | Busca semântica via ferramenta (`PreloadMemoryTool`)
|

### 💡 Exemplo Visual de Atuação Conjunta

```text
Estado da Sessão: "O que está acontecendo NESTA conversa?"
├── Tópico atual (temp:current_topic)
├── Contagem de requisições (request_count)
└── Nível do usuário (user:tier)

Memory Bank: "O que eu aprendi EM TODAS as conversas?"
├── "Usuário prefere notificações por e-mail" (aprendido na semana passada)
├── "Já teve um problema com o faturamento" (do mês passado)
└── "Tem interesse na API Enterprise" (histórico acumulado)

```

---

## 🔄 Ciclo de Vida e Funcionamento do Memory Bank

```text
1. Interação ────> 2. Salvamento ────> 3. Extração ────> 4. Recuperação ────> 5. Resposta
   Usuário          Callback salva        LLM extrai        Busca semântica        Agente responde
   conversa         automaticamente       fatos/atributos   via PreloadTool        com histórico

```

### 🧰 Principais Componentes

1. **`VertexAiMemoryBankService`:** Serviço gerenciado que utiliza LLMs para extração inteligente e estruturada de fatos (não guarda apenas o texto bruto da conversa).


2. **Callback de Salvamento Automático:** Intercepta o fim da execução da etapa para salvar a conversa no banco de memória:


```python
async def auto_save_session_to_memory_callback(callback_context):
    await callback_context._invocation_context.memory_service.add_session_to_memory(
        callback_context._invocation_context.session
    )

```
3. **`PreloadMemoryTool`:** Ferramenta que realiza busca semântica no banco de memória e injeta dados históricos relevantes no contexto do agente no início da conversa.
---