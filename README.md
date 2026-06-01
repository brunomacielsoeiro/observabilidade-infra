# 📊 Observabilidade em Infraestrutura

> Projeto de estudos sobre observabilidade e monitoramento em ambientes de infraestrutura, abordando métricas, logs, traces, Prometheus, Grafana e boas práticas de alertas. Atividade acadêmica para cumprimento de horas complementares.

---

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [O que você vai aprender](#o-que-você-vai-aprender)
- [Estrutura do Repositório](#estrutura-do-repositório)
- [Arquitetura de Observabilidade](#arquitetura-de-observabilidade)
- [Os 3 Pilares](#os-3-pilares)
- [Conexão com outros projetos](#conexão-com-outros-projetos)
- [Referências](#referências)

---

## Sobre o Projeto

Observabilidade é a capacidade de entender o **estado interno** de um sistema a partir dos **sinais externos** que ele emite. Em infraestrutura moderna (cloud, containers, microserviços), é impossível operar sem observabilidade.

### Por que observabilidade é essencial?

- Detectar problemas **antes** que afetem usuários
- Entender a **causa raiz** de incidentes rapidamente
- Tomar decisões baseadas em **dados reais** (não intuição)
- Garantir **SLAs/SLOs** com evidências mensuráveis
- Base para práticas DevOps e SRE

---

## O que você vai aprender

| Tema | Arquivo | Descrição |
|------|---------|-----------|
| Conceitos | [conceitos-observabilidade.md](./conceitos-observabilidade.md) | Métricas, logs, traces e como se complementam |
| Prometheus + Grafana | [prometheus-grafana.md](./prometheus-grafana.md) | Ferramentas de coleta e visualização |
| Exemplos Prometheus | [prometheus-exemplos.md](./prometheus-exemplos.md) | Configurações práticas (YAML) |
| Alertmanager | [alertmanager.md](./alertmanager.md) | Regras de alerta e notificações |
| Arquitetura | [arquitetura-monitoramento.md](./arquitetura-monitoramento.md) | Fluxo completo de monitoramento |
| Boas Práticas | [boas-praticas-observabilidade.md](./boas-praticas-observabilidade.md) | Padrões recomendados |
| Cloud | [observabilidade-cloud.md](./observabilidade-cloud.md) | Observabilidade em AWS |
| Glossário | [glossario.md](./glossario.md) | Termos e definições |

---

## Estrutura do Repositório

```
observabilidade-infra/
├── README.md                          ← Este arquivo (visão geral)
├── conceitos-observabilidade.md       ← Fundamentos: métricas, logs, traces
├── prometheus-grafana.md              ← Prometheus + Grafana explicados
├── prometheus-exemplos.md             ← Configurações YAML práticas
├── alertmanager.md                    ← Regras de alerta + notificações
├── arquitetura-monitoramento.md       ← Fluxo de monitoramento
├── boas-praticas-observabilidade.md   ← Padrões e recomendações
├── observabilidade-cloud.md           ← Observabilidade em AWS
├── glossario.md                       ← Termos e definições
├── CONTRIBUTING.md
└── LICENSE
```

---

## Arquitetura de Observabilidade

```
┌─────────────────────────────────────────────────────────────────────┐
│                    STACK DE OBSERVABILIDADE                           │
│                                                                       │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐           │
│  │  Aplicação   │    │  Aplicação   │    │  Aplicação   │           │
│  │  (métricas)  │    │  (logs)      │    │  (traces)    │           │
│  └──────┬───────┘    └──────┬───────┘    └──────┬───────┘           │
│         │                   │                   │                     │
│         ▼                   ▼                   ▼                     │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐           │
│  │  Prometheus  │    │  Loki / ELK  │    │    Jaeger    │           │
│  │  (coleta)    │    │  (agregação) │    │  (tracing)   │           │
│  └──────┬───────┘    └──────┬───────┘    └──────┬───────┘           │
│         │                   │                   │                     │
│         └───────────────────┼───────────────────┘                     │
│                             │                                         │
│                             ▼                                         │
│                      ┌──────────────┐                                 │
│                      │   Grafana    │                                 │
│                      │ (dashboards) │                                 │
│                      └──────┬───────┘                                 │
│                             │                                         │
│                             ▼                                         │
│                      ┌──────────────┐                                 │
│                      │ Alertmanager │                                 │
│                      │(notificações)│                                 │
│                      └──────┬───────┘                                 │
│                             │                                         │
│                    ┌────────┼────────┐                                │
│                    ▼        ▼        ▼                                │
│                 Slack    Email   PagerDuty                            │
│                                                                       │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Os 3 Pilares

| Pilar | O que é | Ferramenta | Quando usar |
|-------|---------|-----------|-------------|
| **Métricas** | Valores numéricos ao longo do tempo | Prometheus, CloudWatch | Alertas, tendências, SLOs |
| **Logs** | Registros textuais de eventos | Loki, ELK, CloudWatch Logs | Investigação, auditoria |
| **Traces** | Caminho de uma requisição entre serviços | Jaeger, X-Ray | Latência, dependências |

### Como se complementam

```
ALERTA (métrica) → "Latência subiu para 2s"
    │
    ▼
DASHBOARD (métrica) → "Endpoint /api/orders está lento"
    │
    ▼
TRACE → "Chamada ao banco demorou 1.8s"
    │
    ▼
LOG → "Query SELECT * FROM orders WHERE... executou full table scan"
    │
    ▼
FIX → Adicionar índice na tabela
```

---

## Tecnologias Abordadas

| Ferramenta | Função | Tipo |
|-----------|--------|------|
| **Prometheus** | Coleta e armazenamento de métricas | Open source |
| **Grafana** | Visualização e dashboards | Open source |
| **Alertmanager** | Gerenciamento de alertas | Open source |
| **PromQL** | Linguagem de consulta de métricas | Query language |
| **Node Exporter** | Métricas de servidor (CPU, RAM, disco) | Exporter |
| **CloudWatch** | Métricas e logs na AWS | Managed |

---

## Conexão com outros projetos

| Projeto | Relação com Observabilidade |
|---------|---------------------------|
| `fundamentos-devops` | Monitor é fase do ciclo DevOps |
| `networking-cloud-fundamentos` | Monitorar tráfego e latência de rede |
| `containers-docker-fundamentos` | Métricas de containers |
| `k8s-resource-report` | Monitoramento de recursos K8s |
| `seguranca-cloud-iam` | Auditoria via CloudTrail |

---

## Referências

- [Prometheus Documentation](https://prometheus.io/docs/)
- [Grafana Documentation](https://grafana.com/docs/)
- [Google SRE Book — Monitoring](https://sre.google/sre-book/monitoring-distributed-systems/)
- [OpenTelemetry](https://opentelemetry.io/)
- [AWS CloudWatch](https://docs.aws.amazon.com/cloudwatch/)

---

## 📄 Licença

MIT License
