# Royal-blue recolor — brief for Claude Code

## Goal
Recolor the existing Beitan Music Foundation site to a **royal-blue + gold** palette.
**Only the color system changes.** Do NOT touch HTML structure, copy, fonts, layout,
spacing, animations, or JS. Keep the existing `data-theme` dark/light toggle working.
Dark is the primary/default theme; light is the alternate.

Files in scope: `index.html`, `exhibition-stradivari.html` (and any other pages sharing
the same CSS token system — apply the same mapping).

## Palette tokens (source of truth)

### Dark theme
| Role            | HEX / value                     |
|-----------------|---------------------------------|
| Background base | `#13235A`                       |
| Band / section  | `#18306E`                       |
| Deepest (nav, footer, deep panels) | `#0E1B45`    |
| Card surface    | `#1F3A8A`                       |
| Feature module (e.g. Archinto) | `#18306E`        |
| Text (primary)  | `#EDF1FB`                       |
| Text muted      | `rgba(237,241,251,.74)`         |
| Text faint      | `rgba(237,241,251,.50)`         |
| Gold (accent)   | `#D7B36B`                       |
| Gold deep       | `#C9A227`                       |
| Hairline        | `rgba(237,241,251,.16)`         |
| Hairline soft   | `rgba(237,241,251,.08)`         |
| Feature visual gradient | `linear-gradient(135deg,#22409C,#13235A)` |

### Light theme (much lighter)
| Role            | HEX / value                     |
|-----------------|---------------------------------|
| Background base | `#EDF2FB`                       |
| Band / section  | `#E1E9F7`                       |
| Deepest (nav, footer) | `#D6E1F3`                 |
| Card surface    | `#FFFFFF`                       |
| Feature module  | `#DCE4F5`                       |
| Text (primary)  | `#16285C`                       |
| Text muted      | `rgba(22,40,92,.76)`            |
| Text faint      | `rgba(22,40,92,.50)`            |
| Gold (accent)   | `#A9822F`                       |
| Gold deep       | `#8C6A1E`                       |
| Hairline        | `rgba(22,40,92,.16)`            |
| Hairline soft   | `rgba(22,40,92,.08)`            |
| Feature visual gradient | `linear-gradient(135deg,#C9D6F0,#E5ECF8)` |

Accent rule: gold on blue is the only accent (buttons, eyebrows, section titles,
links, key headings). No red/bordo/mahogany/amber anywhere.

## index.html — variable mapping
Remap the `:root` (dark default) and `html[data-theme="light"]` token blocks:

Dark `:root`:
- `--carbon` → `#13235A`
- `--carbon-2` → `#0E1B45`
- `--mahogany` → `#18306E`
- `--mahogany-2` → `#13235A`
- `--gold` → `#D7B36B`
- `--gold-bright` → `#C9A227`
- `--amber` → `#C9A227`
- `--slate` → `rgba(237,241,251,.50)`
- `--ivory` → `#EDF1FB`
- `--ivory-mute` → `rgba(237,241,251,.74)`
- `--ivory-faint` → `rgba(237,241,251,.50)`
- `--line` → `rgba(237,241,251,.16)`
- `--line-soft` → `rgba(237,241,251,.08)`

Light `html[data-theme="light"]`:
- `--carbon` → `#EDF2FB`; `--carbon-2` → `#D6E1F3`
- `--mahogany` → `#E1E9F7`; `--mahogany-2` → `#DCE4F5`
- `--gold` → `#A9822F`; `--gold-bright` → `#8C6A1E`; `--amber` → `#8C6A1E`
- `--slate` → `rgba(22,40,92,.50)`
- `--ivory` → `#16285C`; `--ivory-mute` → `rgba(22,40,92,.76)`; `--ivory-faint` → `rgba(22,40,92,.50)`
- `--line` → `rgba(22,40,92,.16)`; `--line-soft` → `rgba(22,40,92,.08)`

Notes:
- The `.bm-logo .f` gold gradient (`#DFBA73 → #B08D57 → #85642E`): re-tune to a brighter
  champagne range `#E6C988 → #D7B36B → #B68A38` so it reads on deep blue.
