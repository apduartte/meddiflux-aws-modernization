# Runbook — Rollback (MeddiFlux)

## Objetivo
Retornar rapidamente para uma versão estável do MeddiFlux.

## 1) Quando fazer rollback
- Healthcheck falhando após deploy
- Elevação de 5xx/latência associada à versão
- Erro crítico funcional reportado pelo cliente

## 2) Rollback via Elastic Beanstalk (console)
1. Abrir o ambiente EB do ambiente (dev/homolog/prod).
2. Ir em **Application versions**.
3. Selecionar a última versão estável.
4. Executar **Deploy** desta versão para o ambiente.
5. Acompanhar eventos do EB.

## 3) Rollback via pipeline (recomendado)
- Re-executar pipeline informando a versão/tag anterior (conforme padrão do projeto).
- A pipeline deve registrar evidências (logs, aprovadores, versão).

## 4) Pós-rollback
- Validar healthcheck e smoke tests.
- Checar logs/alarms no CloudWatch.
- Abrir item de ação para RCA (causa raiz):
  - O que quebrou?
  - Como evitar reincidência?
  - Qual teste faltou?

## 5) Evidências
Salvar em `docs/evidence/<data>-rollback/`:
- print/registro da versão revertida
- eventos do EB
- métricas/alarms relevantes

