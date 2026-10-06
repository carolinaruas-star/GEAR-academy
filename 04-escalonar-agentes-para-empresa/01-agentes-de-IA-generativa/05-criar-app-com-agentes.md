# 🚀 Aula 5 — Como criar aplicativos com agentes

## 🎯 Visão geral

Depois de criar e configurar um agente de IA generativa, o próximo passo é **integrá-lo a aplicações**.

A API Gemini permite incorporar recursos de IA generativa em diferentes tipos de sistemas, desde aplicações Web e dispositivos móveis até softwares de computador e sistemas embarcados.

Nesta aula, são apresentados:

* 🔌 integração por APIs;
* ☁️ Cloud Run functions e Cloud Run;
* 🧩 ferramentas sem código e pouco código;
* 🤝 aplicações multiagentes;
* 🧠 agentes especializados trabalhando em conjunto.

---

# 🔌 Como usar a API

Para utilizar um modelo de IA generativa em uma aplicação, é possível utilizar a **API Gemini**.

O processo de integração depende do ambiente utilizado e das ferramentas escolhidas.

## Google AI Studio

No **Google AI Studio**, é possível gerar uma **chave de API** para utilizar a API Gemini em aplicações.

```text
Google AI Studio
       ↓
Gerar chave de API
       ↓
Aplicação
       ↓
API Gemini
       ↓
Modelo de IA
```

---

## ☁️ Vertex AI Studio

No **Vertex AI Studio**, a integração envolve a configuração de mecanismos de **autenticação e autorização**.

Isso permite que aplicações utilizem os modelos e recursos de IA disponibilizados pelo Google Cloud.

---

# 🌐 Integrando a API aos aplicativos

Com a API ou com o código correspondente, o agente pode ser utilizado dentro de aplicações.

A API Gemini pode ser integrada a praticamente qualquer aplicação capaz de realizar **solicitações HTTP**.

Isso inclui:

* 🌐 aplicações Web;
* 📱 aplicativos para dispositivos móveis;
* 💻 softwares para computador;
* ⚙️ sistemas embarcados.

A ideia central é:

```text
Aplicação
    ↓
Solicitação HTTP
    ↓
API Gemini
    ↓
Modelo de IA
    ↓
Resposta
    ↓
Aplicação
```

Isso torna a integração bastante flexível.

---

# ☁️ Serviços para integração

A aula apresenta algumas opções que podem ser utilizadas para incorporar os agentes e modelos às aplicações.

## ⚙️ Cloud Run functions

Permite executar funções que podem interagir com a API e fazer parte da aplicação.

## ☁️ Cloud Run

Pode ser utilizado para executar aplicações e serviços que utilizam os recursos de IA generativa.

Essas opções permitem colocar o código responsável pela integração em execução e conectá-lo aos aplicativos.

---

# 🧩 Desenvolvimento sem código e pouco código

A integração com IA generativa não precisa necessariamente exigir uma aplicação desenvolvida totalmente do zero.

Também é possível utilizar ferramentas de **no-code e low-code** do Google.

### 📝 Apps Script

Pode ser utilizado para criar automações e integrar recursos de IA a aplicações e fluxos baseados no ecossistema Google.

### 📱 AppSheet

Permite criar aplicações utilizando uma abordagem de pouco código, podendo incorporar recursos de IA generativa.

Assim, diferentes níveis de conhecimento técnico podem ser utilizados para incorporar IA aos processos e aplicações.

---

# 🤝 Aplicações multiagentes

Algumas aplicações podem exigir **mais de um agente**.

Nesse cenário, utiliza-se uma arquitetura **multiagente**, na qual diferentes agentes são especializados em tarefas específicas.

Em vez de um único agente tentar realizar tudo, cada agente pode assumir uma responsabilidade.

```text
                 Aplicação
                     ↓
              Agente principal
             ↙       ↓       ↘
            ↓        ↓        ↓
        Agente    Agente    Agente
        Voos      Hotéis   Atrações
```

---

# ✈️ Exemplo: aplicativo de reserva de viagens

Imagine uma aplicação responsável por organizar uma viagem.

