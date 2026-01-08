# MeddiFlux AWS Modernization

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?logo=amazonaws&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-IaC-7B42BC?logo=terraform&logoColor=white)
![CI/CD](https://img.shields.io/badge/CI%2FCD-CodePipeline%20%2B%20CodeBuild-blue?logo=amazonaws&logoColor=white)
![Security](https://img.shields.io/badge/Security-IAM%20%2B%20Secrets%20Manager-black?logo=amazonaws&logoColor=white)
![Observability](https://img.shields.io/badge/Observability-CloudWatch%20%2B%20CloudTrail-orange?logo=amazoncloudwatch&logoColor=white)

Projeto de **Modernização, Otimização e Segurança** do ambiente AWS da **MeddiFlux Systems**, com foco em:
- **Redução de custos (FinOps)**
- **Escalabilidade e performance**
- **Governança e segregação de ambientes (DEV/HOM/PROD)**
- **Segurança (least privilege, sem bastion, segredos centralizados)**
- **Observabilidade e auditoria (logs e trilhas centralizadas)**

> ⚠️ Nota (boas práticas): se este repositório for público, **não inclua dados sensíveis** (contas, ARNs, segredos, nomes internos, URLs privadas). Use exemplos e variáveis.

---

## 🎯 Objetivos do projeto

- Modernizar a arquitetura AWS com **ambientes segregados** (DEV/HOM/PROD)
- Otimizar infraestrutura com **Auto Scaling e right-sizing**
- Descarregar conteúdo estático com **S3 + CloudFront**
- Automatizar deploys com **CI/CD** e promoção controlada entre ambientes
- Reforçar segurança com **IAM mínimo necessário**, **Secrets Manager** e **remoção de bastion**
- Centralizar observabilidade e auditoria com **CloudWatch + CloudTrail + logs centralizados**

---

## 🧭 Arquitetura alvo (visão macro)

```mermaid
flowchart TB
  U[Usuários / Navegadores] -->|HTTPS| R53[Route 53]
  R53 --> CF[CloudFront]
  CF -->|Estáticos| S3[S3 (Static Content)]
  CF -->|Dinâmico| ALB_P[ALB - PROD]

  subgraph PROD[PROD (VPC isolada)]
    ALB_P --> ASG_P[ASG 2–4x t3.medium]
    ASG_P --> APP_P[Aplicação]
    APP_P --> RDS_P[(RDS Multi-AZ)]
    SM_P[Secrets Manager] --> APP_P
    CW_P[CloudWatch] <---> APP_P
  end

  subgraph GOV[Governança / Auditoria]
    CT[CloudTrail] --> LOGS[S3 Logs Centralizados]
    IAM[IAM Least Privilege] --> PROD
  end

  ADM[Admin/DevOps] -->|SSM Session Manager| ASG_P
