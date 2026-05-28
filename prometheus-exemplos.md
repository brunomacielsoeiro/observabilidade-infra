# Exemplos de Configuração do Prometheus

## O que é um `scrape_config`

O Prometheus usa `scrape_configs` para descobrir e coletar métricas de targets.
Cada target é uma fonte de métricas que expõe um endpoint HTTP, geralmente `/metrics`.

## Exemplo básico de `prometheus.yml`

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: 'app-principal'
    static_configs:
      - targets: ['app01:9100', 'app02:9100']

  - job_name: 'node-exporter'
    static_configs:
      - targets: ['node1:9100', 'node2:9100']
```

## Exportadores

Exportadores convertem métricas de serviços que não falam Prometheus nativamente.
Exemplos comuns:

- `node_exporter` para métricas de servidor
- `blackbox_exporter` para checagens de disponibilidade
- `mysql_exporter` para bancos de dados

## Labels e boas práticas

As labels permitem filtrar e agrupar métricas:

```yaml
- job_name: 'app-principal'
  static_configs:
    - targets: ['app01:9100']
      labels:
        environment: 'homolog'
        service: 'painel-vendas'
```

### Boas práticas

- usar `scrape_interval` consistente
- nomear jobs de forma clara
- aplicar labels úteis como `environment`, `service` e `region`
- não coletar métricas desnecessárias (evita sobrecarga)
