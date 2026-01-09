# Diagramas — Arquitetura e CI/CD (MeddiFlux AWS Modernization)

## 1) Arquitetura alvo (visão macro)
```mermaid
flowchart TB
  U[Usuário] -->|HTTPS| R53[Route 53]
  R53 --> CF[CloudFront]
  CF -->|Estático| S3[(S3 Static)]
  CF -->|Dinâmico| ALB[ALB]

  subgraph ENV["Ambientes segregados (VPC por ambiente)"]
    direction TB

    subgraph DEV["DEV"]
      ALB_DEV[ALB DEV] --> ASG_DEV[ASG App]
      ASG_DEV --> RDS_DEV[(RDS)]
    end

    subgraph HOM["HOM"]
      ALB_HOM[ALB HOM] --> ASG_HOM[ASG App]
      ASG_HOM --> RDS_HOM[(RDS)]
    end

    subgraph PROD["PROD"]
      ALB_PROD[ALB PROD] --> ASG_PROD[ASG 2–4 x t3.medium]
      ASG_PROD --> RDS_PROD[(RDS Multi-AZ)]
    end
  end

  subgraph SEC["Segurança e Acesso"]
    SM[Secrets Manager] --> ASG_PROD
    ADM[Admin/DevOps] --> SSM[SSM Session Manager] --> ASG_PROD
  end

  subgraph OBS["Observabilidade e Auditoria"]
    CW[CloudWatch Logs/Metrics] <---> ASG_PROD
    CT[CloudTrail] --> LOGS[(S3 Logs Centralizados)]
  end

flowchart LR
  DEVCOMMIT[Git push / PR] --> CP[CodePipeline]
  CP --> CB[CodeBuild\n(build + testes)]
  CB --> DDEV[Deploy DEV]
  DDEV --> G1{Gate de aprovação}
  G1 --> DHOM[Deploy HOM]
  DHOM --> T1[Testes + migrações]
  T1 --> G2{Gate de aprovação}
  G2 --> DPROD[Deploy PROD]
  DPROD --> POST[Smoke test + monitoramento]
