# Alertmanager

## O que é Alertmanager?

Alertmanager é o componente do ecossistema Prometheus responsável por receber,
agrupar e encaminhar alertas para canais de notificação.

## Exemplo de regras de alerta (`alert.rules`)

```yaml
groups:
  - name: infra-alerts
    rules:
      - alert: HighCpuUsage
        expr: node_cpu_seconds_total{mode="idle"} < 0.2
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "CPU alta em {{ $labels.instance }}"
          description: "A CPU está acima de 80% por mais de 5 minutos."
```

## Exemplo de configuração do Alertmanager (`alertmanager.yml`)

```yaml
route:
  receiver: 'team-notifications'
  routes:
    - match:
        severity: warning
      receiver: 'slack-warning'
    - match:
        severity: critical
      receiver: 'slack-critical'

receivers:
  - name: 'team-notifications'
  - name: 'slack-warning'
    slack_configs:
      - channel: '#infra-warning'
  - name: 'slack-critical'
    slack_configs:
      - channel: '#infra-critical'
```

## Boas práticas de alertas

- configurar alertas acionáveis e claros
- evitar alertas de baixo valor ou de curto prazo
- usar `for` para reduzir flapping
- agrupar alertas similares para reduzir ruído
- definir níveis de severidade (`warning`, `critical`)
