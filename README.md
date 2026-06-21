# StegVerse Manifests

![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)

Canonical source repository for StegVerse ecosystem manifests, pricing data, package metadata, configuration declarations, and downstream-consumer contracts.

This repository is a data source. It does not execute governance decisions or create admission authority.

---

## Repositories that consume this

| Repo | Purpose | Files used |
|---|---|---|
| `StegVerse-Labs/Site` | Marketing site, demo, docs | `pricing.json`, `packages.json` |
| `StegVerse-org/StegVerse-SDK` | SDK distribution, docs | `pricing.json`, `packages.json`, `tiers.json` |
| `GCAT-BCAT-Engine` | Engine builds, CI | `packages.json` |

---

## Schema

### `pricing.json`

```json
{
  "_schema": "stegverse-pricing-v2",
  "_updated": "ISO-8601 timestamp",
  "currency": "USD",
  "economic_model": {},
  "tiers": {},
  "calculator": { "enabled": true },
  "notes": []
}
```

Required pricing consumers must treat `pricing.json` as canonical. Pages, SDK docs, calculators, and product surfaces may render from this file, but they must not maintain independent pricing tier copies.

### `packages.json`

Defines SDK versions, release channels, dependency matrices, and package references.

### `tiers.json`

Defines feature entitlement matrices and tier unlock behavior.

---

## Update process

1. Propose change through a pull request.
2. Run TV/TVC validation and schema validation.
3. Review governance impact.
4. Merge after approval.
5. Propagate through downstream consumers.

---

## TV/TVC integration

Write access to this repo is managed through TrustVault / TrustVaultController patterns:

- no long-lived tokens in files;
- commits should be signed or traceable through controlled artifacts;
- iOS, desktop, and CI workflows must preserve manifest integrity.

---

## Cache behavior

Manifests are fetched with `cache: no-store` by default.

For production surfaces, consumers should use short CDN TTLs, versioned URLs for major releases, and ETag support for conditional fetches.

---

## Failure behavior

If the primary source fails, consumers should show a clear operational error rather than silently rendering stale embedded pricing. This preserves the one-edit pricing model and prevents drift between the Site, SDK, and future commercial surfaces.

A local or generated fallback may exist for development, but it must be visibly marked as non-canonical and must not become a second pricing source of truth.

---

## Boundary rule

Manifests declare data and configuration. They do not create execution authority, admission authority, endorsement, compatibility recognition, provenance recognition, collaboration, or validation.
