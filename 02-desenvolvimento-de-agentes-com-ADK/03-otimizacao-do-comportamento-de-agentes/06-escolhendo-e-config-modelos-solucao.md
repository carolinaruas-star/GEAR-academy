## ⚙️ Google ADK — Configuração Estratégica do Modelo

### A solução: configuração estratégica do modelo

### 🎯 Objetivo

Aprender a selecionar o modelo adequado e configurar seus parâmetros de geração de acordo com o objetivo do agente, equilibrando:

**Qualidade → Consistência → Criatividade → Segurança → Custo**

A configuração é realizada principalmente por meio do `GenerateContentConfig`.

---

### 🤖 Seleção do modelo

A escolha do modelo deve considerar a **complexidade da tarefa**, a qualidade necessária, o custo e a velocidade de resposta.

Uma estratégia recomendada é começar com um modelo mais capaz para estabelecer um **baseline de qualidade** e, posteriormente, avaliar modelos mais econômicos.

#### 🧠 Gemini 2.5 Pro

Indicado para:

* Análises complexas
* Tarefas que exigem maior qualidade
* Raciocínio avançado
* Prototipagem e avaliação inicial
* Estabelecimento de valores de referência (*quality baseline*)

#### ⚡ Gemini 2.5 Flash

Indicado quando:

* Velocidade é prioridade
* O custo precisa ser reduzido
* A tarefa não exige o máximo nível de raciocínio
* Existe uma grande quantidade de requisições em produção

### 📊 Estratégia de otimização

```text
Gemini 2.5 Pro
      ↓
Estabelecer baseline de qualidade
      ↓
Testar Gemini 2.5 Flash
      ↓
Análise de lacunas
      ↓
Verificar se a qualidade atende ao requisito
      ↓
Produção com maior eficiência
```

A ideia não é simplesmente escolher o modelo mais barato, mas encontrar o **modelo de menor custo que ainda atende aos requisitos de qualidade**.

---

## 🎛️ `GenerateContentConfig`

O ADK permite personalizar o comportamento do modelo utilizando:

```python id="x7k0q3"
from google.genai import types
```

E configurando:

```python id="h6j3v9"
generate_content_config=types.GenerateContentConfig(
    temperature=0.2,
    max_output_tokens=250,
    top_p=0.8,
    top_k=10
)
```

Os principais parâmetros são:

| Parâmetro           | Função                                            |
| ------------------- | ------------------------------------------------- |
| `temperature`       | Controla aleatoriedade/criatividade               |
| `max_output_tokens` | Define o tamanho máximo da resposta               |
| `top_p`             | Controla a amostragem por probabilidade acumulada |
| `top_k`             | Limita as opções de tokens consideradas           |
| `safety_settings`   | Define políticas de filtragem de conteúdo         |

---

## 🌡️ Temperatura

A temperatura controla o grau de **aleatoriedade na geração da resposta**.

### 🔵 Baixa — `0.0` a `0.3`

Prioriza:

**Consistência + previsibilidade**

Ideal para:

* 📊 Extração de dados
* 🔎 Perguntas factuais
* 📋 Classificação
* 🧩 Saída estruturada

Exemplo:

```python id="e3zn9w"
factual_config = types.GenerateContentConfig(
    temperature=0.1
)
```

---

### 🟡 Média — `0.4` a `0.7`

Equilibra:

**Criatividade + consistência**

Ideal para:

* 💬 Atendimento ao cliente
* 🧭 Orientações
* 💭 Conversas gerais

```python id="9q5m2a"
balanced_config = types.GenerateContentConfig(
    temperature=0.7
)
```

---

### 🔴 Alta — `0.8` a `1.0`

Prioriza:

**Criatividade + diversidade**

Ideal para:

* ✍️ Escrita criativa
* 💡 Brainstorming
* 📢 Marketing
* 🧠 Geração de ideias

```python id="v5c8jk"
creative_config = types.GenerateContentConfig(
    temperature=0.9
)
```

### 📌 Regra prática

```text
0.0 ───── 0.3 ───── 0.7 ───── 1.0
 │          │          │          │
Factual  Consistente  Equilíbrio  Criativo
```

---

## 🛡️ Configurações de segurança

O `GenerateContentConfig` também permite definir políticas específicas de segurança.

```python id="7qv4ne"
strict_config = types.GenerateContentConfig(
    safety_settings=[
        types.SafetySetting(
            category=types.HarmCategory.HARM_CATEGORY_DANGEROUS_CONTENT,
            threshold=types.HarmBlockThreshold.BLOCK_LOW_AND_ABOVE
        ),
        types.SafetySetting(
            category=types.HarmCategory.HARM_CATEGORY_HARASSMENT,
            threshold=types.HarmBlockThreshold.BLOCK_LOW_AND_ABOVE
        ),
        types.SafetySetting(
            category=types.HarmCategory.HARM_CATEGORY_HATE_SPEECH,
            threshold=types.HarmBlockThreshold.BLOCK_LOW_AND_ABOVE
        ),
        types.SafetySetting(
            category=types.HarmCategory.HARM_CATEGORY_SEXUALLY_EXPLICIT,
            threshold=types.HarmBlockThreshold.BLOCK_LOW_AND_ABOVE
        )
    ]
)
```

### 🚦 Níveis de filtragem

| Threshold                | Comportamento                              |
| ------------------------ | ------------------------------------------ |
| `BLOCK_NONE`             | Sem filtragem                              |
| `BLOCK_ONLY_HIGH`        | Bloqueia apenas alta probabilidade de dano |
| `BLOCK_MEDIUM_AND_ABOVE` | Bloqueia probabilidade média e alta        |
| `BLOCK_LOW_AND_ABOVE`    | Filtragem mais rigorosa                    |

