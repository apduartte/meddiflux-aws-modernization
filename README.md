# 🚀 Modernização da Arquitetura AWS – MeddiFlux Systems

## 🎯 Objetivo

Esta proposta visa modernizar a infraestrutura AWS da MeddiFlux Systems com foco em:

- Redução de custos operacionais
- Otimização de desempenho, escalabilidade e governança
- Reforço da segurança e mitigação de riscos críticos

---

## 🧩 Visão Geral da Solução

### 1. Organização em Ambientes Isolados

- **DEV**: Ambiente seguro para desenvolvimento
- **HOM**: Uso otimizado em horário comercial (220h/mês)
- **PROD**: Auto Scaling, RDS otimizado, CDN e segurança reforçada

### 2. Otimização de Infraestrutura e Custos

- Substituição de 6 instâncias `m4.large` por Auto Scaling com 2–4 instâncias `t3.medium`
- Redimensionamento do RDS para `t3.large` Multi-AZ
- Uso de **CloudFront + S3** para conteúdo estático
- VPCs isoladas por ambiente para governança

### 3. CI/CD e Automação

- **CodePipeline + CodeBuild** para DEV, HOM e PROD
- Deploy automatizado via `git push`
- Execução automática de testes e migrações
- Fluxo padronizado com aprovações e revisões

---

## 💰 Pilar Financeiro – Redução de Custos

| Item                   | Atual | Projetado |
|------------------------|-------|-----------|
| DEV                   | $0    | $36       |
| HOM                   | $48   | $36       |
| PROD                  | $477  | $207      |
| Bastion Host          | $5    | $0        |
| Serviço CI/CD         | $0    | $13       |
| **Total Mensal**      | $530  | $291      |
| **Economia Mensal**   | -     | $239 (45%)|
| **Projeção Anual**    | $6.360| $3.498    |

### 💡 Oportunidades Adicionais

- **Savings Plans PROD**: até 40% (~$82/mês)
- **RDS Reserved Instances**: até 30% (~$60/mês)
- **Remoção de NAT Gateway DEV/HOM**: ~$20/mês
- **Economia Total Potencial**: $401/mês (-76%)

---

## ⚙ Pilar Operacional – Eficiência e Escalabilidade

- Auto Scaling conforme demanda
- CloudFront para cache e distribuição
- S3 para conteúdo estático
- Monitoramento com **CloudWatch** e **CloudTrail**

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

## 🔐 Pilar de Risco – Segurança e Governança

- Eliminação do Bastion Host
- Migrações via pipeline com scripts versionados
- IAM com permissões mínimas e **Secrets Manager**
- VPCs independentes e tráfego criptografado fim a fim
- Auditoria com CloudTrail e logs centralizados

---

## 📅 Cronograma de Implementação (8 semanas)

| Fase | Atividades |
|------|------------|
| **1. Fundos (Semanas 1–2)** | VPCs, sub-redes, segurança, ambiente DEV |
| **2. Homologação (Semanas 3–4)** | Recriação do HOM, testes DEV → HOM |
| **3. Produção (Semanas 5–6)** | Novo PROD com Auto Scaling, RDS, CDN |
| **4. Testes (Semana 7)** | Testes de carga, failover, segurança |
| **5. Go-live (Semana 8)** | Corte de DNS, monitoramento, desligamento antigo |

---

## 💵 Custo do Serviço de Consultoria

- **Valor único**: R$ 35.000,00
- **Suporte mensal (a partir de jan/2026)**: R$ 1.624,00

---

## 📊 Análise de Custo-Benefício

- **Economia estimada**: R$ 15.588,00 ao ano
- **Retorno sobre investimento**: em menos de 3 meses

---

## 📌 Próximos Passos

- ✅ Aprovação executiva
- ✅ Validação do cronograma
- ✅ Alinhamento com equipe de desenvolvimento
- 🚀 Início da Fase 1 – Ambiente DEV

---

## ✅ Conclusão

A proposta entrega uma combinação clara de:

- 💸 Redução de custos
- ⚙️ Otimização operacional
- 🔐 Fortalecimento da segurança

A MeddiFlux Systems estará preparada para crescer com previsibilidade, governança e alta disponibilidade na AWS.

---