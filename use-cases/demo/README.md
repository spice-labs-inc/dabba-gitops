# demo

The default use case: [podinfo](https://github.com/stefanprodan/podinfo) behind the gateway,
with its UI banner delivered from OpenBao via an ExternalSecret. It's the end-to-end smoke
test — if the banner shows the message that was written into OpenBao, then the gateway, TLS,
External Secrets, OpenBao, and Flux are all working together.

## What it deploys

| Manifest | Role |
|----------|------|
| `podinfo.yml` | the podinfo HelmRelease |
| `gateway.yml` | an HTTPRoute exposing it at `https://podinfo.<domain>` |
| `secrets.yml` | an ExternalSecret pulling the banner message from OpenBao (`secret/demo/podinfo`) |

Reachable at `https://podinfo.<domain>` (e.g. `https://podinfo.localtest.me:31443` locally).
