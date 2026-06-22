# Claude Code — Build Brief: Beitan Music Foundation site

**Date:** 21.06.2026
**Files in scope:** `index.html` and `exhibition-stradivari.html`
**Source audits:** `2026-06-21-audit-beitanmusicfoundation.md`, `2026-06-21-audit-exhibition-stradivari.md`
**Colour spec:** `2026-06-21-bmf-royal-blue-family-tokens.md` (authoritative for all colour values)

---

## 0. GLOBAL RULES (read first)

1. **Minimal diffs.** Change only what each task names. Do not refactor, reformat, or "improve" unrelated code.
2. **Do NOT invent facts.** Items in **Part E** are human-verification flags — do not edit that text; leave it and report it.
3. **Copy changes** are only the exact before/after strings in **Part B**. Do not rewrite any other copy.
4. Keep both pages' **theme toggle**, animations, and JS working.
5. After each Part, run the checks in **Part F** before moving on. Stop and report if a check fails.
6. Work in this order: **A (colour) → D (unify) → B (index fixes) → C (exhibition fixes) → E (report only)**.

---

## PART A — Recolour to the family navy + gold system

Apply `2026-06-21-bmf-royal-blue-family-tokens.md` exactly, to **both** pages.

- Dark theme (default): base `#13235A`, bands/modules `#18306E`, deepest `#0E1B45`, card `#1F3A8A`, text `#EDF1FB`, muted `#9DB0D8`, gold `#C9A227` (soft `#B08D57`).
- Light theme: **warm ivory** base `#FAF8F5`, soft `#F1ECE3`, card `#ECE6DA`, navy ink `#13235A`, muted `#5C6680`, gold `#8A6A2E`.
- Replace the hardcoded reds in `exhibition-stradivari.html`: `.archinto`/`.cta-band` bg `#D7262D` → `#18306E`; `footer` bg `#D7262D` → `#0E1B45`; `.split .txt h3`/`.eyebrow`/`h3 em` `#D7262D` → `#1F3A8A` (light) / `#C9A227` (dark); photo fallbacks `#2a1c1e`/`#2a1113` → `#101a3a`.
- Update `<meta name="theme-color">` on both pages → `#13235A`.
- **Change ONLY colours.** No HTML/copy/layout/font/JS edits in this Part.
- After: `grep -nE "#D7262D|#6E1E2A|#D7B36B|#F3ECDF"` across both files must return nothing.

---

## PART D — Cross-page unification (one design system)

