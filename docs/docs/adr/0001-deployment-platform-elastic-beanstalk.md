# ADR-0001 — Plataforma de Deploy: Elastic Beanstalk

- **Status**: Aprovado
- **Data**: _TODO (YYYY-MM-DD)_

## Contexto
Precisamos de uma plataforma de execução para o MeddiFlux que permita:
- Deploy rápido e repetível
- Escalabilidade básica
- Monitoramento de saúde do ambiente
- Baixa complexidade operacional no MVP

## Decisão
Utilizar **AWS Elastic Beanstalk (EB)** como plataforma de deploy do MeddiFlux.

## Racional
- EB abstrai parte do esforço de provisionamento/gestão (sem impedir controle dos recursos AWS)
- Suporta versionamento/rollback operacional
- Integração nativa com CloudWatch (logs/métricas)
- Adequado para MVP e para um cliente que valoriza **previsibilidade e evidências**

## Consequências
### Positivas
- Menos atrito inicial para colocar o sistema em produção
- Operação mais simples (saúde do ambiente visível)
- Rollback mais direto

### Negativas / Riscos
- Menor flexibilidade que uma orquestração mais avançada (ex.: EKS) para casos complexos
- Dependência de padrões do EB (plataformas/stack suportadas)

## Alternativas consideradas
- **ECS/Fargate**: mais flexível; maior setup inicial (pipeline, tasks, serviços, logs)
- **EKS**: alto poder; alto custo de operação e curva de aprendizado
- **EC2 “na mão”**: flexível; risco e esforço operacional maiores

## Critérios para revisar esta decisão
Reavaliar se ocorrer qualquer um dos itens:
- Necessidade de múltiplos serviços/microserviços com deploy independente
- Requisitos avançados de rede/segurança que o EB não atenda bem
- Crescimento significativo de escala que exija fine-tuning além do EB

## Evidências
- Link do PR: _TODO_
- Demo/print do deploy: `docs/evidence/` (_TODO_)
