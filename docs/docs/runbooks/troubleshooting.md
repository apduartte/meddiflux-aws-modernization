# Runbook — Troubleshooting (MeddiFlux)

## Objetivo
Acelerar diagnóstico e correção de incidentes comuns.

## 1) Checklist rápido
- Ambiente EB está **Healthy/Green**?
- Existe aumento de **5xx** ou **latência**?
- Logs mostram erro de conexão com banco?
- Secret/variável de ambiente mudou?

## 2) Sintomas comuns → ações

### 2.1 5xx após deploy
- Confirmar versão ativa no EB.
- Verificar logs da aplicação (CloudWatch Logs).
- Executar smoke test manual (endpoint de health).
- Se o problema começou após a mudança, considerar rollback.

### 2.2 Timeout / alta latência
- Verificar CPU/memória das instâncias.
- Checar saturação de conexões no banco.
- Validar autoscaling (se métricas/thresholds estão adequados).

### 2.3 Falha de conexão com RDS
- Conferir Security Groups (EC2 → RDS liberado apenas para o SG da app).
- Conferir secret usado (nome/ARN e valores).
- Validar se o RDS está disponível e em rede correta.

### 2.4 Falha de secret/config
- Confirmar existência do secret no Secrets Manager.
- Garantir que o role do EB tem permissão de leitura no secret.
- Conferir se variáveis de ambiente apontam para o secret correto.

## 3) Evidências mínimas (para auditoria)
- Hora do incidente e ambiente
- Versão/commit em produção
- Prints/links de logs e métricas
- Ação executada (fix/rollback) e resultado

## 4) Escalonamento
- Owner técnico: _TODO_
- Owner cliente: Professor (cliente)

> Importante: registrar o post-mortem (mesmo simples) em `docs/evidence/`.
