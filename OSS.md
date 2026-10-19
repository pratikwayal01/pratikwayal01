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

## In review

### [argoproj/argo-cd#29728](https://github.com/argoproj/argo-cd/pull/29728) — multi-source autosync uses spec revisions
- Auto-sync for multi-source apps compared against stale sync-status revisions instead of the spec's target revisions; now uses the spec. Includes regression test.

### [BerriAI/litellm#41801](https://github.com/BerriAI/litellm/pull/41801) — cost calculator fix
- Fixes incorrect cost computation in `cost_calculator.py`, with regression tests.
