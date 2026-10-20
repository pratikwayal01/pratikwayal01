# Open Source Contributions

## Merged

### [kubernetes-sigs/external-dns#6755](https://github.com/kubernetes-sigs/external-dns/pull/6755) — Gateway API TCPRoute source migrated to v1
- Fixes [#6749](https://github.com/kubernetes-sigs/external-dns/issues/6749): the TCPRoute informer still watched `gateway.networking.k8s.io/v1alpha2`, which Gateway API v1.6+ no longer serves on the Standard channel — so the source failed cache sync and external-dns crashlooped.
- Mirrored the earlier TLSRoute migration (#6367): informer, types and TypeMeta moved to `v1`, test fakes updated, docs version table corrected.
- Verified against Gateway API v1.6.2 (TCPRoute graduated to Standard in v1.6.0; `v1alpha2` deprecated, removal pending).
- First merged OSS PR. 🎉

### [external-secrets/external-secrets#6999](https://github.com/external-secrets/external-secrets/pull/6999) — Vault KV metadata path fallback fix
- Fixes [#6968](https://github.com/external-secrets/external-secrets/issues/6968): a Vault `PushSecret` deadlocked because metadata was read from a path that did not account for the mount prefix, so the versioned secret metadata 404'd instead of resolving.
- `buildMetadataPath` now strips the mount prefix, with a fallback to the legacy metadata path for setups that relied on the old lookup.
- Covered by `make test` + `make check-diff`. First merged PR outside external-dns. 🎉

### [clastix/cluster-api-control-plane-provider-kamaji#425](https://github.com/clastix/cluster-api-control-plane-provider-kamaji/pull/425) — configurable security contexts for the control plane
- Fixes [#368](https://github.com/clastix/cluster-api-control-plane-provider-kamaji/issues/368): `KamajiControlPlane` had no way to set a pod or container `securityContext`, so the control plane could not run under a restricted Pod Security Standard.
- Ports [clastix/kamaji#1181](https://github.com/clastix/kamaji/pull/1181): adds `spec.deployment.podSecurityContext` and `spec.deployment.containerSecurityContexts` and forwards them to the `TenantControlPlane`.
- Regenerated deepcopy, CRDs and the single-file installer; `make test` and the full CI suite pass.

## In review

### [traefik/traefik-helm-chart#2042](https://github.com/traefik/traefik-helm-chart/pull/2042) — app.kubernetes.io/version label
- Fixes [#2029](https://github.com/traefik/traefik-helm-chart/issues/2029): the chart set name, instance, chart and managed-by labels but not the application version, so rollouts could not be tracked by label.
- Added `app.kubernetes.io/version` to the `traefik.labels` helper, resolved through a new `traefik.appVersion` template that follows the running image (image.tag, versionOverride, marketplace, Hub) rather than only `appVersion`, and sanitized to a valid label value.
- Deliberately kept out of the immutable selector. Covered by exact unit tests per version source.

### [argoproj/argo-cd#29728](https://github.com/argoproj/argo-cd/pull/29728) — multi-source autosync uses spec revisions
- Auto-sync for multi-source apps compared against stale sync-status revisions instead of the spec's target revisions; now uses the spec. Includes regression test.

### [BerriAI/litellm#41801](https://github.com/BerriAI/litellm/pull/41801) — cost calculator fix
- Fixes incorrect cost computation in `cost_calculator.py`, with regression tests.
