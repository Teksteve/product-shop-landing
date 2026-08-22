# STATUS

Authoritative record of PriceScout build and design state. Update with every session that changes design or build.

Last updated: 2026-08-22

## Design canon

The deployed app is the single source of truth for PriceScout's look and feel:

- **Live app:** https://pricescout-rho.vercel.app
- **Source:** `Teksteve/pricescout` (private) — Next.js, TypeScript, Supabase, deployed via Vercel
- Everything in this repo (`product-shop-landing`) is a static preview or historical prototype, styled to match the app, never the other way around.

### Design tokens (extracted live from the deployed app, 2026-08-22)

Font: system stack (`system-ui, -apple-system, "Segoe UI", Roboto, Helvetica, Arial, sans-serif`). No webfonts.
Radii: card 20px, row 14px, badge 999px.

| Token | Light | Dark |
|---|---|---|
| bg | `#fff` | `#202123` |
| fg | `#1d1d1f` | `#f2f2f3` |
| fg-2 | `#1d1d1f99` | `rgba(242,242,243,.62)` |
| fg-3 | `#1d1d1f61` | `rgba(242,242,243,.4)` |
| rule | `#00000014` | `rgba(255,255,255,.1)` |
| surface | `#f5f5f7` | `#2b2b30` |
| good | `#d9f2e2` | `rgba(48,209,88,.16)` |
| good-ink | `#0f7b3f` | `#4cd97b` |
| wait (proposed) | `#ff9f0a24` | `rgba(255,159,10,.16)` |
| wait-ink (proposed) | `#a05a00` | `#ffb340` |

The `wait` pair is proposed by Proto-004 and not yet in the app — the app currently has no amber state.

## Current state

- `pricescout/index.html` — static preview rebuilt in the canonical design system (this commit). Shows the app hero plus the Proto-004 verdict card. Links to the live app.
- The deployed app has price comparison, deal assessment ("good deal" pill vs cross-seller spread), watchlist, and accounts — **but no Buy/Wait verdict layer yet**. Proto-004 is the design spec for that missing feature.

## Prototype history

- Proto-001 — paper/ink static page (Archivo / Inter / IBM Plex Mono). Superseded.
- Proto-002 — `pricescout-prototype-v2.jsx`, Today/Watchlist tabs, target band rail. Chat artifact, superseded visually; interaction decisions carry forward.
- Proto-003 — minimal verdict card, paper/ink. Superseded same day by the design-canon change.
- **Proto-004** — `verdict-card` in the canonical Vercel system, light+dark. Current verdict card spec.

## Verdict framework (settled decisions)

Three-way verdict: Buy Online / Buy Local Today / Wait. Color signals timing, not channel (both buy states green, wait amber). Reasoning always visible, numbered. Price and stock freshness are separate per-offer timestamps; stale stock degrades honestly to "call ahead." Track record is call-type specific ("Wait calls on memory: 74% of 19 graded"). Every verdict gets a permanent public URL. Target band rail on Wait verdicts.

## Next

1. Add the verdict layer to the app (`Teksteve/pricescout`), styled per Proto-004, including the amber wait token pair.
2. Grade and store calls so the track-record line is backed by a real graded-calls table before any accuracy claim ships.
3. RAM Market Index concept.
