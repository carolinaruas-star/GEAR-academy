# 🤖 Sistemas Multiagentes e Implantação com ADK

Curso da **GEAR Academy** sobre a criação de sistemas multiagentes utilizando o **Agent Development Kit (ADK)** do Google e a infraestrutura do **Google Cloud**.

O curso aborda desde a arquitetura e orquestração de múltiplos agentes até a implantação e o gerenciamento de agentes de IA em ambientes de produção.

---

## 🎯 Objetivo

Conhecer a arquitetura e a implantação de **sistemas multiagentes com o ADK**, aprendendo a:

* 🌳 Projetar estruturas hierárquicas de agentes;
* 🤖 Trabalhar com agentes baseados em LLM;
* ⚙️ Utilizar agentes de fluxo de trabalho;
* 🔢 Criar fluxos sequenciais;
* 🔄 Trabalhar com processos iterativos;
* ⚡ Executar agentes em paralelo;
* 🛠️ Criar fluxos de trabalho personalizados;
* ☁️ Escolher ambientes adequados para hospedagem;
* 🔐 Aplicar conceitos de segurança e controle de acesso;
* 📊 Monitorar agentes em produção;
* 📈 Preparar agentes para ambientes escaláveis e confiáveis.

---

## 📚 Conteúdo

### 1. Criar sistemas multiagentes com o ADK

Introdução à arquitetura de sistemas multiagentes e à organização de agentes em uma estrutura hierárquica.

Principais conceitos:

* 🌳 Estrutura pai/mãe e subagentes;
* 🔀 Transferência entre agentes;
* 🤖 Agentes baseados em LLM;
* ⚙️ Agentes de fluxo de trabalho;
* 🔢 `SequentialAgent`;
* 🔄 `LoopAgent`;
* ⚡ `ParallelAgent`;
* 🛠️ Agentes de fluxo de trabalho personalizados.

A estrutura hierárquica permite controlar como os agentes se comunicam e realizam transferências, tornando o sistema mais previsível e confiável.

---

### 2. Como implantar e gerenciar agentes de IA em produção

Estudo das principais opções de infraestrutura e dos recursos necessários para levar agentes de IA para ambientes de produção.

#### ☁️ Opções de infraestrutura

* **Vertex AI Agent Engine** — ambiente gerenciado para agentes desenvolvidos com ADK;
* **Cloud Run** — execução serverless baseada em contêineres;
* **Google Kubernetes Engine (GKE)** — orquestração de aplicações complexas e de alto desempenho;
* **App Engine** — plataforma serverless para aplicações web;
* **Compute Engine** — máquinas virtuais com maior nível de personalização.

#### 🔐 Segurança

* Identity and Access Management (**IAM**);
* **VPC Service Controls**;
* Contas de serviço e credenciais com escopo;
* Princípio do menor privilégio;
* Proteção contra acesso e exfiltração não autorizada de dados.

#### 📊 Monitoramento

* **Cloud Logging** — geração e análise de registros;
* **Cloud Trace** — rastreamento e análise de latência;
* **Cloud Monitoring** — acompanhamento de métricas operacionais;
* Métricas específicas para avaliar o desempenho dos agentes.

#### 🔄 Ciclo de vida

* Controle de versões;
* Separação de ambientes;
* Atualizações;
* Reversões para versões estáveis;
* Gerenciamento contínuo dos agentes em produção.

---

## 📝 Avaliação

O curso possui uma **verificação obrigatória de conhecimentos**.

### Teste

Conteúdos avaliados:

* Agentes de fluxo de trabalho;
* `LoopAgent`;
* Segurança em ambientes de produção;
* `VPC Service Controls`.

**Nota mínima para aprovação:** 50%.

---

## 🏆 Conclusão

Ao concluir este curso, foram desenvolvidos conhecimentos sobre o ciclo completo de sistemas multiagentes, desde a **arquitetura e orquestração dos agentes** até sua **implantação, segurança, monitoramento e gerenciamento em produção**.

> 💡 **Principal aprendizado:** agentes de IA prontos para produção precisam ser não apenas inteligentes, mas também **seguros, escaláveis, observáveis e confiáveis**.

---

## 🔗 Conteúdos do curso

* [🎥 Criar sistemas multiagentes com o ADK](https://www.skills.google/paths/3802/course_sessions/45241014/video/637477)
* [📖 Como implantar e gerenciar agentes de IA em produção](https://www.skills.google/paths/3802/course_sessions/45241014/documents/637478)
* [📝 Teste](https://www.skills.google/paths/3802/course_sessions/45241014/quizzes/637479)

---

## 📂 Estrutura

GEAR-academy/
│
├── 01-introdução-aos agentes-e-ao-ecossistema-google/
├── 02-desenvolvimento-de-agentes-com-ADK/
├── 03-implantar-agentes-prontos-producao/
│   ├── 01-criacao-e-implantacao/
│   │   ├── 01-sistemas-multiagentes-com-adk.md
│   │   ├── 02-agentes-de-IA-em-producao.md
│   │   └── 03-badge-conclusao.md
│   ├── 02-primeiro-agente/
│   ├── 03-arquiteturas-multiagentes/
│   ├── 04-implantar-agentes-prontos/
│   └── README.md
└── README.md
```

> 📚 **GEAR Academy** — Estudos sobre desenvolvimento, arquitetura e implantação de agentes de IA com tecnologias do Google Cloud.
