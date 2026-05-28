# Conceitos de Observabilidade

## O que é observabilidade?

Observabilidade é a capacidade de compreender o comportamento interno de um sistema
por meio de sinais externos gerados por ele. Em sistemas de infraestrutura e aplicações
modernas, ela permite identificar falhas, analisar desempenho e tomar decisões com base
em dados.

## Diferença entre logs, métricas e traces

### Logs

- Registros de eventos e atividades que ocorrem em um sistema.
- Normalmente são textos com informações sobre erros, avisos e operações.
- Usados para investigação detalhada de problemas e auditoria.

### Métricas

- Dados quantitativos coletados ao longo do tempo, como uso de CPU, memória ou latência.
- São estruturadas e normalmente representadas como números.
- Ideais para análise de tendência, alertas e dashboards.

### Traces

- Rastreiam a jornada de uma solicitação através de componentes de um sistema.
- Mostram o tempo gasto em cada etapa, dependências e fluxo de execução.
- Muito úteis em arquiteturas distribuídas para diagnosticar latência e falhas.

## Como eles se complementam

- Logs ajudam a entender o que aconteceu e por que aconteceu.
- Métricas mostram o estado geral do sistema e alertam para desvios.
- Traces revelam o caminho de uma transação e onde ocorreram atrasos.

## Importância na infraestrutura

Em infraestrutura, a observabilidade permite:

- detectar problemas antes que afetem os usuários,
- entender a causa raiz de incidentes,
- manter a confiabilidade e a performance de serviços.
