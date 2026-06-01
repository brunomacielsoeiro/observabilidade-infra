# 📘 Glossário de Observabilidade

## Termos Fundamentais

| Termo | Definição |
|-------|-----------|
| **Observabilidade** | Capacidade de entender o estado interno de um sistema a partir dos sinais externos que ele emite |
| **Monitoramento** | Prática de coletar, agregar e alertar sobre métricas pré-definidas |
| **Telemetria** | Dados emitidos por um sistema (métricas, logs, traces) |

---

## Métricas

| Termo | Definição |
|-------|-----------|
| **Métrica** | Valor numérico coletado ao longo do tempo que representa o estado do sistema |
| **Counter** | Métrica que só cresce (ex: total de requisições) |
| **Gauge** | Métrica que sobe e desce (ex: uso de CPU) |
| **Histogram** | Distribuição de valores em buckets (ex: latência) |
| **Série temporal** | Sequência de valores indexados por timestamp |
| **Cardinalidade** | Número de combinações únicas de labels em uma métrica |
| **Scrape** | Ação do Prometheus de coletar métricas de um target |
| **PromQL** | Linguagem de consulta do Prometheus |

---

## Logs

| Termo | Definição |
|-------|-----------|
| **Log** | Registro textual de um evento discreto com timestamp |
| **Log estruturado** | Log em formato parseável (JSON) com campos definidos |
| **Log level** | Severidade do evento (DEBUG, INFO, WARN, ERROR, FATAL) |
| **Agregação de logs** | Centralizar logs de múltiplas fontes em um único local |
| **Retenção** | Período que logs são mantidos antes de serem deletados |

---

## Traces

| Termo | Definição |
|-------|-----------|
| **Trace** | Rastreamento completo de uma requisição através de múltiplos serviços |
| **Span** | Uma operação individual dentro de um trace (com início e fim) |
| **Trace ID** | Identificador único que conecta todos os spans de uma requisição |
| **Parent Span** | Span que iniciou outro span (relação causal) |
| **Propagação de contexto** | Passar trace ID entre serviços via headers HTTP |

---

## Alertas

| Termo | Definição |
|-------|-----------|
| **Alerta** | Notificação disparada quando uma condição é atendida |
| **Alertmanager** | Componente que recebe, agrupa e roteia alertas |
| **Threshold** | Limiar que dispara um alerta (ex: CPU > 80%) |
| **Flapping** | Alerta que fica alternando entre ativo e resolvido rapidamente |
| **Severidade** | Nível de urgência (info, warning, critical) |
| **Silencing** | Suprimir alertas temporariamente (ex: durante manutenção) |
| **Grouping** | Agrupar alertas similares para reduzir ruído |

---

## Ferramentas

| Termo | Definição |
|-------|-----------|
| **Prometheus** | Sistema de monitoramento e armazenamento de métricas (pull-based) |
| **Grafana** | Plataforma de visualização de dados e criação de dashboards |
| **Exporter** | Componente que expõe métricas de um serviço para o Prometheus |
| **Node Exporter** | Exporter para métricas de servidor (CPU, RAM, disco, rede) |
| **Loki** | Sistema de agregação de logs (Grafana Labs) |
| **Jaeger** | Plataforma de distributed tracing |
| **OpenTelemetry** | Framework unificado para métricas, logs e traces |
| **CloudWatch** | Serviço de monitoramento gerenciado da AWS |

---

## SRE e Confiabilidade

| Termo | Definição |
|-------|-----------|
| **SLI** (Service Level Indicator) | Métrica que mede a qualidade do serviço |
| **SLO** (Service Level Objective) | Meta interna para um SLI |
| **SLA** (Service Level Agreement) | Contrato formal com o cliente sobre disponibilidade |
| **Error Budget** | Margem de erro permitida antes de violar o SLO |
| **MTTR** (Mean Time to Recover) | Tempo médio para recuperar de uma falha |
| **MTTD** (Mean Time to Detect) | Tempo médio para detectar uma falha |
| **Toil** | Trabalho manual, repetitivo e automatizável |

---

## Dashboard e Visualização

| Termo | Definição |
|-------|-----------|
| **Dashboard** | Painel visual que agrupa métricas e gráficos |
| **Panel** | Componente individual dentro de um dashboard (gráfico, tabela) |
| **Data source** | Origem dos dados consultados pelo Grafana |
| **Annotation** | Marcação em um gráfico indicando um evento (deploy, incidente) |
| **Variable** | Parâmetro dinâmico em dashboards (filtro por ambiente, serviço) |
