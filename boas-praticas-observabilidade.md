# Boas Práticas de Observabilidade

## Estruture métricas e logs com consistência

- use labels/tags padronizados: `environment`, `service`, `instance`, `region`
- nomeie métricas de forma clara: `app_request_duration_seconds`
- evite métricas com cardinalidade excessiva

## Alertas acionáveis

- crie alertas que indiquem ação concreta
- evite alertas redundantes e de baixa prioridade
- defina respostas claras para cada nível de severidade

## Dashboards eficientes

- mantenha dashboards focados em objetivos operacionais
- use gráficos simples e métricas principais
- separe dashboards de saúde geral e painéis de troubleshooting

## Logs e correlação

- centralize logs para facilitar busca e análise
- inclua identificadores de correlação (`trace_id`, `request_id`)
- use logs para aprofundar causas de incidentes identificados por métricas

## Monitoramento contínuo

- valide mudanças com métricas após deploy
- revise alertas e dashboards periodicamente
- monitore tanto disponibilidade quanto experiência de usuário
