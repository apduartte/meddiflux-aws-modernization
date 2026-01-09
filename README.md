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

---

## 🎯 Objetivos do projeto
- Modernizar a arquitetura AWS com **ambientes segregados** (DEV/HOM/PROD)
- Otimizar infraestrutura com **Auto Scaling e right-sizing**
- Descarregar conteúdo estático com **S3 + CloudFront**
- Automatizar deploys com **CI/CD** e promoção controlada entre ambientes
- Reforçar segurança com **IAM mínimo necessário**, **Secrets Manager** e **remoção de bastion**
- Centralizar observabilidade e auditoria com **CloudWatch + CloudTrail + logs centralizados**

---

## 📌 Escopo
### Inclui
- Criação/Padronização dos ambientes **DEV / HOM / PROD**
- Arquitetura otimizada: **ALB + ASG**, **RDS Multi-AZ**, **CloudFront + S3**
- Pipeline **CodePipeline + CodeBuild** (promoção entre ambientes)
- Implementação de **SSM Session Manager** para administração (sem bastion)
- Segurança e governança (IAM least privilege, segredos centralizados, auditoria)
- Observabilidade (métricas, logs e trilhas) e evidências de validação

### Fora de escopo (ajuste se necessário)
- Refatorações profundas na aplicação (além do necessário para build/deploy/observabilidade)
- Funcionalidades de produto/código de negócio não relacionadas ao objetivo do projeto
- Integrações corporativas avançadas (SIEM, ITSM, etc.), caso não previstas

---

## Diagramas (Arquitetura e CI/CD)
Veja em: [docs/architecture.md](docs/architecture.md)
  
