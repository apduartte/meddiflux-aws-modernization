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
  PRODDEP --> MON[Smoke test + monitoramento]

```mermaid

## Legenda (o que cada etapa significa)

- **Git push / PR**: alteração de código + abertura de Pull Request para revisão.
- **CodePipeline**: orquestra o fluxo de entrega (stages e aprovações).
- **CodeBuild (build + testes)**: compila, executa testes e gera artefato.
- **Deploy DEV**: publica em DEV para validação rápida.
- **Approval Gate**: aprovação manual (ex.: lead/sponsor) para promover ambiente.
- **Deploy HOM**: publica em homologação para testes integrados.
- **Testes + migrações**: testes de integração + execução de migrações versionadas (quando aplicável).
- **Deploy PROD**: publica em produção com controle e rastreabilidade.
- **Smoke test + monitoramento**: checagem mínima pós-deploy + verificação de logs/métricas.

