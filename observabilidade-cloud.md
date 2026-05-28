# Observabilidade em Cloud

## Por que observabilidade é importante na nuvem?

Ambientes em nuvem são dinâmicos e escaláveis, o que torna essencial o monitoramento
centralizado de métricas, logs e eventos.

## Componentes típicos em cloud

- instâncias e VMs
- contêineres e clusters Kubernetes
- serviços gerenciados (DB, filas, storage)
- redes e balanceadores

## Exemplo de fluxo em AWS

1. Aplicação em EC2 ou ECS expõe métricas
2. Prometheus coleta métricas ou usa exportadores
3. Logs são enviados para um serviço central (CloudWatch, Loki, ELK)
4. Grafana exibe dashboards e alerta via Alertmanager

## Integrando com serviços gerenciados

- use AWS CloudWatch Metrics para métricas nativas de serviços
- use CloudWatch Logs para centralizar logs
- combine métricas do Prometheus e do CloudWatch no Grafana

## Vantagens em nuvem

- escalabilidade de coleta e armazenamento
- maior visibilidade de recursos mutáveis
- capacidade de usar serviços gerenciados para logs e alertas