1. **Type system.** The two pages currently use different font stacks. Make both pages load and use the **same** stack. **Recommended canonical** (already used by `exhibition-stradivari.html`): `Spectral` (serif body), `Inter` (sans), `Cinzel` + `Playfair Display italic` (BMƒ wordmark). Align `index.html` to this stack. → *If Max prefers the other stack, this is a one-line swap; flag it, don't guess silently.*
2. **Theme persistence.** Use one `localStorage` key and one default on both pages. Canonical: key `bmf-theme`, default `dark`. Make `exhibition-stradivari.html` default to **dark** (currently `data-theme="light"`) and `index.html` use the same key/default.
3. **Favicon.** `exhibition-stradivari.html` uses `mb-monogram.svg` (Max's personal mark). Replace its `<link rel="icon">` set with the Foundation **BMƒ** monogram/favicons used by `index.html`.
4. **Footer / tagline — one canonical line everywhere** (footer of both pages + meta descriptions where the tagline appears):
   `Promoting classical music · championing emerging artists · stewarding fine Italian instruments.`
5. **City list — one canonical order everywhere** (titles, OG, hero eyebrow, footer): `Rīga · Lugano · Milano`. Fix `index.html` `<title>`/OG that currently drop Rīga ("Lugano · Milano").

---

## PART B — index.html fixes

> Source of `index.html` was not available to the auditor; locate each element by the cue given.

**B1 (P0) Anchor offset.** Sticky header hides section/card titles on anchor jump. Add:
```css
html { scroll-padding-top: 96px; }      /* match real header height */
section[id] { scroll-margin-top: 96px; }
```

**B2 (P1) CTA shape.** Hero CTAs and "Send message" are full pill `border-radius:999px`. Change to `border-radius: 3px`. Keep primary = solid gold, secondary = thin gold outline (no fill).

**B3 (P1) Eyebrow/label contrast.** Dim gold/grey overline labels and form labels on dark must reach **≥4.5:1** for text < 18px. Lift the muted token used for these labels (e.g. toward `#9DB0D8` on navy) until AA passes.

**B4 (P1) Copy — apply these exact swaps (and only these):**
- Card "Artistic Support" body:
  - FROM: `Robust platforms and development for young musicians, composers and artists — helping them launch and sustain international careers.`
  - TO: `Stages, mentorship and patronage for young musicians, composers and artists — building careers that endure on the international circuit.`
- Mission paragraph:
  - FROM: `The Beitan Music Foundation is a cultural foundation promoting classical music, championing emerging artists, and fostering multicultural dialogue through music, poetry and art.`
  - TO: `The Beitan Music Foundation brings exceptional classical music to European audiences, gives emerging artists a stage, and lets music, poetry and art speak across cultures.`
- Contact intro:
  - FROM: `For patronage, donations, programming proposals or press — we would love to hear from you.`
  - TO: `For patronage, donations, programming proposals or press — write to us directly.`

**B5 (P1) JSON-LD.** Add an `Organization`/`NGO` block in `<head>` (see snippet in Part G).

**B6 (P2) Email.** Serve the contact email through one method only — the Cloudflare email-protection link used elsewhere — not once as plain text and once protected.

**B7 (P2) Nav active state.** Add an `active`/`aria-current` highlight on the nav item for the section currently in view (IntersectionObserver; CSS only for the indicator).

---

## PART C — exhibition-stradivari.html fixes

**C1 (P1) Lazy-load.** Add `loading="lazy"` to every `<img>` below the first viewport (gallery `figure img`, press `img`). Leave the hero (CSS background) as is.

**C2 (P1) JSON-LD.** Add an `ExhibitionEvent`/`VisualArtsEvent` block (name, location = Art Museum Rīga Bourse, organizer = Beitan Music Foundation, founder Max Beitan, url). See Part G.

**C3 (handled by Part A)** The red-band contrast issue resolves once `#D7262D` → navy `#18306E`/`#0E1B45`. Verify body text ≥4.5:1 on the new navy bands.

**C4 (consistency)** Roman numerals: page sections use `i. / ii. / iii.` — fine. No change unless Part D type swap affects them.

---

## PART E — DO NOT auto-edit — human verification flags (report only)

These are factual/attribution items. **Leave the text exactly as is.** List them back to Max so he can confirm against source documents:

1. Rostropovich pull-quote: `"One of the best Stradivari I have ever seen." — Mstislav Rostropovich` (on the Archinto). Needs a documented source.
2. `Riccardo Muti` / Luigi Cherubini Orchestra at the Baltic Musical Seasons concert. Needs programme confirmation.
3. Organiser named `Fine Violins Vienna` here, vs `Florian Leonhard Fine Violins (London)` credited on the homepage / in foundation records. Confirm which — possibly two different events.
4. Hero "Curated by Max Beitan" vs body "organised by Fine Violins Vienna in cooperation with… Max Beitan" — pick one role word.

Do not change these strings without Max's explicit confirmation.

---

## PART F — Acceptance checklist

- [ ] `grep -nE "#D7262D|#6E1E2A|#D7B36B|#F3ECDF"` → no matches (both files).
- [ ] One gold only present: `#B08D57` / `#C9A227` / `#8A6A2E`.
- [ ] Light theme base is warm ivory `#FAF8F5` (not cool grey-blue).
- [ ] Both pages: same font stack, same `localStorage` key `bmf-theme`, same default `dark`.
- [ ] `theme-color` meta = `#13235A` on both.
- [ ] Footer tagline + city list identical on both pages (canonical strings above).
- [ ] `index.html`: `scroll-padding-top` present; CTAs `border-radius:3px`; 3 copy swaps applied; JSON-LD present.
- [ ] `exhibition-stradivari.html`: BMƒ favicon; `loading="lazy"` on below-fold imgs; JSON-LD present.
- [ ] WCAG AA: body text ≥4.5:1 on `#13235A` and on `#FAF8F5`; eyebrow labels pass.
- [ ] No changes to Part E strings, copy outside B4, layout, or JS logic.
- [ ] Theme toggle works on both pages; reduced-motion respected.

---

## PART G — Snippets

**JSON-LD — index.html**
```html
<script type="application/ld+json">
{ "@context":"https://schema.org","@type":"NGO",
  "name":"The Beitan Music Foundation","alternateName":"Beitan Mūzikas Fonds",
  "url":"https://beitanmusicfoundation.org",
  "logo":"https://beitanmusicfoundation.org/img/og-foundation.jpg",
  "foundingDate":"2019",
  "founder":{"@type":"Person","name":"Max Beitan","url":"https://maxbeitan.com"},
  "address":{"@type":"PostalAddress","streetAddress":"Krišjāņa Barona iela 32",
    "addressLocality":"Rīga","postalCode":"LV-1011","addressCountry":"LV"},
  "email":"info@beitanmusicfoundation.org",
  "sameAs":["https://maxbeitan.com"],
  "areaServed":["Latvia","Switzerland","Italy"] }
</script>
```

**JSON-LD — exhibition-stradivari.html**
```html
<script type="application/ld+json">
{ "@context":"https://schema.org","@type":"ExhibitionEvent",
  "name":"Stradivari · Guarneri · Amati — Legendary Italian String Instruments",
  "url":"https://beitanmusicfoundation.org/exhibition-stradivari.html",
  "image":"https://beitanmusicfoundation.org/img/riga-bourse-stradivari-exhibit.jpg",
  "location":{"@type":"Place","name":"Art Museum Rīga Bourse",
    "address":{"@type":"PostalAddress","addressLocality":"Rīga","addressCountry":"LV"}},
  "organizer":{"@type":"Organization","name":"The Beitan Music Foundation",
    "url":"https://beitanmusicfoundation.org"} }
</script>
```

---

## PART H — Ready-to-paste command for Claude Code

> Work through `2026-06-21-claude-code-build-instructions.md` Parts A→D→B→C→E in order, on `index.html` and `exhibition-stradivari.html`. Use the colour values from `2026-06-21-bmf-royal-blue-family-tokens.md`. Make minimal diffs: only the changes each Part names. Apply copy edits ONLY for the three exact strings in Part B4. Do NOT touch any Part E text — list those back to me instead. Keep HTML structure, layout, JS, and the theme toggle intact; dark stays default. After finishing, run the Part F checklist and the grep checks, then give me a short diff summary per file and the Part E verification list.

---

## Suggested commit sequence

1. `recolor: navy+gold family palette (both pages)`
2. `unify: shared fonts, theme key/default, favicon, tagline, city order`
3. `index: anchor offset, CTA radius, label contrast, copy, JSON-LD`
4. `exhibition: lazy-load images, JSON-LD`
5. *(manual, after Max confirms)* attribution text fixes from Part E
