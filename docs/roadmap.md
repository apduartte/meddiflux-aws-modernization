# Roadmap — MeddiFlux AWS Modernization (DEV → HOM → PROD)

## Objetivo
Modernizar, otimizar custos (FinOps) e reforçar segurança/observabilidade do ambiente AWS com:
- Ambientes segregados: **DEV / HOM / PROD**
- **Auto Scaling + right-sizing**
- **CloudFront + S3** para conteúdo estático
- **CI/CD** (CodePipeline + CodeBuild) com promoção controlada
- Segurança: **IAM least privilege**, **Secrets Manager**, **SSM (sem bastion)**
- Observabilidade/auditoria: **CloudWatch + CloudTrail + logs centralizados**

---

## Datas
- **Entrega oficial:** 12/02/2026
- **Meta interna:** 05/02/2026 (1 semana para ajustes e apresentação)
- **Buffer:** 06/02 a 12/02 (correções, evidências finais, ensaio)

---

## Milestones (semanas)
### W1 — Fundação + DEV (Meta: DEV operacional + pipeline DEV)
**Entregas**
- [ ] Base do repositório / estrutura IaC (Terraform)
- [ ] DEV: VPC, subnets, rotas, SGs, padrões e tags
- [ ] Acesso seguro via **SSM Session Manager** (sem bastion)
- [ ] Logs mínimos em CloudWatch (app/instâncias)
- [ ] Pipeline DEV: build + deploy (CodePipeline/CodeBuild)

**Saída (aceite)**
- DEV acessível e funcional + pipeline executando com evidência.

---

### W2 — HOM + Promoção DEV→HOM (Meta: HOM validado)
**Entregas**
- [ ] HOM: infraestrutura e padrões semelhantes ao PROD
- [ ] Gate 1 (aprovação) + deploy HOM
- [ ] Smoke test e checklist de validação em HOM
- [ ] CloudFront + S3 (mínimo funcional) em HOM
- [ ] Documentação curta: como validar em HOM

**Saída (aceite)**
- HOM promovido via pipeline + validação + evidências.

---

### W3 — PROD + Segurança completa (Meta: PROD pronto e seguro)
**Entregas**
- [ ] PROD: ALB + ASG (2–4) e parâmetros principais
- [ ] RDS Multi-AZ (quando aplicável) + parâmetros básicos
- [ ] Secrets Manager integrado (sem segredos no repo)
- [ ] IAM least privilege (roles/policies)
- [ ] CloudTrail habilitado + logs centralizados em S3
- [ ] Gate 2 (aprovação) + deploy PROD (controlado)

**Saída (aceite)**
- PROD operacional + segurança/auditoria aplicadas + evidências.

---

### W4 — Testes finais + FinOps + Pacote de entrega (Meta: pronto até 05/02)
**Entregas**
- [ ] Teste de performance/carga (básico) + relatório curto
- [ ] Plano de rollback + simulação/documentação
- [ ] FinOps: antes/depois (ou estimado) + racional das escolhas
- [ ] Runbook: deploy/rollback/troubleshooting
- [ ] Pacote de evidências organizado em `/docs/evidences`

**Saída (aceite)**
- Projeto “entregável”: documentação, evidências, custo e validação final.

---

### Buffer (06/02 → 12/02) — Ajustes finais + Apresentação
- [ ] Correções finas e polimento da documentação
- [ ] Atualização final de prints/evidências
- [ ] Ensaio da apresentação (10–15 min)
- [ ] Checklist final de entrega

---

## Definition of Done (DoD)
Um item só é considerado **Entregue** se possuir:
- Implementado e funcionando
- Evidência (print/log/link)
- Documentação mínima (README/RUNBOOK/checklist)
- Validação (smoke test ou checklist)

---

## Evidências (padrão)
Armazenar em `docs/evidences/`:
- Prints do CodePipeline/CodeBuild (execuções e stages)
- Prints do ambiente (ALB/ASG/RDS/CloudFront/S3)
- CloudWatch (logs/dashboards/alarmes)
- CloudTrail + S3 logs centralizados
- Resultados de testes (smoke/performance)
- Checklist de validação por ambiente

---

## Ritual de acompanhamento (grupo)
- **Segunda:** planejamento + priorização (30 min)
- **Quarta:** remoção de bloqueios + ajuste de rota (30 min)
- **Sexta:** demo + evidências + atualização Kanban (30 min)