Para aplicações reais, a configuração deve considerar o **contexto, público e requisitos de segurança** do agente.

> ⚠️ As configurações de segurança apresentadas são específicas dos modelos Gemini. Outros provedores, como Claude ou GPT, possuem APIs e parâmetros próprios.

---

## 🧮 Tokens e amostragem

Também é possível controlar o tamanho e a diversidade das respostas.

### Respostas mais completas

```python id="q8x2mz"
comprehensive_config = types.GenerateContentConfig(
    temperature=0.7,
    max_output_tokens=2000,
    top_p=0.95,
    top_k=40
)
```

### Respostas mais concisas

```python id="n3v6pa"
concise_config = types.GenerateContentConfig(
    temperature=0.3,
    max_output_tokens=100,
    top_p=0.8,
    top_k=10
)
```

### 🔎 Principais parâmetros

**`max_output_tokens`**

Define o número máximo de tokens que podem ser utilizados na resposta.

**`top_p`**

Realiza *nucleus sampling*, considerando os tokens dentro de uma determinada massa acumulada de probabilidade.

**`top_k`**

Limita a seleção aos `K` tokens mais prováveis em cada etapa da geração.

---

## 🛠️ Exemplo prático — Comparação de agentes

O exercício utiliza dois agentes com objetivos diferentes:

```text
                 Modelos + Configurações
                         │
              ┌──────────┴──────────┐
              ▼                     ▼
       Data Extractor        Creative Brainstormer
              │                     │
        Gemini Flash          Gemini Pro
        Temp. 0.1             Temp. 0.9
        500 tokens             2000 tokens
              │                     │
        Consistência            Criatividade
```

### 📊 Agente factual

```python id="t8x5q1"
factual_agent = LlmAgent(
    model="gemini-2.5-flash",
    name="data_extractor",
    description="Extrai informações factuais com alta consistência",
    instruction="""
Você é um extrator de dados preciso.

Extraia os fatos exatamente como apresentados.

Não:
- Adicione informações que não estejam na entrada.
- Faça deduções ou inferências.
- Utilize linguagem criativa.

Seja preciso, conciso e determinista.
""",
    generate_content_config=types.GenerateContentConfig(
        temperature=0.1,
        max_output_tokens=500,
        top_p=0.8,
        top_k=10
    )
)
```

### 🎨 Agente criativo

```python id="c1r9vk"
creative_agent = LlmAgent(
    model="gemini-2.5-pro",
    name="creative_brainstormer",
    description="Gera ideias criativas e explora possibilidades",
    instruction="""
Você é um parceiro de criação de ideias inovadoras.

Gere ideias variadas e imaginativas.

Fique à vontade para:
- Combinar conceitos inesperados.
- Explorar abordagens pouco convencionais.
- Analisar novas possibilidades.

Seja criativo, diversificado e instigante.
""",
    generate_content_config=types.GenerateContentConfig(
        temperature=0.9,
        max_output_tokens=2000,
        top_p=0.95,
        top_k=40
    )
)
```

---

### 🧪 Comparação dos comportamentos

#### 📊 Agente factual

Entrada:

```text
Extraia as informações principais:
"O iPhone 15 Pro foi lançado em setembro de 2023
e custa a partir de US$ 999 com 128 GB."
```

Comportamento esperado:

* ✅ Respostas consistentes
* ✅ Extração precisa
* ✅ Sem interpretações criativas
* ✅ Formato previsível
* ✅ Repetibilidade entre execuções

#### 💡 Agente criativo

Entrada:

```text
Discuta ideias sobre 5 recursos inovadores
para um smartphone de última geração.
```

Comportamento esperado:

* 💡 Ideias variadas
* 🔀 Maior diversidade entre respostas
* 🚀 Sugestões inovadoras
* 📝 Respostas mais detalhadas
* 🧠 Exploração de possibilidades

---

## 📈 Comparação das configurações

| Característica | Factual          | Criativo       |
| -------------- | ---------------- | -------------- |
| Modelo         | Gemini 2.5 Flash | Gemini 2.5 Pro |
| Temperatura    | `0.1`            | `0.9`          |
| Max tokens     | `500`            | `2000`         |
| Top P          | `0.8`            | `0.95`         |
| Top K          | `10`             | `40`           |
| Prioridade     | Consistência     | Criatividade   |
| Uso            | Extração         | Brainstorming  |

---

### 💡 Principais aprendizados

1. **A escolha do modelo deve considerar a tarefa**, e não apenas a capacidade máxima disponível.
2. O **Gemini 2.5 Pro** pode ser utilizado como referência inicial de qualidade.
3. O **Gemini 2.5 Flash** pode ser utilizado para otimizar custo e velocidade quando a qualidade for suficiente.
4. **Temperatura baixa** favorece consistência e previsibilidade.
5. **Temperatura alta** favorece criatividade e diversidade.
6. `max_output_tokens` controla o tamanho máximo da resposta.
7. `top_p` e `top_k` influenciam o processo de amostragem.
8. `safety_settings` permite adaptar a filtragem de conteúdo ao contexto.
9. A configuração ideal depende do **caso de uso**.
10. A otimização deve buscar o melhor equilíbrio entre **qualidade, custo, velocidade e segurança**.

### 🔑 Conceitos-chave

`Gemini 2.5 Pro` · `Gemini 2.5 Flash` · `GenerateContentConfig` · `temperature` · `max_output_tokens` · `top_p` · `top_k` · `safety_settings` · `Model Selection` · `Sampling` · `Safety` · `Cost Optimization`
