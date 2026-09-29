# Design and Interaction QA

Reviewed: 2026-09-30. Branch: `codex/profile-redesign`.
Result: local verification passed; owner authorized committing and pushing the redesign branch. Production Pages source remains `main`.

Latest content cleanup: the PKUSSI description now uses the owner's exact coursework sentence with grades of 95/100 and 87/100, verified in the rendered preview (`.claude/qa/2026-09-30-cv-icon/summer-school-grades.jpg`). Removed the repeated HKU expected-graduation note at the owner's request. Actual preview at `/#education` confirms the minor and CGPA remain, with `Sep 2025–Jun 2029` only in the date column. Screenshot: `.claude/qa/2026-09-30-cv-icon/education-note-removed.jpg`. No style, script or PDF change.

## Current refinement: quiet footer update date

Added `Last updated: Sep 30, 2026` below the footer signature, with a matching
`datetime="2026-09-30"`. It inherits the existing 11px muted footer typography.
The footer can wrap at narrow widths. Actual dark desktop at 1280×720 and mobile
at 375×812 passed, with the complete date visible and no horizontal overflow;
a source-derived light fixture also passed. JavaScript and link destinations
are unchanged; `git diff --check` passed. Evidence is in
`.claude/qa/2026-09-30-footer-date/` (`desktop-dark.jpg`, `mobile-dark.jpg`,
`desktop-light.jpg`). OS appearance settings were not changed.

## Previous refinement: CV letter icon

The CV link now appears as the fourth contact-row target, using only the letters
`CV`. It shares the other icons' 44×44px click area, 24px icon area, color changes,
keyboard outline and 180ms/3px motion. The public `cv.pdf` URL, new-tab behavior,
and `noopener noreferrer` remain; the link has a PDF tooltip and descriptive
accessible name. The former separate CV line, PDF suffix and arrow were removed.

Actual desktop dark and 375×812 mobile screenshots were inspected; the four icons
align in one row, and mobile has no horizontal overflow. Keyboard focus returned
a 2px outline and a sampled in-progress upward transform. Source-derived light
and reduced-motion fixtures were checked; reduced motion computes no transform
and zero transition duration. OS settings were not changed. Main content, script,
all 20 references and public PDF hash are unchanged; IDs are unique and all
internal/local targets resolve. `git diff --check` passed. No full interaction
suite was repeated for this local presentation change.

Evidence: `.claude/qa/2026-09-30-cv-icon/` includes `desktop.jpg`,
`desktop-light.jpg`, `desktop-focus.jpg`, `mobile.jpg`, `desktop-final.jpg`, source-derived
fixtures and a `before/` snapshot. Current four-icon treatment supersedes the
three-icon/separate-CV descriptions in the historical reports below.

## Previous refinement: reference colors and stronger glow

The owner requested stronger illumination and colors closer to Brittany Chiang's
reference. The live reference was inspected again: background `#0F172A`, primary
text `#E2E8F0`, body `#94A3B8`, teal emphasis `#5EEAD4`, and a blue pointer glow
`rgba(29,78,216,.15)` fading to transparent at 480px from its center.

The current dark palette uses those base colors. The glow has an explicit 400px
radius (800px box), center alpha 0.15 dark / 0.09 light, half strength at 50%, and
transparency at 100%. This strengthens the previous 680px / 0.065 dark glow while
keeping a smaller footprint than the reference. The 140ms follow transition remains.
The glow is now behind the content, so it cannot wash over the text. Normal links
and navigation use the main text color; teal is reserved for emphasis, project hover,
and keyboard outlines. Hover panels use translucent slate, with the same lift and
layered shadows. Sibling opacity is 0.9, replacing 0.7 to retain readable body text.
Light mode uses `#F1F5F9`, `#0F172A`, `#475569`, and `#115E59` respectively.
The browser theme colors and favicon were coordinated with the palette.

| Check | Result |
| --- | --- |
| Live reference | Read computed background, heading/body colors, teal accents and glow gradient; saved a reference screenshot. |
| Dark desktop, 1280×800 | New colors and active glow visually inspected. Glow/content layers compute to z=0/1. No horizontal overflow. |
| Project hover | Surface remains at y=-3px; title becomes teal; layered panel shadow and 0.9 sibling opacity confirmed. Full-surface hit still resolves to the original Shelter Seconds source URL. |
| Navigation | Clicking Projects reached the section with exactly one current item. Native scrolling and inline script are unchanged. |
| Light palette | Source-derived light fixture visually inspected with the raised project surface. |
| Reduced motion | Source-derived fixture computes immediate scrolling, hidden glow, and zero surface transition duration. |
| Mobile, 375×812 | Actual source inspected: no overflow or glow, identity wording intact and all three contact targets 44×44px. |
| Readability | CSS alpha-compositing checks at the glow center with dimmed sibling text yield 4.99:1 light / 5.34:1 dark. Normal body contrast is 6.92:1 / 6.96:1. This is a targeted color calculation, not a complete accessibility audit. |
| Preservation | Body markup, copy, links, identity and script are byte-identical to the pre-palette source. Public PDF unchanged. |
| Console and diff | No browser console warnings/errors observed; `git diff --check` passed. |

