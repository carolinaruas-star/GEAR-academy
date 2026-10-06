# 🤖 Aula 1 - Introdução e evolução dos agentes de IA generativa

## 🎯 Contexto do curso

**Agentes de IA generativa: transforme sua organização** é o quinto e último curso do programa de aprendizado **Líder em IA generativa do Google Cloud**.

O curso apresenta como as organizações podem utilizar **agentes de IA generativa personalizados** para solucionar desafios específicos de negócio e transformar seus processos.

O foco desta introdução está em compreender **o que são agentes, como eles evoluíram e quais componentes permitem que eles sejam mais flexíveis e úteis**.

---

# 🏢 1. Por que utilizar agentes personalizados?

Aplicações padrão nem sempre conseguem atender às necessidades específicas de uma organização.

Em muitos casos, é necessário desenvolver soluções capazes de:

* 🔗 Conectar-se aos sistemas da empresa;
* ⚙️ Integrar-se aos processos existentes;
* 🎯 Atender necessidades específicas do negócio;
* 🤖 Utilizar agentes para realizar tarefas e solucionar problemas.

Porém, uma solução personalizada não significa necessariamente construir tudo do zero.

O cenário de IA generativa pode ser compreendido por diferentes camadas:

1. 🏗️ **Infraestrutura**
2. 🧠 **Modelos**
3. 🛠️ **Plataforma**
4. 🤖 **Agentes**
5. 📱 **Aplicativos com tecnologia de IA generativa**

Neste curso, o foco está principalmente na camada de **agentes**.

---

# 🤖 2. O que são agentes de IA?

Agentes são sistemas capazes de **observar uma situação, utilizar recursos disponíveis e executar ações** para atingir determinado objetivo.

Ao longo do tempo, esses agentes evoluíram de sistemas altamente previsíveis e limitados para sistemas capazes de compreender linguagem natural, acessar informações e executar tarefas de maneira mais flexível.

Essa evolução pode ser dividida em três grandes estágios:

```text
Agentes determinísticos
        ↓
Agentes generativos
        ↓
Agentes generativos + RAG
```

Os agentes atuais também podem combinar características **determinísticas e generativas**, formando sistemas híbridos.

---

# 🕰️ 3. Evolução dos agentes

## 3.1 Agentes determinísticos

Os primeiros agentes virtuais eram predominantemente **determinísticos**.

Eles funcionavam com base em:

* 🔀 Fluxos predefinidos;
* 🌳 Árvores de decisão;
* ⚙️ Regras específicas;
* ⚡ Eventos;
* 🎯 Ações previamente determinadas.

Nesse modelo, uma equipe precisava definir antecipadamente o comportamento do agente em cada situação.

### 🔒 Característica principal

Um agente determinístico apresenta **alto grau de controle e previsibilidade**.

Para uma mesma entrada, espera-se que o sistema produza a mesma saída.

```text
Entrada → Regras/Fluxo → Saída
```

### ⚠️ Limitações

Embora sejam previsíveis, esses agentes podem apresentar dificuldades quando recebem situações que não foram previstas durante sua criação.

Um exemplo clássico são os antigos sistemas de atendimento telefônico:

> "Pressione 1 para agendamento, 2 para informações..."

Se o usuário apresenta uma solicitação fora dos caminhos programados, o agente pode não saber como responder.

---

# 🧠 4. Agentes generativos

A chegada da **IA generativa** transformou significativamente as capacidades dos agentes.

Diferentemente dos sistemas baseados apenas em palavras-chave e caminhos predefinidos, os agentes generativos utilizam **modelos de linguagem** para compreender o significado e a intenção por trás das mensagens.

Isso permite:

* 💬 Conversas mais naturais;
* 🧠 Compreensão de intenção;
* 🔄 Maior flexibilidade;
* 🎯 Interpretação de perguntas formuladas de diferentes maneiras;
* ✨ Respostas mais criativas e variadas.

Uma mesma pergunta pode produzir respostas diferentes, pois existe um grau maior de variabilidade no comportamento generativo.

### Comparação

| Característica        | Determinístico           | Generativo                    |
| --------------------- | ------------------------ | ----------------------------- |
| Funcionamento         | Regras e fluxos          | Modelo de IA generativa       |
| Previsibilidade       | Alta                     | Menor                         |
| Flexibilidade         | Baixa                    | Alta                          |
| Compreensão           | Regras/intenção limitada | Significado e intenção        |
| Respostas             | Predeterminadas          | Geradas dinamicamente         |
| Situações inesperadas | Maior dificuldade        | Maior capacidade de adaptação |

---

# 🧩 5. Os componentes dos agentes

A evolução dos agentes está relacionada à combinação de diferentes componentes.

Os três componentes principais destacados no curso são:

### 🧠 Modelo de fundação

É o componente responsável pelas capacidades de compreensão e geração de linguagem do agente.

Nos agentes generativos, o modelo permite interpretar o significado e a intenção das solicitações.

### 🛠️ Ferramentas

Permitem que o agente **interaja com recursos externos** e realize ações.

As ferramentas ampliam as capacidades do modelo, permitindo que o agente vá além de simplesmente gerar uma resposta.

### 🔄 Raciocínio de repetição

