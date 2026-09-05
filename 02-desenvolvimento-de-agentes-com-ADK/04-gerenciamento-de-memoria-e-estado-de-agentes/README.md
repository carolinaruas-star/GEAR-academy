# 🧠 Módulo 4: Gerenciamento de Memória e Estado de Agentes

<p align="center">
  <strong>Google Cloud Skills Boost • Google Agent Development Kit (ADK)</strong>
</p>

<p align="center">
  <strong>Dando memória e contexto aos agentes de IA.</strong>
</p>

---

## 📚 Sobre o módulo

Este módulo apresenta como utilizar **estado e memória** para transformar agentes de LLM que respondem de forma independente em agentes capazes de **manter contexto, armazenar informações e oferecer experiências mais personalizadas**.

A abordagem parte de um problema comum em sistemas conversacionais: o histórico da conversa, por si só, nem sempre oferece o controle programático necessário sobre as informações utilizadas pelo agente.

Com os recursos de **Session State** do Google ADK, é possível armazenar e manipular informações durante a execução dos agentes, além de controlar como esses valores são utilizados nas instruções.

---

## 🎯 Objetivos de aprendizagem

Ao longo do módulo, os principais objetivos são:

* 🧠 Compreender o conceito de **estado da sessão**;
* 💾 Armazenar informações relevantes durante uma interação;
* 🔄 Utilizar valores de estado nas instruções dos agentes;
* 🧩 Modelar instruções dinamicamente utilizando `{var}`;
* 🗂️ Organizar diferentes tipos de estado utilizando **namespaces**;
* 🎯 Controlar quais informações devem permanecer disponíveis em diferentes contextos;
* 🤖 Criar agentes capazes de oferecer experiências mais personalizadas.

---

## 🧩 Conteúdos do módulo

### 01 — 💬 Estado da sessão

Primeiro contato com o problema de manter informações úteis além do simples histórico de mensagens.

**Principais conceitos:**

* Session State;
* Contexto da conversa;
* Persistência de informações;
* Estado versus histórico de conversação;
* Controle programático do contexto.

O estado permite que o agente trabalhe com informações armazenadas de maneira estruturada durante a sessão.

---

### 02 — 🔄 Modelagem de estado com `{var}`

Estudo de como os valores armazenados no estado podem ser utilizados dinamicamente pelas instruções dos agentes.

**Principais conceitos:**

* `{var}`;
* Templates de instrução;
* Valores dinâmicos;
* Personalização das respostas;
* Integração entre estado e `instruction`.

A utilização de variáveis permite que as instruções sejam adaptadas de acordo com as informações disponíveis na sessão.

---

### 03 — 🗂️ Namespaces de estado

Nem todas as informações precisam possuir o mesmo nível de persistência ou compartilhamento.

Os **namespaces** permitem organizar o estado de acordo com seu escopo e finalidade.

**Principais conceitos:**

* Namespaces;
* Escopo do estado;
* Organização das informações;
* Persistência;
* Separação entre diferentes tipos de dados;
* Controle de acesso às informações de estado.

---

## 🧠 Estado x Histórico da conversa

Um dos principais conceitos apresentados no módulo é a diferença entre simplesmente possuir um **histórico de mensagens** e possuir um **estado controlável programaticamente**.

```text
💬 HISTÓRICO DA CONVERSA
        │
        │ mensagens anteriores
        ▼
   Contexto textual
        │
        │
        ▼
🧠 ESTADO DA SESSÃO
        │
        ├── Preferências
        ├── Informações do usuário
        ├── Dados temporários
        ├── Resultados intermediários
        └── Configurações
                │
                ▼
        🤖 AGENTE PERSONALIZADO
```

O estado adiciona uma camada estruturada que permite ao sistema **armazenar, recuperar e utilizar informações de forma programática**.

---

## 🔄 Fluxo conceitual

```text
👤 Usuário
    │
    ▼
💬 Interação
    │
    ▼
🧠 Session State
    │
    ├── Armazena informações
    │
    ├── Atualiza valores
    │
    └── Disponibiliza contexto
            │
            ▼
      📝 {var}
            │
            ▼
     🤖 Instrução dinâmica
            │
            ▼
      🎯 Resposta personalizada
```

---

## 🛠️ Conceitos fundamentais

| Conceito                    | Função                                                           |
| --------------------------- | ---------------------------------------------------------------- |
| 🧠 **Session State**        | Armazena informações associadas à sessão                         |
| 🔄 **`{var}`**              | Permite utilizar valores de estado dinamicamente nas instruções  |
| 📝 **Instruction Template** | Define como o agente utiliza informações armazenadas             |
| 🗂️ **Namespaces**          | Organizam o estado de acordo com seu escopo                      |
| 💾 **Persistência**         | Determina por quanto tempo uma informação permanece disponível   |
| 🎯 **Contexto**             | Fornece informações relevantes para personalizar o comportamento |

