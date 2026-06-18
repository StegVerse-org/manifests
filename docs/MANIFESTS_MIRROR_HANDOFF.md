# Manifests Mirror Handoff

## Purpose

This handoff lets the next build session continue manifest-driven pricing, package, and configuration alignment without needing prior chat context.

## Current Goal

```text
Goal: canonical pricing manifest activation and downstream consumer alignment
Repository: StegVerse-org/manifests
Primary consumer repositories: StegVerse-Labs/Site, StegVerse-org/StegVerse-SDK
Canonical file: pricing.json
Activation state: canonical_pricing_manifest_present_site_consumer_partially_aligned
```

## Source-of-Truth Contract

The manifests repository is the commercial and configuration source of truth for shared StegVerse surfaces.

```text
pricing.json = canonical pricing data
packages.json = future package/version/release-channel data
tiers.json = future entitlement matrix data
```

Consumers may render, cache, validate, or generate derived files from these manifests, but they must not become independent source-of-truth copies.

## Current Pricing Manifest State

```text
pricing.json exists at repository root.
_schema is stegverse-pricing-v2.
pricing.json includes audit, sdk, platform, calculator, value_tiers, economic_model, and notes.
```

## Downstream Site State

```text
StegVerse-Labs/Site/assets/js/pricing-fetcher.js fetches the canonical raw pricing manifest first.
StegVerse-Labs/Site/pricing.html is manifest-driven.
StegVerse-Labs/Site/pricing-dynamic.html has been added as a manifest-driven compatibility route.
```

The Site fetcher must not embed full pricing tiers. If the canonical manifest cannot be loaded, the consumer should show an operational error rather than stale pricing.

## Required Canonical Raw URL

```text
https://raw.githubusercontent.com/StegVerse-org/manifests/main/pricing.json
```

## Verification Commands Or Manual Checks

```text
1. Open raw pricing URL and confirm JSON renders.
2. Confirm _schema is stegverse-pricing-v2.
3. Confirm tiers.audit, tiers.sdk, and tiers.platform exist.
4. Open Site pricing.html and confirm pricing cards render.
5. Open Site pricing-dynamic.html and confirm the compatibility route renders.
6. Make a harmless pricing.json note change and confirm Site rendering updates without editing Site HTML.
```

## Pending Work

```text
1. Add JSON schema validation for pricing.json.
2. Add CI validation for pricing.json, packages.json, and tiers.json as those files mature.
3. Confirm StegVerse-SDK derives pricing docs or displays from pricing.json.
4. Add generated pricing docs only if clearly marked as derived artifacts.
5. Add packages.json and tiers.json schemas when their model becomes concrete.
6. Add account monitoring targets once ops@stegverse.org and security@stegverse.org exist.
```

## Cross-Repo Activation Boundary

The manifest-driven pricing path can be marked activated only after:

```text
1. pricing.json raw URL resolves successfully.
2. Site pricing.html renders from pricing.json.
3. Site pricing-dynamic.html renders or routes to the same manifest-driven pricing surface.
4. SDK pricing surface is confirmed to derive from pricing.json.
5. One manifest edit updates all visible pricing surfaces without editing consumer HTML/docs.
6. Monitoring exists for pricing.json raw URL and pricing page render health.
```

## Current Delta

```text
Resolved: pricing.json exists in StegVerse-org/manifests.
Resolved: manifests README now states consumers must not render stale embedded pricing as canonical.
Resolved: Site pricing-fetcher.js uses pricing.json as canonical and rejects unsupported schemas.
Resolved: Site pricing.html is manifest-driven.
Resolved: Site pricing-dynamic.html exists as a manifest-driven compatibility route.
Pending: SDK pricing alignment verification.
Pending: raw URL and deployed Site render verification after GitHub Pages refresh.
Pending: schema validation and CI.
Pending: ops/security email and monitoring integration.
```

## Archive Readiness

This handoff contains the repo state, source-of-truth boundary, downstream consumer status, verification path, pending work, and activation boundary needed to continue. The prior chat thread is no longer required for forward progress once this file is present in the repository.
