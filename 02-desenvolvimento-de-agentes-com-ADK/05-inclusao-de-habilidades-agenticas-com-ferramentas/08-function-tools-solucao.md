# 🛠️ A solução: ferramentas de função personalizadas

<p align="center">
  <strong>Escreva funções em Python para criar recursos agênticos personalizados.</strong>
</p>

<p align="center">
  <strong>Transformando lógica de negócio própria em ferramentas que o agente pode utilizar.</strong>
</p>

---

## 🧭 Introdução

Na etapa anterior, vimos que ferramentas genéricas nem sempre conseguem atender às necessidades específicas de uma empresa.

Cada negócio possui:

* 🏢 Regras próprias;
* 📊 Dados específicos;
* 🗄️ Sistemas internos;
* 🔌 APIs proprietárias;
* ⚙️ Fluxos de trabalho particulares.

A solução apresentada pelo ADK é permitir que o desenvolvedor **crie suas próprias ferramentas utilizando funções Python**.

A ideia central é simples:

```text
🐍 Função Python
      │
      ▼
🔍 ADK inspeciona a função
      │
      ├── Nome
      ├── Parâmetros
      ├── Dicas de tipo
      ├── Docstring
      └── Tipo de retorno
      │
      ▼
🧩 FunctionTool
      │
      ▼
🤖 Agente
```

Quando uma função Python é adicionada à lista `tools` de um agente, o ADK a encapsula automaticamente como uma **`FunctionTool`**.

---

# 🔄 Como funciona?

O processo pode ser dividido em quatro etapas.

### 01 — 🐍 Você escreve

Cria uma função Python contendo a lógica necessária.

### 02 — 🔍 O ADK inspeciona

O framework analisa os metadados da função:

* Nome;
* Parâmetros;
* Dicas de tipo;
* Docstring;
* Tipo de retorno.

### 03 — 🧩 O ADK gera

Essas informações são utilizadas para gerar o **esquema da ferramenta** que será apresentado ao LLM.

### 04 — 🤖 O agente utiliza

O LLM utiliza o esquema e a descrição para decidir **quando e como chamar a ferramenta**.

```text
🐍 Função Python
       │
       ▼
🔍 Inspeção pelo ADK
       │
       ▼
📋 Esquema da ferramenta
       │
       ▼
🧠 LLM interpreta
       │
       ▼
🔧 Chamada da ferramenta
       │
       ▼
📤 Resultado
```

---

# 🧩 Exemplo simples

Uma ferramenta para calcular custos de envio pode ser implementada diretamente em Python:

```python
from google.adk.agents import LlmAgent


def calculate_shipping_cost(
    weight_kg: float,
    country: str
) -> dict:
    """Calcula o custo de envio com base no peso e destino do pacote."""

    rates = {
        "usa": 10,
        "canada": 12,
        "uk": 15
    }

    if country.lower() not in rates:
        return {
            "status": "error",
            "error_message": f"Não enviamos para {country}"
        }

    cost = weight_kg * rates[country.lower()]

    return {
        "status": "success",
        "cost_usd": cost
    }


agent = LlmAgent(
    model='gemini-2.5-flash',
    instruction="Você ajuda os clientes com estimativas de custos de envio.",
    tools=[calculate_shipping_cost]
)
```

O ponto importante é:

```python
tools=[calculate_shipping_cost]
```

Não é necessário criar manualmente um objeto `FunctionTool`.

O ADK realiza esse encapsulamento automaticamente.

---

# 🚀 O que isso possibilita?

As ferramentas de função personalizadas permitem:

* 🏢 Integrar lógica específica do negócio;
* 🗄️ Acessar sistemas próprios por meio de Python;
* 🧮 Implementar cálculos específicos do domínio;
* ⚙️ Controlar completamente a implementação;
* 📋 Gerar automaticamente o esquema utilizado pelo LLM.

---

# 🧠 Agente x Ferramenta

Uma distinção fundamental é entender os papéis do **LLM** e da **ferramenta**.

```text
🤖 LLM
   │
   │ Decide QUANDO chamar
   ▼
🔧 Ferramenta
   │
   │ Executa O QUE fazer
   ▼
🏢 Sistema / API / Banco
```

O agente é responsável pelo **raciocínio e seleção da ferramenta**.

A ferramenta é responsável pela **execução da operação**.

---

