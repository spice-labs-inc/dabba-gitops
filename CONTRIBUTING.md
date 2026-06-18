# Contributing to dabba-gitops

Thank you for your interest. These manifests are maintained as part of our own infrastructure
and shared in the hope they are useful. We welcome bug reports, questions, and documentation
fixes. For features, please open an issue first so we can align before you invest time — and
note that reviews may be slow. The maintainers make the final call on what fits the project.

## Reporting bugs

Open a [new issue](../../issues/new) with a clear title, what you expected vs. what happened,
and relevant output (`flux get kustomizations`, `kubectl describe` of the failing object).

## Working in this repo

These are the FluxCD manifests for the [dabba](https://github.com/spice-labs-inc/dabba)
platform, reconciled from `clusters/<name>/`. Two conventions keep it reusable:

- **The base stays cloud-free.** `crds/base` and `platform/base` must not contain anything
  substrate- or cloud-specific. Cloud/local concerns (DNS, cert issuers, load balancers,
  secret backends) live in `platform/components/` and are composed by overlays
- **Per-cluster values come from substitution**, not hardcoding — manifests reference
  `${domain}`, `${cluster_issuer}`, etc., supplied via the `cluster-vars` ConfigMap with
  `postBuild.substituteFrom`

A new environment is a new `platform/overlays/<env>` + `clusters/<env>` composing the same
base with the components it needs.

## Tests and CI

- Every overlay must render: `kubectl kustomize <overlay-dir>` (components are not built
  standalone). The [dabba](https://github.com/spice-labs-inc/dabba) repo's `hack/validate.sh`
  checks them all
- `flux build` is useful for validating substitutions without a cluster

## Opening a pull request

- Reference the issue you aligned on, explain why, keep commits focused
- Confirm the affected overlays still render

## Licensing

Contributions are under the project's [Apache-2.0 license](LICENSE); by submitting, you agree
to license them under the same terms and confirm you have the right to.

## Community

Spice Labs open-source discussions are on Matrix at
https://matrix.to/#/#spice-labs:matrix.org
