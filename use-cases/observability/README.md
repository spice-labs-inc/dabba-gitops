# observability

Opt-in logs/metrics/traces stack. Enable it with `observability.enabled: true` in
your dabba config; dabba then adds this use-case to the cluster's Flux selection.

## What it deploys

| Component | Role |
|-----------|------|
| [Vector](https://vector.dev) (DaemonSet) | Collects every pod's logs and ships them to the backend. The sink is the pluggable seam — point it at a different backend or add alerting here. |
| [OpenTelemetry Collector](https://opentelemetry.io/docs/collector/) | Receives OTLP traces/metrics from apps (`otel-collector.observability.svc:4317`) and forwards them to the backend. |
| [OpenObserve](https://openobserve.ai) | Self-hosted, single-binary backend + UI for logs/metrics/traces. Reached at `https://o2.<domain>` (gateway). |

## License note — OpenObserve is AGPL-3.0

OpenObserve is licensed **AGPL-3.0**. Running it unmodified — which is all dabba does
(it deploys the stock container; it does not modify or link its code) — carries **no
copyleft obligation**, and it does **not** affect dabba's or your application's license.
The AGPL network-source clause only triggers if you *modify* OpenObserve and serve the
modified version to others.

That said, some organizations have blanket AGPL policies. The backend is a **swap point**
(Vector's sink / the OTEL exporter), so if you need a permissive self-hosted alternative,
Apache-2.0 options like [Quickwit](https://quickwit.io) or
[VictoriaLogs](https://victoriametrics.com/products/victorialogs/) drop in by repointing
the Vector sink and the OTEL exporter — the rest of the pipeline is unchanged.

## Tier-0 caveats

Ephemeral storage (`emptyDir`, data is lost on pod restart). The admin login is
`admin@dabba.local`; the password is a per-env random in OpenBao — `dabba secret get
dabba/openobserve`. Not production-hardened as-is.