# 🔄 Como as ferramentas se integram ao agente?

Considere uma solicitação de cálculo de frete:

```text
👤 Usuário
"Calcular frete para o Canadá"
        │
        ▼
🤖 Agente
Analisa a solicitação
        │
        ▼
🧠 Seleciona a ferramenta
calculate_shipping_cost
        │
        ▼
🔧 Ferramenta
weight=5
country="Canada"
        │
        ▼
🏢 Sistema / regras de negócio
        │
        ▼
🧮 5 kg × US$ 12/kg
        │
        ▼
📤 {"status": "success", "cost_usd": 60}
        │
        ▼
🤖 Agente
"O custo do frete é de US$ 60."
```

---

# 🧩 Principais conceitos

## 01 — 📝 Assinaturas de função importam

A assinatura da função é fundamental porque o ADK utiliza suas informações para gerar o esquema que o LLM irá interpretar.

```python
def get_shipping_cost(
    weight: float,
    destination: str
) -> dict:
    """Recupera o custo de frete de um pacote."""
    pass
```

A assinatura fornece informações importantes sobre:

```text
get_shipping_cost(
    weight: float,
    destination: str
) -> dict
      │
      ├── Nome da função
      ├── Parâmetros
      ├── Tipos
      └── Tipo de retorno
```

---

## 02 — 🏷️ Nomes de função descritivos

O nome da função ajuda o LLM a entender sua finalidade.

### ✅ Bom

Utilize nomes claros, preferencialmente no padrão:

```text
verbo + substantivo
```

Exemplos:

```python
def get_shipping_cost(...):
    pass


def calculate_loyalty_points(...):
    pass


def search_available_flights(...):
    pass
```

Esses nomes comunicam claramente a intenção da ferramenta.

### ❌ Ruim

```python
def process(data):
    pass


def do_stuff(x):
    pass


def handler(amount):
    pass
```

O LLM terá menos informações para determinar quando essas ferramentas devem ser utilizadas.

---

# 🏷️ Dicas de tipo

As **type hints** informam ao ADK quais tipos de valores o LLM deve fornecer.

### ✅ Recomendado

```python
def lookup_order(
    order_id: str,
    user_id: int
) -> dict:
    """Consulta informações do pedido."""
    pass
```

```python
def calculate_discount(
    price: float,
    customer_tier: str
) -> dict:
    """Calcula o desconto com base no nível do cliente."""
    pass
```

### ❌ Evite

```python
def lookup_order(order_id, user_id):
    pass
```

Sem as dicas de tipo, fica menos claro para o esquema da ferramenta quais valores devem ser fornecidos.

---

# 📦 Tipos de parâmetros

Prefira tipos simples e serializáveis em JSON.

### ✅ Compatíveis

```text
str
int
float
bool
list
dict
```

Exemplo:

```python
def book_flight(
    destination: str,
    departure_date: str,
    passengers: int
) -> dict:
    pass
```

### ❌ Evite tipos complexos

```python
from datetime import datetime
from custom_models import Customer


def book_flight(
    destination: str,
    departure_date: datetime,
    customer: Customer
) -> dict:
    pass
```

Objetos personalizados e tipos complexos podem dificultar a representação da ferramenta no esquema esperado pelo LLM.

---

# ⚠️ Parâmetros obrigatórios

Uma recomendação importante é **não depender de valores padrão nos parâmetros**.

### ✅ Recomendado

```python
def book_flight(
    destination: str,
    date: str,
    passengers: int
) -> dict:
    """Reserva um voo."""
    pass
```

### ⚠️ Não recomendado

```python
def search_flights(
    destination: str,
    max_price: float = 1000.0,
    class_type: str = "economy"
) -> dict:
    """Busca voos."""
    pass
```

Os valores padrão podem não ser utilizados de forma confiável pelos modelos.

Por isso, quando possível:

> **Prefira parâmetros explicitamente obrigatórios.**

---

# 📚 Docstrings são cruciais

A docstring da função funciona como uma **descrição da ferramenta para o LLM**.

Ela ajuda o modelo a entender:

* O que a ferramenta faz;
* Quando deve ser utilizada;
* Quais parâmetros recebe;
* O que retorna;
* Como interpretar possíveis erros.

---

## 📝 Estrutura recomendada

