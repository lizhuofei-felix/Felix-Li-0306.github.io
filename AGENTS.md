# AGENTS.md

Working instructions for any coding agent in this repository. `CLAUDE.md` is a
symlink to this file — edit this one, never the symlink.

## What this is

A single-page professional profile for LI Zhuofei, served by GitHub Pages at
`lizhuofei.com`. Plain HTML with inline CSS and a small inline JavaScript
progressive enhancement. **No framework, package manager, build step, or
JavaScript dependencies.** `index.html` *is* the site; content and links must
remain usable without JavaScript.

## Files

| Path | Role |
| --- | --- |
| `index.html` | The entire site: markup + inline `<style>` and enhancement `<script>`. Must stay at repo root. |
| `favicon.svg` | Active browser icon. Referenced from `index.html`. |
| `apple-touch-icon.png` | 180px icon for iOS, drawn from the favicon geometry. |
| `og-image.png` | 1200x630 share card referenced by `og:image` (name, degree, domain). Regenerate it if the name or degree line changes. |
| `fonts/` | Self-hosted latin-subset `woff2` files for Inter and EB Garamond, loaded by `@font-face` in `index.html`. No external font requests. |
| `cv.pdf` | Published CV, linked from the identity column's contact block. **It must always be the `Public` variant built by the CV repo** (`variants/public/pdf/LI_ZHUOFEI_Resume_Public_2026.pdf`; `output/pdf/` now holds only the private Print base), with the phone number stripped. Never copy the phone-bearing source attachment, Standard, or Print deliverable here. Refresh it whenever the approved CV content changes, and re-check extracted text for phone numbers before committing. |
| `CNAME` | Custom domain (`lizhuofei.com`). Must stay at repo root — deleting it breaks the domain. A Pages site can hold exactly one custom domain; the former `me.byfelix.xyz` now redirects here. |
| `CV/` | **Symlink to `../CV`**, a *separate private* repo (`Felix-Li-0306/CV`) holding the résumé sources and generated PDF/DOCX. Git-ignored via `/CV` — **never commit it or its contents**. This repo is public and GitHub Pages serves everything tracked here, and the CV files carry a phone number (the Chinese ones an address) that the site does not publish. |
| `README.md` | **Authoritative design constraints.** Read before any UI change. |
| `CLAUDE.md` | **Symlink to `AGENTS.md`** (git mode `120000`), so both names resolve to this one file. Never write through it. |
| `PROGRESS.md` | Cross-session handoff state. Update after substantial work. |
| `design-qa.md` | Last visual-QA report. Verify screenshot availability before relying on its evidence; temporary paths can expire. |
| `.claude/launch.json` | Local preview config. **Git-ignored** (`.gitignore` excludes `.claude/`), not deployed. |

## Preview

Run a local server from the repository root:

```bash
python3 -m http.server 4173 --bind 127.0.0.1
```

Open `http://127.0.0.1:4173` in the browser. The ignored `.claude/launch.json`
also defines a local preview; it is not a deployment dependency.

There is **no test, lint, format, or build command.** Do not invent one. If you add
tooling, document it here before relying on it. Keep the static document and
dependency-free enhancement; the owner's approval for reference-site interactions
does not authorize a framework or build pipeline.

## Page structure

Desktop layout: a sticky `<header id="profile" class="identity">` beside one
continuous `<main id="content" class="content">`. The identity header contains
the name, `.preferred-name`, `.identity-degree`, `.role`, navigation, and a `#contact` block with
GitHub, LinkedIn, Email, and CV icons in a single row. All four links use named
44×44px targets. The first three have 24px inline SVGs, kept `aria-hidden` and
non-focusable; retain the email address in its link label. The fourth displays
only `CV` in a 24px `.cv-mark` area, at 17px/700, with the mark `aria-hidden`.
Keep the `cv.pdf` destination, accessible PDF/new-tab label, title, and external
tab relationship protections. Do not restore a separate View CV row or CV arrow.