Ela poderia utilizar:

### ✈️ Agente de voos

Responsável por pesquisar opções de voos.

### 🏨 Agente de hotéis

Responsável por encontrar hospedagens.

### 📍 Agente de atrações

Responsável por sugerir atrações e atividades no destino.

Os agentes podem trabalhar:

* de forma independente;
* de maneira coordenada;
* interagindo uns com os outros.

O resultado é uma experiência integrada para o usuário.

---

# ⭐ Vantagens dos sistemas multiagentes

A divisão das responsabilidades entre diferentes agentes pode proporcionar:

### 🧩 Modularidade

Cada agente possui uma função específica.

### ⚡ Eficiência

As tarefas podem ser distribuídas entre diferentes agentes.

### 🔄 Flexibilidade

É possível modificar ou substituir um agente específico sem necessariamente alterar todo o sistema.

### 📈 Escalabilidade

A arquitetura pode ser expandida com novos agentes e capacidades conforme as necessidades aumentam.

---

# 🤖 Um agente também pode ser uma ferramenta

Um conceito importante apresentado na aula é que **um agente pode ser utilizado como ferramenta por outro agente**.

Por exemplo:

```text
Agente de atendimento
        ↓
Agente de análise de sentimento
        ↓
Avalia a satisfação do usuário
        ↓
Resultado retorna ao
agente de atendimento
```

### 💡 Exemplo

Durante uma conversa com um cliente, um agente de atendimento pode utilizar um **agente especializado em análise de sentimento** para avaliar o nível de satisfação do usuário.

Dessa forma, um agente pode aproveitar a capacidade especializada de outro agente.

---

# 🔄 Arquitetura de uma aplicação multiagente

Uma aplicação mais complexa pode combinar vários agentes especializados:

```text
                    👤 Usuário
                        ↓
                 🤖 Agente principal
                        ↓
          ┌─────────────┼─────────────┐
          ↓             ↓             ↓
      ✈️ Voos       🏨 Hotéis     📍 Atrações
          ↓             ↓             ↓
          └─────────────┼─────────────┘
                        ↓
                 Resultado integrado
                        ↓
                     👤 Usuário
```

Essa arquitetura permite distribuir tarefas complexas entre componentes especializados.

---

# 🆚 Aplicação com um agente × aplicação multiagente

| Característica    | Um agente                              | Multiagente                                |
| ----------------- | -------------------------------------- | ------------------------------------------ |
| Responsabilidades | Centralizadas                          | Distribuídas                               |
| Especialização    | Um agente pode executar várias tarefas | Cada agente pode ter uma função específica |
| Complexidade      | Mais simples                           | Mais complexa                              |
| Modularidade      | Menor                                  | Maior                                      |
| Escalabilidade    | Pode ser limitada                      | Pode ser ampliada com novos agentes        |
| Exemplo           | Assistente geral                       | Sistema de reserva de viagens              |

---

# 🧠 Principais aprendizados

* 🔌 A **API Gemini** permite integrar modelos de IA generativa a aplicações.
* 🌐 Aplicações capazes de realizar solicitações HTTP podem utilizar a API.
* ☁️ **Cloud Run functions** e **Cloud Run** são opções para executar componentes da integração.
* 📝 Ferramentas como **Apps Script** permitem desenvolver soluções com pouco código.
* 📱 **AppSheet** possibilita criar aplicações utilizando uma abordagem low-code.
* 🤝 Sistemas **multiagentes** utilizam agentes especializados para realizar diferentes tarefas.
* 🧩 A especialização torna as aplicações mais modulares e flexíveis.
* 🔗 Um agente também pode atuar como **ferramenta de outro agente**.
* 📈 A arquitetura multiagente pode facilitar a expansão de sistemas mais complexos.

> 🎯 **Conclusão:** Os agentes de IA generativa podem ser integrados a diferentes tipos de aplicações por meio de APIs, serviços de execução e ferramentas no-code ou low-code. Para tarefas mais complexas, arquiteturas multiagentes permitem distribuir responsabilidades entre agentes especializados, aumentando a modularidade, flexibilidade e escalabilidade das soluções.