```python
def tool_name(
    param1: type1,
    param2: type2
) -> dict:
    """
    Resumo em uma linha do que a ferramenta faz.

    Contexto adicional sobre quando usar esta ferramenta.

    Argumentos:
        param1 (type1): descrição do parâmetro.
        param2 (type2): descrição do parâmetro.

    Retorna:
        dict: descrição do retorno.

        Em caso de sucesso:
        {'status': 'success', 'key': value}

        Em caso de erro:
        {'status': 'error', 'error_message': 'explanation'}
    """

    pass
```

---

# 📦 Exemplo completo de docstring

```python
def calculate_shipping_cost(
    weight_kg: float,
    country: str
) -> dict:
    """
    Calcula o custo de frete com base no peso da embalagem
    e no país de destino.

    Utilize esta ferramenta quando um cliente perguntar
    sobre os custos de frete do pedido.

    Argumentos:
        weight_kg (float): peso da embalagem em quilogramas.
        country (str): nome do país de destino.

    Retorna:
        dict: informações sobre custos de frete.

        Em caso de sucesso:
        {
            'status': 'success',
            'cost_usd': 25.50,
            'delivery_days': 5
        }

        Em caso de erro:
        {
            'status': 'error',
            'error_message': 'Sem envio para o país'
        }
    """
```

Quanto mais clara for a descrição, mais informações o LLM terá para selecionar e utilizar corretamente a ferramenta.

---

# 🔍 O que o LLM vê?

A implementação interna da função não é o único elemento relevante.

O ADK transforma os metadados da função em uma descrição estruturada.

```text
🔧 Tool: calculate_shipping_cost

Descrição:
Calcula o custo de frete com base no peso do pacote
e no país de destino.

Quando utilizar:
Quando um cliente perguntar sobre custos de frete.

Parâmetros:
├── weight_kg → float
└── country → str

Retorno:
└── dict
    ├── status
    ├── cost_usd
    └── delivery_days
```

O LLM utiliza essas informações para decidir:

* **Quando chamar** a ferramenta;
* **Quais parâmetros** fornecer;
* **O que esperar** como resultado.

---

# ⚙️ Como o ADK gera o esquema

```text
🐍 Sua função Python
        │
        ├── 🏷️ Nome
        ├── 📋 Parâmetros
        ├── 🏷️ Type hints
        ├── 📚 Docstring
        └── 📤 Tipo de retorno
        │
        ▼
🟡 Geração automática do esquema
        │
        ├── Nome da ferramenta
        ├── Descrição
        ├── Tipos dos parâmetros
        └── Saída esperada
        │
        ▼
🧠 Seleção da ferramenta pelo LLM
        │
        ▼
🔧 Chamada com os parâmetros corretos
```

### 💡 Insight

Não é necessário configurar manualmente todo o esquema da ferramenta.

O ADK utiliza os metadados da função Python para gerar essas informações automaticamente.

---

# 📤 Retornos com `status`

Uma boa prática é retornar **dicionários estruturados**.

O resultado deve indicar claramente se a operação foi bem-sucedida.

## ✅ Sucesso

```python
return {
    "status": "success",
    "data_key": value,
    "another_key": another_value
}
```

## ❌ Erro

```python
return {
    "status": "error",
    "error_message": "Explicação clara do que aconteceu."
}
```

---

# 🧠 Por que utilizar `status`?

Um status explícito ajuda o LLM a entender o resultado da operação.

```text
🔧 Ferramenta
     │
     ▼
📤 Resultado
     │
     ├── status="success"
     │       │
     │       ▼
     │   🤖 Continuar
     │
     └── status="error"
             │
             ▼
        🤖 Tratar erro
```

Isso facilita:

* 🧠 Interpretação pelo LLM;
* 🔄 Decisão da próxima ação;
* ⚠️ Tratamento de erros;
* 📊 Estruturação dos resultados;
* 💬 Geração de respostas mais confiáveis.

---

# 🧪 Exemplo: consulta de produto

```python
def lookup_product(product_id: str) -> dict:
    """
    Consulta informações do produto por ID.

    Argumentos:
        product_id (str): ID do produto a ser pesquisado.

    Retorna:
        dict: informações do produto.
    """

    products = {
        "PROD001": {
            "name": "Widget Pro",
            "price": 99.99,
            "in_stock": True
        },
        "PROD002": {
            "name": "Gadget Plus",
            "price": 149.99,
            "in_stock": False
        }
    }

    if product_id in products:
        return {
            "status": "success",
            "product_id": product_id,
            "product": products[product_id]
        }

    return {
        "status": "error",
        "error_message": (
            f"Produto {product_id} não encontrado no banco de dados."
        )
    }
```