Main section IDs and navigation order:

`#about` · `#education` · `#project` ("Projects") · `#experience` ·
`#activities` ("Activities & Service") · `#skills` ("Skills")

The corresponding content headings include "Selected Projects" and
"Activities & Service". Sections use hairline dividers, with no separate cards.
At 960px and below, the identity header becomes normal-flow content above the
main. `#top` belongs to the root HTML element and is the target of the name and footer links;
keep `#profile` for existing links. The skip link targets focusable `#content`.

## Design rules — do not violate

`README.md` holds the full rationale. The page must read as a carefully typeset
personal document. The owner approved the September 2026 redesign based on
Brittany Chiang's two-column reading structure. These rules replace the former
780px single-column sheet, topbar, and emerald palette; implementing this
approved direction does not require another design approval.

The owner then explicitly requested matching the reference site's interactions.
This authorizes the inline scrollspy, smooth anchor scrolling, expanding nav
rails, entry hover/focus panels, sibling dimming, link-arrow movement, and radial
pointer glow described below, together with actual hover elevation and
reference-style contact icons. The latest explicit direction calls for a stronger
glow and colors closer to the reference: slate backgrounds, teal accents, and a
blue background glow. It supersedes the intermediate steel-blue accent and
faint-glow settings. The old blanket no-JavaScript, no-gradient, and
no-hover-movement rules remain superseded within this interaction scope.

- Serif (`EB Garamond`) is only for `h1`. Everything else is `Inter`.
  Keep the name as `LI Zhuofei` (mixed case) with slight positive tracking.
- One content accent color (`--accent`, teal). The separately authorized pointer
  glow uses a translucent blue radial gradient behind content. Do not introduce
  other content accents or decorative gradients.
- Cool gray page background — never warm cream/ivory.
- No scroll-reveal gating, parallax, per-entry icon badges, or numbered section
  kickers ("01 / 02"). Smooth anchor scrolling and the approved hover/focus
  transitions are allowed. Entry panels and subtle shadows remain transient.
- Maximum layout width is 1120px, with a 320px identity column, a 96px gap,
  and the remaining space for content. Between 961px and 1100px, reduce the
  identity column to 290px and the gap to 64px. The identity header is sticky
  at 72px from the top on desktop. At 641–760px viewport height, keep it sticky
  with a 32px top offset, 32px page top margin, and compact spacing; at 640px and below, make it static
  to keep contact links reachable. Use a single-column layout at 960px and below.
- No outer paper border, permanent card frames, or separate content scroll pane.

Preserve this direction for routine changes. A technology change or factual
claim stronger than the approved sources still needs the owner's authorization.

## CSS notes

- Colors are CSS custom properties on `:root`, **redefined in a
  `@media (prefers-color-scheme: dark)` block**.
  Any color token change must be applied to *both* palettes, or dark mode breaks.
- Light palette: page `#F1F5F9`, text `#0F172A`, muted `#475569`, accent
  `#115E59`, divider `#D7E0EB`.
- Dark palette: page `#0F172A`, text `#E2E8F0`, muted `#94A3B8`, accent
  `#5EEAD4`, divider `#233249`.
- Maintain matching light/dark tokens for entry-hover backgrounds, subtle edges,
  both shadow layers, selection colors, and the blue pointer glow with its falloff.
- Ordinary links use the main text color by default and teal on hover. Headings,
  active/hovered navigation, and hovered social icons use the main text color;
  project hover, result labels, and focus outlines use teal.
- Keep the fixed glow at `z-index: 0` and the positioned layout at `z-index: 1`.
  It must remain behind text rather than tinting glyphs. Check body and link
  contrast against both the illuminated background and hover panels.
- Skills use a label/value grid, collapsed to one column at 600px and below.
  Keep long values wrapping without horizontal overflow. Entry dates use 13px
  text and stack below titles on small screens and the narrower desktop layout.