Evidence: `.claude/qa/2026-09-30-palette/` contains `desktop-glow-dark.jpg`,
`desktop-hover-dark.jpg`, `desktop-hover-light.jpg`, `mobile-dark.jpg`,
`reference.jpg`, `mobile.json`, `contrast.json`, and `before/` source snapshots.
Light and reduced-motion checks used isolated fixtures; OS preferences were not
changed. The existing script tests were not repeated because its bytes are unchanged.
This pass is local and uncommitted. Its colors/glow/opacity values supersede the
historical values in the reports below.

## Previous refinement: softer glow, raised surfaces, contact icons

The preceding revision added the owner's requested refinements after the baseline
interaction pass documented below:

- Glow diameter 1200px → 680px, center alpha 0.035 light / 0.065 dark, a second lower-opacity stop at 35%, and transparency at 70%. Position changes ease over 140ms.
- Stable outer entries contain moving `.entry-surface` elements. Desktop hover/focus lifts the surface 3px over 220ms with two soft shadow layers and a fine top edge. Other entries remain at 0.7 opacity. A stationary transparent buffer covers the original outer hover bounds; the expanded project link stays above it.
- GitHub, LinkedIn, and Email use a horizontal SVG icon row with 44×44px link targets and 24px artwork. Accessible names, native titles, keyboard outlines, and the original destinations remain. View CV stays below the row.
- The identity is `LI ZHUOFEI` / `Felix` / `Statistics Undergraduate at HKU`. Browser and Open Graph titles are `LI ZHUOFEI (Felix) | Statistics Undergraduate at HKU`.

Latest checks:

| Check | Result |
| --- | --- |
| Desktop dark hover | Surface transform measured at y=-3px; layered shadow and 680px glow visually inspected at 1280×720. |
| Project link hit area | A body-area point still resolved to the original Shelter Seconds GitHub link. |
| Hover boundary | A point 14px below the stationary article bottom hit the nonmoving article buffer. Eight sampled states remained hovered at -3px, without the previously identified exit/re-entry gap. |
| Contact accessibility | Three links had explicit names, 44×44px targets, decorative SVGs, and preserved destinations. Email keyboard focus showed a solid outline; icon lift was observed without opening a mail client. |
| Light appearance | Derived light fixture visually inspected in the raised project state. |
| Reduced motion | Derived fixture computed immediate scrolling, hidden glow, no surface or arrow transform, and zero transition duration. |
| Mobile | Actual page reviewed at 375×812; role, preferred name, contact icons, and CV fit. At 320px there was no horizontal overflow. |
| Narrow/short desktop | 961px layout passed. Initial 1280×641 check exposed a clipped CV link after adding Felix; setting the compact page top margin to 32px moved its bottom to y=616.5px and resolved it. |
| Structure and content | Eight surfaces, three labelled SVG links, 20 unchanged reference destinations, unchanged section copy and script, Public PDF parity, and diff whitespace check passed. |

Evidence is in `.claude/qa/2026-09-30-refinement/`: `desktop-identity.jpg`,
`desktop-hover-dark.jpg`, `desktop-hover-light.jpg`, `mobile-identity.jpg`,
`compact-desktop.jpg`, `edge-check.json`, and `responsive.json`. The preceding
files are retained under `before/`. Light/reduced modes use isolated fixtures;
system appearance and motion settings were not changed. The script is byte-for-byte
unchanged, so the earlier 15 passing actual-script smoke cases were not repeated.
No blocking finding remains in this refinement. It is local and uncommitted.

## Baseline interaction pass

The observations below describe the preceding reference-interaction revision.
Current values and screenshots above supersede its 0.5 sibling opacity,
1200px glow, and text-based contact treatment.

## Approved scope and references

