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
- Arquitetura (visão macro): [docs/diagram-architecture.md](docs/diagram-architecture.md)
- Fluxo CI/CD: [docs/diagram-cicd.md](docs/diagram-cicd.md)
- Roadmap: [docs/roadmap.md](docs/roadmap.md)
-------------------------------------------------------------------------------------------------------------------------------------
# MedFlux — Arquitetura, CI/CD e Infraestrutura como Código (Terraform)

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?logo=amazonaws&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-Infrastructure%20as%20Code-7B42BC?logo=terraform&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Containers-2496ED?logo=docker&logoColor=white)
![ECS](https://img.shields.io/badge/Amazon%20ECS-Fargate-FF9900?logo=amazonaws&logoColor=white)
![ECR](https://img.shields.io/badge/Amazon%20ECR-Container%20Registry-232F3E?logo=amazonaws&logoColor=white)
![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)
![Security](https://img.shields.io/badge/Security-IAM%20%7C%20ACM-black?logo=amazonaws&logoColor=white)
![Observability](https://img.shields.io/badge/Observability-CloudWatch-orange?logo=amazoncloudwatch&logoColor=white)

# MedFlux — Arquitetura, CI/CD e Infraestrutura como Código (Terraform)

Projeto de **modernização da arquitetura AWS** da plataforma **MedFlux**, com foco em **padronização de ambientes**, **automação de deploy**, **segurança**, **observabilidade** e **governança**, seguindo boas práticas de **DevOps, Cloud Architecture e FinOps**.

---

## 🎯 Objetivos do Projeto

- Padronizar e segregar ambientes **DEV / HOMOLOG / PROD**
- Automatizar build, testes e deploy com **CI/CD**
- Modernizar a hospedagem utilizando **containers gerenciados**
- Aumentar segurança com **least privilege**, **segredos centralizados** e **sem bastion**
- Garantir **observabilidade, auditoria e rastreabilidade**
- Facilitar escalabilidade, manutenção e evolução da plataforma

---

## 🧭 Visão Macro do Negócio

Fluxo de entrega contínua conforme o desenho arquitetural do grupo:

**Planejamento**  
→ **Desenvolvimento (testes automatizados)**  
→ **DEV / HOMOLOG**  
→ **Aprovação**  
→ **Produção**  
→ **Monitoramento & Segurança**

### Ambientes
- **DEV**  
  Validação técnica, integração contínua e testes automatizados

- **HOMOLOG**  
  Validação funcional com **OA + Negócio**

- **PROD**  
  Ambiente produtivo utilizado por **Hospitais e Clínicas**

---

## 🌿 Estratégia de Branches (Git Flow simplificado)

- `dev`  
  Integração contínua, testes e deploy automático em DEV

- `homolog`  
  Validação funcional e aceite de negócio

- `master`  
  Produção, com controle, aprovação e governança

---

## 🧱 Stack Tecnológica

Arquitetura alinhada ao desenho técnico do projeto:

- **ECR (Elastic Container Registry)**  
  Repositório de imagens Docker (backend e frontend)

- **ECS Fargate**  
  Orquestração e execução de containers sem gerenciamento de servidores

- **Application Load Balancer (ALB)**  
  Entrada HTTP/HTTPS e balanceamento de carga

- **ACM (AWS Certificate Manager)**  
  Certificados TLS para comunicação segura

- **RDS (PostgreSQL / SQL Server)**  
  Banco de dados gerenciado com foco em alta disponibilidade

- **CloudWatch**  
  Logs, métricas, alarmes e monitoramento contínuo

---

## 📁 Estrutura do Repositório

```txt
app/
 ├─ backend/       # Aplicação backend + Dockerfile
 └─ frontend/      # Aplicação frontend + Dockerfile

infra/
 └─ terraform/     # Infraestrutura como código (Terraform)
    ├─ modules/    # Módulos reutilizáveis (network, ecs, ecr, alb, rds)
    └─ envs/       # Ambientes segregados (dev / homolog / prod)

cicd/
 └─ github-actions/
    └─ workflows/  # Pipelines CI/CD