- Keep navigation and contact links usable when they wrap. Check the 960px
  layout transition and narrow mobile widths after changing either column.
- The old `.topbar`, metrics grid, and matched 140px skills/contact grids are
  no longer layout requirements. Do not restore them to satisfy obsolete notes.

## Interaction implementation

- Keep JavaScript as a small inline progressive enhancement, with no library,
  framework, package manager, or external script. The script must not hide
  content or become necessary for navigation, contact links, or CV access.
- Scrollspy updates only the matching navigation link's `aria-current="location"`.
  Batch geometry reads with `requestAnimationFrame`; use passive scroll handling,
  a stable reading line, and a bottom-of-document fallback so Skills can activate.
  Recalculate after resize, hash changes, page restore, load, and font readiness.
- Preserve native anchor behavior, keyboard focus, fragments, and browser history.
  Do not rewrite the hash during manual scrolling. `#top` and the skip link must
  still work with the script disabled.
- Nav rails expand from 32px to 64px on hover/focus/current state; mobile uses a
  current-item underline. Approximately 150ms transitions match the reference.
- Each `.entry` remains a stationary hover/focus boundary around a positioned
  `.entry-surface`. Its isolated stacking context and stationary transparent
  `::before` buffer cover the expanded hover area behind the surface; retain this
  buffer to prevent flicker at the moving project link's outer edge. It must not
  intercept clicks on the visible project surface. On fine-pointer desktop
  layouts with motion allowed, lift the
  surface 3px with a 220ms return/lift transition. A fine top edge and two-layer
  shadow create depth; sibling entries dim to 0.9 opacity to preserve readability.
- Keep the panel background and expanded project-link hit area positioned
  against `.entry-surface`. Do not transform `.project-footer` independently:
  that would change the stretched link's containing block. Keep focus outlines
  around the expanded target and prevent overlap with neighboring targets.
- Project arrows move 4px up and right on hover/focus. They are decorative and
  must be hidden from assistive technology. All four contact/CV marks inherit
  the link color and lift 3px over 180ms on hover/focus only when motion is
  allowed; their outer 44px link targets remain stationary. The CV mark contains
  only its two letters and has no arrow.
- The radial pointer glow runs only for mouse input on fine-pointer desktop
  layouts when reduced motion is not requested. Keep it `pointer-events: none`
  and `aria-hidden`, batch pointer updates per animation frame, and hide it on
  pointer leave, window blur, or changes to the applicable media query. Its
  diameter is 800px with an explicit 400px radial-gradient radius. Light mode
  uses RGB `59, 130, 246` with center alpha 0.09 and midpoint alpha 0.045;
  dark mode uses RGB `29, 78, 216` with center alpha 0.15 and midpoint alpha
  0.075. The midpoint is at 50% radius; the glow reaches transparency at 100%.
  Pointer-follow movement uses a 140ms transition. Keep the glow hidden for
  printing and preserve its layer behind the content.
- Under `prefers-reduced-motion: reduce`, use immediate scrolling and disable
  transitions, surface/icon lift, arrow movement, and the pointer glow. Static
  hover depth, active navigation, and keyboard focus remain functional. Content
  must never depend on an animation.

## Content rules

- Keep `.role`, `<meta name="description">`, and `og:description` in sync — all
  three currently carry the same sentence.
- Keep the footer's `Last updated` date static and truthful. For content or UI
  changes, synchronize its `<time datetime="YYYY-MM-DD">` value and visible date
  to the actual website update date; do not use the visit date or
  `document.lastModified` to imply an update.
- Keep `LI Zhuofei` in `h1` and `Felix` in a separate `.preferred-name` line
  beneath it, using Inter. The visible `.identity-degree` text is
  `Statistics Undergraduate at HKU`. Keep both the page title and `og:title` as
  `LI Zhuofei (Felix) | Statistics Undergraduate at HKU`; preserve the preferred
  name and undergraduate qualification in these identity labels.