The owner first approved the silver-gray/ink-blue profile redesign, then asked
for smooth interactions and explicitly directed matching the reference site's
interactions. The final behavior follows [Brittany Chiang](https://brittanychiang.com/):
current-section navigation, expanding rails, native smooth anchors, desktop
entry hover/focus surfaces and sibling dimming, moving external-link arrows,
project-wide link targets, and a pointer-following radial glow. Reference DOM,
computed styles, and a screenshot were inspected live. Emil Kowalski's
[7 Practical Animation Tips](https://emilkowal.ski/ui/7-practical-animation-tips)
was also consulted before the owner's explicit reference-parity instruction.

The original content and blue palette remain intact. Motion uses CSS and one
inline dependency-free enhancement script. No framework, external script,
scroll-reveal gate, or custom scrolling pane was added.

## Browser verification

| Check | Observation |
| --- | --- |
| Smooth anchor scrolling | Recorded multiple intermediate scroll positions between the initial view and Projects, followed by the expected target position. Scrolling remains natively interruptible. |
| Six navigation targets | About, Education, Projects, Experience, Activities & Service, and Skills each became current at the corresponding reading location. Only one link carries `aria-current="location"`. |
| Manual scrolling | Reverse scroll updated the active item while retaining the existing URL hash. |
| Keyboard navigation | Back to top returned to `#top` at scroll position 0; Skip to content focused `main#content`. |
| History | Browser Back restored Skills at the page bottom; Forward restored the prior Projects position and active item. |
| Page end | Skills became current with zero remaining scroll distance. At 1440×1000, clicking Activities kept Activities current, with its top near 96px and 39px of scroll remaining. |
| Rail feedback | Inactive rails computed as 32px and the active rail as 64px. Color and width transition in 150ms. |
| Entry feedback | Desktop hover/focus highlighted Shelter Seconds and reduced AirHelper opacity to 0.5. The arrow computed a 4px right/up translation. Keyboard focus had a visible full-entry outline. |
| Project target | Hit testing within the project body resolved to the matching source link. Existing native external-link destinations and new-tab behavior are retained. |
| Pointer glow | Mouse position updated the glow coordinates; the overlay remained non-interactive. Reviewed in both palettes. |
| Responsive layout | No horizontal overflow at widths 320, 375, 960, 961, 1280, and 1440. Desktop height checks included 640, 641, 720, 900, and 1000. At 1280×641, the 564.5px sidebar plus 32px offset fits the viewport. |
| Mobile | At 375×812, the identity area and wrapped navigation remain in document flow, current navigation uses an underline, and desktop glow/hover panels are disabled. |
| Reduced motion | Forced-mode fixture computed `scroll-behavior: auto`, zero-duration nav transitions, hidden glow, and immediate Skills positioning with correct highlighting. |
| No JavaScript | Script-free fixture had zero scripts and zero false current markers. Native Projects and Skills anchors reached their targets; the CV link still resolved to `/cv.pdf`. |
| Console | No errors or warnings were returned during inspection. |

The initial redesign's Back to top, skip-link focus, public PDF rendering, and
other baseline content/layout checks remain recorded in `PROGRESS.md` and the
original `.claude/qa/2026-09-30/` evidence. No content/PDF change occurred in this
interaction pass.

## Source and script checks

- HTML IDs remain unique; all 20 references are unchanged and internal/local targets resolve.
- Page copy is unchanged after excluding decorative arrow characters. Dates, metadata, domain, public PDF, and existing symlinks are preserved.
- Inline script syntax check and `git diff --check` passed.
- A separate Node VM ran the actual inline script through 15 behavior checks; 15 passed and none failed. Coverage includes upward/downward scroll, footer selection, resize and geometry changes, load/font/history events, event coalescing, conditional pointer motion, pointer leave/blur, and safe missing-section exit.
- A burst of 80 scroll/resize events resulted in one queued geometry update; a pointer burst resulted in one frame using the last coordinates. These are controlled behavior checks, not a real-device frame-rate benchmark.
- Public PDF remains byte-identical to the canonical private-repository Public output. SHA-256: `ef03dc28ae061e6b05f889623e06251d47674f107ca1ee87b1b0c8b271d46ced`.
- Independent review of the implementation and revised repository instructions found no blocking issue.

## Evidence and limits

Current evidence is in the ignored directory
`/Users/lizhuofei/projects/Felix-Li-0306/lizhuofei.com/.claude/qa/2026-09-30-motion/`:

- `smooth-scroll-samples.json`: intermediate native scroll positions.
- `responsive.json`: viewport, overflow, sidebar, and active-item checks.
- `project-focus-dark.jpg`, `project-hover-dark.jpg`: actual dark desktop interaction states, including keyboard focus.
- `project-hover-light.jpg`: light palette hover/focus state.
- `mobile-top.jpg`, `mobile-projects.jpg`: actual mobile first screen and Projects state.
- `mobile-final.jpg`: final actual mobile Projects state.
- `smoke.cjs`, `smoke-results.json`, `inline-script.snapshot.js`: actual-script VM checks and results.
- `before/`: the preceding local revision of the changed files.

Light, reduced-motion, and no-script browser checks used local fixtures derived
from the current source. Light forces the light palette; reduced mode forces
both CSS and script media conditions; no-script removes only the script. Asset
links are root-relative in these fixtures so their own fragment navigation
remains intact. Operating-system appearance/motion settings were not changed.
The actual source media queries were reviewed, and the VM independently tested
the script's reduced-motion/pointer conditions.

A background/stale browser tab produced an inconclusive navigation wait; that
attempt was not counted as a pass. The corresponding checks were repeated in a
fresh active preview tab with visible final positions and navigation state.

No blocking layout or interaction defect remains in the tested states. Fonts
still use Google Fonts with system fallbacks. Live GitHub Pages behavior and
production asset parity were not checked because this revision is local.
