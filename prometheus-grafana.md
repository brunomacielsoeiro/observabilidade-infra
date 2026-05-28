# Prometheus e Grafana

## O que é Prometheus?

Prometheus é uma ferramenta de monitoramento e armazenamento de métricas em séries temporais.
Ele coleta métricas de aplicações e infraestrutura por meio de scrapes HTTP e armazena os dados
localmente em um formato eficiente.

### Características do Prometheus

- Modelo de dados baseado em séries temporais
- Consulta com linguagem PromQL
- Coleta de métricas por pull (scraping)
- Exportadores para muitos serviços e sistemas

## O que é Grafana?

Grafana é uma plataforma de visualização de dados que cria dashboards e gráficos a partir
de várias fontes, incluindo Prometheus.
Ele permite criar painéis interativos para acompanhar o desempenho de sistemas e alertas.

### Características do Grafana

- Dashboards customizáveis
- Suporte a múltiplas fontes de dados
- Painéis visuais para métricas, logs e traces
- Integração com alertas e notificações

## Como Prometheus e Grafana funcionam juntos

1. Prometheus coleta métricas de targets (aplicações, serviços, clusters).
2. As métricas são armazenadas como séries temporais.
3. Grafana consulta o Prometheus usando PromQL.
4. Grafana exibe painéis e gráficos com as métricas coletadas.

## Como coletam métricas

- Prometheus usa endpoints HTTP expostos por serviços (como `/metrics`).
- Exportadores convertem métricas de sistemas que não falam Prometheus.
- O Grafana consome essas métricas para visualização e interpretação.

## Benefícios dessa combinação

- Observabilidade em tempo real de infraestrutura
- Fácil criação de dashboards operacionais
- Suporte para alertas baseados em métricas
- Permite análise de tendências e capacidade de resposta rápida
