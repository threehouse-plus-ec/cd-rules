# T(h)reehouse +EC — Corporate Design Blueprint

**Endorsement Marker:** Local candidate framework — T(h)reehouse +EC stewardship. No external endorsement implied.

**Status:** Active
**Authority:** Harbourmaster
**Licence:** Split architecture (see Section 0.3)
**Canonical location:** `threehouse-plus-ec/corporate-design/blueprint.md`
**Classification:** This document contains both Coastline (hard constraint) and Sail (adaptive guidance) material. Each section is labelled.

---

## 0. Governing Principles · Coastline

These principles are constraints, not guidelines. Violations require Harbourmaster review.

### 0.1 Open-source materials only

Every typeface, library, tool, and dependency must be available under an OSI-approved or OFL-compatible open-source licence. No proprietary fonts. No "free for personal use" assets. If a licence cannot be verified, the material is not used.

| Material | Licence | Verified |
|----------|---------|----------|
| IBM Plex Mono | SIL Open Font License 1.1 | Yes |
| Crimson Pro | SIL Open Font License 1.1 | Yes |

### 0.2 No licence misuse

All assets declare their licence. Downstream uses must respect the declared terms. Each layer of the system carries its own licence (see 0.3). Consumers must check the licence of the specific layer they are using, not assume a uniform licence across the system.

### 0.3 Split licence architecture

The design system uses different licences for different layers, mirroring the Harbour's own epistemic architecture: coastlines (frameworks) are open infrastructure; sails (interpretive works) are protected authorial output; handbooks (tools and assets) are maximally integrable.

**The test:** Could a group at NIST, PTB, or AIMS integrate parts of this system into their workflow without legal consultation? For coastlines and assets, the answer must be yes. For essays and authored works, reasonable restrictions apply.

#### Licence matrix

| Layer | Harbour term | Content | Licence | SPDX | Rationale |
|-------|-------------|---------|---------|------|-----------|
| Core frameworks | Coastline | This blueprint, method definitions, the ADM-EC protocol description, construction rules, tokens | CC BY-SA 4.0 | CC-BY-SA-4.0 | Freely reusable, must stay open. Attribution required. SA ensures derivatives remain open. No NC friction. Any research group can adopt without legal consultation. |
| Authored works | Sail | Essays, teaching stories, kids' pieces, case analyses, Kompass dossiers | CC BY-NC-SA 4.0 | CC-BY-NC-SA-4.0 | Interpretive work protected from commercial repackaging without the epistemic commitments that give it meaning. NC is appropriate because these are authored works, not infrastructure. |
| Design assets | Handbook | SVG emblems, wordmarks, `tokens.css`, CSS code snippets | MIT | MIT | Maximum integrability. A collaborator at PTB or AIMS can embed the emblem in their page without consulting a lawyer. Attribution by convention, not legal enforcement. |
| Code and tooling | Infrastructure | Scripts, build tools, runners, CI configurations | MIT | MIT | Standard open-source practice. No friction with GitHub ecosystems, ARTIQ, or any computational workflow. |
| Fonts | External | IBM Plex Mono, Crimson Pro | SIL OFL 1.1 | OFL-1.1 | Governed by their own licence. Not relicensed by this system. |

#### Why not NC-SA everywhere?

A uniform NC-SA licence would be internally consistent but externally frictional. It creates licence islands that cannot interoperate with the open-source ecosystems this project touches (ARTIQ, Sinara, DAX, GitHub-native workflows, reproducible research tooling). The NC clause introduces legal ambiguity for universities, spin-offs, and mixed-funding organisations, producing a chilling effect even when use is benign. The SA clause propagates constraints into downstream projects, causing people to avoid the material entirely or to fork conceptually without attribution.

