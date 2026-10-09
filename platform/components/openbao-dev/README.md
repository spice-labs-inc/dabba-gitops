# openbao-dev

In-cluster [OpenBao](https://openbao.org/) in dev mode: in-memory storage, no seal, plus an
`openbao` ClusterSecretStore so External Secrets can read from it. OpenBao is the Linux
Foundation's Apache-2 fork of Vault and is API-compatible, so the ESO `vault` provider works
against it unchanged. The root token is generated per-environment by the dabba CLI and
substituted in via `${openbao_root_token}` from `cluster-vars` (retrieve it with
`dabba secret get local/openbao-root`).

**Demos only.** Dev mode persists nothing, has no seal, and its root token sits in plaintext in
the `cluster-vars` ConfigMap. It is reachable only inside the cluster (External Secrets, and
`dabba secret` via `kubectl exec`). The separate `openbao-dev-ui` component publishes it at
`bao.${domain}` on the gateway. Only the local overlay includes that, for workstation clusters;
remove it there if your cluster is reachable from the internet. For anything real, see the repo
README.
