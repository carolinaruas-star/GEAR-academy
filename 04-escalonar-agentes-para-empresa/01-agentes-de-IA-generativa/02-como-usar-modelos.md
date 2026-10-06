# 🧠 Aula 2 — Como usar modelos

## 🎯 Visão geral

Os **modelos de IA generativa** são o cérebro dos agentes de IA. Eles são responsáveis por compreender entradas, identificar padrões e gerar respostas ou conteúdos.

Depois que um modelo é treinado e disponibilizado para uso, ainda é possível **ajustar seu comportamento** por meio de parâmetros e configurações.

Esses ajustes permitem adaptar as respostas do modelo de acordo com o objetivo da aplicação, como:

* 📝 Produzir textos mais criativos;
* 📌 Gerar respostas mais objetivas;
* 📚 Criar resumos concisos;
* 💬 Manter determinado tom;
* 🎯 Controlar o nível de variabilidade das respostas.

---

# ⚙️ 1. Parâmetros de amostragem

Os **parâmetros de amostragem** funcionam como controles que influenciam a forma como o modelo escolhe o conteúdo que será gerado.

Entre os principais parâmetros apresentados estão:

* 🔢 Contagem de tokens;
* 🌡️ Temperatura;
* 🎯 Top-K;
* 📊 Top-P;
* 🔐 Configurações de segurança;
* 📏 Tamanho do resultado.

O ajuste desses parâmetros permite alinhar o comportamento do modelo às necessidades da aplicação.

---

# 🔢 2. Contagem de tokens

Os modelos processam textos em unidades chamadas **tokens**.

Um token pode representar uma palavra, parte de uma palavra, pontuação ou outro fragmento de texto.

Os modelos possuem um limite de tokens que conseguem processar por vez.

### Quanto maior a quantidade de tokens disponível:

* 💬 Conversas mais longas podem ser processadas;
* 📚 Contextos mais complexos podem ser utilizados;
* ⚙️ Maior capacidade de processamento pode ser necessária.

Como referência apresentada no curso, **100 tokens correspondem aproximadamente a 60–80 palavras em inglês**, embora a quantidade varie conforme o idioma e o conteúdo.

---

# 🌡️ 3. Temperatura

A **temperatura** controla o grau de aleatoriedade das respostas do modelo.

### 🔽 Temperatura baixa

Restringe a seleção às palavras com maior probabilidade.

É mais adequada para tarefas que precisam de respostas:

* 📌 Objetivas;
* 📚 Factuais;
* 📝 Consistentes;
* 🔎 Menos variadas.

**Exemplos:** respostas a perguntas e criação de resumos.

### 🔼 Temperatura alta

Permite maior variedade na escolha das palavras, incluindo opções menos prováveis.

Pode ser útil para:

* ✨ Criação de conteúdo;
* 💡 Ideias;
* 🎨 Textos criativos;
* 🧠 Respostas mais inesperadas.

### Resumo

```text
Temperatura baixa → mais previsibilidade
Temperatura alta   → mais criatividade/variabilidade
```

---

# 🎯 4. Top-K

O **Top-K** limita a seleção às **K palavras mais prováveis**.

Por exemplo, com:

```text
Top-K = 2
```

o modelo seleciona aleatoriamente entre as duas opções com maior probabilidade.

Isso permite que uma alternativa com alta probabilidade também tenha oportunidade de ser escolhida, em vez de selecionar sempre a opção mais provável.

### ⚠️ Limitação

O Top-K pode não ser ideal quando a distribuição de probabilidades é muito desigual.

Se uma palavra tiver probabilidade muito alta e as demais forem muito improváveis, selecionar um conjunto fixo de palavras pode gerar resultados menos adequados.

---

# 📊 5. Top-P

O **Top-P**, também chamado de **amostragem de núcleo (nucleus sampling)**, utiliza um conjunto de palavras definido dinamicamente com base na probabilidade acumulada.

Em vez de definir uma quantidade fixa de palavras, o modelo seleciona o menor conjunto cuja soma das probabilidades atinja ou ultrapasse o valor de **P**.

### Exemplo

Com:

```text
Top-P = 0,75
```

o modelo considera um conjunto de palavras cuja probabilidade cumulativa seja igual ou superior a 75%.

A quantidade de palavras consideradas pode variar conforme a distribuição de probabilidades.

### Top-K × Top-P

| Parâmetro | Critério                               |
| --------- | -------------------------------------- |
| **Top-K** | Número fixo de palavras mais prováveis |
| **Top-P** | Probabilidade acumulada mínima         |
| **Top-K** | Conjunto de tamanho fixo               |
| **Top-P** | Conjunto de tamanho variável           |

---

# 🛡️ 6. Configurações de segurança

Além dos parâmetros relacionados à geração de conteúdo, os modelos também podem possuir **configurações de segurança** para controlar determinados tipos de conteúdo produzidos ou processados pela aplicação.

Essas configurações fazem parte do controle do comportamento do modelo dentro de uma solução de IA generativa.

---

# 📏 7. Tamanho do resultado

O tamanho máximo da resposta também pode ser configurado.

Um resultado menor pode ser útil quando se busca:

* 📌 Concisão;
* ⚡ Respostas rápidas;
* 📝 Resumos.

Já resultados maiores podem ser necessários para conteúdos mais detalhados ou complexos.

---

# 🧪 8. Como os parâmetros influenciam o modelo?

Uma combinação de parâmetros pode ser utilizada de acordo com o objetivo da aplicação.

### Resposta concisa e factual

```text
Temperatura → baixa
Tamanho do resultado → menor
```

### Conteúdo criativo e aberto

```text
Temperatura → alta
Top-P → ajustado para permitir maior variedade
```

