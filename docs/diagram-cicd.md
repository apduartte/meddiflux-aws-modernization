# Diagrama — CI/CD (DEV → HOM → PROD)

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
<<<<<<< HEAD
  PRODDEP --> MON[Smoke test + monitoring]


# Diagrama — CI/CD (DEV → HOM → PROD)

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
=======
>>>>>>> 04d9256a574f1308367ded3204b56397ac7c459b
  PRODDEP --> MON[Smoke test + monitoramento]