- Entry shape: `.entry-title` = the organisation, institution, or project;
  `.entry-subtitle` = the role, degree, or location; `.entry-meta` = the date.
  Every section follows this, so the first line is always the *what*, not the *who*.
- The supplied CV and LinkedIn are content sources. The owner explicitly chose
  **LinkedIn dates where the sources differ**. The current approved dates are:
  HKU `Sep 2025&ndash;Jun 2029` (expected graduation); PKUSSI `Jul 2026`;
  Shelter Seconds and AirHelper `Jan 2026&ndash;May 2026`; CAS `Jun 2026`;
  IMC Challenge `Jun 2026&ndash;Jul 2026`; Tencent LIGHT Creative Camp
  `Mar 2026&ndash;May 2026`; RSA `Sep 2026&ndash;Present`.
- Date format: single month (`Jun 2026`) or a month-level range with an en dash
  (`Sep 2026&ndash;Present`). Same-year ranges can share the year
  (`Jan&ndash;May 2026`). For the HKU website entry, show `Jun 2029` only in
  the date range; the owner explicitly removed the repeated
  `Expected graduation: Jun 2029` note beside `Minor in Computer Science`.
  This presentation choice does not change the expected date or the Public CV.
- Copy uses HTML entities (`&ndash;`, `&times;`) rather than literal characters.
  Match that.
- **No em dashes in page copy.** The owner asked for them removed, so `&mdash;` and
  a literal `—` appear nowhere in `index.html` and must not come back. A colon,
  parentheses, or a reworked sentence carries the same break. The en dash in date
  ranges is a different mark and stays.
- Keep dates and entry structure consistent across Education, Projects,
  Experience, and Activities, and with the Public CV generated by the CV repo.
- Label course grades and project scores separately. Describe AI, data science,
  and quantitative research as interests unless the source establishes completed
  research work.
- **Do not strengthen claims** about roles, ownership, or outcomes without the
  owner's confirmation. "Participated in" / "Attended" reflect the real scope and
  must not be upgraded to ownership verbs on your own initiative.
- Use clear semantic HTML, keyboard-visible focus styles, and responsive layouts.
- Do not delete or relocate `CNAME`, `index.html`, or `favicon.svg` without
  explicit approval and a reference check.

## Verification before committing

1. Enumerate the current internal anchors, local assets, and external links.
   Confirm targets resolve, `favicon.svg` and `cv.pdf` exist, and HTML parses.
   Record the actual counts rather than carrying forward a fixed reference count.
2. Preview desktop, the 960px layout transition, and narrow mobile widths in
   light *and* dark appearance. Check wrapping, overflow, keyboard focus, and
   navigation to every section.
3. For interaction changes, verify manual scrolling both ways, every anchor,
   bottom-of-page selection, direct fragment loads, browser back/forward,
   keyboard focus, expanded project targets, contact-icon labels/44px targets,
   hover-boundary stability, and pointer leave/blur. Cover
   reduced motion, touch/mobile behavior, disabled JavaScript, the 960/961px
   width transition, and the 640/641/760/761px desktop height transitions.
   Check for runtime errors; do not infer success solely from static inspection.
4. When `cv.pdf` changes, confirm it matches the private repository's Public
   output, inspect extracted text for phone numbers (including `+852`/`+86`),
   and visually check the PDF. Never substitute a Standard or Print variant.
5. Run `git diff --check`, then read the full diff.
6. Update `PROGRESS.md` and, for visual changes, `design-qa.md` with the checks
   actually performed. Do not record incomplete verification as passed.

## Git

- Never commit `.DS_Store`, `.claude/`, temp servers, generated previews, or
  credentials — `.gitignore` covers the first two.
- Preserve unrelated and uncommitted work.
- Keep commits focused; describe the visible or content-level change.
- `AGENTS.md` and `PROGRESS.md` are intentionally tracked. Do not gitignore them.
