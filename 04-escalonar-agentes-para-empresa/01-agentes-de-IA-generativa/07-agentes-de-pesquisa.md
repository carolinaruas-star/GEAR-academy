# 🔎 Aula 7 — O poder dos agentes de pesquisa

## 🎯 Visão geral

Os **agentes de pesquisa** permitem conectar experiências de busca e recomendação a dados empresariais, utilizando recursos de IA generativa para ajudar os usuários a encontrar, compreender e utilizar informações.

Nesta aula, o destaque é a **Vertex AI para Pesquisa**, solução do Google Cloud que combina:

* 🔎 pesquisa;
* 💡 recomendações;
* 📚 conexão com dados;
* 🧠 IA generativa;
* 🔗 embasamento;
* 🔄 RAG.

A solução pode ser utilizada tanto em experiências voltadas aos clientes quanto em bases de conhecimento internas.

---

# ☁️ Vertex AI para Pesquisa

A **Vertex AI para Pesquisa** oferece soluções para **pesquisa e recomendação**.

Ela pode conectar diferentes tipos de dados e permitir que usuários encontrem informações relevantes de maneira mais eficiente.

```text id="4rj8xw"
              Vertex AI para Pesquisa
                       ↓
             ┌─────────┴─────────┐
             ↓                   ↓
         🔎 Pesquisa          💡 Recomendação
             ↓                   ↓
       Encontrar dados      Sugerir conteúdos
```

---

# 🔎 Soluções de pesquisa

A funcionalidade de pesquisa pode ser utilizada para criar experiências de busca para sites públicos.

Ela consegue indexar e pesquisar diferentes tipos de dados, incluindo:

* 📊 dados estruturados no **BigQuery**;
* 📄 documentos não estruturados no **Google Cloud Storage**.

Isso permite que o usuário encontre informações independentemente da forma como os dados estão armazenados.

---

## 📚 Pesquisa de documentos

Indicada para grandes repositórios de **documentos não estruturados** armazenados no Google Cloud Storage.

É especialmente útil para conteúdos com grande quantidade de texto, como:

* bases de conhecimento internas;
* arquivos empresariais;
* repositórios de documentos.

---

## 🎥 Pesquisa de mídia

Permite trabalhar com conteúdos relacionados a mídia.

---

## 🏥 Pesquisa de serviços de saúde

Oferece recursos direcionados à pesquisa no contexto de serviços de saúde.

---

## 🛒 Pesquisa de comércio

É voltada para experiências de pesquisa relacionadas ao comércio eletrônico.

---

# 💡 Soluções de recomendação

Além da pesquisa, a Vertex AI para Pesquisa oferece mecanismos de **recomendação**.

O mecanismo de recomendação de uso geral pode analisar:

* comportamento do usuário;
* atributos dos conteúdos;
* características dos itens.

Com essas informações, pode oferecer recomendações personalizadas.

### Objetivos

As recomendações podem ajudar a:

* aumentar o engajamento;
* facilitar a descoberta de conteúdos;
* personalizar a experiência do usuário.

---

## 🎥 Recomendações de mídia

Permitem recomendar conteúdos relacionados ao consumo de mídia.

## 🛍️ Recomendações de varejo

Podem ser utilizadas para sugerir produtos e melhorar experiências de compra.

---

# ⚙️ Como funciona a Vertex AI para Pesquisa?

A Vertex AI para Pesquisa combina três elementos importantes:

```text id="6v0q9a"
      Conexão de dados
            +
         Embasamento
            +
      IA generativa
            ↓
    Vertex AI para Pesquisa
```

A solução pode acessar diferentes tipos de repositórios:

* 📊 bancos de dados estruturados;
* 📄 repositórios de documentos não estruturados;
* 🔀 combinação dos dois.

---

# 🤖 Vertex AI para Pesquisa como agente

A conexão com os dados permite que a Vertex AI para Pesquisa funcione de maneira semelhante a um agente.

Ela pode:

1. 👀 observar a consulta ou o contexto do usuário;
2. 🔎 acessar os repositórios de dados;
3. 📚 recuperar informações relevantes;
4. 💡 sugerir conteúdos ou itens;
5. 💬 apresentar informações ao usuário.

Nesse processo, os repositórios de dados funcionam como **ferramentas** utilizadas para responder à necessidade do usuário.

```text id="v3m8qp"
Usuário
   ↓
Consulta
   ↓
Vertex AI para Pesquisa
   ↓
Repositórios de dados
   ↓
Recuperação de informações
   ↓
IA generativa
   ↓
Resposta / recomendação
```

---

# 🔗 Relação entre Vertex AI para Pesquisa e RAG

Um dos principais recursos da Vertex AI para Pesquisa é a possibilidade de **fundamentar as respostas da IA generativa nos próprios dados da organização**.

As fontes podem incluir:

* 🏢 dados próprios;
* 🔗 dados de terceiros selecionados;
* 🌐 informações provenientes do Google, por meio do embasamento com a Pesquisa Google.

Essa abordagem ajuda a reduzir o risco de **alucinações** e a fornecer informações mais confiáveis.

### RAG nesse processo

Quando as fontes de dados são utilizadas para fundamentar as respostas do LLM, a Vertex AI para Pesquisa utiliza o conceito de **RAG**.

```text id="p4h7sa"
Dados da organização
        ↓
     Recuperação
        ↓
Informações relevantes
        ↓
Aumento do contexto
        ↓
       LLM
        ↓
Resposta fundamentada
```

