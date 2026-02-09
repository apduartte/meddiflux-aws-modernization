# Infra — Terraform (MeddiFlux)

## Objetivo
Provisionar e manter a infraestrutura do MeddiFlux na AWS de forma controlada.

## Princípios
- **Ambientes isolados**: `dev`, `homolog`, `prod`
- **Módulos**: reuso e padronização
- **State remoto**: backend S3 + state locking (preferir locking nativo do S3 quando disponível)
- **Mudança segura**: PR → `terraform plan` → aprovação → `terraform apply`

## Estrutura sugerida

```text
infra/
├─ modules/
│  ├─ network/
│  ├─ beanstalk/
│  ├─ rds/
│  ├─ secrets/
│  └─ observability/
└─ envs/
   ├─ dev/
   ├─ homolog/
   └─ prod/
```

## Como executar (local)

> Preferência: aplicar via pipeline. Uso local é exceção.

```bash
cd infra/envs/dev
terraform init
terraform plan -out tfplan
terraform apply tfplan
```

## Variáveis e segredos
- **Nunca** versionar segredos.
- Parametrizar por ambiente.
- Secrets devem viver no **Secrets Manager**.

## Convenções (recomendado)
- Tags obrigatórias: `Project=meddflux`, `Env=dev|homolog|prod`, `Owner=<time>`
- Naming: prefixar recursos com `meddflux-<env>-...`

## Checklist de PR (infra)
- `terraform fmt` ok
- `terraform validate` ok
- Plan revisado e anexado como evidência
- Recursos com tags

