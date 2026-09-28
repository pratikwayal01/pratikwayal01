# Open Source Contributions

## Merged

### [kubernetes-sigs/external-dns#6755](https://github.com/kubernetes-sigs/external-dns/pull/6755) — Gateway API TCPRoute source migrated to v1
- Fixes [#6749](https://github.com/kubernetes-sigs/external-dns/issues/6749): the TCPRoute informer still watched `gateway.networking.k8s.io/v1alpha2`, which Gateway API v1.6+ no longer serves on the Standard channel — so the source failed cache sync and external-dns crashlooped.
- Mirrored the earlier TLSRoute migration (#6367): informer, types and TypeMeta moved to `v1`, test fakes updated, docs version table corrected.
- Verified against Gateway API v1.6.2 (TCPRoute graduated to Standard in v1.6.0; `v1alpha2` deprecated, removal pending).
- First merged OSS PR. 🎉

## In review

### [external-secrets/external-secrets#6999](https://github.com/external-secrets/external-secrets/pull/6999) — Vault KV metadata path fallback fix
- Corrects the metadata read path when Vault namespaces/prefixes are in play, so versioned secret metadata resolves instead of 404ing.

### [argoproj/argo-cd#29728](https://github.com/argoproj/argo-cd/pull/29728) — multi-source autosync uses spec revisions
- Auto-sync for multi-source apps compared against stale sync-status revisions instead of the spec's target revisions; now uses the spec. Includes regression test.

### [BerriAI/litellm#41801](https://github.com/BerriAI/litellm/pull/41801) — cost calculator fix
- Fixes incorrect cost computation in `cost_calculator.py`, with regression tests.