Permite que o agente trabalhe de forma iterativa, combinando raciocínio e utilização de ferramentas para chegar a um resultado.

Uma representação simplificada é:

```text
Observar
   ↓
Raciocinar
   ↓
Utilizar ferramenta
   ↓
Observar resultado
   ↓
Raciocinar novamente
   ↓
Executar próxima ação
```

Esses componentes trabalham em conjunto para permitir que o agente **observe o contexto e aja utilizando os recursos disponíveis**.

---

# 📚 6. O surgimento da RAG

Os primeiros agentes generativos já utilizavam modelos e ferramentas, mas existia uma limitação importante.

Os modelos não conseguiam necessariamente **incorporar diretamente as informações obtidas por ferramentas ao seu conhecimento**.

Como consequência, as respostas poderiam:

* ❌ Não estar atualizadas;
* ❌ Não ser relevantes para o caso de uso;
* ❌ Não estar fundamentadas nas informações mais recentes.

Uma solução importante para esse problema foi a **RAG — Retrieval-Augmented Generation**, ou **Geração Aumentada por Recuperação**.

---

## 🔎 6.1 Como funciona a RAG?

A RAG permite que o modelo acesse informações provenientes de **fontes externas de dados** e utilize essas informações para gerar suas respostas.

De forma simplificada:

```text
Pergunta do usuário
        ↓
Busca por informações relevantes
        ↓
Dados recuperados
        ↓
Modelo de IA
        ↓
Resposta fundamentada
```

Isso permite trabalhar com informações:

* 📚 Mais relevantes;
* 🕐 Mais atualizadas;
* 🔎 Provenientes de fontes externas;
* 🎯 Mais adequadas ao contexto da tarefa.

---

# 🔗 7. A evolução dos agentes

A evolução apresentada no curso pode ser resumida da seguinte maneira:

### 1️⃣ Agentes determinísticos

Baseados em regras, fluxos e caminhos predefinidos.

```text
Regras + Fluxos
```

⬇️

### 2️⃣ Agentes generativos

Passam a utilizar modelos de IA generativa para compreender linguagem e gerar respostas.

```text
Modelo + Raciocínio + Ferramentas
```

⬇️

### 3️⃣ Agentes generativos com RAG

Passam a utilizar informações externas para produzir respostas mais relevantes e atualizadas.

```text
Modelo + Raciocínio + Ferramentas + Informações externas
```

⬇️

### 4️⃣ Agentes híbridos

Os agentes mais complexos podem combinar **comportamentos determinísticos e generativos**.

```text
Determinístico + Generativo
          ↓
      Agente híbrido
```

Essa combinação permite utilizar a **previsibilidade dos fluxos determinísticos** em situações que exigem controle e a **flexibilidade da IA generativa** em situações que exigem interpretação e adaptação.

---

# 🧠 8. Agentes híbridos

Os agentes atuais não precisam escolher entre ser exclusivamente determinísticos ou exclusivamente generativos.

Eles podem combinar os dois modelos.

### 🔒 Componentes determinísticos

São úteis quando é necessário:

* Controle;
* Previsibilidade;
* Regras específicas;
* Fluxos obrigatórios.

### ✨ Componentes generativos

São úteis quando é necessário:

* Flexibilidade;
* Interpretação de linguagem;
* Compreensão de intenção;
* Geração de respostas;
* Adaptação a diferentes situações.

A combinação dos dois permite construir agentes mais **poderosos e adequados a diferentes cenários empresariais**.

---

# 📝 9. Ordem de evolução dos agentes

A atividade de revisão apresenta três categorias para ordenar conforme a inovação técnica:

1. **Agentes determinísticos**
2. **Agentes generativos sem RAG**
3. **Agentes generativos com RAG**

Essa sequência representa a evolução dos agentes em direção a sistemas com maior capacidade de **compreensão, flexibilidade e acesso a informações externas**.

---

# 🔑 Principais aprendizados

* 🤖 Agentes virtuais existem há muito tempo, mas suas capacidades evoluíram significativamente.
* 🔒 Agentes determinísticos utilizam regras e caminhos predefinidos.
* 🧠 Agentes generativos utilizam modelos de linguagem para compreender significado e intenção.
* 🛠️ Ferramentas permitem que agentes interajam com recursos externos e realizem ações.
* 🔄 O raciocínio de repetição permite que o agente execute ciclos iterativos.
* 📚 A RAG permite acessar informações externas para gerar respostas mais relevantes e atualizadas.
* 🔗 Agentes modernos podem combinar componentes determinísticos e generativos.
* 🏢 A evolução dos agentes amplia suas possibilidades de aplicação em organizações.

---

> 🎯 **Conclusão:** a evolução dos agentes de IA passou de sistemas determinísticos, baseados em regras e fluxos predefinidos, para agentes generativos capazes de compreender intenção, utilizar ferramentas e acessar informações externas por meio de RAG. Hoje, a combinação entre **controle determinístico e flexibilidade generativa** permite criar agentes mais poderosos e adequados às necessidades das organizações.

---

## 📌 Próximo conteúdo

A partir daqui, o curso começa a aprofundar individualmente os principais componentes dos agentes, começando pelos **modelos de IA generativa**.
