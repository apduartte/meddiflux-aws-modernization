# MeddiFlux — Arquitetura (AWS Elastic Beanstalk)

## 1) Visão (diagrama lógico)

```text
Usuário -> (DNS/HTTPS) -> ALB -> Elastic Beanstalk Env (EC2/ASG) -> RDS
                               |-> CloudWatch Logs/Metrics/Alarms
                               |-> Secrets Manager (configs/credenciais)
```

## 2) Componentes e responsabilidades

### 2.1 Entrada (DNS/HTTPS)
- **Route53 (opcional)**: resolução DNS.
- **ALB/Listener (recomendado)**: termina TLS (HTTPS), distribui tráfego para as instâncias do ambiente.

### 2.2 Execução (Elastic Beanstalk)
- Provisiona e orquestra o ambiente (ASG, instâncias EC2, health check e deploy de versões).
- Mantém histórico de versões e permite rollback operacional.
- Integra com CloudWatch para logs/métricas.

### 2.3 Dados (RDS)
- Banco gerenciado.
- Recomenda-se Multi-AZ para produção (dependendo de orçamento/escopo).

### 2.4 Configurações e segredos (Secrets Manager)
- Armazena credenciais e segredos (DB, API keys etc.).
- Aplicação lê segredos em runtime (ou via injeção controlada pelo ambiente).

### 2.5 Observabilidade (CloudWatch)
- **Logs**: centralização e retenção.
- **Métricas**: CPU, memória (quando aplicável), latência, 5xx, saúde do EB.
- **Alarmes**: triggers para incidentes.

## 3) Networking (recomendação)

- **VPC** com subnets privadas para EC2/RDS.
- **Subnets públicas** para ALB (caso usado).
- **Security Groups**:
  - ALB → EC2 (porta da aplicação)
  - EC2 → RDS (porta do banco)
- **Egress** controlado (NAT Gateway se necessário para dependências externas).

## 4) Disponibilidade e escalabilidade

- **Auto Scaling** via EB (mín/máx) com políticas baseadas em métricas.
- **Health checks** no ALB e no EB (endpoint `/health` recomendado).
- Estratégia de deploy recomendada:
  - MVP: *Rolling* (baixa complexidade)
  - Produção: *Rolling with additional batch* (reduz risco) ou *Blue/Green* quando aplicável

## 5) Fluxo de entrega (pipeline)

1. Commit/PR → validações (lint/testes)
2. Build artefato (zip/container conforme stack)
3. Publicação da versão
4. Deploy no EB
5. Smoke test + health check

Detalhes operacionais: `docs/runbooks/deploy.md`.

## 6) Padrões de configuração

- **Variáveis por ambiente**: `dev/homolog/prod`.
- **Sem segredos no Git**: usar Secrets Manager.
- **Logs estruturados** (JSON) facilitam filtros e alertas.

## 7) Decisões registradas (ADR)

- `docs/adr/0001-deployment-platform-elastic-beanstalk.md`

## 8) Pontos em aberto (ajustar ao escopo)

- Stack da aplicação (linguagem/runtime, buildpack ou container).
- Estratégia de banco (single-AZ vs multi-AZ).
- Requisitos de compliance (retenção de logs, criptografia, segregação de contas).

