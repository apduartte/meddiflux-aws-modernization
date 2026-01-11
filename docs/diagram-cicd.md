```md
# Diagrama — CI/CD (DEV → HOM → PROD)

> **Objetivo:** entregar com velocidade sem perder governança, usando aprovações entre ambientes e validação pós-deploy para aumentar confiabilidade em produção.

```mermaid
flowchart LR
  COMMIT[Git push / PR] --> CP[CodePipeline]
  CP --> CB[CodeBuild: build + testes]
  CB --> DEVDEP[Deploy DEV]
  DEVDEP --> G1{Approval Gate}
  G1 --> HOMDEP[Deploy HOM]
  HOMDEP --> T[Testes + migrações]
  T --> G2{Approval Gate}
  G2 --> PRODDEP[Deploy PROD]
  PRODDEP --> MON[Smoke test + monitoramento]