The split architecture resolves this: authority for coastlines and assets flows from use and citation (matching the project's epistemology), while authority for authored works flows from both use and licence restriction (matching the nature of interpretive output).

#### Per-folder licence declaration

Each folder in the repo carries a `LICENCE` file or a `LICENCE` reference in its README declaring which licence applies. The root `LICENCE` file states the split and directs readers to per-folder declarations. When in doubt, the licence matrix in this section governs.

#### Relicensing

The Harbourmaster may relicense specific assets to a more permissive licence (e.g. CC BY-SA to CC BY, or MIT to CC0) but never to a more restrictive one. Relicensing from Sail (NC-SA) to a permissive licence requires explicit Harbourmaster decision and is recorded in the version history.

### 0.4 Consistent folder structure

All repos under `threehouse-plus-ec/` follow the folder convention in Section 14. Deviations require documented justification in the repo README.

### 0.5 Markdown first, web-rendered for access

The authoritative version of every document is a Markdown file. Web pages derive from Markdown, not the reverse. If Markdown and HTML diverge, the Markdown is correct.

**Rendering invariant:** Rendered HTML must be reproducible from the Markdown source + `tokens.css` via a defined build step. The build method is documented in the repo README. Currently: manual rendering. When the number of consuming repos exceeds five, a CI check should be introduced.

### 0.6 No version numbers in filenames

Versioning belongs in git, not filenames. Files are named by function: `emblem-16.svg`, not `emblem-v7-16.svg`.

**Breaking-change rule:** If a visual change to an asset would cause existing documents or pages that embed the old version to render differently in a way that alters meaning or legibility, the changed asset must use a new filename or path (e.g. `emblem-16-v2.svg` or a new folder). Cosmetic refinements (minor stroke weight tuning, sub-pixel spacing) that do not alter the mark's identity do not require a new filename.

### 0.7 Endorsement marker on all documents

Every document published under T(h)reehouse +EC carries an endorsement marker declaring scope and stewardship. Harbour-level requirement.

### 0.8 Deprecation, not deletion

Superseded assets move to `archive/` with a dated deprecation note. Never deleted. Git history is not a substitute for visible archival.

### 0.9 Testable rules vs adaptive guidance

Design rules are stated as testable constraints wherever possible. This document labels each section as **Coastline** (hard, testable) or **Sail** (adaptive, contextual). Coastline rules can be checked mechanically or by visual inspection against a defined criterion. Sail guidance requires judgement and may be adapted to context.

### 0.10 Asset propagation: Model B (distributed copy + checksum)

This design system uses **distributed copies with checksum validation**. Each consuming repo copies assets from `corporate-design/assets/` into its own `assets/` folder.

**Propagation rules:**

| Rule | Detail |
|------|--------|
| Source | Always `corporate-design/assets/` at a tagged commit |
| Copy record | Consuming repo's README or `assets/SOURCE.md` records: source repo, commit hash, date |
| Checksum | `assets/SOURCE.md` includes SHA-256 hashes of each copied file |
| Update responsibility | When `corporate-design/` tags a new release, consuming repos should update within one release cycle |
| Drift detection | Compare local file hashes against `corporate-design/` tagged hashes. If mismatch exists and no local justification is documented, the local copy is stale |

This model accepts that copies may temporarily lag behind the source. The checksum record makes drift visible rather than silent.

### 0.11 Cross-repo reference pattern

- **Emblem SVGs:** Copy from `corporate-design/assets/` using Model B rules above.
- **Colour tokens:** Import or copy `tokens.css`. Do not redefine token values locally.
- **Typography:** Reference the canonical Google Fonts import URL in Section 6. Do not host font files locally unless offline use is required.
- **Blueprint reference:** Link to this document. Do not paraphrase design rules in downstream READMEs.

### 0.12 Single source of truth

This repo (`corporate-design/`) is the sole authority. Consuming repos hold copies (Model B), not alternative definitions. If a consuming repo's `tokens.css` diverges from the source, the source is correct.

---

## 1. Generative Sentence · Sail

> A survey marker that knows it is fallible and has encoded how to find truth again.

Every design decision derives from this sentence. It encodes four heritage strands: transmission, plurality, correction, and shared standards. This sentence is guidance for design judgement, not a testable constraint.

---

## 2. Emblem: Construction III — The Maintained Point · Coastline

### 2.1 Description

A single maintained truth-claim (centre point) inside a broken circle (boundary of comparison). Three witness marks at exact 120-degree intervals, rotated so one sits at 6 o'clock. Circle broken in the upper-right quadrant. Correction dot in the gap.

### 2.2 Element roles

| Element | Role | Colour token |
|---------|------|-------------|
| Broken circle | Boundary; maintained, not final | `--ink` |
| Centre point | Maintained reference | `--sea` |
| Three witnesses | Triangulation at 120 degrees | `--ink` |
| Gap | Correction entry; not closed | (absence) |
| EC dot | Correction record | `--signal` |

### 2.3 Geometry

**emblem-64.svg:**

| Element | SVG |
|---------|-----|
| Circle | `<path d="M 53 50 A 28 28 0 1 1 58 22" stroke-width="1.5" stroke-linecap="round"/>` |
| Centre | `<circle cx="32" cy="32" r="3.2"/>` |
| Witness bottom | `<circle cx="32" cy="61" r="1.8"/>` |
| Witness upper-left | `<circle cx="7" cy="17" r="1.8"/>` |
| Witness upper-right | `<circle cx="57" cy="17" r="1.8"/>` |
| EC dot | `<circle cx="60" cy="36" r="1.8"/>` |

**emblem-32.svg:**

| Element | SVG |
|---------|-----|
| Circle | `<path d="M 26.5 25 A 14 14 0 1 1 29 11" stroke-width="1.2" stroke-linecap="round"/>` |
| Centre | `<circle cx="16" cy="16" r="2.2"/>` |
| Witness bottom | `<circle cx="16" cy="30.5" r="1.1"/>` |
| Witness upper-left | `<circle cx="3" cy="8.5" r="1.1"/>` |
| Witness upper-right | `<circle cx="29" cy="8.5" r="1.1"/>` |
| EC dot | `<circle cx="30" cy="18" r="1.1"/>` |

**emblem-16.svg:**

| Element | SVG |
|---------|-----|
| Circle | `<path d="M 13 12.5 A 7 7 0 1 1 14.5 5" stroke-width="1.0" stroke-linecap="round"/>` |
| Centre | `<circle cx="8" cy="8" r="1.4"/>` |
| Witness bottom | `<circle cx="8" cy="15" r="0.8"/>` |
| Witness upper-left | `<circle cx="1.5" cy="4" r="0.8"/>` |
| Witness upper-right | `<circle cx="14" cy="4.5" r="0.8"/>` |
| EC dot | `<circle cx="14.5" cy="8.5" r="0.7"/>` |

### 2.4 Monochrome behaviour

Single-colour contexts: centre point enlarged ~25%, EC dot reduced ~15%. Structure readable without colour.

### 2.5 Construction rules (testable)

| # | Rule | Test method |
|---|------|-------------|
| C1 | Witness marks are filled circles | SVG element check |
| C2 | Witnesses at 120-degree intervals | Angle measurement |
| C3 | Gap in upper-right quadrant | Visual inspection |
| C4 | EC dot in gap at ~3 o'clock | Position check |
| C5 | Centre radius > witness radius | Radius comparison |
| C6 | EC dot radius <= witness radius | Radius comparison |
| C7 | Stroke linecap = round | SVG attribute |
| C8 | Minimum size: 16px screen, 8mm print | Measurement |
| C9 | Maximum 1 emblem instance per page/view | Count |

---

## 3. Usage Levels · Coastline

| Level | Name | Use | Min size |
|-------|------|-----|----------|
| 1 | Identity emblem | Favicon, tab, footer, stamp, seal | 16px |
| 2a | Network seal | Hero, title page, poster, PDF front | 64px |
| 2b | Interpretive ext. | Diagrams only. Archived. Not identity | 96px |
| Seal I | Benchmark | Large-format ceremonial only | 48px |

**Testable:** Level 2a is never used as favicon. Seal I is never used below 48px.

---

## 4. Wordmark · Coastline

### 4.1 Variants

| Variant | Form | Default context |
|---------|------|----------------|
| B-silent | `T[h]ree` | Compact lockups with emblem inside content modules; secondary signatures |
| B-full | `T[h]ree +EC` | Formal naming, default site header, and emblem-absent contexts |

### 4.2 Specification

| Element | Font | Weight | Colour |
|---------|------|--------|--------|
| "T" | IBM Plex Mono | 400 | `--ink` |
| Box | stroke 1.2px, radius 2px | — | `--sea` |
| "h" | IBM Plex Mono | 500 | `--sea` |
| "ree" | IBM Plex Mono | 400 | `--ink` |
| "+EC" | IBM Plex Mono | 400, 0.46x, super | `--signal` |

### 4.3 CSS

```css
.wm-h {
  font-weight: 500;
  color: var(--sea);
  border: 1px solid var(--sea);
  border-radius: 2px;
  padding: 0.04em 0.1em;
  margin: 0 0.03em;
}

.wm-ec {
  font-size: 0.62em;
  font-weight: 400;
  color: var(--signal);
  vertical-align: super;
  margin-left: 0.12em;
}
```

---

## 5. Colour System · Coastline

### 5.1 Tokens

Defined in `assets/tokens.css`:

```css
:root {
  --ink: #1a1a1a;
  --sea: #2c5f7c;
  --signal: #c0392b;
  --stone: #6b6b6b;
  --parchment: #f5f0e8;
  --grid: #e0dbd2;
  --warm-white: #faf8f4;
}
```

### 5.2 Semantic hierarchy

| Token | Role | Category |
|-------|------|----------|
| `--ink` | Structure: what holds | Primary |
| `--sea` | Reference: what is maintained | Primary |
| `--signal` | Correction: what is open to repair | Primary |
| `--stone` | Secondary text, metadata | Secondary |
| `--parchment` | Page background | Secondary |
| `--grid` | Rules, borders | Secondary |
| `--warm-white` | Card backgrounds | Secondary |

### 5.3 Usage constraints (testable)

| # | Rule | Test |
|---|------|------|
| K1 | `--signal` is used only for EC/correction elements, principle markers, and "+EC" text | Colour audit |
| K2 | `--sea` is used only for reference elements, labels, links, and wordmark "h" | Colour audit |
| K3 | `--stone` is never used for primary body text | Font-colour check |
| K4 | No design token is used for elements unrelated to its semantic role | Manual review |
| K5 | Base background is always `--parchment` or `--warm-white`; overlays may only be low-contrast treatments derived from `--grid` or the same base field | Background audit |

### 5.4 Contrast (WCAG AA)

| Pair | Ratio | AA normal (4.5:1) | AA large (3:1) | AAA normal (7:1) |
|------|-------|--------------------|----------------|-------------------|
| Ink / Parchment | 13.8:1 | Pass | Pass | Pass |
| Sea / Parchment | 5.5:1 | Pass | Pass | Fail |
| Signal / Parchment | 5.0:1 | Pass | Pass | Fail |
| Stone / Parchment | 3.9:1 | **Fail** | Pass | Fail |
| Ink / Warm-white | 14.5:1 | Pass | Pass | Pass |
| Sea / Warm-white | 5.8:1 | Pass | Pass | Fail |
| Stone / Warm-white | 4.1:1 | **Fail** | Pass | Fail |

**Constraints (testable):**

| # | Rule | Test |
|---|------|------|
| K6 | `--stone` is never used for text smaller than 18px (or bold 14px) | Computed size + colour audit |
| K7 | All text–background pairs meet WCAG AA (4.5:1 normal, 3:1 large) | Contrast audit |
| K8 | Interactive element labels (links, buttons, nav) must meet 4.5:1 regardless of size | Contrast audit |

---

## 6. Typography · Coastline

### 6.1 Typefaces

| Typeface | Licence | Weights |
|----------|---------|---------|
| IBM Plex Mono | SIL OFL 1.1 | 300, 400, 500, 600 |
| Crimson Pro | SIL OFL 1.1 | 300, 400, 600; italic 300, 400 |

Canonical import:

```
https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@300;400;500;600&family=Crimson+Pro:ital,wght@0,300;0,400;0,600;1,300;1,400&display=swap
```

### 6.2 Roles and constraints (testable)

| # | Rule | Test |
|---|------|------|
| T1 | Body text: Crimson Pro only | Font-family check |
| T2 | Labels, nav, metadata: IBM Plex Mono only | Font-family check |
| T3 | No page uses more than 3 distinct font weights | Weight audit |
| T4 | Body text is never set in uppercase | Text-transform check |
| T5 | IBM Plex Mono is never used for body paragraphs | Font-family check |
| T6 | Crimson Pro is never used for labels or navigation | Font-family check |
| T7 | No typeface outside the two declared faces is introduced | Font-family audit |

### 6.3 Scale

Base: 17px desktop, 16px mobile (below 640px).

**Minimum rendered size:** No text element may render below **12px** (0.75rem at 16px base). This is a Coastline constraint. The previous scale included sizes as small as 0.48rem (~8px), which fails WCAG readability guidance and is illegible on mobile devices.

| Element | Size | Line height | Min rendered (mobile) |
|---------|------|-------------|----------------------|
| Body | 1rem | 1.68 | 16px |
| Section intro | 1.15rem | 1.55 | 18.4px |
| Entrance tagline | 1.35rem | 1.55 | 21.6px |
| Section headings | 0.75rem | 1.3 | 12px |
| Nav links | 0.75rem | 1.3 | 12px |
| Layer labels | 0.75rem | 1.3 | 12px |
| Footer text | 0.75rem | 1.5 | 12px |
| Footer status | 0.75rem | 1.3 | 12px |

**Testable:**

| # | Rule | Test |
|---|------|------|
| T8 | No text renders below 12px at any viewport width | Computed font-size check |
| T9 | Line height for multi-line text is >= 1.3 | Computed line-height check |

---

## 7. Spacing · Coastline

| Property | Desktop | Mobile (≤ 640px) |
|----------|---------|-------------------|
| Content measure | 38rem | 100% − 2 × gutter |
| Page gutter | 1.5rem | 1.25rem |
| Section top padding | 3.5rem | 2.5rem |
| Section rule | 1.5rem wide, 1px tall, `--grid` | same |
| Rule-to-heading | 1.2rem | 1rem |
| Paragraph spacing | 0.85rem | 0.85rem |
| Layer stack left column | 2.8rem | 2.2rem |
| Layer gap | 1px | 1px |
| Entrance top padding | 6rem | 4rem |
| Emblem to tagline | 2.5rem | 2rem |
| Header emblem size | 32px | 32px |
| Header wordmark width | 7.05rem | 7.05rem |
| Nav link spacing | — | min 44px height (touch target) |

---

## 8. Lockup Rules · Coastline

| # | Rule | Test |
|---|------|------|
| L1 | Emblem left, wordmark right, vertically centred | Visual |
| L2 | Gap: 0.5rem header, 0.6rem display | Measurement |
| L3 | Header lockup uses a Level 1 emblem at 32px | Size check |
| L4 | Site header uses wordmark B-full by default | Attribute |
| L5 | Clear space >= centre point radius | Measurement |
| L6 | Emblem min: 16px screen, 8mm print | Measurement |
| L7 | Level 2a min: 64px | Size check |
| L8 | Seal I min: 48px | Size check |
| L9 | Max 1 emblem per header/footer | Count |

---

## 9. Forbidden Treatments · Coastline

| # | Treatment | Reason |
|---|-----------|--------|
| F1 | Gradient, shadow, glow on emblem | Colophon register |
| F2 | Closing the gap | Destroys EC semantics |
| F3 | Moving or removing witnesses | Breaks triangulation |
| F4 | Changing 120-degree interval | Construction rule |
| F5 | Emblem in bordered container | Double framing |
| F6 | Emblem as repeating pattern | Destroys singularity |
| F7 | Rotating emblem | Gap position is semantic |
| F8 | Text inside circle | Spatial hierarchy |
| F9 | Replacing EC dot | EC dot is the record |
| F10 | Design tokens on unrelated elements | Palette drift |
| F11 | Role-inverted typography | See T5, T6 |
| F12 | Level 2a as favicon | Too complex at 16px |
| F13 | Seal I below 48px | Detail loss |

---

## 10. Component Patterns · Coastline

### Section rule
`<hr>`: 1.5rem wide, 1px tall, `--grid`.

### Section header split
Two-column introduction block for sectioned pages: left column contains the mono label plus serif heading; right column contains a supporting paragraph. Desktop grid: `minmax(0, 1fr) minmax(15rem, 24rem)`. Below 880px it collapses to one column.

### Layer stack
Two-column grid: left 2.8rem, right 1fr. Background `--warm-white`. Left border-right: 1px `--grid`. Row gap: 1px.

### Gate layer
Layer stack variant: marker and label in `--signal`. Used for EC lens only.

### Research callout
Background `--warm-white`. Left border: 3px `--sea`. Label: Plex Mono uppercase `--sea`.

### Entrance / hero block
For demonstrators, specimen pages, and index pages, an entrance block may use a two-column grid: primary copy at left, interpretive or specimen panel at right. Desktop grid: `minmax(0, 1.45fr) minmax(16rem, 0.85fr)`. Below 880px it collapses to one column.

Hero heading uses Crimson Pro at display scale. Supporting paragraph sits at body or section-intro scale. Entrance actions may follow beneath as a horizontal wrap with 0.75rem gap.

### Action buttons
Action buttons use IBM Plex Mono at 0.75rem / 1.3, minimum 44px height, 1px border, no fill gradients, and no drop shadows. Primary action: `--ink` border on `--warm-white`. Secondary action: `--grid` border with `--sea` text on transparent field.

### Specimen / hero panel
Background `--warm-white` or warm-white translucent field between 0.88 and 0.94 opacity. Border: 1px `--grid`. No drop shadow. A single low-contrast radial accent derived from `--grid` may be used inside the panel provided it remains subordinate to the content.

### Metrics strip
Short quantitative or categorical readouts may appear inside a specimen panel as a simple grid of cells separated by top borders in `--grid`. Labels use Plex Mono 0.75rem in `--sea`; values use Crimson Pro in `--ink`.

### Evidence cards
Supporting cards may be used in groups of two or three. Background `--warm-white`. Border: 1px `--grid`. Heading: Plex Mono 0.75rem, weight 500, `--sea`. Body: Crimson Pro at body size. No iconography, coloured header blocks, or shadow stacks.

### Site header
Sticky at the top edge. Uses the header lockup rules above: Level 1 emblem at 32px plus B-full wordmark by default.

The header wordmark is sized at 7.05rem, a 1.5x increase over the previous compact lockup.

On mobile (≤ 640px), the header may auto-hide on downward scroll to return vertical space to the reading surface. It reappears on upward scroll, at the top of the page, and whenever navigation is expanded or focused.

### Web surface treatments
The page field may carry a low-contrast registration grid derived from `--grid` to give large parchment surfaces structure. Such treatments remain strictly subordinate: no more than one overlaid line system, no strong contrast, and no chromatic gradients unrelated to the token system.

Sticky headers may use a light backdrop blur on web surfaces to preserve legibility during scroll, provided the apparent background still reads as parchment.

### Colophon footer
Two variants are permitted:

- Minimal colophon: Level 1 emblem, all elements `--stone`, opacity 0.3. Text: Plex Mono 0.54rem. Status: 0.48rem uppercase. Maxim: Crimson Pro italic 0.82rem.
- Web colophon card: 1px `--grid` border on `--warm-white`, B-full wordmark, status in Plex Mono 0.75rem uppercase `--stone`, optional maxim in Crimson Pro italic, and supporting metadata in Plex Mono 0.75rem `--stone`.

### Tables

Tables are for **tabular data only** — never for layout. Every table must be readable on both desktop and mobile without horizontal scrolling under normal conditions.

#### Structure rules (testable)

| # | Rule | Test |
|---|------|------|
| TB1 | Every `<table>` has a `<thead>` with `<th>` cells | Source check |
| TB2 | Header cells use `scope="col"` or `scope="row"` | Source check |
| TB3 | Tables with complex headers use `id` / `headers` attributes | Source check |
| TB4 | Tables never used for page layout (use CSS Grid/Flexbox) | Source audit |
| TB5 | Each table has an accessible name: `<caption>`, `aria-label`, or `aria-describedby` | Source check |

#### Visual design

Clean, open tables. No outer border. No cell borders. Horizontal rules only between rows. Header visually distinct via weight, not background colour.

| Property | Value |
|----------|-------|
| Font | IBM Plex Mono `var(--font-mono)` for headers; Crimson Pro `var(--font-serif)` for body cells |
| Header weight | 500 |
| Header text transform | none (no uppercase) |
| Header colour | `--ink` |
| Header size | 0.75rem |
| Cell font size | 0.85rem |
| Cell line height | 1.5 |
| Cell padding | `0.55rem 0.75rem` |
| Row border | 1px solid `--grid` (bottom of each row) |
| Header border | 1px solid `--stone` (bottom of `<thead>`) — heavier than row borders |
| Outer border | none |
| Column borders | none |
| Table width | 100% of content measure |
| Text alignment | Left (default); right for numeric columns |
| Header background | transparent |
| Row background | transparent (no zebra striping) |
| Row hover | `--warm-white` background (desktop only, optional) |

#### CSS reference implementation

```css
table {
  width: 100%;
  border-collapse: collapse;
  border-spacing: 0;
  font-variant-numeric: tabular-nums;
  margin-block: 1.2rem;
}

thead th {
  font-family: var(--font-mono);
  font-weight: 500;
  font-size: 0.75rem;
  color: var(--ink);
  text-align: left;
  padding: 0.55rem 0.75rem;
  border-bottom: 1px solid var(--stone);
  vertical-align: bottom;
}

tbody td {
  font-family: var(--font-serif);
  font-size: 0.85rem;
  line-height: 1.5;
  color: var(--ink);
  padding: 0.55rem 0.75rem;
  border-bottom: 1px solid var(--grid);
  vertical-align: top;
}

/* Numeric columns — opt-in via class */
th.num, td.num {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

/* Optional row hover (desktop) */
@media (hover: hover) {
  tbody tr:hover {
    background: var(--warm-white);
  }
}
```

#### Mobile behaviour (≤ 640px)

Tables must remain readable on small screens. Two strategies are permitted:

**Strategy A — Horizontal scroll wrapper** (default for wide tables):

```css
.table-wrap {
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
  margin-inline: calc(-1 * var(--gutter));
  padding-inline: var(--gutter);
}

/* Visual scroll hint — fade on right edge */
.table-wrap::after {
  content: '';
  position: sticky;
  right: 0;
  display: block;
  width: 1.5rem;
  background: linear-gradient(to left, var(--parchment), transparent);
  pointer-events: none;
}
```

```html
<div class="table-wrap" role="region" aria-label="Scrollable table" tabindex="0">
  <table> ... </table>
</div>
```

**Strategy B — Stacked layout** (for 2–3 column tables):

```css
@media (max-width: 640px) {
  table.stackable thead { display: none; }

  table.stackable tr {
    display: block;
    padding: 0.75rem 0;
    border-bottom: 1px solid var(--grid);
  }

  table.stackable td {
    display: block;
    padding: 0.2rem 0;
    border: none;
    font-size: 0.85rem;
  }

  table.stackable td::before {
    content: attr(data-label);
    display: block;
    font-family: var(--font-mono);
    font-size: 0.75rem;
    font-weight: 500;
    color: var(--stone);
    margin-bottom: 0.15rem;
  }
}
```

#### Mobile rules (testable)

| # | Rule | Test |
|---|------|------|
| TB6 | Tables wider than viewport are wrapped in a scrollable `role="region"` container with `aria-label` and `tabindex="0"` | Source + a11y check |
| TB7 | Scroll containers are keyboard-navigable (focusable via `tabindex="0"`) | Tab test |
| TB8 | Stacked tables use `data-label` on `<td>` to preserve header context | Source check |
| TB9 | No table text renders below 12px on any viewport | Computed size check |
| TB10 | Cell padding is never less than `0.4rem` vertically | Computed style check |

#### Forbidden treatments

| # | Treatment | Reason |
|---|-----------|--------|
| TF1 | Zebra-stripe row backgrounds | Visual noise; conflicts with `--parchment` register |
| TF2 | Coloured header backgrounds | Weight, not colour, distinguishes headers |
| TF3 | Cell borders (vertical lines between columns) | Clutters the table; horizontal rules are sufficient |
| TF4 | Outer table border / box | Double-framing; conflicts with open register |
| TF5 | Fixed-width columns via inline `width` attributes | Breaks responsive flow |
| TF6 | Tables for layout | Use CSS Grid or Flexbox |

---

## 11. Heritage and Register · Sail

This section is adaptive guidance, not testable constraint.

### Heritage

**Metrological stamp:** Circular boundary, central point, comparison against external reference.

**Witness tree:** Peripheral marks enabling relocation of the true point.

**Colophon restraint:** Placed on a work, not as a work.

### Register

Should feel: found, not designed. Benchmark on a survey post. Correction term in a manuscript margin.

Should never feel: startup logo, personal monogram, corporate badge, decorative illustration.

### Epistemic reading

Level 1: maintained point, triangulated, open to correction.
Level 2a: each local point opens into further structured comparison.
Together: truth preserved by recursively related local reference systems.

### Adaptation principle

The Coastline sections (0, 2-10) are hard constraints. This Sail section may be adapted to context. A page for children may feel warmer; a technical dossier may feel more austere. The register guidance shapes tone, not structure. If a contextual adaptation conflicts with a Coastline rule, the Coastline rule prevails.

---

## 12. Web Rendering · Coastline

Markdown is authoritative. HTML derives from it.

**Rendering invariant:** Any rendered HTML page must be reproducible from: (1) the source Markdown, (2) `tokens.css`, (3) the documented build method. Current build method: manual. When consuming repos exceed five, introduce a CI hash-check.

All pages import the canonical Google Fonts URL and the same `:root` tokens. Local styles may extend but must not override token values.

---

## 12A. Accessibility · Coastline

Every page published under T(h)reehouse +EC must meet **WCAG 2.2 Level AA** as a minimum. These rules are Coastline constraints.

### 12A.1 Viewport

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

| # | Rule | Test |
|---|------|------|
| A1 | Every page includes the viewport meta tag above | Source check |
| A2 | `maximum-scale` and `user-scalable=no` are **never** set | Source check |
| A3 | Content is readable and functional from 320px to 2560px without horizontal scrolling | Visual / responsive test |

### 12A.2 Touch Targets (mobile)

All interactive elements (links, buttons, form controls) must meet minimum touch-target sizes.

| # | Rule | Min size | Standard |
|---|------|----------|----------|
| A4 | Interactive elements have a touch target of at least 24×24 CSS px | `var(--min-target-aa)` | WCAG 2.5.8 AA |
| A5 | Primary navigation and action buttons target 44×44 CSS px | `var(--min-target)` | WCAG 2.5.5 AAA |
| A6 | Spacing between adjacent touch targets is at least 8px | 8px gap | Prevents mis-taps |

**Implementation guidance:**

```css
/* Minimum for all interactive elements */
a, button, [role="button"], input, select, textarea {
  min-height: var(--min-target-aa);    /* 24px */
}

/* Primary nav and action buttons — AAA target */
.site-nav a, .nav-toggle, button[type="submit"] {
  min-height: var(--min-target);       /* 44px */
  padding-block: 0.5rem;
}
```

### 12A.3 Focus Indicators

All interactive elements must have a visible focus indicator. The browser default outline must not be removed without a replacement that meets WCAG 2.4.7 / 2.4.11.

| # | Rule | Test |
|---|------|------|
| A7 | Focus ring is visible on all interactive elements when navigated via keyboard | Tab-through test |
| A8 | Focus indicator has minimum 2px width and contrasts 3:1 against adjacent colours | Visual / computed check |
| A9 | `outline: none` or `outline: 0` is never used without an equivalent replacement | Source audit |

**Implementation guidance:**

```css
:focus-visible {
  outline: var(--focus-ring);           /* 2px solid var(--sea) */
  outline-offset: var(--focus-offset);  /* 2px */
}
```

### 12A.4 Reduced Motion

Respect user motion preferences. Animations and transitions must be suppressed when the user has enabled "reduce motion" in their OS settings.

| # | Rule | Test |
|---|------|------|
| A10 | `scroll-behavior: smooth` is wrapped in `prefers-reduced-motion: no-preference` | Source check |
| A11 | All CSS transitions/animations are disabled or reduced under `prefers-reduced-motion: reduce` | Computed style check |
| A12 | If entrance animations are used, they are limited to opacity plus single-axis translation, <= 800ms, and remain decorative rather than essential | Source + interaction check |

**Implementation guidance:**

```css
@media (prefers-reduced-motion: no-preference) {
  html { scroll-behavior: smooth; }
}

@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

### 12A.5 Semantic Structure

| # | Rule | Test |
|---|------|------|
| A13 | Every page has exactly one `<main>` element | Source check |
| A14 | `<html>` declares `lang` attribute | Source check |
| A15 | Heading hierarchy is sequential (no skipped levels) | Heading audit |
| A16 | Navigation uses `<nav>` with `aria-label` when multiple `<nav>` exist | Source check |
| A17 | Decorative images use `aria-hidden="true"` or empty `alt=""` | Source check |
| A18 | Meaningful images have descriptive `alt` text | Manual review |

### 12A.6 Skip Navigation

Every page must provide a skip-to-content link as the first focusable element.

| # | Rule | Test |
|---|------|------|
| A19 | A "Skip to content" link exists as the first focusable element | Tab test |
| A20 | The link targets `<main>` or `#content` | Source check |

**Implementation guidance:**

```css
.skip-link {
  position: absolute;
  top: -100%;
  left: 0;
  padding: 0.75rem 1.5rem;
  background: var(--ink);
  color: var(--parchment);
  font-family: var(--font-mono);
  font-size: 0.75rem;
  z-index: 1000;
}

.skip-link:focus {
  top: 0;
}
```

```html
<body>
  <a href="#content" class="skip-link">Skip to content</a>
  <!-- ... header / nav ... -->
  <main id="content"> ... </main>
</body>
```

### 12A.7 Mobile Navigation

The mobile navigation (below 640px) must remain fully accessible when collapsed behind a toggle.

| # | Rule | Test |
|---|------|------|
| A21 | Nav toggle button has `aria-expanded` reflecting open/closed state | Source + JS check |
| A22 | Nav toggle has accessible label (`aria-label` or visible text) | Source check |
| A23 | Hidden nav uses `display: none` or `visibility: hidden` (not just visual hiding) so it is removed from the tab order | Tab-through test |
| A24 | Nav toggle is operable via keyboard (Enter and Space) | Keyboard test |
| A25 | On mobile, a sticky header that occupies reading space auto-hides on downward scroll and reappears on upward scroll or at scroll top | Manual mobile test |
| A26 | The mobile header remains visible whenever the navigation drawer is expanded or receives keyboard focus | Source + interaction check |

### 12A.8 Responsive Typography

| # | Rule | Test |
|---|------|------|
| A27 | Text can be resized to 200% without loss of content or functionality (WCAG 1.4.4) | Browser zoom test |
| A28 | No text is set with `!important` on `font-size` that would block user zoom | Source audit |
| A29 | Line length does not exceed 80 characters on desktop (`var(--measure): 38rem` enforces this) | Character count |

---

## 13. Asset Inventory · Coastline

All assets live in `assets/` in this repo. Each file carries the licence of its layer (see Section 0.3).

| Filename | Content | Licence |
|----------|---------|---------|
| `assets/emblem-16.svg` | Level 1, 16px | MIT |
| `assets/emblem-32.svg` | Level 1, 32px | MIT |
| `assets/emblem-64.svg` | Level 1, 64px | MIT |
| `assets/wordmark-full.svg` | B-full | MIT |
| `assets/wordmark-silent.svg` | B-silent | MIT |
| `assets/tokens.css` | Colour, font, and layout tokens | MIT |
| `assets/LICENCE` | MIT licence text for assets folder | — |
| `blueprint.md` | This document | CC BY-SA 4.0 |
| `LICENCE` | Root licence (split declaration) | — |
| `archive/` | Deprecated assets with dated notes | Original licence preserved |

---

## 14. Folder Structure · Coastline

### Corporate design repo

```
corporate-design/
  blueprint.md            CC BY-SA 4.0
  LICENCE                 Split declaration (points to per-folder)
  README.md
  index.html              Renders blueprint
  assets/
    LICENCE               MIT
    SOURCE.md             (not needed here; this is the source)
    emblem-16.svg
    emblem-32.svg
    emblem-64.svg
    wordmark-full.svg
    wordmark-silent.svg
    tokens.css
  archive/
```

### Standard repo structure

```
repo-name/
  index.html
  LICENCE                 Declares which layer(s) apply
  README.md
  assets/
    LICENCE               MIT (if assets copied from corporate-design)
    SOURCE.md             Origin commit hash, checksums
  archive/
  docs/
```

### Content-heavy repos (website, essays)

```
repo-name/
  index.html
  LICENCE                 Split: page chrome = MIT, authored content = CC BY-NC-SA
  README.md
  assets/
    LICENCE               MIT
    SOURCE.md
  essays/                 CC BY-NC-SA 4.0 (authored works)
  cases/                  CC BY-NC-SA 4.0
  stories/                CC BY-NC-SA 4.0
  kids/                   CC BY-NC-SA 4.0
  docs/
  archive/
```

The root `LICENCE` file in content-heavy repos must state explicitly which folders carry which licence. When a folder contains mixed content, the more restrictive licence applies unless individual files carry their own header declarations.

---

## 15. Deprecation Protocol · Coastline

1. Move old file to `archive/`.
2. Add `archive/YYYY-MM-DD-filename-deprecated.md`.
3. Update asset inventory (Section 13).
4. Tag repo: `cd-vX.Y.Z`.
5. Notify consuming repos via issue or commit message.

---

## 16. Version History

| Version | Date | Change |
|---------|------|--------|
| CD 1.0.0 | 2026-04-02 | Initial blueprint |
| CD 1.1.0 | 2026-04-02 | Governing principles, folder structure, deprecation protocol, cleaned filenames |
| CD 1.2.0 | 2026-04-02 | Guardian review: asset propagation model B + checksum, rendering invariant, licence intent, breaking-change rule, testable rules, coastline/sail classification |
| CD 1.3.0 | 2026-04-02 | Split licence architecture: CC BY-SA for coastlines/blueprint, MIT for assets/code, CC BY-NC-SA for authored works. Per-folder licence declarations. Licence matrix. NIST/PTB integration test. Relicensing protocol. |
| CD 1.4.0 | 2026-04-03 | Accessibility hardening: WCAG 2.2 AA baseline. Minimum 12px text floor (raised from 8px). Touch target rules (24px AA / 44px AAA). Focus indicator requirements. Reduced motion. Skip navigation. Mobile nav a11y. Contrast constraints tightened (K6–K8). Responsive spacing table. Accessibility tokens added to `tokens.css`. |
| CD 1.5.0 | 2026-04-03 | Table component rules: structure (TB1–TB5), visual design spec, CSS reference implementation, mobile strategies (scroll wrapper + stacked layout, TB6–TB10), forbidden treatments (TF1–TF6). |
| CD 1.6.0 | 2026-04-03 | Header refinements: compact 32px header lockup, site-header component note, and mobile auto-hide behaviour added to navigation/accessibility rules. |
| CD 1.6.1 | 2026-04-03 | Header lockup default corrected: site header now uses the B-full wordmark by default rather than B-silent. |
| CD 1.6.2 | 2026-04-03 | Header wordmark width increased by 1.5x to improve default header legibility. |
| CD 1.7.0 | 2026-04-03 | Demonstrator mapping expansion: wordmark context table corrected; section-header split, entrance block, action buttons, specimen panel, metrics strip, evidence cards, web surface treatments, and web colophon card added; motion and accessibility numbering extended accordingly. |

---

*T(h)reehouse +EC. Local candidate framework. The emblem is the seed; the network is its recursive unfolding.*
