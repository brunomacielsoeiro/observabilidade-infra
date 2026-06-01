# 📖 Conceitos de Observabilidade

## 1. O que é Observabilidade?

Observabilidade é a capacidade de entender o **estado interno** de um sistema a partir dos **sinais externos** que ele emite (métricas, logs, traces).

### Monitoramento vs Observabilidade

| Aspecto | Monitoramento | Observabilidade |
|---------|--------------|-----------------|
| Abordagem | "O que eu sei que pode quebrar" | "O que eu não sei que pode quebrar" |
| Perguntas | Pré-definidas (dashboards fixos) | Ad-hoc (explorar dados) |
| Foco | Alertar sobre problemas conhecidos | Investigar problemas desconhecidos |
| Exemplo | "CPU > 80% → alerta" | "Por que a latência subiu 3x às 14h?" |

---

## 2. Os 3 Pilares

```
┌─────────────────────────────────────────────────────────────┐
│                  3 PILARES DA OBSERVABILIDADE                 │
│                                                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   MÉTRICAS   │  │     LOGS     │  │    TRACES    │      │
│  │              │  │              │  │              │      │
│  │ • Numéricos  │  │ • Textuais   │  │ • Distribuído│      │
│  │ • Agregáveis │  │ • Detalhados │  │ • Temporal   │      │
│  │ • Séries     │  │ • Eventos    │  │ • Causal     │      │
│  │   temporais  │  │   discretos  │  │              │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
│                                                              │
│  "O QUÊ está       "POR QUÊ                "ONDE está       │
│   acontecendo?"     aconteceu?"              o gargalo?"     │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

---

## 3. Métricas

### O que são?

Valores **numéricos** coletados ao longo do tempo. Representam o estado quantitativo do sistema.

### Tipos de métricas

| Tipo | Descrição | Exemplo |
|------|-----------|---------|
| **Counter** | Só cresce (acumulativo) | Total de requisições |
| **Gauge** | Sobe e desce | Uso de CPU, memória |
| **Histogram** | Distribuição de valores | Latência (P50, P95, P99) |
| **Summary** | Similar ao histogram (client-side) | Duração de requests |

### Exemplos práticos

| Métrica | Tipo | O que indica |
|---------|------|-------------|
| `http_requests_total` | Counter | Volume de tráfego |
| `node_cpu_usage_percent` | Gauge | Carga do servidor |
| `http_request_duration_seconds` | Histogram | Performance |
| `node_memory_available_bytes` | Gauge | Capacidade |

### Nomenclatura (convenção Prometheus)

```
<namespace>_<nome>_<unidade>

Exemplos:
http_requests_total
http_request_duration_seconds
node_cpu_usage_percent
app_queue_messages_waiting
```

---

## 4. Logs

### O que são?

Registros **textuais** de eventos discretos que acontecem no sistema. Cada log é um evento com timestamp.

### Níveis de log

| Nível | Quando usar | Exemplo |
|-------|-------------|---------|
| `DEBUG` | Detalhes para desenvolvimento | "Query executada: SELECT..." |
| `INFO` | Operações normais | "Servidor iniciado na porta 8080" |
| `WARN` | Algo inesperado mas não crítico | "Retry #2 para serviço externo" |
| `ERROR` | Falha que precisa de atenção | "Falha ao conectar no banco" |
| `FATAL` | Sistema não pode continuar | "Porta 8080 já em uso, encerrando" |

### Log estruturado vs não estruturado

```
❌ Não estruturado:
2025-01-15 14:30:22 ERROR Falha ao processar pedido 12345

✅ Estruturado (JSON):
{
  "timestamp": "2025-01-15T14:30:22Z",
  "level": "ERROR",
  "message": "Falha ao processar pedido",
  "order_id": "12345",
  "error": "timeout connecting to payment-service",
  "trace_id": "abc123def456"
}
```

> 💡 Logs estruturados são **pesquisáveis** e **correlacionáveis** com métricas e traces.

---

## 5. Traces (Distributed Tracing)

### O que são?

Rastreiam o **caminho completo** de uma requisição através de múltiplos serviços. Mostram onde o tempo é gasto.

### Anatomia de um trace

```
Trace ID: abc-123-def-456
│
├── Span 1: API Gateway (2ms)
│   └── Span 2: Auth Service (15ms)
│       └── Span 3: User DB Query (12ms)
│
├── Span 4: Order Service (150ms)
│   ├── Span 5: Inventory Check (30ms)
│   └── Span 6: Payment Service (110ms)  ← GARGALO!
│       └── Span 7: External Payment API (105ms)
│
└── Span 8: Response (1ms)

Total: 168ms (Payment é 65% do tempo)
```

### Quando usar traces

| Cenário | Traces ajudam? |
|---------|---------------|
| Monolito simples | ❌ Não (logs bastam) |
| Microserviços (3+ serviços) | ✅ Sim |
| Latência inexplicável | ✅ Sim |
| Dependências entre serviços | ✅ Sim |
| Debug de timeout | ✅ Sim |

---

## 6. Como os 3 pilares se complementam

### Fluxo de investigação de incidente

```
1. ALERTA (métrica)
   "Error rate > 5% no serviço orders"
        │
        ▼
2. DASHBOARD (métrica)
   "Endpoint POST /orders com 503 desde 14:22"
        │
        ▼
3. TRACE
   "Requisições falhando no span payment-service (timeout)"
        │
        ▼
4. LOG
   "payment-service: connection refused to payment-gateway:443"
        │
        ▼
5. CAUSA RAIZ
   "Certificado TLS do payment gateway expirou"
        │
        ▼
6. FIX
   "Renovar certificado + adicionar alerta de expiração"
```

---

## 7. SLI, SLO e SLA

| Conceito | Significado | Exemplo |
|----------|-------------|---------|
| **SLI** (Indicator) | Métrica que mede o serviço | Latência P99, error rate |
| **SLO** (Objective) | Meta interna para o SLI | "P99 < 200ms em 99.9% do tempo" |
| **SLA** (Agreement) | Contrato com o cliente | "99.9% uptime ou crédito" |

### Relação

```
SLI (o que medimos) → SLO (nossa meta) → SLA (promessa ao cliente)

Exemplo:
SLI: disponibilidade = requests_success / requests_total
SLO: disponibilidade >= 99.95% (mensal)
SLA: se < 99.9%, cliente recebe crédito
```

---

## Resumo Visual

```
┌─────────────────────────────────────────────────────────────┐
│              OBSERVABILIDADE - RESUMO                         │
│                                                              │
│  PILARES            FERRAMENTAS        PRÁTICAS              │
│  ───────            ───────────        ────────              │
│  • Métricas         • Prometheus       • SLIs/SLOs          │
│  • Logs             • Grafana          • Alertas acionáveis  │
│  • Traces           • Loki/ELK         • Logs estruturados   │
│                     • Jaeger           • Correlação           │
│                     • Alertmanager     • Dashboards focados   │
│                     • CloudWatch                             │
│                                                              │
│  INVESTIGAÇÃO: Alerta → Dashboard → Trace → Log → Fix       │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```