---

## 💡 Principais aprendizados

### 🧠 Estado é diferente de histórico

O histórico registra a sequência de interações, enquanto o estado fornece uma estrutura para **armazenar e manipular informações que o sistema precisa controlar**.

### 🔄 Instruções podem ser dinâmicas

Com `{var}`, informações armazenadas no estado podem ser incorporadas às instruções, permitindo que o comportamento do agente seja adaptado ao contexto atual.

### 🗂️ Nem todo estado possui o mesmo escopo

Algumas informações são temporárias, enquanto outras podem precisar ser compartilhadas ou mantidas por mais tempo.

Os namespaces ajudam a organizar essas informações de acordo com sua finalidade.

### 🎯 Estado permite personalização

Ao armazenar preferências e informações relevantes, os agentes podem oferecer respostas mais contextualizadas e experiências mais personalizadas.

---

## 🧩 Aplicações práticas

O gerenciamento de estado pode ser utilizado em diversos cenários.

### 👤 Preferências do usuário

```text
Nome: Carolina
Idioma: Português
Preferência: Respostas objetivas
Tema de interesse: Inteligência Artificial
```

O agente pode utilizar essas informações para adaptar suas respostas ao usuário.

---

### 🛒 E-commerce

```text
🧠 Estado da sessão

produto = "Notebook"
categoria = "Tecnologia"
faixa_preco = "R$ 3.000 - R$ 5.000"
```

Essas informações podem ser utilizadas para manter o contexto durante uma jornada de compra.

---

### 🎓 Assistente educacional

```text
🧠 Estado

curso = "Google ADK"
modulo = 4
nivel = "Intermediário"
tema_atual = "Session State"
```

O agente pode utilizar o estado para continuar uma experiência de aprendizagem contextualizada.

---

### 💬 Atendimento ao cliente

```text
🧠 Estado

cliente = "Usuário"
assunto = "Cobrança"
ticket = "12345"
status = "Em análise"
```

O estado permite que diferentes etapas do atendimento utilizem informações já coletadas.

---

## ⚠️ Pontos de atenção

Ao trabalhar com estado, é importante considerar:

* 🔐 Quais informações podem ser armazenadas;
* 🎯 Qual informação é realmente necessária;
* 🗂️ Qual deve ser o escopo de cada dado;
* 💾 Quais informações precisam persistir;
* 🔄 Quando os valores devem ser atualizados;
* 🧹 Quando informações temporárias devem deixar de ser utilizadas;
* 🛡️ Como proteger dados sensíveis.

> O gerenciamento de estado deve ser planejado de acordo com a necessidade da aplicação, evitando armazenar informações desnecessárias ou manter dados além do período necessário.

---

## 🗂️ Organização dos estudos

Os conteúdos do módulo seguem uma progressão baseada no problema → solução → verificação:

```text
01 ── 💬 Estado da sessão
 │
 ├── Problema
 ├── Solução
 └── Teste
        │
        ▼
02 ── 🔄 Modelagem com {var}
 │
 ├── Problema
 ├── Solução
 └── Teste
        │
        ▼
03 ── 🗂️ Namespaces de estado
 │
 ├── Problema
 ├── Solução
 └── Teste
        │
        ▼
📖 Lista de leitura
        │
        ▼
🏁 Conclusão
```

---

## 📌 Estrutura do módulo

```text
04-gerenciamento-de-memoria-e-estado-de-agentes/
│
├── 01-session-state-problema.md
├── 02-session-state-solucao.md
├── 03-state-modeling-problema.md
├── 04-state-modeling-solucao.md
├── 05-state-namespaces-problema.md
├── 06-state-namespaces-solucao.md
├── 07-conclusao.md
├── 08-badge-conclusao.md
│
└── README.md
```

> Os nomes dos arquivos podem ser ajustados para acompanhar exatamente a nomenclatura utilizada no repositório.

---

## 🚀 Próxima etapa

Após aprender a controlar **estado, contexto e memória**, o próximo passo é ampliar as capacidades dos agentes para que eles possam **utilizar ferramentas e interagir com recursos externos**.

Isso permite avançar de agentes que apenas processam informações para sistemas capazes de **consultar dados, executar ações e participar de workflows mais completos**.

---

<p align="center">
  <strong>🧠 Google Agent Development Kit (ADK)</strong><br>
  Dando contexto, memória e estado aos agentes de IA.
</p>
