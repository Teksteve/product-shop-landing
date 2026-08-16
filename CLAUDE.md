# product-shop-landing

The Product Shop's landing page. Static HTML, no build step, no dependencies.
Open `index.html` in a browser to see changes.

## Layout

| Path | What it is |
|---|---|
| `index.html` | The landing page. Single file, inline `<style>`, no JS. Carries `<meta name="robots" content="noindex">`. |
| `preview/index.html` | Public site preview, linked from the footer. No work cards. |
| `pricescout/` | Older standalone PriceScout prototype + `thumb.svg`. Stale and off-brand (blue `#2A56E8`, Archivo/Inter) — it predates the shop styling and is not linked from the landing page. |

## The work section

The `<section>` at the bottom of `index.html` indexes what the shop is building.
Each project is an `.entry` wrapping two parts:

- `a.row` — the whole-row link to the project hub artifact. Owns the name, description, tags, and status.
- `.pieces` — a mono strip of links to the individual artifacts under that project.

`.entry` carries the bottom divider so the row and its pieces read as one block.
**Do not nest an `<a>` inside `a.row`** — that is why pieces live in a sibling
div rather than inside the row.

## Published artifacts

All are private to the account. Anyone else opening these links gets nothing —
they must be shared before the landing page works for a visitor.

| Artifact | UUID | Linked from |
|---|---|---|
| The Product Shop | `7470ef20-5326-4617-95d5-72209d696182` | — (this page, published) |
| Quench — Project | `43188124-150a-4baf-ae10-6944b19b823d` | Quench row |
| Quench — Prototype v2 | `70f9b33f-7ca9-4f81-b577-a74d1f474693` | Quench pieces |
| Quench — App Screens | `3fd56fe0-43de-4c6c-b3e7-343c5ce919b8` | not linked |
| PriceScout — Project | `6819cb25-bf13-449f-ae6b-da445d080333` | PriceScout row |
| PriceScout — Prototype | `5abe7349-cfc8-4355-917b-267a0bcf43b0` | PriceScout pieces |

Quench — Prototype v2 is a before/after harness: the same iOS prototype twice,
toggled, showing what the design critic changed and tracing each fix to a rule
in `quench-design-system.md`.

## Conventions

- Colour, type, and spacing come from the `:root` custom properties at the top
  of the file. Every colour must be defined there, with a
  `@media (prefers-color-scheme:dark)` counterpart. Both themes get checked.
- Type: serif for names and headings, mono for labels and metadata, sans for prose.
- No em dashes in copy. Commas or full stops instead.
- Client work stays anonymous until the client agrees to be listed.
- Respect `prefers-reduced-motion`; transitions are disabled under it.

## Verifying a change

Screenshot both themes with Playwright before calling a visual change done:

```js
import { chromium } from 'playwright';
const b = await chromium.launch({ executablePath: '/opt/pw-browsers/chromium' });
const p = await b.newPage({ viewport:{width:900,height:1200}, colorScheme:'dark' });
await p.goto('file:///home/user/product-shop-landing/index.html');
await p.screenshot({ path:'out.png', fullPage:true });
```
