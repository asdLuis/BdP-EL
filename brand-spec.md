# Brand spec — Bodas de Plata · Eva & Luis

A strict monochrome invitation system: ink on paper, no chromatic accent, silver hairlines standing in for the "plata" of the silver anniversary. Print-reserved, restrained, ceremonial.

## Tokens (`:root`)

| Token | OKLch | Role |
|---|---|---|
| `--bg` | `oklch(0.985 0.0015 285)` | paper white — page field |
| `--surface` | `oklch(1 0 0)` | pure white — cards, form fields |
| `--fg` | `oklch(0.17 0.005 285)` | ink — primary text, never `#000` |
| `--muted` | `oklch(0.49 0.006 285)` | secondary text, captions, labels |
| `--border` | `oklch(0.9 0.004 285)` | hairlines, dividers |
| `--accent` | `oklch(0.17 0.005 285)` | ink — the only "accent"; monochrome by design |

Derived (defined in `:root`, never as raw hex elsewhere):

- `--silver` `= color-mix(in oklch, var(--fg) 42%, var(--bg))` — the metallic nod to 25 years, used for the monogram ring, ornamental rules and the ampersand.
- `--accent-soft`, `--fg-soft` — as in the seed.

## Type

- **Display** — `'Iowan Old Style', 'Charter', Georgia, 'Times New Roman', serif`. High-contrast old-style; carries the names and the "XXV".
- **Body** — `-apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif`. Quiet, legible on phones.
- **Mono** — `ui-monospace, 'JetBrains Mono', 'SF Mono', Menlo, monospace`. Dates, times, eyebrows, deadline stamps — letterspaced uppercase.

## Posture rules (observed)

1. **One accent, and it is ink.** The palette never leaves black / white / grey. Emphasis comes from scale, letterspacing and restraint — not colour.
2. **Silver is a line, not a colour.** `--silver` appears only as 1px ornamental rules, the monogram ring and the ampersand; never as a fill behind text.
3. **Ceremonial whitespace.** Sections breathe at `clamp(48px, 8vw, 96px)`; the cover is intentionally near-empty.
4. **Mono for facts, serif for names.** Every date, hour and deadline is mono uppercase; every name and headline is display serif.
5. **Reserved-colour code is shown, not told.** Dress-code exclusions render as the tone itself — a pale swatch in that colour, struck through — so guests read the tone before the rule, never as a saturated colour chip.
