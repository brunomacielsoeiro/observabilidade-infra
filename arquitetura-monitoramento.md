# Arquitetura de Monitoramento

## Fluxo de monitoramento

- `app` → métricas → Prometheus → Grafana
- A aplicação expõe métricas que são coletadas pelo Prometheus.
- O Grafana consome essas métricas para criar dashboards e relatórios.

## Onde entram os logs

- Logs são gerados pela aplicação e pelos componentes de infraestrutura.
- Eles complementam as métricas com detalhes de eventos e ocorrências.
- Logs podem ser enviados para ferramentas como Elasticsearch, Loki ou um sistema de log central.

## Alertas

- Alertas são regras que verificam métricas e condições do sistema.
- Quando uma métrica ultrapassa um limiar, um alerta é disparado.
- Alertas podem ser enviados por e-mail, Slack, PagerDuty ou outras integrações.

## Exemplo de arquitetura simples

1. Aplicação/Serviço expõe métricas e logs.
2. Prometheus coleta métricas de endpoints configurados.
3. Logs são agregados em um armazenamento centralizado.
4. Grafana cria dashboards com métricas do Prometheus.
5. Sistema de alertas observa métricas e emite notificações.

## Boas práticas de monitoramento

- Coletar métricas relevantes, não apenas todas as métricas possíveis.
- Usar labels consistentes em Prometheus para facilitar consultas.
- Definir alertas acionáveis e evitar falsos positivos.
- Manter dashboards claros e voltados para operação.
- Correlacionar métricas e logs para investigação eficiente.

## Observabilidade como prática

A observabilidade deve ser parte contínua da infraestrutura:

- validar mudanças com métricas e dashboards,
- investigar incidentes com logs e traces,
- aprender com eventos e ajustar alertas.
