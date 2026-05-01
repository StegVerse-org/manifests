# StegVerse Manifests

Single source of truth for pricing, packages, and configuration across the StegVerse ecosystem.

## Repositories That Consume This

| Repo | Purpose | Files Used |
|---|---|---|
| `StegVerse-Labs/Site` | Marketing site, demo, docs | `pricing.json`, `packages.json` |
| `StegVerse-org/StegVerse-SDK` | SDK distribution, docs | `pricing.json`, `packages.json`, `tiers.json` |
| `GCAT-BCAT-Engine` | Engine builds, CI | `packages.json` |

## Schema

### pricing.json

```json
{
  "_schema": "stegverse-pricing-v2",
  "_updated": "ISO-8601 timestamp",
  "currency": "USD",
  "economic_model": { ... },
  "tiers": {
    "audit": { "label": "...", "description": "...", "items": [...] },
    "sdk": { ... },
    "platform": { ... }
  },
  "calculator": { "enabled": true, "fields": [...], "formula": "..." },
  "notes": [...]
}
```

### packages.json

TBD — will define SDK versions, release channels, dependency matrices.

### tiers.json

TBD — will define feature entitlement matrix (what each tier unlocks).

## Update Process

1. **Propose change** — open PR against this repo
2. **TV/TVC validation** — automated check that manifest schema is valid
3. **Review** — governance approval (human or automated policy)
4. **Merge** — commit triggers downstream cache invalidation
5. **Propagate** — consuming repos fetch updated manifest on next page load

## TV/TVC Integration

Write access to this repo is managed through TrustVault/TrustVaultController:
- No long-lived tokens in files
- All commits signed via ephemeral artifacts
- Platform-agnostic — works from iOS, desktop, or CI

## Cache Behavior

Manifests are fetched with `cache: 'no-store'` by default.
For production, consider:
- Short CDN TTL (5 minutes)
- Versioned URLs for major releases: `pricing-v2.json`, `pricing-v3.json`
- ETag support for conditional fetches

## Emergency Override

If the primary source fails, the fetcher falls back to a hardcoded minimal
manifest embedded in `pricing-fetcher.js`. This ensures the pricing page
never renders completely blank.