Se o usuário perguntar:

```text
Fale sobre o produto PROD999.
```

A ferramenta pode retornar:

```python
{
    "status": "error",
    "error_message": (
        "Produto PROD999 não encontrado no banco de dados."
    )
}
```

O LLM consegue interpretar o erro e formular uma resposta adequada ao usuário, sem inventar informações sobre o produto.

---

# 🧱 Padrão recomendado

Uma estrutura consistente para ferramentas personalizadas é:

```python
def your_tool(params) -> dict:
    """
    Descrição clara da ferramenta.
    """

    # Validar entrada
    if validation_fails:
        return {
            "status": "error",
            "error_message": "Explicação clara"
        }

    # Executar operação
    try:
        result = do_something()

        return {
            "status": "success",
            "result_key": result
        }

    except Exception as e:
        return {
            "status": "error",
            "error_message": f"Operação falhou: {str(e)}"
        }
```

---

# 🧠 Estado em ferramentas personalizadas

As ferramentas personalizadas também podem acessar o **estado da sessão**.

Essa possibilidade conecta diretamente este conteúdo ao módulo sobre **memória e estado**.

```text
🤖 Agente
    │
    ▼
🛠️ Ferramenta personalizada
    │
    ▼
🧠 Session State
    │
    ├── user:
    ├── temp:
    ├── app:
    └── estado da sessão
```

> ⚠️ O uso detalhado de `tool_context` será abordado em aulas futuras.

---

## 👤 Personalização com estado

Uma ferramenta pode utilizar preferências armazenadas do usuário.

```python
def recommend_products(category: str, ctx) -> dict:
    """
    Recomenda produtos com base nas preferências
    armazenadas do usuário.
    """

    user_tier = ctx.session.state.get(
        'user:tier',
        'standard'
    )

    user_preferences = ctx.session.state.get(
        'user:preferences',
        {}
    )

    if user_tier == 'premium':
        products = get_premium_products(
            category,
            user_preferences
        )
        discount = 0.15
    else:
        products = get_standard_products(category)
        discount = 0.05

    return {
        "status": "success",
        "products": products,
        "tier": user_tier,
        "discount_applied": discount
    }
```

---

# 🗂️ Namespaces de estado

Os namespaces estudados anteriormente também podem ser utilizados pelas ferramentas.

| Namespace   | Finalidade                 |
| ----------- | -------------------------- |
| `temp:`     | Dados temporários do turno |
| Sem prefixo | Dados da sessão            |
| `user:`     | Preferências do usuário    |
| `app:`      | Configuração global        |

---

## 🔄 Exemplo de fluxo com estado

Imagine um processo de pedido dividido em várias etapas.

```text
🛒 Iniciar pedido
      │
      ▼
🧠 temp:current_order
      │
      ▼
📍 Adicionar endereço
      │
      ▼
🧠 Atualizar estado
      │
      ▼
💳 Finalizar pedido
      │
      ▼
🏢 Processar no sistema
      │
      ▼
🧹 Limpar estado temporário
```

Nesse modelo:

* Uma ferramenta grava informações;
* Outra ferramenta recupera;
* Uma terceira utiliza os dados para finalizar o processo.

Isso permite criar **workflows com estado**.

---

# 🧰 Múltiplas ferramentas trabalhando juntas

Um agente pode utilizar várias funções personalizadas.

```python
tools=[
    check_inventory,
    get_product_price,
    calculate_shipping,
    calculate_total
]
```

Cada ferramenta possui uma responsabilidade específica.

```text
📦 check_inventory
        │
        ▼
💰 get_product_price
        │
        ▼
🚚 calculate_shipping
        │
        ▼
🧮 calculate_total
```

---

## 🔄 Encadeamento de ferramentas

Imagine a pergunta:

> "Qual o custo total do produto PROD001 enviado para o Canadá?"

O agente pode executar:

```text
1️⃣ check_inventory("PROD001")
        │
        ▼
   in_stock: True

2️⃣ get_product_price("PROD001")
        │
        ▼
   price: US$ 99,99

3️⃣ calculate_shipping(weight, "Canada")
        │
        ▼
   shipping: US$ 25,50

4️⃣ calculate_total(99.99, 25.50)
        │
        ▼
   total: US$ 125,49
```

