## 📦 Saídas Estruturadas com `output_schema`

### O Problema: respostas imprevissíveis interrompem as integrações

### 🎯 Do texto aos dados estruturados

Nos módulos anteriores, os agentes retornavam informações em **texto livre**. Embora esse formato seja fácil de compreender para pessoas, ele apresenta limitações quando a resposta precisa ser utilizada por sistemas.

Exemplo:

```python
agent = LlmAgent(
    model="gemini-2.5-flash",
    instruction="Extrair informações do produto das mensagens dos usuários"
)
```

Para uma entrada como:

> "Eu quero o iPhone 15 Pro com 256 GB"

O agente poderia responder:

> "O usuário tem interesse em um iPhone 15 Pro com armazenamento de 256 GB."

Apesar de correta para um leitor humano, essa resposta não possui uma estrutura confiável para ser processada automaticamente.

---

### ⚠️ Problema: respostas em formato livre

Quando um agente retorna texto sem um esquema definido, podem ocorrer:

* ❌ **Formato inconsistente** — cada resposta pode apresentar uma estrutura diferente
* ❌ **Dificuldade de análise** — exige processamento adicional do texto
* ❌ **Ausência de validação** — campos importantes podem ser omitidos
* ❌ **Integrações frágeis** — bancos de dados e APIs precisam de dados estruturados

Por exemplo, uma mesma informação pode ser retornada de diferentes maneiras:

```text
Produto: iPhone 15 Pro, preço: US$ 999, armazenamento: 256 GB
```

```text
O iPhone 15 Pro custa US$ 999 e possui 256 GB de armazenamento.
```

```text
iPhone 15 Pro - US$ 999 - 256 GB
```

Para um ser humano, as três respostas são compreensíveis. Para um sistema, entretanto, **não existe garantia de que o formato será sempre o mesmo**.

---

### 💡 Solução: `output_schema`

O **ADK** disponibiliza o parâmetro `output_schema` para definir uma estrutura esperada para a saída do agente.

Em vez de solicitar apenas:

```text
"Extraia nome, preço e armazenamento."
```

é possível definir explicitamente **quais campos devem ser retornados e qual estrutura eles devem seguir**.

O resultado esperado passa a ser um objeto estruturado, por exemplo:

```json
{
  "produto": "iPhone 15 Pro",
  "preco": 999,
  "armazenamento": "256 GB"
}
```

---

### 🔗 Por que utilizar dados estruturados?

O uso de um esquema de saída permite que o resultado do agente seja:

**LLM → Dados estruturados → Aplicação → Banco de dados/API**

Isso facilita:

* 🔄 Integração entre sistemas
* 📊 Processamento automático
* ✅ Validação dos dados
* 🗄️ Armazenamento em bancos de dados
* 🔌 Consumo por APIs e aplicações
* 🛡️ Redução de erros causados por formatos imprevisíveis

---

### 🧠 Conceito-chave

> **Texto livre é otimizado para comunicação humana; dados estruturados são essenciais quando a resposta precisa ser consumida por sistemas.**

O `output_schema` transforma a saída do agente em um **contrato estruturado entre o LLM e a aplicação**, tornando as respostas mais previsíveis e fáceis de integrar.
