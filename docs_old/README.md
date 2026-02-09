# 📚 Documentação

## 🏗️ Arquitetura AWS
- [Diagrama ECS + EC2](./architecture/aws-ecs-diagram.html) - Visualização de uma das arquiteturas propostas para iniciar no treinamento e evoluir na Formação AWS.
# MeddiFlux — Documentação Técnica (AWS Elastic Beanstalk)

> **Objetivo**: padronizar a entrega do MeddiFlux na AWS com **Infra as Code (Terraform)**, **CI/CD**, **segurança por padrão** e **observabilidade**.

## 1) Visão geral

O MeddiFlux é implantado na AWS utilizando **Elastic Beanstalk (EB)** como plataforma de execução (ambiente gerenciado) e **Terraform** para provisionamento e mudanças controladas de infraestrutura.

**Principais resultados esperados**
- Deploy repetível e rastreável (commit → pipeline → versão publicada)
- Ambientes consistentes (dev/homolog/prod) definidos por código
- Segredos e configurações sensíveis fora do repositório
- Telemetria mínima (logs, métricas, alarmes) e runbooks

## 2) Arquitetura (alto nível)

- **Entrada**: DNS/HTTPS (ex.: Route53 + ALB) 
- **Execução**: Elastic Beanstalk Environment (EC2 + Auto Scaling)
- **Dados**: RDS (ex.: PostgreSQL)
- **Segredos**: AWS Secrets Manager
- **Observabilidade**: CloudWatch Logs/Metrics/Alarms

📌 Detalhes e diagramas: `docs/architecture.md`.

## 3) Requisitos

### Acesso
- Conta AWS (ou subconta/OU) com permissões para EB, VPC, EC2, IAM, RDS, CloudWatch, Secrets Manager e S3.

### Ferramentas locais
- Terraform (versão definida pelo projeto)
- AWS CLI configurada (`aws configure`)
- (Opcional) EB CLI, se adotado para operações locais

## 4) Estrutura do repositório (sugerida)

```text
.
├─ infra/
│  ├─ modules/
│  └─ envs/
│     ├─ dev/
│     ├─ homolog/
│     └─ prod/
├─ docs/
│  ├─ architecture.md
│  ├─ adr/
│  └─ runbooks/
└─ .github/workflows/   (ou equivalente do seu CI)
```

## 5) Ambientes

| Ambiente | Finalidade | Regras | Observações |
|---|---|---|---|
| dev | Desenvolvimento | deploy automático (opcional) | recursos mínimos |
| homolog | Validação | deploy via PR/approval | replica cenário |
| prod | Produção | approval obrigatório | alarmes e rollback testado |

## 6) Configuração (variáveis e segredos)

**Regras de ouro**
- ❌ Não versionar segredos no Git
- ✅ Segredos em **Secrets Manager** (ou Parameter Store) e injetados no runtime
- ✅ Variáveis não sensíveis via EB Environment Properties

**Padrão recomendado de nomes (exemplos)**
- `meddflux/<env>/db` (secret JSON com host, user, password, dbname)
- `meddflux/<env>/app` (secret JSON com tokens/keys)

## 7) Infraestrutura como Código (Terraform)

### Fluxo padrão
```bash
cd infra/envs/<env>
terraform fmt -recursive
terraform init
terraform validate
terraform plan -out plan.tfplan
terraform apply plan.tfplan
```

### Estado remoto (recomendação)
- Backend: **S3**
- Locking: **S3 native locking** (preferencial) ou **DynamoDB (legado)**, conforme a versão do Terraform e as políticas do projeto.

📌 Detalhes: `infra/README.md`.

## 8) Deploy da aplicação (Elastic Beanstalk)

Existem duas abordagens comuns:

1) **Build/artefato** (ZIP) publicado no EB
- Pipeline gera artefato versionado (ex.: `app-<git_sha>.zip`)
- Pipeline atualiza a versão do EB e promove para o ambiente

2) **Container** (Docker) no EB
- Pipeline publica imagem (ex.: ECR)
- EB usa `Dockerrun.aws.json` (single ou multicontainer)

📌 Procedimento detalhado: `docs/runbooks/deploy.md`.

## 9) Rollback

Rollback deve ser **rápido e previsível**:
- Reverter para uma **Application Version** anterior no EB
- Validar health/status + logs

📌 Procedimento detalhado: `docs/runbooks/rollback.md`.

## 10) Observabilidade

Mínimo recomendado:
- Logs centralizados por ambiente (CloudWatch Logs)
- Alarmes: 5xx, latência, CPU/Memory, saúde do EB
- Dashboard básico por ambiente

📌 Runbook: `docs/runbooks/troubleshooting.md`.

## 11) Segurança

Checklist mínimo:
- IAM com **least privilege**
- Segredos centralizados (Secrets Manager)
- CloudTrail habilitado (auditoria)
- Proteções no repositório (branch protection + code review)

## 12) Checklist de aceite (cliente/professor)

- [ ] Infra sobe via Terraform (sem cliques manuais)
- [ ] Deploy publica versão no Elastic Beanstalk via pipeline
- [ ] Healthcheck e logs comprovam funcionamento
- [ ] Alarmes mínimos configurados
- [ ] Rollback documentado e executável

---

## Contatos / Responsáveis
- **Owner técnico**: _TODO_
- **Owner produto/cliente**: _Professor (cliente)_
