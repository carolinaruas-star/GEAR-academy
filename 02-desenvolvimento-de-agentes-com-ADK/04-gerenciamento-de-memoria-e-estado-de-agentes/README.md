# 🧠 Módulo 4 — Gerenciamento de Memória e Estado de Agentes

[![Google Cloud - Manage Agent Memory and State](https://img.shields.io/badge/Google%20Cloud-Manage%20Agent%20Memory-4285F4?logo=googlecloud&logoColor=white)](./08-badge-conclusao.md)

Este módulo aborda como utilizar **estado e memória** para transformar agentes de LLM que respondem de forma independente em sistemas capazes de **manter contexto, armazenar informações estruturadas e oferecer experiências personalizadas**. 

Através do **Session State** do Google Agent Development Kit (ADK), é possível superar a limitação do histórico conversacional puro, garantindo acesso e controle programático sobre os dados da sessão.

---

## 🎯 Objetivos do Módulo

- 🧠 **Diferenciar Histórico de Estado:** Compreender que o histórico fornece contexto textual ao LLM, enquanto o estado possibilita dados estruturados e acessíveis para o código.
- 💾 **Persistência Programática:** Acessar e manipular `session.state` via Python e automatizar o armazenamento de respostas com `output_key`.
- 🔄 **Injeção Dinâmica de Estado (`{var}`):** Modelar instruções que se adaptam dinamicamente ao contexto usando `{var}`, `{var?}` e `{var?default}`.
- 🗂️ **Gestão de Escopos e Ciclos de Vida:** Organizar e isolar dados aplicando os namespaces de estado: `temp:`, sessão, `user:` e `app:`.

---

## 📚 Conteúdo do Módulo

| Seção | Descrição / Foco Principal | Arquivos |
| :--- | :--- | :---: |
| **01 — Estado da Sessão** | Como transformar conversas em dados estruturados acessíveis ao código via `session.state` e `output_key`. | [Problema](./01-desafio-historico-conversas.md) / [Solução](./02-solucao-estado-sessao.md) |
| **02 — Modelagem de Estado (`{var}`)** | Injeção dinâmica de variáveis de estado diretamente no prompt do agente com tratamento de valores padrão. | [Problema](./03-desafio-como-agentes-usam-valores.md) / [Solução](./04-modelagem-de-estado.md) |
| **03 — Namespaces de Estado** | Gestão dos diferentes ciclos de vida dos dados usando os escopos `temp:`, sessão, `user:` e `app:`. | [Problema](./05-desafio-diferentes-ciclos-estado.md) / [Solução](./06-solucao-namespaces.md) |
| **04 — Conclusão do Módulo** | Síntese sobre persistência, controle programático e tabelas de decisão rápida. | [Acessar](./07-conclusao.md) |
| **05 — Badge de Conclusão** | Registro da conquista da credencial oficial *Manage Agent Memory and State*. | [Acessar](./08-badge-conclusao.md) |

---

## 💬 Histórico da Conversa vs. 🧠 Estado da Sessão

```text
💬 HISTÓRICO DA CONVERSA                  🧠 ESTADO DA SESSÃO
 (Texto Livre / Contexto)                 (Dados Estruturados / Código)
┌─────────────────────────┐              ┌─────────────────────────────┐
│ Usuário: "Meu nome é    │              │ session.state = {           │
│           Alex"         │ ───────────> │   "user_name": "Alex",      │
│ Agente:  "Prazer Alex!" │              │   "user_language": "pt-BR", │
└─────────────────────────┘              │   "user:theme": "dark"      │
                                         │ }                           │
                                         └──────────────┬──────────────┘
                                                        │
                                                        ▼
                                           💻 Leitura Programática no Code
                                           📝 Injeção no Prompt via {var}

```

* **Histórico da Conversa:** Serve para interpretação de texto e contexto natural pelo LLM.


* **Estado da Sessão:** Funciona como um dicionário chave-valor que o código Python lê, valida, atualiza e usa em condicionais.



---

## 🗂️ Os 4 Namespaces de Estado

Os namespaces definem a duração e o alcance das informações no sistema:

| Namespace | Prefixo | Ciclo de Vida / Persistência | Casos de Uso Recomendados |
| --- | --- | --- | --- |
| **⚡ Temporário** | `temp:` | Válido apenas durante a invocação/turno atual.| Passos intermediários, flags e cálculos voláteis.|
| **💬 Sessão** | *(sem)* | Mantido ao longo da conversa/sessão atual.| Tópico da conversa, carrinho da sessão e contadores.|
| **👤 Usuário** | `user:` | Persiste entre diferentes sessões do mesmo usuário. | Idioma preferido, tema visual e nível de assinatura.|
| **🌐 Aplicação** | `app:` | Compartilhado globalmente por todos os usuários. | Endpoints de API, versão do sistema e feature flags. |

---

## 🗂️ Estrutura da Pasta

```text
04-gerenciamento-de-memoria-e-estado-de-agentes/
├── README.md
├── 01-desafio-historico-conversas.md
├── 02-solucao-estado-sessao.md
├── 03-desafio-como-agentes-usam-valores.md
├── 04-modelagem-de-estado.md
├── 05-desafio-diferentes-ciclos-estado.md
├── 06-solucao-namespaces.md
├── 07-conclusao.md
└── 08-badge-conclusao.md
```

<div align="center">

## 👩‍💻 Autora

**Ana Carolina Pereira Ruas**  
Engenheira Florestal  
**Foco em Dados, Machine Learning, IA Generativa, LLMs, Agentes e Cloud**  

---
⭐ *Repositório desenvolvido como parte dos estudos da GEAR — Gemini Enterprise Agent Platform.*

</div>