- Hero photo, `.vignette`, and `.fade` overlays must STAY cinematic-dark in both themes —
  do not tint them blue. The `.fade` bottom gradient should fade to `var(--carbon)` so it
  still merges into the (now blue) page.

## exhibition-stradivari.html — variable mapping
Dark `html[data-theme="dark"]` and light `:root`:
- `--paper` → dark `#13235A` / light `#EDF2FB`
- `--paper-2` → dark `#18306E` / light `#E1E9F7`
- `--paper-3` → dark `#0E1B45` / light `#D6E1F3`
- `--ink` → dark `#EDF1FB` / light `#16285C`
- `--ink-2` → dark `rgba(237,241,251,.74)` / light `rgba(22,40,92,.76)`
- `--ink-3` → dark `rgba(237,241,251,.50)` / light `rgba(22,40,92,.50)`
- `--bordo` → `#D7B36B` (now the gold accent)  — both themes a gold tone (dark `#D7B36B`, light `#A9822F`)
- `--bordo-2` → dark `#C9A227` / light `#8C6A1E`
- `--bordo-deep` → dark `#0E1B45` / light `#D6E1F3`
- `--brass` → dark `#D7B36B` / light `#A9822F`
- `--gold` → dark `#C9A227` / light `#8C6A1E`
- `--line` → dark `rgba(237,241,251,.16)` / light `rgba(22,40,92,.16)`
- `--line-2` → dark `rgba(237,241,251,.08)` / light `rgba(22,40,92,.08)`

Hardcoded hex to replace (these were the red feature panels):
- `#D7262D` used as a **panel background** (`.archinto`, `.cta-band`, `footer`) → `#18306E`
- `#D7262D` used as **text color** (`.split .txt h3`, `.split .txt .eyebrow`, `.split .txt h3 em`) → gold `#D7B36B` (dark) — make it theme-aware so light uses `#A9822F`
- `.ex-hero` / `.archinto .vis` brown image backings (`#2a1c1e`, `#2a1113`) → keep dark, or
  retune to `#101A3A` so photo placeholders read blue-dark, not brown
- Warm caption/eyebrow tints inside dark panels (`#E7C9AE`, `#EBD0B6`, `#EFE0D6`, `#F3E3D8`)
  → shift to ivory-blue `#EDF1FB` / muted `rgba(237,241,251,.74)` and gold `#D7B36B`
- `<meta name="theme-color">` → `#13235A`

## Constraints
- Change colors only. No edits to text, markup, class names, fonts, animations, JS.
- Keep WCAG AA: body text on blue must stay ≥ 4.5:1 (the `#EDF1FB` on `#13235A` pair passes).
  Gold `#D7B36B` is for accents/large text only, not long body copy.
- Both themes must be fully consistent — no leftover red/bordo/mahogany/amber/paper-cream.
- Test the `data-theme` toggle: every section, button, hairline, and card recolors correctly
  in BOTH dark and light.

## Acceptance checklist
- [ ] No `#6E1E2A` / `#892532` / `#551722` / `#D7262D` / `#C24350` / cream `#F3ECDF`-as-bg left
- [ ] Dark default renders deep blue `#13235A` background, gold accents
- [ ] Light theme renders pale blue `#EDF2FB`, navy text, darker gold
- [ ] Hero photos/overlays remain cinematic-dark (not blue-washed)
- [ ] Theme toggle flips all tokens cleanly on both pages
- [ ] Buttons, eyebrows, section numbers, links all use gold accent

---

## One-line command (paste into Claude Code)
> Recolor this site to a royal-blue + gold palette using the exact tokens in
> `2026-06-21-royal-blue-recolor-prompt.md`. Change ONLY the CSS color system
> (`:root` and `html[data-theme=...]` variable blocks plus the hardcoded red/cream
> hexes) in `index.html` and `exhibition-stradivari.html`. Do not change HTML,
> copy, fonts, layout, or JS. Dark stays default. Keep the theme toggle working,
> keep hero photos cinematic-dark, and verify WCAG AA for body text. Follow the
> variable mapping and acceptance checklist in that file.
