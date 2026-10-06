# 🔎 Aula 6 — Geração aumentada por recuperação (RAG) e ferramentas

## 🎯 Visão geral

A **Geração Aumentada por Recuperação (RAG — Retrieval-Augmented Generation)** permite que modelos de linguagem utilizem informações provenientes de **fontes externas de conhecimento** para produzir respostas mais precisas, relevantes e atualizadas.

Antes da RAG, os modelos podiam utilizar ferramentas para buscar informações, mas tinham limitações para **processar e integrar essas informações ao contexto utilizado para gerar respostas**.

Nesta aula, são apresentados:

* 🔎 o funcionamento da RAG;
* 🛠️ a relação entre RAG e ferramentas;
* 📚 fontes externas de conhecimento;
* 🗄️ repositórios de dados;
* 🧠 bancos de dados vetoriais;
* 🔄 recuperação iterativa;
* 🌐 dados estruturados e não estruturados.

---

# 🕰️ Histórico anterior à RAG

Antes da RAG, os modelos de linguagem dependiam principalmente dos **dados utilizados durante seu treinamento**.

Eles podiam utilizar ferramentas para consultar informações externas, mas os dados recuperados tinham uso limitado dentro daquela interação.

De forma simplificada:

```text id="8zv1fp"
Modelo
  ↓
Dados de treinamento
  ↓
Conhecimento disponível

Ferramenta
  ↓
Busca informação externa
  ↓
Resultado utilizado na consulta
```

O modelo não conseguia utilizar facilmente essas informações externas como parte de uma base de conhecimento integrada.

Isso limitava sua capacidade de responder utilizando informações:

* mais recentes;
* específicas;
* internas;
* provenientes de fontes externas.

A RAG surgiu para melhorar esse processo.

---

# 🔎 O que é RAG?

**RAG** significa **Retrieval-Augmented Generation**, ou **Geração Aumentada por Recuperação**.

A técnica permite que um LLM:

1. 🔎 recupere informações relevantes de fontes externas;
2. ➕ utilize essas informações para aumentar o contexto;
3. ✍️ gere uma resposta fundamentada nesse conhecimento.

O fluxo básico é:

```text id="n8bq6v"
Consulta do usuário
        ↓
     🔎 Recuperação
        ↓
Informações relevantes
        ↓
     ➕ Aumento
        ↓
Contexto para o LLM
        ↓
     ✍️ Geração
        ↓
      Resposta
```

---

# 🧩 Etapas da RAG

O funcionamento da RAG pode ser dividido em três etapas principais.

## 1. 🔎 Recuperação

O LLM utiliza ferramentas para encontrar informações relevantes em fontes externas.

Essas fontes podem incluir:

* 🗄️ repositórios de dados;
* 🔢 bancos de dados vetoriais;
* 🔎 mecanismos de pesquisa;
* 🕸️ mapas de informações.

O objetivo é recuperar documentos ou trechos relacionados à consulta do usuário.

---

## 2. ➕ Aumento

As informações recuperadas são utilizadas para **aumentar o contexto disponível para o modelo**.

Em vez de depender apenas do conhecimento adquirido durante o treinamento, o LLM recebe informações adicionais relacionadas à solicitação.

```text id="l2d6k9"
Pergunta do usuário
        +
Informações recuperadas
        ↓
     Contexto
        ↓
       LLM
```

---

## 3. ✍️ Geração

Com o contexto enriquecido pelas informações recuperadas, o LLM gera a resposta ao usuário.

O objetivo é produzir uma resposta:

* mais relevante;
* mais precisa;
* mais atualizada;
* fundamentada em fontes externas.

---

# 🗂️ Fontes utilizadas na recuperação

A RAG pode trabalhar com diferentes tipos de fontes.

## 🗄️ Repositórios de dados

Podem ser bancos de dados internos ou outras fontes estruturadas e não estruturadas.

## 🔢 Bancos de dados vetoriais

Armazenam **embeddings**, que são representações numéricas de conteúdos.

Esses embeddings permitem encontrar informações que possuem **similaridade semântica** com a consulta do usuário.

O processo pode ser representado assim:

```text id="q0w1t6"
Consulta do usuário
       ↓
Criação do embedding
       ↓
Busca no banco vetorial
       ↓
Documentos semanticamente semelhantes
       ↓
Contexto para o LLM
```

---

## 🔎 Mecanismos de pesquisa

O agente pode utilizar mecanismos de pesquisa, por meio de extensões ou APIs, para encontrar:

* páginas da Web;
* artigos;
* informações online;
* outros conteúdos relevantes.

Essa possibilidade é especialmente útil quando o agente precisa acessar informações que podem estar sendo atualizadas.

---

## 🕸️ Mapas de informações

São bancos de dados estruturados que armazenam informações sobre:

* entidades;
* relações entre entidades;
* fatos relacionados.

O LLM pode consultar esses mapas para recuperar informações e relações relevantes para uma determinada consulta.

---

# 🔄 RAG iterativa

A recuperação não precisa acontecer apenas uma vez.

Em alguns sistemas, o LLM pode **repetir o processo de recuperação** quando os resultados iniciais não são suficientes.

Por exemplo:

```text id="v6w4j2"
Consulta
  ↓
Recuperação
  ↓
Resultados insuficientes?
  ↓
    SIM
    ↓
Refinar consulta
    ↓
Nova recuperação
    ↓
Resultados melhores
```

