## 🧩 Saídas Estruturadas com Pydantic e `output_schema`

### A solução: saída estruturada com Pydantic

### 🎯 Objetivo

Aprender a transformar respostas livres de agentes LLM em **dados estruturados e previsíveis**, utilizando **Pydantic `BaseModel`** e o parâmetro `output_schema` do ADK.

A estruturação permite que os resultados dos agentes sejam utilizados de forma confiável por aplicações, APIs, bancos de dados e outros agentes em um fluxo multiagente.

---

### 🧠 Pydantic + `output_schema`

O **Pydantic** permite definir exatamente quais campos devem existir na resposta do agente, seus respectivos tipos e descrições.

```python
from pydantic import BaseModel, Field

class ProductInfo(BaseModel):
    product_name: str = Field(description="O nome do produto")
    price: float = Field(description="O preço em USD")
    storage: str = Field(description="A capacidade de armazenamento")
```

O modelo é então associado ao agente por meio do `output_schema`:

```python
structured_agent = LlmAgent(
    model="gemini-2.5-flash",
    instruction="Extrair informações do produto e responder com JSON.",
    output_schema=ProductInfo
)
```

O `output_schema` funciona como um **contrato de saída**, garantindo que a resposta siga a estrutura definida pelo modelo Pydantic.

### 📌 Regras importantes

* O esquema deve herdar de `BaseModel`.
* Cada campo deve possuir um tipo (`str`, `int`, `float`, `bool` etc.).
* `Field(description=...)` ajuda o LLM a compreender o significado de cada campo.
* Deve ser utilizada a **classe** no `output_schema`, e não uma instância.
* Dicionários ou classes Python comuns não substituem um `BaseModel`.

```python
# ✅ Correto
output_schema=ProductInfo

# ❌ Incorreto
output_schema={"product_name": "string"}
```

---

### 🔄 `output_schema` x resposta livre

Sem um esquema, o mesmo dado pode ser retornado em diferentes formatos:

```text
Produto: iPhone 15 Pro, preço: US$ 999, armazenamento: 256 GB
```

ou:

```text
O iPhone 15 Pro custa US$ 999 e possui 256 GB.
```

ou:

```text
iPhone 15 Pro - US$ 999 - 256 GB
```

Com `output_schema`, a aplicação passa a receber uma estrutura previsível:

```json
{
  "product_name": "iPhone 15 Pro",
  "price": 999.0,
  "storage": "256GB"
}
```

**Ideia central:**

> Texto livre é otimizado para comunicação com pessoas; dados estruturados são otimizados para integração com sistemas.

---

### 💾 Armazenando resultados com `output_key`

O parâmetro `output_key` permite salvar automaticamente a resposta no estado da sessão:

```python
structured_agent = LlmAgent(
    model="gemini-2.5-flash",
    instruction="Extrair a capital como JSON",
    output_schema=CapitalOutput,
    output_key="found_capital"
)
```

O resultado fica disponível em:

```python
session.state["found_capital"]
```

Isso é especialmente útil para:

* 🔄 Compartilhar dados entre agentes
* 💾 Armazenar informações extraídas
* 🔗 Conectar diferentes etapas de um workflow
* 🤖 Construir pipelines multiagente

---

### 🤖 Saída estruturada em sistemas multiagente

O `output_schema` não precisa estar somente no `root_agent`.

Subagentes também podem produzir dados estruturados para serem utilizados por outros agentes:

```python
extraction_agent = LlmAgent(
    model="gemini-2.5-flash",
    name="data_extractor",
    output_schema=ProductInfo,
    output_key="extracted_data"
)

analysis_agent = LlmAgent(
    model="gemini-2.5-flash",
    name="data_analyzer"
)
```

Nesse cenário:

```text
Usuário
   ↓
Extraction Agent
   ↓
Dados estruturados
   ↓
Session State
   ↓
Analysis Agent
   ↓
Resultado
```

A estrutura consistente reduz problemas de interpretação quando os dados são transferidos entre diferentes agentes.

---

### 🧱 Esquemas complexos

O Pydantic permite representar estruturas mais sofisticadas:

```python
from pydantic import BaseModel, Field
from typing import List, Optional

class ProductDetails(BaseModel):
    name: str = Field(description="Nome do produto")
    price: float = Field(description="Preço em USD")
    storage_options: List[str] = Field(
        description="Capacidades de armazenamento disponíveis"
    )
    in_stock: bool = Field(
        description="Se o produto está em estoque"
    )
    discount: Optional[float] = Field(
        default=None,
        description="Percentual de desconto, se houver"
    )
```

