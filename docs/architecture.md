cat > docs/architecture.md <<'EOF'
# Diagramas — Arquitetura e CI/CD (MeddiFlux AWS Modernization)

## 1) Arquitetura alvo (visão macro)

```mermaid
flowchart TB
  U[Usuarios] -->|HTTPS| R53[Route 53] --> CF[CloudFront]
  CF -->|Estaticos| S3[(S3 Static Content)]
  CF -->|Dinamico| ALB_PROD[ALB - PROD]

  subgraph DEV[DEV]
    ALB_DEV[ALB - DEV] --> ASG_DEV[ASG - App] --> RDS_DEV[(RDS)]
  end

  subgraph HOM[HOM]
    ALB_HOM[ALB - HOM] --> ASG_HOM[ASG - App] --> RDS_HOM[(RDS)]
  end

  subgraph PROD[PROD]
    ALB_PROD --> ASG_PROD[ASG 2-4 x t3.medium] --> APP[Aplicacao] --> RDS_PROD[(RDS Multi-AZ)]
  end

  SM[Secrets Manager] --> APP
  CW[CloudWatch (Logs/Metrics)] <---> APP
  ADM[Admin/DevOps] --> SSM[SSM Session Manager] --> ASG_PROD
  CT[CloudTrail] --> LOGS[(S3 Logs Centralizados)]