### 🧠 O que está acontecendo?

O agente realiza **orquestração de ferramentas**:

* 🔄 Chamadas sequenciais;
* 🔗 Encadeamento de resultados;
* 🧠 Seleção automática;
* 💬 Síntese dos resultados.

---

# ✈️ Exemplo prático

## Agência de viagens com ferramentas personalizadas

O projeto consiste em criar um agente capaz de:

* ✈️ Pesquisar voos;
* 🏨 Pesquisar hotéis;
* 💰 Calcular o orçamento da viagem;
* 🤖 Orquestrar múltiplas ferramentas.

---

## 01 — Criar o projeto

```bash
adk create travel_agent
cd travel_agent
```

---

## 02 — Criar as ferramentas

### ✈️ `search_flights`

```python
def search_flights(
    destination: str,
    departure_date: str
) -> dict:
    """
    Busca voos disponíveis para um destino
    em uma data específica.

    Utilize esta ferramenta quando um cliente
    quiser saber as opções de voo.

    Argumentos:
        destination (str): cidade de destino.
        departure_date (str): data no formato AAAA-MM-DD.

    Retorna:
        dict: resultados da pesquisa.
    """

    available_flights = {
        "paris": [
            {
                "flight_number": "AF123",
                "price_usd": 450,
                "duration_hours": 8
            },
            {
                "flight_number": "BA456",
                "price_usd": 480,
                "duration_hours": 7.5
            }
        ],
        "tokyo": [
            {
                "flight_number": "JL789",
                "price_usd": 850,
                "duration_hours": 13
            },
            {
                "flight_number": "ANA101",
                "price_usd": 820,
                "duration_hours": 12.5
            }
        ]
    }

    dest_key = destination.lower()

    if dest_key not in available_flights:
        return {
            "status": "error",
            "error_message": (
                f"Nenhum voo encontrado para {destination}. "
                "Tente Paris ou Tóquio."
            )
        }

    return {
        "status": "success",
        "destination": destination,
        "departure_date": departure_date,
        "flights": available_flights[dest_key],
        "count": len(available_flights[dest_key])
    }
```

---

### 🏨 `search_hotels`

```python
def search_hotels(
    city: str,
    check_in_date: str
) -> dict:
    """
    Busca hotéis disponíveis em uma cidade
    para uma data específica de check-in.
    """

    available_hotels = {
        "paris": [
            {
                "name": "Hotel Eiffel",
                "price_per_night_usd": 150,
                "rating": 4.5
            },
            {
                "name": "Louvre Inn",
                "price_per_night_usd": 120,
                "rating": 4.2
            }
        ],
        "tokyo": [
            {
                "name": "Shibuya Grand",
                "price_per_night_usd": 180,
                "rating": 4.7
            },
            {
                "name": "Tokyo Bay Hotel",
                "price_per_night_usd": 140,
                "rating": 4.3
            }
        ]
    }

    city_key = city.lower()

    if city_key not in available_hotels:
        return {
            "status": "error",
            "error_message": (
                f"Nenhum hotel encontrado em {city}. "
                "Tente Paris ou Tóquio."
            )
        }

    return {
        "status": "success",
        "city": city,
        "check_in_date": check_in_date,
        "hotels": available_hotels[city_key],
        "count": len(available_hotels[city_key])
    }
```

---

### 💰 `calculate_trip_budget`

```python
def calculate_trip_budget(
    flight_price: float,
    hotel_price: float,
    num_nights: int
) -> dict:
    """
    Calcula o orçamento total da viagem,
    incluindo voos e hospedagem.
    """

    hotel_total = hotel_price * num_nights
    total = flight_price + hotel_total

    return {
        "status": "success",
        "total_usd": round(total, 2),
        "breakdown": {
            "flight_cost": flight_price,
            "hotel_cost_per_night": hotel_price,
            "num_nights": num_nights,
            "hotel_total": round(hotel_total, 2)
        }
    }
```

---

## 03 — Criar o agente

