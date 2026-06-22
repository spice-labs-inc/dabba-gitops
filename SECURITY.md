# Security Policy

## Reporting a vulnerability

Please **do not open a public issue** for security problems. Report privately through GitHub:
on the repository's **Security** tab, choose **Report a vulnerability**. We'll acknowledge the
report and work a fix with you before any public disclosure.

## Supported versions

Security fixes target the latest released tag.

## Notes

This repository is the platform's gitops content (Flux manifests). It contains **no secrets** —
credentials are generated per-environment by the [`dabba`](https://github.com/spice-labs-inc/dabba)
CLI and delivered at runtime via OpenBao + External Secrets; manifests reference them by
`secretKeyRef`, never inline. The `openbao-dev` component is **local-only** dev-mode OpenBao
(documented in its README). The broader platform security model is in the
[dabba SECURITY policy](https://github.com/spice-labs-inc/dabba/blob/main/SECURITY.md).
