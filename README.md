# 🚀 Modernização da Arquitetura AWS – MeddiFlux Systems

## 🎯 Objetivo

Esta proposta visa modernizar a infraestrutura AWS da MeddiFlux Systems com foco em:

- Redução de custos operacionais
- Otimização de desempenho, escalabilidade e governança
- Reforço da segurança e mitigação de riscos críticos

---

## 🧩 Visão Geral da Solução

### 1. Organização em Ambientes Isolados

- **DEV**: Ambiente seguro para desenvolvimento
- **HOM**: Uso otimizado em horário comercial (220h/mês)
- **PROD**: Auto Scaling, RDS otimizado, CDN e segurança reforçada

### 2. Otimização de Infraestrutura e Custos

- Substituição de 6 instâncias `m4.large` por Auto Scaling com 2–4 instâncias `t3.medium`
- Redimensionamento do RDS para `t3.large` Multi-AZ
- Uso de **CloudFront + S3** para conteúdo estático
- VPCs isoladas por ambiente para governança

### 3. CI/CD e Automação

- **CodePipeline + CodeBuild** para DEV, HOM e PROD
- Deploy automatizado via `git push`
- Execução automática de testes e migrações
- Fluxo padronizado com aprovações e revisões

---

## 💰 Pilar Financeiro – Redução de Custos

| Item                   | Atual | Projetado |
|------------------------|-------|-----------|
| DEV                   | $0    | $36       |
| HOM                   | $48   | $36       |
| PROD                  | $477  | $207      |
| Bastion Host          | $5    | $0        |
| Serviço CI/CD         | $0    | $13       |
| **Total Mensal**      | $530  | $291      |
| **Economia Mensal**   | -     | $239 (45%)|
| **Projeção Anual**    | $6.360| $3.498    |

### 💡 Oportunidades Adicionais

- **Savings Plans PROD**: até 40% (~$82/mês)
- **RDS Reserved Instances**: até 30% (~$60/mês)
- **Remoção de NAT Gateway DEV/HOM**: ~$20/mês
- **Economia Total Potencial**: $401/mês (-76%)

---

## ⚙ Pilar Operacional – Eficiência e Escalabilidade

- Auto Scaling conforme demanda
- CloudFront para cache e distribuição
- S3 para conteúdo estático
- Monitoramento com **CloudWatch** e **CloudTrail**

---

## 🔐 Pilar de Risco – Segurança e Governança

- Eliminação do Bastion Host
- Migrações via pipeline com scripts versionados
- IAM com permissões mínimas e **Secrets Manager**
- VPCs independentes e tráfego criptografado fim a fim
- Auditoria com CloudTrail e logs centralizados

---

## 📅 Cronograma de Implementação (8 semanas)

| Fase | Atividades |
|------|------------|
| **1. Fundos (Semanas 1–2)** | VPCs, sub-redes, segurança, ambiente DEV |
| **2. Homologação (Semanas 3–4)** | Recriação do HOM, testes DEV → HOM |
| **3. Produção (Semanas 5–6)** | Novo PROD com Auto Scaling, RDS, CDN |
| **4. Testes (Semana 7)** | Testes de carga, failover, segurança |
| **5. Go-live (Semana 8)** | Corte de DNS, monitoramento, desligamento antigo |

---

## 💵 Custo do Serviço de Consultoria

- **Valor único**: R$ 35.000,00
- **Suporte mensal (a partir de jan/2026)**: R$ 1.624,00

---

## 📊 Análise de Custo-Benefício

- **Economia estimada**: R$ 15.588,00 ao ano
- **Retorno sobre investimento**: em menos de 3 meses

---

## 📌 Próximos Passos

- ✅ Aprovação executiva
- ✅ Validação do cronograma
- ✅ Alinhamento com equipe de desenvolvimento
- 🚀 Início da Fase 1 – Ambiente DEV

---

## ✅ Conclusão

A proposta entrega uma combinação clara de:

- 💸 Redução de custos
- ⚙️ Otimização operacional
- 🔐 Fortalecimento da segurança

A MeddiFlux Systems estará preparada para crescer com previsibilidade, governança e alta disponibilidade na AWS.

---