```python
from google.adk.agents import LlmAgent


root_agent = LlmAgent(
    model='gemini-2.5-flash',
    name='travel_agent',

    description=(
        'Ajuda os usuários a planejar viagens, '
        'encontrando voos e hotéis.'
    ),

    instruction="""
    Você é um assistente de viagens prestativo.

    Suas capacidades:
    - Pesquisar voos usando search_flights
    - Pesquisar hotéis usando search_hotels
    - Calcular o orçamento usando calculate_trip_budget

    Ao ajudar os usuários:

    1. Se perguntarem sobre voos, use search_flights.
    2. Se perguntarem sobre hotéis, use search_hotels.
    3. Para uma estimativa completa, use as duas
       ferramentas de pesquisa e depois
       calculate_trip_budget.
    4. Apresente as opções claramente,
       incluindo os preços.
    5. Se uma ferramenta retornar um erro,
       peça desculpas e sugira os destinos
       disponíveis.

    Seja amigável e ajude os usuários
    a planejar a viagem.
    """,

    tools=[
        search_flights,
        search_hotels,
        calculate_trip_budget
    ]
)
```

---

# 🧪 Testando o agente

## Teste 01 — ✈️ Pesquisa de voos

**Usuário:**

```text
Quero um voo para Paris em 2025-12-15.
```

### Comportamento esperado

```text
👤 Usuário
     │
     ▼
🤖 Agente
     │
     ▼
🔧 search_flights
     │
     ▼
📋 2 opções de voo
     │
     ▼
💬 Resposta natural
```

O agente deve extrair:

```text
destination = "Paris"
departure_date = "2025-12-15"
```

e apresentar as opções disponíveis.

---

# 🧪 Teste 02 — 🌎 Planejamento completo

**Usuário:**

```text
Planeje uma viagem de 3 noites
para Tóquio a partir de 2025-12-20.
```

### Comportamento esperado

```text
1️⃣ search_flights
        │
        ▼
2️⃣ search_hotels
        │
        ▼
3️⃣ calculate_trip_budget
        │
        ▼
📋 Plano completo da viagem
```

O agente deve combinar os resultados e apresentar uma estimativa final.

### 🧠 Insight

Esse cenário demonstra que **múltiplas ferramentas podem trabalhar em conjunto**.

---

# 🧪 Teste 03 — ⚠️ Tratamento de erros

**Usuário:**

```text
Encontre hotéis em Londres.
```

A ferramenta retorna:

```python
{
    "status": "error",
    "error_message": (
        "Nenhum hotel encontrado em Londres. "
        "Tente Paris ou Tóquio."
    )
}
```

O agente deve:

* ❌ Não inventar hotéis;
* 🙏 Pedir desculpas;
* 💡 Sugerir destinos disponíveis;
* 💬 Manter um tom profissional.

Esse comportamento demonstra a importância de fornecer **erros estruturados e compreensíveis para o LLM**.

---

# 🧪 Teste 04 — 🧮 Apenas cálculo

**Usuário:**

```text
Qual é o custo total de um voo de US$ 450
e um hotel de US$ 150 por noite por 4 noites?
```

O agente deve utilizar diretamente:

```text
calculate_trip_budget(
    flight_price=450,
    hotel_price=150,
    num_nights=4
)
```

Resultado:

```text
✈️ Voo: US$ 450
🏨 Hotel: 4 × US$ 150 = US$ 600

💰 Total: US$ 1.050
```

### 💡 Insight

O agente não precisa chamar ferramentas de pesquisa quando a informação necessária já foi fornecida pelo usuário.

Isso demonstra uma **seleção de ferramentas orientada pela necessidade**.

---

# 🧠 Principais aprendizados

## 🛠️ Ferramentas de função

* 🐍 São implementadas como funções Python;
* 🔌 Podem integrar sistemas próprios;
* ⚙️ Permitem controle total da lógica;
* 🧩 São automaticamente encapsuladas pelo ADK como `FunctionTool`.

## 📝 Metadados importantes

Uma ferramenta bem definida deve possuir:

```text
🏷️ Nome descritivo
       +
📋 Parâmetros tipados
       +
📚 Docstring clara
       +
📤 Retorno estruturado
```

## 📤 Retornos

Prefira:

```python
{
    "status": "success",
    ...
}
```

ou:

```python
{
    "status": "error",
    "error_message": "..."
}
```

## 🤖 Orquestração

Um agente pode:

* Selecionar ferramentas;
* Executá-las em sequência;
* Utilizar resultados anteriores;
* Combinar diferentes resultados;
* Produzir uma resposta natural.

---