O agente também pode utilizar outras ferramentas de recuperação ou até mesmo **pedir esclarecimentos ao usuário**.

Essa capacidade iterativa pode melhorar a qualidade e a relevância das respostas.

---

# 📰 Exemplo: pergunta sobre um evento recente

Imagine que um usuário faça uma pergunta sobre um acontecimento recente.

O conhecimento utilizado pelo modelo durante o treinamento pode não conter as informações mais atuais.

Com RAG, o processo pode ser:

```text id="t8n7r3"
👤 Consulta do usuário
        ↓
🔎 Recuperação de informações
        ↓
📚 Conteúdo externo relevante
        ↓
➕ Aumento do contexto
        ↓
🤖 LLM
        ↓
✍️ Resposta fundamentada
```

Se os resultados não forem suficientes, o agente pode realizar uma nova recuperação.

> 💡 **Ideia principal:** a RAG permite combinar a capacidade de geração do LLM com informações externas recuperadas dinamicamente.

---

# 🗃️ Repositórios de dados

Os **repositórios de dados** são componentes importantes de aplicações que utilizam RAG.

Eles funcionam como fontes de conhecimento que podem ser utilizadas pelo agente.

Essas fontes podem conter informações:

* estruturadas;
* não estruturadas;
* públicas;
* internas;
* atuais.

---

# 🌐 Tipos de dados utilizados

## 🌎 Sites

O agente pode acessar informações diretamente de páginas da Web.

Isso permite:

* acompanhar acontecimentos atuais;
* acessar informações públicas;
* recuperar conteúdos disponíveis online.

---

## 📊 Dados estruturados

São informações organizadas de maneira definida, como:

* tabelas;
* arquivos JSON;
* catálogos de produtos;
* bancos de dados de clientes;
* bases de conhecimento internas.

A Vertex AI pode compreender automaticamente a estrutura dos dados ou permitir que ela seja definida.

---

## 📄 Dados não estruturados

São informações armazenadas em arquivos que não seguem necessariamente uma estrutura tabular.

Exemplos:

* HTML;
* PDF;
* DOCX.

Esses documentos podem ser utilizados como fontes de conhecimento para o agente.

---

# 🧪 RAG em ação

A aula apresenta uma atividade prática utilizando o **Google AI Studio** e o embasamento com a **Pesquisa Google**.

O objetivo é observar como a utilização de informações recuperadas da Web pode produzir resultados mais relevantes.

O processo apresentado é:

```text id="c8h2m5"
1. Abrir o Google AI Studio
          ↓
2. Atualizar o modelo
          ↓
3. Executar um comando
          ↓
4. Receber resultados embasados
```

A atividade demonstra, na prática, como a recuperação de informações externas pode complementar o conhecimento do modelo.

---

# 🛠️ RAG + ferramentas

A relação entre RAG e ferramentas é fundamental.

As ferramentas fornecem ao agente os meios para **buscar informações externas**, enquanto a RAG define como essas informações podem ser utilizadas para enriquecer a geração da resposta.

```text id="u2e6r9"
             AGENTE
                ↓
            Ferramentas
                ↓
      ┌─────────┼─────────┐
      ↓         ↓         ↓
   Pesquisa  Banco      Dados
     Web     vetorial   internos
      └─────────┼─────────┘
                ↓
          Informações
           relevantes
                ↓
             Contexto
                ↓
               LLM
                ↓
             Resposta
```

---

# ⚖️ RAG sem fonte externa × RAG com fontes externas

| Característica     | Sem recuperação      | Com RAG                                        |
| ------------------ | -------------------- | ---------------------------------------------- |
| Fonte principal    | Dados de treinamento | Dados de treinamento + fontes externas         |
| Informações atuais | Limitadas            | Podem ser recuperadas dinamicamente            |
| Dados internos     | Limitados            | Podem ser utilizados                           |
| Busca externa      | Não necessariamente  | Parte importante do processo                   |
| Contexto           | Baseado no modelo    | Enriquecido com dados recuperados              |
| Relevância         | Pode ser limitada    | Pode ser aumentada com informações específicas |

---

# 🧠 Principais aprendizados

* 🔎 **RAG** significa Retrieval-Augmented Generation.
* 📚 A RAG permite que LLMs utilizem informações provenientes de fontes externas.
* 🛠️ Ferramentas podem ser utilizadas para recuperar essas informações.
* ➕ Os dados recuperados aumentam o contexto disponível para o modelo.
* ✍️ O LLM utiliza o contexto enriquecido para gerar a resposta.
* 🔢 Bancos de dados vetoriais utilizam embeddings para encontrar informações semanticamente semelhantes.
* 🔎 Mecanismos de pesquisa podem fornecer informações disponíveis na Web.
* 🗄️ Repositórios de dados podem conter informações estruturadas ou não estruturadas.
* 🔄 A recuperação pode ser repetida quando os resultados iniciais não forem suficientes.
* 🌐 Sites, bancos de dados, arquivos PDF, HTML e DOCX podem servir como fontes de conhecimento.

> 🎯 **Conclusão:** A RAG permite conectar modelos de linguagem a fontes externas de conhecimento, tornando suas respostas potencialmente mais precisas, relevantes e atualizadas. Quando combinada com ferramentas e repositórios de dados, ela amplia significativamente a capacidade dos agentes de acessar e utilizar informações externas.
