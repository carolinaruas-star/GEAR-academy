# 🤖 Abstração de Agentes

A **abstração de agentes** representa uma evolução na forma como sistemas de IA utilizam modelos de linguagem. A principal diferença está na passagem do **saber para o fazer**: enquanto um LLM pode fornecer orientações e sugestões, um agente consegue utilizar ferramentas, planejar ações e executá-las de forma autônoma.

## 🧩 Da LLM aos agentes

A evolução pode ser entendida em três etapas.

### 1. APIs de LLM

Os LLMs permitem conversar com a IA, fazer perguntas e gerar conteúdos. Porém, são **desconectados do mundo externo**: conseguem processar informações, mas não podem interagir diretamente com sistemas como e-mails, calendários ou serviços de reserva.

### 2. LLMs com chamadas de função

As chamadas de função permitem que o modelo utilize **funções, APIs e bancos de dados**. Isso amplia suas capacidades, mas ainda exige que alguém coordene o fluxo e determine quais funções devem ser chamadas e em qual sequência.

### 3. Agentes

O agente adiciona **autonomia** ao processo. Em vez de receber instruções para cada etapa, ele recebe um objetivo e pode determinar quais ferramentas utilizar, em qual sequência e como adaptar suas ações de acordo com os resultados.

> **💡 Exemplo:** em vez de apenas ensinar como planejar uma viagem para Paris, um agente pode pesquisar voos, verificar hotéis, considerar orçamento e agenda e apresentar uma combinação adequada para aprovação.

## 🧠 O que diferencia um agente?

Um agente não é simplesmente um LLM conectado a ferramentas. Ele é um sistema capaz de **atingir objetivos de forma autônoma**, mantendo contexto, planejando antecipadamente e tomando iniciativa.

As principais características são **operação autônoma, raciocínio e planejamento, aprendizado contínuo, consciência ambiental e uso de ferramentas**.

## 🌦️ Exemplo prático

Considere a pergunta: **"Será que eu deveria usar um casaco hoje?"**

Um LLM tradicional pode fornecer uma recomendação genérica, mas não possui acesso ao ambiente atual.

Um LLM com chamada de função consegue consultar uma API meteorológica, mas o usuário ainda precisa conduzir o fluxo: solicitar a consulta e depois fazer uma nova pergunta.

Um **agente**, por outro lado, pode buscar autonomamente a localização, consultar a previsão, verificar atividades na agenda e considerar o horário em que a pessoa estará fora. Com essas informações, pode fornecer uma recomendação contextualizada.

A diferença fundamental é que o agente **busca e combina o contexto necessário sem precisar receber instruções para cada etapa**.

## 🔄 Problemas adequados para agentes

Os agentes são especialmente úteis quando uma tarefa exige múltiplas ações coordenadas e adaptação ao ambiente.

**Fluxos de trabalho complexos:** podem executar uma sequência de etapas, como extrair recibos, categorizar despesas, verificar políticas, solicitar aprovação e atualizar sistemas contábeis.

**Solução dinâmica de problemas:** conseguem adaptar o plano quando as condições mudam, como em uma reserva de viagem na qual voos ficam indisponíveis ou preços são alterados.

**Gerenciamento contínuo:** podem monitorar uma situação e agir quando uma condição é atendida, como acompanhar o preço de uma passagem e realizar uma ação quando atingir determinado valor.

**Experiências integradas:** podem coordenar diferentes sistemas para alcançar um único objetivo, utilizando ferramentas como calendários, bancos de dados, serviços externos e plataformas de comunicação.

## 🎯 Principal diferença

A principal capacidade que diferencia agentes de **LLMs com chamadas de função** é a **autonomia para escolher as ferramentas e determinar a sequência em que serão utilizadas**.

O modelo deixa de apenas executar funções quando solicitado e passa a decidir **como utilizar suas capacidades para alcançar um objetivo**.

## 📌 Pontos principais

A abstração de agentes representa uma mudança de paradigma:

**De reativo → para proativo:** o agente não apenas responde, mas busca alcançar objetivos.

**De isolado → para integrado:** mantém contexto e interage com diferentes sistemas.

**De consultor → para executor:** não apenas informa o que deve ser feito, mas pode realizar as ações necessárias.

**De estático → para adaptativo:** ajusta sua abordagem conforme recebe novas informações do ambiente.

> **💡 Ideia central:** a diferença entre um LLM com ferramentas e um agente está principalmente na **autonomia**. O agente recebe um objetivo, decide como agir, utiliza as ferramentas necessárias e adapta o processo até alcançar o resultado esperado.