Assim, a Aula 8 aplica na prática o conceito apresentado na Aula 7.

---

# ✨ Recursos de IA generativa

A Vertex AI para Pesquisa pode adicionar recursos generativos às experiências de pesquisa.

## 📝 Resumos de pesquisa

A solução pode gerar **resumos concisos e informativos** dos resultados encontrados.

Isso pode ajudar o usuário a obter rapidamente uma visão geral.

Os resumos podem ser utilizados para:

* resumir documentos;
* comparar produtos;
* sintetizar descobertas de vários resultados.

---

## 💬 Respostas e perguntas complementares

A pesquisa também pode fornecer **respostas geradas por IA** com base nos resultados encontrados.

O usuário pode fazer perguntas utilizando linguagem natural e, depois, realizar perguntas complementares.

```text id="n5k3cd"
Pergunta do usuário
        ↓
Pesquisa
        ↓
Resultados relevantes
        ↓
Resposta gerada por IA
        ↓
Pergunta complementar
        ↓
Nova resposta
```

Isso torna a experiência de pesquisa mais próxima de uma conversa.

---

# 🏢 Recursos para empresas

A Vertex AI para Pesquisa foi desenvolvida considerando necessidades empresariais.

Entre os recursos destacados estão:

### 🔐 Segurança

Oferece controles de acesso granulares para proteger os dados.

### 📊 Análises

Permite analisar tendências de pesquisa e comportamento dos usuários.

### 📈 Escalabilidade

Possui infraestrutura preparada para lidar com grandes volumes de dados e solicitações.

### 🔗 Integração

Pode ser integrada aos sistemas empresariais existentes por meio de:

* APIs;
* SDKs.

---

# 🏢 Aplicações empresariais

A Vertex AI para Pesquisa pode ser utilizada em diferentes contextos.

### 👥 Experiência voltada ao cliente

Pode melhorar a pesquisa em sites e aplicações utilizadas pelos consumidores.

### 📚 Base de conhecimento interna

Pode ajudar funcionários a encontrar informações dentro de documentos e dados da organização.

```text id="x8j2nk"
               Vertex AI para Pesquisa
                         ↓
              ┌──────────┴──────────┐
              ↓                     ↓
          👥 Clientes          👨‍💼 Funcionários
              ↓                     ↓
       Pesquisa pública       Conhecimento interno
```

---

# 👕 Caso de uso: experiência de compra

A aula apresenta um caso de uso envolvendo uma **empresa de roupas**.

O objetivo é utilizar a Vertex AI para Pesquisa para tornar a experiência de compra online:

* mais intuitiva;
* personalizada;
* eficiente.

Nesse cenário, recursos de pesquisa e recomendação podem ajudar os consumidores a encontrar produtos e informações relevantes com mais facilidade.

---

# 🧠 Pesquisa tradicional × agentes de pesquisa

| Característica | Pesquisa tradicional | Agente de pesquisa                      |
| -------------- | -------------------- | --------------------------------------- |
| Busca          | Localiza informações | Localiza e interpreta informações       |
| Dados externos | Pode utilizar        | Pode utilizar                           |
| IA generativa  | Não necessariamente  | Integrada                               |
| RAG            | Pode não existir     | Pode fundamentar respostas              |
| Resumos        | Limitados            | Pode gerar resumos                      |
| Conversação    | Limitada             | Pode responder perguntas complementares |
| Personalização | Variável             | Pode utilizar contexto e comportamento  |

---

# 🔗 Relação com as aulas anteriores

A Aula 8 reúne vários conceitos apresentados anteriormente:

```text id="r5d1qm"
Aula 4
ReAct + CoT
     ↓
Aula 5
Ferramentas
     ↓
Aula 7
RAG + fontes externas
     ↓
Aula 8
Vertex AI para Pesquisa
     ↓
Pesquisa + Recomendações + IA generativa
```

Isso mostra como os conceitos de **raciocínio, ferramentas e RAG** podem ser combinados em uma solução empresarial.

---

# 🧠 Principais aprendizados

* 🔎 A **Vertex AI para Pesquisa** oferece soluções de pesquisa e recomendação.
* 📊 Ela pode trabalhar com dados estruturados e não estruturados.
* 📚 Documentos armazenados no Google Cloud Storage podem ser utilizados como fontes de pesquisa.
* 💡 O mecanismo de recomendação pode utilizar comportamento do usuário e atributos do conteúdo.
* 🤖 A solução pode funcionar de maneira semelhante a um agente, utilizando repositórios de dados como ferramentas.
* 🔗 A **RAG** permite fundamentar respostas da IA generativa nos dados disponíveis.
* 📝 A Vertex AI para Pesquisa pode gerar resumos dos resultados.
* 💬 Também pode fornecer respostas em linguagem natural e perguntas complementares.
* 🔐 Recursos empresariais incluem controles de acesso, análises e escalabilidade.
* 🏢 A solução pode ser utilizada tanto em experiências para clientes quanto em bases de conhecimento internas.

> 🎯 **Conclusão:** Os agentes de pesquisa combinam pesquisa, dados, RAG e IA generativa para transformar uma simples experiência de busca em uma interação mais inteligente. A Vertex AI para Pesquisa permite que organizações conectem seus próprios dados a recursos de pesquisa, recomendação e geração de respostas fundamentadas.
