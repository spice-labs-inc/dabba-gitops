# openbao-dev

In-cluster [OpenBao](https://openbao.org/) in dev mode: in-memory storage, no seal, plus an
`openbao` ClusterSecretStore so External Secrets can read from it. OpenBao is the Linux
Foundation's Apache-2 fork of Vault and is API-compatible, so the ESO `vault` provider works
against it unchanged. The root token is generated per-environment by the dabba CLI and
substituted in via `${openbao_root_token}` from `cluster-vars` (retrieve it with
`dabba secret get local/openbao-root`).

**Local clusters only.** Dev mode persists nothing and holds its root token in a plaintext
ConfigMap — fine for a throwaway local cluster, not for anything real. Cloud overlays use an
external OpenBao/Vault with a proper seal instead.
