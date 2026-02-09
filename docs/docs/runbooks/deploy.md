# Runbook — Deploy (MeddiFlux)

## Objetivo
Executar deploy do MeddiFlux de forma **controlada**, **rastreável** e **repetível**.

## 1) Pré-condições
- Infra do ambiente aplicada (Terraform ok)
- Pipeline configurado (CI/CD)
- Secrets configurados no **Secrets Manager**
- Healthcheck/endpoints conhecidos

## 2) Fluxo padrão (CI/CD)
1. Abrir PR com mudança.
2. Validar checks obrigatórios (lint/testes).
3. Aprovar PR (política do time).
4. Merge na branch de deploy (ex.: `main`).
5. Pipeline executa:
   - build artefato
   - testes
   - publicação da versão
   - deploy no Elastic Beanstalk
   - smoke test

## 3) Evidências (obrigatório)
Armazenar em `docs/evidence/<data>/`:
- link do pipeline executado
- versão/commit publicado
- print do EB com versão ativa
- print/log de healthcheck bem-sucedido

## 4) Deploy manual (somente contingência)
> **Evitar**. Usar apenas quando o pipeline estiver indisponível.

Checklist mínimo:
- registrar motivo e janela
- publicar nova versão no EB
- validar healthcheck
- gerar evidência

## 5) Critérios de sucesso
- ambiente **Healthy/Green**
- smoke test ok
- logs sem erros críticos pós-deploy

## 6) Critérios de rollback
- healthcheck falha por > _TODO_ minutos
- aumento sustentado de 5xx/latência pós-deploy
- erro funcional impeditivo

➡️ Em caso de rollback, seguir `docs/runbooks/rollback.md`.
