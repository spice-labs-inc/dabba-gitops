# selfsigned-issuer

A `dabba-ca` ClusterIssuer backed by a generated in-cluster root CA (bootstrapped via a
self-signed issuer). Gateways reference it through the `${cluster_issuer}` substitution
variable. Browsers will warn unless the root (secret `dabba-root-ca` in `cert-manager`)
is imported into the host trust store.

Cloud overlays use an ACME issuer instead.