Tipos utilizados:

| Tipo      | Exemplo                       |
| --------- | ----------------------------- |
| Básicos   | `str`, `int`, `float`, `bool` |
| Coleções  | `List[T]`, `Dict[str, T]`     |
| Opcionais | `Optional[T]`                 |
| Aninhados | Outros `BaseModel`            |

---

### 📐 Integridade do esquema

O esquema define a **estrutura exata da resposta**.

Se determinado campo não estiver definido no `BaseModel`, ele não faz parte da estrutura esperada.

Por exemplo:

```python
class ApiResponse(BaseModel):
    status: str
    status_code: int
    data: dict
    metadata: dict
    errors: list[str] = []
```

Nesse caso, `status`, `status_code`, `data`, `metadata` e `errors` fazem parte do contrato de saída.

Isso permite representar estruturas complexas como:

```text
API Response
├── status
├── status_code
├── data
├── metadata
└── errors
```

**O schema funciona como um contrato:** define quais dados devem existir e como eles devem ser organizados.

---

## 🛠️ Exemplo prático — Product Extractor

### 1. Criando o projeto

```bash
adk create product_extractor
cd product_extractor
```

### 2. Definindo o schema

```python
from pydantic import BaseModel, Field

class ProductInfo(BaseModel):
    product_name: str = Field(
        description="O nome completo do produto"
    )
    price: float = Field(
        description="O preço em USD"
    )
    storage: str = Field(
        description="Capacidade de armazenamento"
    )
    color: str = Field(
        default="Não especificado",
        description="Cor do produto, se mencionada"
    )
```

### 3. Criando o agente

```python
from google.adk.agents import LlmAgent

root_agent = LlmAgent(
    model="gemini-2.5-flash",
    name="product_extractor",
    description="Extrai informações de produtos e retorna JSON estruturado",
    instruction="""
Você é um extrator de informações de produtos.

Sua tarefa:
- Ler a mensagem do usuário.
- Extrair product_name, price, storage e color.
- Retornar apenas JSON válido.

Regras:
- price deve ser um número.
- storage deve incluir a unidade (GB ou TB).
- Se a cor não for mencionada, utilizar "Não especificado".
- Não adicionar texto explicativo.
""",
    output_schema=ProductInfo,
    output_key="extracted_product"
)
```

### 4. Executando o agente

```bash
adk web
```

O agente pode ser testado com diferentes formatos de entrada.

**Entrada:**

```text
Eu quero o iPhone 15 Pro com 256 GB em Space Black por US$ 999
```

**Saída:**

```json
{
  "product_name": "iPhone 15 Pro",
  "price": 999.0,
  "storage": "256GB",
  "color": "Space Black"
}
```

Outro exemplo:

```text
Samsung Galaxy S24 com 512 GB, valor US$ 1.199
```

Resultado:

```json
{
  "product_name": "Samsung Galaxy S24",
  "price": 1199.0,
  "storage": "512GB",
  "color": "Não especificado"
}
```

---

### 🧪 Resultados observados

A utilização de `output_schema` proporciona:

* ✅ JSON estruturado
* ✅ Mesma estrutura entre respostas
* ✅ Tipos de dados definidos
* ✅ Valores padrão para campos opcionais
* ✅ Maior facilidade de parsing
* ✅ Integração simplificada com APIs e bancos de dados
* ✅ Compartilhamento consistente entre agentes

---

### 💡 Principais aprendizados

1. **`output_schema`** permite definir uma estrutura de saída previsível para agentes ADK.
2. **Pydantic `BaseModel`** é utilizado para representar o schema da resposta.
3. O `output_schema` recebe a **classe Pydantic**, e não uma instância.
4. **`Field(description=...)`** fornece contexto adicional para os campos.
5. **`output_key`** permite armazenar a resposta no estado da sessão.
6. Schemas estruturados também podem ser utilizados por **subagentes** em workflows multiagente.
7. O schema funciona como um **contrato entre o agente e a aplicação**.
8. Estruturas complexas podem ser representadas utilizando listas, opcionais, dicionários e modelos Pydantic aninhados.

### 🔗 Conceitos-chave

`Pydantic` · `BaseModel` · `Field` · `output_schema` · `output_key` · `JSON` · `Structured Output` · `Session State` · `Multi-Agent Workflow` · `LlmAgent`
