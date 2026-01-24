````md
# 🚀 MeddiFlux Systems — Modernização da Arquitetura AWS

![AWS](https://img.shields.io/badge/AWS-Cloud-%23FF9900.svg?style=for-the-badge&logo=amazonaws&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-IaC-%237B42BC.svg?style=for-the-badge&logo=terraform&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Containers-%232496ED.svg?style=for-the-badge&logo=docker&logoColor=white)
![ECS](https://img.shields.io/badge/Amazon%20ECS-Fargate-%23FF9900.svg?style=for-the-badge&logo=amazonecs&logoColor=white)
![ECR](https://img.shields.io/badge/Amazon%20ECR-Registry-%23232F3E.svg?style=for-the-badge&logo=amazonaws&logoColor=white)
![S3](https://img.shields.io/badge/Amazon%20S3-Storage-%23569A31.svg?style=for-the-badge&logo=amazons3&logoColor=white)
![IAM](https://img.shields.io/badge/AWS%20IAM-Security-%23DD344C.svg?style=for-the-badge&logo=amazoniam&logoColor=white)
![CloudWatch](https://img.shields.io/badge/CloudWatch-Logs%2FMetrics-%23FF4F8B.svg?style=for-the-badge&logo=amazoncloudwatch&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)

---

## 📌 Visão Geral

Este repositório documenta a **modernização da arquitetura AWS da MeddiFlux Systems**, aplicando **Cloud/DevOps, Segurança (Security by Design) e FinOps**, com foco em:

- 💸 Redução de custos operacionais
- ⚙️ Escalabilidade, automação e eficiência
- 🔐 Segurança, governança e mitigação de riscos
- 🎓 Aprendizado prático com arquitetura baseada em cenário real

A iniciativa é voltada para **uso acadêmico e profissional**, com documentação objetiva, evidências técnicas e racional arquitetural claro.

---

## 🎯 Objetivos do Projeto

- Modernizar a arquitetura legada para **containers em ECS Fargate**
- Implementar **Infraestrutura como Código (Terraform)**
- Automatizar **CI/CD por ambiente (DEV, HOM, PROD)**
- Garantir **segurança por padrão** (Least Privilege, Secrets, auditoria)
- Aplicar **FinOps** para controle e otimização de custos
- Manter um **roadmap evolutivo, rastreável e explicável**

---

## 🧩 Visão Geral da Arquitetura

### Ambientes isolados

- **DEV:** desenvolvimento contínuo e testes
- **HOM:** validação funcional (uso controlado – 220h/mês)
- **PROD:** alta disponibilidade, escalabilidade e segurança reforçada

### Componentes principais

- **VPC + Subnets + Security Groups:** isolamento de rede por ambiente
- **ECS Fargate:** execução de containers sem gestão de servidores
- **ECR:** versionamento e armazenamento de imagens Docker
- **ALB:** balanceamento de carga para as aplicações
- **RDS Multi-AZ:** persistência de dados com alta disponibilidade
- **S3 (Infra & Conteúdo):**
  - armazenamento de artefatos (ex.: frontend estático, evidências, exports)
  - suporte a estados/artefatos de infraestrutura quando aplicável
- **CloudFront + S3 (conteúdo estático):** cache e distribuição global (quando usado)
- **CloudWatch + CloudTrail:** observabilidade, auditoria e rastreabilidade

---

## 🏗️ Stack Tecnológica

| Categoria              | Tecnologia                                |
|------------------------|-------------------------------------------|
| Cloud                  | AWS                                       |
| Containers             | Docker                                    |
| Orquestração           | ECS Fargate                               |
| Registry               | Amazon ECR                                |
| Storage (Infra/Assets) | Amazon S3                                 |
| Infra como Código      | Terraform                                 |
| CI/CD                  | GitHub Actions                            |
| Observabilidade        | CloudWatch                                |
| Auditoria              | CloudTrail                                |
| Segurança              | IAM, Secrets Manager                      |
| CDN                    | CloudFront (quando aplicável)             |
| Banco de Dados         | RDS (PostgreSQL / SQL Server)             |

---

## 📁 Estrutura do Repositório

```txt
meddiflux-aws-modernization/
│
├── app/
│   ├── backend/              # Backend + Dockerfile
│   └── frontend/             # Frontend + Dockerfile (ou build estático)
│
├── infra/
│   └── terraform/
│       ├── modules/          # Módulos reutilizáveis (network, iam, ecs, ecr, s3, observability, etc.)
│       └── envs/             # DEV / HOM / PROD (main.tf, variables.tf, outputs.tf, tfvars)
│
├── cicd/
│   └── github-actions/
│       └── workflows/        # Pipelines CI/CD por ambiente
│
├── docs/
│   └── evidences/            # Prints, logs, outputs, evidências de execução
│
├── README.md
└── LICENSE
````

---

## 🌿 Estratégia de Branches (Git Flow)

| Branch    | Objetivo                     |
| --------- | ---------------------------- |
| `dev`     | Integração contínua e testes |
| `homolog` | Validação funcional          |
| `master`  | Produção com governança      |

🔁 **Promoção controlada:** `dev → homolog → master`

---

## 🔁 Workflow Operacional (Resumo)

1. Desenvolvedor realiza `git push` na branch do ambiente
2. Pipeline CI/CD é acionada (GitHub Actions)
3. Build da imagem Docker
4. Push da imagem para o **ECR**
5. Deploy automatizado no **ECS Fargate**
6. Logs e métricas no **CloudWatch**

---

## 🔐 Segurança e Governança

* IAM com **Least Privilege**
* Segredos no **AWS Secrets Manager**
* ❌ Eliminação de Bastion Host (acesso controlado e rastreável)
* Deploy/migrações **somente via pipeline**
* Auditoria e trilha de eventos com **CloudTrail**
* Ambientes isolados por **VPC**

---

## 💰 FinOps e Otimização de Custos

### Estratégias aplicadas

* Right sizing de recursos
* Auto Scaling sob demanda (quando aplicável)
* DEV e HOM com uso controlado e rastreável
* Avaliação de Savings Plans / Reserved Instances (para PROD)

📉 **Resultado esperado:** redução significativa de custos com ganho de eficiência operacional.

---

## 🗺️ Roadmap de Implementação

### 🟦 Fase 1 — Fundação (Semanas 1–2)

* VPC DEV
* IAM
* ECR
* S3 base (infra/artefatos, quando aplicável)
* ECS Fargate DEV
* Terraform versionado

### 🟩 Fase 2 — Automação (Semanas 3–4)

* CI/CD DEV
* Ambiente HOM
* Promoção controlada

### 🟥 Fase 3 — Produção (Semanas 5–6)

* ECS PROD
* Auto Scaling
* RDS Multi-AZ
* ALB + (CloudFront quando aplicável)

### 🟨 Fase 4 — Testes (Semana 7)

* Testes de carga
* Failover
* Segurança

### 🟪 Fase 5 — Go-live (Semana 8)

* Corte de DNS
* Monitoramento ativo
* Desligamento do legado

---

## 📊 Evidências Técnicas

As evidências ficam em:

```txt
docs/evidences/
```

Incluem:

* Prints da VPC e recursos criados
* ECR com imagens versionadas
* ECS em execução
* Logs/Métricas no CloudWatch
* Pipelines CI/CD
* Outputs do Terraform

---

## 🎓 Contexto Acadêmico

Projeto desenvolvido como:

* Laboratório prático de **Arquitetura em Nuvem**
* Exercício de **DevOps e Automação**
* Estudo aplicado de **FinOps**
* Material de apresentação para **grupo e professor**

---

## ✅ Conclusão

A modernização proposta entrega:

* 💸 Redução de custos
* ⚙️ Eficiência operacional
* 🔐 Segurança e governança
* 🎓 Aprendizado estruturado
* 🏗️ Arquitetura alinhada a práticas de mercado