# 🧭 Quando usar ferramentas personalizadas?

Ferramentas de função personalizadas são especialmente úteis para:

| Necessidade             | Exemplo                                   |
| ----------------------- | ----------------------------------------- |
| 💰 Cálculo específico   | Frete, descontos, impostos                |
| 🗄️ Banco próprio       | Pedidos, estoque, clientes                |
| 🔌 API interna          | Serviços corporativos                     |
| 📋 Regra de negócio     | Precificação, reservas                    |
| 🏢 Sistema proprietário | Aplicações internas                       |
| ⚙️ Lógica exclusiva     | Funcionalidades específicas do aplicativo |

---

# ⚖️ Ferramentas integradas x personalizadas

| Aspecto      | Integradas              | Função personalizada          |
| ------------ | ----------------------- | ----------------------------- |
| Configuração | Importar e usar         | Escrever a função             |
| Manutenção   | Equipe do ADK           | Desenvolvedor                 |
| Customização | Limitada                | Controle total                |
| Integração   | Recursos comuns         | Sistemas e regras específicas |
| Uso ideal    | Necessidades universais | Lógica de negócio             |

---

# 🔄 Visão geral da evolução

```text
🧠 MODELO
    │
    ▼
🧰 Ferramentas integradas
    │
    │ Necessidades comuns
    ▼
🔗 Ferramentas MCP
    │
    │ Recursos externos existentes
    ▼
🛠️ Ferramentas personalizadas
    │
    │ Lógica própria
    ▼
🏢 SISTEMAS DO NEGÓCIO
```

A ideia não é escolher uma única abordagem para tudo.

O objetivo é utilizar **a ferramenta mais adequada para cada necessidade**.

---

# 🧠 Insight principal

As ferramentas de função personalizadas representam o ponto em que o agente deixa de depender apenas de capacidades genéricas e passa a incorporar **conhecimento operacional específico do negócio**.

```text
🐍 Código Python
      │
      ▼
🧩 FunctionTool
      │
      ▼
🤖 Agente
      │
      ▼
🏢 Lógica do negócio
      │
      ├── 📦 Produtos
      ├── 💰 Preços
      ├── 🗄️ Dados
      ├── 📋 Regras
      └── 🔌 Sistemas
```

> **O LLM decide quando utilizar a ferramenta; a função Python executa a lógica necessária.**

---

# 🗂️ Organização dos estudos

Esta etapa corresponde à solução para o problema das **ferramentas genéricas versus necessidades específicas de negócio**.

```text
📚 Módulo 5
│
├── 01 — O problema: agentes limitados pelos dados de treinamento
│
├── 02 — A solução: ferramentas integradas
│
├── 03 — Teste do módulo
│
├── 04 — O problema: reproduzir habilidades comuns
│
├── 05 — A solução: ferramentas integradas
│
├── 06 — A solução: Protocolo de Contexto de Modelo (MCP)
│
├── 07 — Teste do módulo
│
├── 08 — O problema: ferramentas genéricas
│
├── 09 — 🛠️ A solução: ferramentas de função personalizadas
│
└── ...
```

### 📌 Conceitos-chave

```text
🛠️ Function Tools
│
├── 🐍 Funções Python
├── 🏷️ Nomes descritivos
├── 📋 Type hints
├── 📚 Docstrings
├── 📤 Retorno com status
├── 🧠 Integração com estado
├── 🔄 Múltiplas ferramentas
└── 🤖 Orquestração pelo agente
```

---

# 🚀 Próxima etapa

Depois de aprender a criar ferramentas personalizadas, o próximo desafio é compreender **como controlar e orientar essas ferramentas de maneira segura e eficiente**.

A evolução continua:

```text
🧰 Ferramentas integradas
        │
        ▼
🔗 MCP
        │
        ▼
🛠️ Funções personalizadas
        │
        ▼
🧠 Orientação estratégica
        │
        ▼
🔐 Agentes mais seguros e confiáveis
```

O próximo passo será aprofundar o uso de **instruções estratégicas**, permitindo orientar o agente sobre **quando, como e com quais restrições** suas ferramentas devem ser utilizadas.

---

<p align="center">
  <strong>🛠️ Funções personalizadas transformam código Python em capacidades agênticas.</strong>
</p>

<p align="center">
  <strong>Do recurso genérico para a lógica específica do negócio.</strong>
</p>
