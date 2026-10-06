# 07. Como Implantar no Cloud Run

## 🎯 Visão Geral (Cloud Run vs. Agent Engine)

Enquanto o **Vertex AI Agent Engine** é o caminho mais simples e padrão para agentes do ADK, o **Cloud Run** surge como uma alternativa flexível baseada em contêineres serverless.

| Fator | Vertex AI Agent Engine | Cloud Run |
| :--- | :--- | :--- |
| **Facilidade de uso** | Mais fácil (um comando)| Moderada |
| **Serviço de sessão** | Automático| Configuração manual |
| **Interface da Web** | Apenas no Console do Cloud | Pode incluir interface gráfica nativa (`--with_ui`) |
| **Ideal para** | Agentes padrão do ADK| Necessidades personalizadas e implantação de UI |

---

## 💡 Regra de Decisão

> **A recomendação padrão é usar o Agent Engine.** 
> 
> Use o **Cloud Run** quando precisar de:
> * Interface da Web implantada junto com o agente (`--with_ui`).
> * Configuração e dependências de contêiner customizadas.
> * Reaproveitar infraestrutura existente no Cloud Run.

---

## 💻 Comando de Implantação

```bash
adk deploy cloud_run \
  --project=$GOOGLE_CLOUD_PROJECT \
  --region=$GOOGLE_CLOUD_LOCATION \
  --service_name=meu-agente \
  --with_ui \
  /caminho/para/o/agente

```

### 📋 Parâmetros Utilizados

* `--project`: ID do seu projeto no Google Cloud.


* `--region`: Região de implantação (ex: `us-central1`).


* `--service_name`: Nome que identificará o serviço no Cloud Run.


* `--with_ui`: Flag opcional que inclui uma interface web interativa pronta para uso.


* `/caminho/para/o/agente`: Diretório contendo os arquivos do seu agente.

---

## ⚡ O que Acontece Durante o Deploy (Duração: 5 a 8 min)

1. O ADK empacota o código do agente.


2. Gera automaticamente a imagem do contêiner Docker.


3. Realiza o deploy e provisionamento no Cloud Run.


4. Retorna uma URL HTTPS pública para acesso imediato ao agente.
---