O ponto principal é que **não existe uma configuração universalmente ideal**.

Os parâmetros devem ser testados e ajustados de acordo com o resultado desejado.

---

# 🔌 9. APIs de IA generativa

Uma maneira comum de acessar modelos de IA generativa é por meio de **APIs (Application Programming Interfaces)**.

Uma API permite que diferentes sistemas de software se comuniquem e troquem informações.

Em uma aplicação de IA generativa, o fluxo pode ser representado assim:

```text
Aplicação
    ↓
API
    ↓
Modelo de IA generativa
    ↓
Resposta
    ↓
Aplicação
```

Além de enviar o comando ao modelo, a aplicação pode incluir **parâmetros e configurações** na solicitação para personalizar o comportamento da IA.

---

# ☁️ 10. APIs de IA generativa do Google

As APIs de IA generativa do Google disponibilizam **modelos de linguagem grandes pré-treinados**, que podem ser utilizados e adaptados para diferentes tarefas.

Entre os recursos apresentados estão:

* ✍️ Preenchimento de texto;
* 💬 Conversas multiturno;
* 💻 Geração de código;
* 🖼️ Geração de imagens.

Um exemplo citado é a **API Imagen**, utilizada para geração e personalização de imagens.

---

# 🧪 11. Google AI Studio e Vertex AI Studio

O Google disponibiliza duas ferramentas importantes para experimentar e utilizar APIs de modelos de IA generativa:

* **Google AI Studio**
* **Vertex AI Studio**

Embora ambas permitam trabalhar com a API Gemini, elas possuem propostas diferentes.

## 🔵 Google AI Studio

É uma interface simplificada para explorar os recursos do Gemini e experimentar diferentes configurações.

### Características

* 👩‍💻 Voltado a iniciantes, entusiastas e pessoas em fase inicial de desenvolvimento;
* 🧪 Facilita testes e prototipação;
* 🎛️ Permite experimentar parâmetros;
* 📝 Possibilita testar diferentes formatos de conteúdo;
* 🔑 Pode ser acessado com uma Conta do Google;
* 📊 Possui limites de uso, sendo menos adequado para aplicações de grande escala.

É especialmente útil para **aprender, experimentar e criar protótipos iniciais**.

---

## 🟢 Vertex AI Studio

Faz parte da plataforma **Vertex AI do Google Cloud** e oferece um ambiente mais completo para desenvolvimento profissional.

### Características

* 👨‍💻 Voltado a profissionais, pesquisadores e desenvolvedores;
* ☁️ Integrado ao Google Cloud;
* 📈 Mais adequado para soluções profissionais e escaláveis;
* 🔐 Oferece recursos de segurança e compliance de nível empresarial;
* 📊 Possui cotas de uso mais flexíveis;
* 💰 O uso está sujeito a cobrança conforme o serviço utilizado.

---

# ⚖️ 12. Google AI Studio × Vertex AI Studio

| Característica           | Google AI Studio              | Vertex AI Studio                    |
| ------------------------ | ----------------------------- | ----------------------------------- |
| **Foco**                 | Experimentação e prototipação | Desenvolvimento profissional        |
| **Público**              | Iniciantes e entusiastas      | Profissionais e desenvolvedores     |
| **Acesso**               | Conta Google                  | Google Cloud                        |
| **Uso**                  | Testes e protótipos           | Soluções profissionais e escaláveis |
| **Limites**              | Limites de uso                | Cotas mais flexíveis                |
| **Segurança/Compliance** | Mais limitado                 | Recursos empresariais               |
| **Cobrança**             | Adequado para experimentação  | Cobrança conforme utilização        |

### 📌 Regra prática

> **Google AI Studio** → ideal para começar, experimentar e criar protótipos.

> **Vertex AI Studio** → mais adequado para desenvolver soluções profissionais, escaláveis e voltadas ao ambiente empresarial.

---

# 🧪 13. Experimentação prática

O curso propõe utilizar o **Google AI Studio** como um playground para observar na prática como diferentes parâmetros alteram o comportamento do Gemini.

A atividade envolve:

1. Abrir o Google AI Studio;
2. Criar um comando criativo;
3. Testar diferentes valores de temperatura;
4. Experimentar outros parâmetros de amostragem;
5. Observar e analisar as mudanças nas respostas.

Essa experimentação ajuda a compreender que pequenas alterações nas configurações podem produzir resultados diferentes.

---

# 🧠 Principais aprendizados

* 🧠 Modelos de IA generativa são o **cérebro dos agentes**.
* ⚙️ Parâmetros permitem ajustar o comportamento do modelo.
* 🔢 Tokens representam unidades de processamento do texto.
* 🌡️ Temperatura controla o grau de aleatoriedade.
* 🎯 Top-K limita a seleção às K opções mais prováveis.
* 📊 Top-P utiliza uma probabilidade acumulada para definir dinamicamente o conjunto de opções.
* 📏 O tamanho do resultado pode ser controlado conforme a necessidade.
* 🔌 APIs permitem integrar modelos de IA generativa às aplicações.
* 🧪 **Google AI Studio** é indicado principalmente para experimentação e prototipação.
* ☁️ **Vertex AI Studio** é mais adequado para soluções profissionais e escaláveis.
* 🔄 A experimentação é importante para encontrar as configurações mais adequadas a cada caso de uso.

---

> 🎯 **Conclusão:** os modelos de IA generativa são o cérebro dos agentes, mas o resultado obtido depende também de como esses modelos são configurados e utilizados. Parâmetros como **temperatura, Top-K, Top-P, tokens e tamanho da resposta** permitem controlar seu comportamento, enquanto ferramentas como **Google AI Studio e Vertex AI Studio** facilitam a experimentação e a integração dos modelos em aplicações.
