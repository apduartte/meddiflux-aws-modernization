# 🚀 MeddiFlux Systems — Modernização da Arquitetura AWS

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?logo=amazonaws&logoColor=white)*
![Docker](https://img.shields.io/badge/Docker-Container-2496ED?logo=docker&logoColor=white)*
![ECS](https://img.shields.io/badge/ECS-Containers-blue?logo=amazonecs&logoColor=white) *
![ECR](https://img.shields.io/badge/ECR-Registry-blue?logo=amazonaws&logoColor=white)*
![IAM](https://img.shields.io/badge/IAM-Security-black?logo=amazonaws&logoColor=white) *
![CloudWatch](https://img.shields.io/badge/CloudWatch-Logs%2FMetrics-orange?logo=amazoncloudwatch&logoColor=white)*

## 📌 Visão Geral

Este projeto tem como objetivo **modernizar a infraestrutura AWS da MeddiFlux Systems**, aplicando **boas práticas de Cloud, DevOps, Segurança e FinOps**, com foco em:

- 💸 Redução de custos operacionais  
- ⚙️ Escalabilidade, automação e eficiência  
- 🔐 Segurança, governança e mitigação de riscos  
- 🎓 Aprendizado prático com arquitetura real de mercado  

A iniciativa foi estruturada para **uso acadêmico e profissional**, com documentação clara, evidências técnicas e racional arquitetural sólido.
# Document Heading 
---

## 🎯 Objetivos do Projeto

** Modernizar a arquitetura legada para **containers em ECS Fargate**
** Implementar **Infraestrutura como Código (Terraform)**
** Automatizar **CI/CD por ambiente (DEV, HOM, PROD)**
** Garantir **segurança por padrão (Security by Design)**
* *Aplicar **FinOps** para redução e controle de custos
* *Criar um **roadmap evolutivo e explicável**

---

## 🧩 Visão Geral da Arquitetura

### Ambientes Isolados

* **DEV:** desenvolvimento contínuo e testes
* **HOM:** validação funcional (uso controlado – 220h/mês)
* **PROD:** alta disponibilidade, escalabilidade e segurança reforçada

### Componentes Principais

* **ECS Fargate:** execução de containers sem gerenciamento de servidores
* **ECR:** versionamento e armazenamento de imagens Docker
* **ALB:** balanceamento de carga
* **RDS Multi-AZ:** persistência de dados com alta disponibilidade
* **CloudFront + S3:** cache e distribuição de conteúdo
* **CloudWatch + CloudTrail:** observabilidade e auditoria

---

## 🏗️ Stack Tecnológica

| Categoria         | Tecnologia                    |
| ----------------- | ----------------------------- |
| Cloud             | AWS                           |
| Containers        | Docker                        |
| Orquestração      | ECS Fargate                   |
| Registry          | Amazon ECR                    |
| Infra como Código | Terraform                     |
| CI/CD             | GitHub Actions                |
| Observabilidade   | CloudWatch                    |
| Segurança         | IAM, Secrets Manager          |
| CDN               | CloudFront                    |
| Banco de Dados    | RDS (PostgreSQL / SQL Server) |

---

## 📁 Estrutura do Repositório

```
meddiflux-aws-modernization/
│
├── app/
│   ├── backend/        # Backend + Dockerfile
│   └── frontend/       # Frontend + Dockerfile
│
├── infra/
│   └── terraform/
│       ├── modules/    # Módulos reutilizáveis
│       └── envs/       # DEV / HOM / PROD
│
├── cicd/
│   └── github-actions/
│       └── workflows/ # Pipelines CI/CD
│
├── docs/
│   └── evidences/      # Prints, logs, outputs
│
├── README.md
└── LICENSE
```

---

## 🌿 Estratégia de Branches (Git Flow)

| Branch    | Objetivo                     |
| --------- | ---------------------------- |
| `dev`     | Integração contínua e testes |
| `homolog` | Validação funcional          |
| `master`  | Produção com governança      |

🔁 **Promoção controlada:**
`dev → homolog → master`

---

## 🔁 Workflow Operacional (Resumo)

1. Desenvolvedor realiza `git push`
2. Pipeline CI/CD é acionada
3. Build da imagem Docker
4. Push da imagem no ECR
5. Deploy automático no ECS Fargate
6. Logs e métricas no CloudWatch

---

## 🔐 Segurança e Governança

* IAM com **Least Privilege**
* Secrets no **AWS Secrets Manager**
* ❌ Eliminação de Bastion Host
* Deploy e migrações **somente via pipeline**
* Auditoria completa com **CloudTrail**
* Ambientes isolados por VPC

---

## 💰 FinOps e Otimização de Custos

### Principais Estratégias

* Right sizing de instâncias
* Auto Scaling sob demanda
* Ambientes DEV e HOM com custo controlado
* Avaliação de Savings Plans e Reserved Instances

📉 **Resultado esperado:**
Redução significativa de custos com aumento de eficiência operacional.

---

## 🗺️ Roadmap de Implementação

### 🟦 Fase 1 — Fundação (Semanas 1–2)

* VPC DEV
* IAM
* ECR
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
* ALB + CloudFront

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

As evidências estão disponíveis em:

```
docs/evidences/
```

Incluem:

* Prints da VPC
* ECR com imagens
* ECS em execução
* Logs do CloudWatch
* Pipelines CI/CD
* Outputs do Terraform

---

## 🎓 Contexto Acadêmico

Este projeto foi desenvolvido como:

* Laboratório prático de **Arquitetura em Nuvem**
* Exercício de **DevOps e Automação**
* Estudo aplicado de **FinOps**
* Material de apresentação para **grupo e professor**

---

## ✅ Conclusão

A modernização da arquitetura AWS da MeddiFlux Systems entrega:

* 💸 Redução de custos
* ⚙️ Eficiência operacional
* 🔐 Segurança e governança
* 🎓 Aprendizado estruturado
* 🏗️ Arquitetura real de mercado

---

