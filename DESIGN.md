# Design brief: samanehzamanifard.github.io (v3)

## Subject, audience, job
- **Subject:** a human-centered computing researcher (eye tracking and pupillometry, LLM reasoning,
  AI tutors) on the faculty job market.
- **Audience:** search committees skimming dozens of candidate sites, plus collaborators and students.
- **Primary job:** in about 10 seconds, show who she is, what her research agenda is, and where the CV is.
  Everything else stays one click deeper.

## Feedback this version answers
1. "Too crowded": fewer elements per screen, more white space, and detail moved behind clicks.
2. "No dark blue background": light only. No dark mode, and no inverted navy band.
3. "Picture in a circle frame": circular portrait, which also clips the gaze heatmap.
4. "Professional icons": one consistent line-icon set (Lucide geometry: 24px grid, 1.75 stroke, round caps),
   inlined as an SVG sprite, so there's no icon font and no extra requests.

## The one bold idea (kept, quieter)
The circular portrait is still a live eye-tracking stimulus. Where a visitor's cursor rests becomes a fixation
heatmap. Its only text is a one-line hint with an eye icon. No counter, button or paragraph.

## Color tokens (light only)
| token           | hex       | role |
|-----------------|-----------|------|
| `--bg`          | `#FFFFFF` | page |
| `--surface`     | `#F3F6F5` | quiet sage-grey panels (highlights strip, agenda tiles, honors) |
| `--ink`         | `#1E2329` | text: neutral charcoal, no blue cast |
| `--ink-soft`    | `#56606B` | metadata, dates |
| `--line`        | `#DDE3E1` | hairlines and dividers |
| `--accent`      | `#0B6E79` | deep teal: links, primary button, icons, photo ring |
| `--accent-soft` | `#E2F0F1` | icon tiles, hover fills |
| `--amber`       | `#D9961A` | one accent dot (status) and the heatmap's warm end. Never text. |

No gradients as decoration and no drop shadows. Panels are separated by tint, not by borders or shadows.

## Type
- **Familjen Grotesk** for headings, navigation, buttons and labels. **Literata** for reading text.
- Scale 1.25 (major third) on a 17px base: 13.6 · 17 · 21.3 · 26.6 · 33.2 · 41.5; hero name `clamp(40px, 6vw, 64px)`.
- Measure ≤ 65ch. Sentence case. No all-caps labels.

## Spacing and radii
- 8px base: `4 8 12 16 24 32 48 72 112`. Sections are separated by 112px on desktop and 72px on mobile.
- Radii by role: buttons and pills `999px`; panels and icon tiles `12px`; portrait `50%`.

## Layout
```
┌──────────────────────────────────────────────────────────────┐
│ Samaneh Zamanifard        Research  Publications  Teaching … │  slim sticky white nav
├──────────────────────────────────────────────────────────────┤
│  ● Seeking faculty positions                  ╭────────╮     │
│  Samaneh Zamanifard, Ph.D.                   │ photo  │     │  circle, teal ring
│  one-sentence research statement             │ +heat  │     │
│  [Download CV] (Email) (Scholar)              ╰────────╯     │
│                                               eye-icon hint  │
├──────────────────────────────────────────────────────────────┤
│ [icon] Meta Fellow  [icon] 20 papers  [icon] 1,317 students … │  surface strip
├──────────────────────────────────────────────────────────────┤
│ Research agenda: 3 tiles (icon, title, 2 sentences)          │
│ Projects: 2-column list, 1–2 sentences each                  │
│ Publications: 6 selected + "Show all 20"                     │
│ Teaching | Experience (compact timeline) | Honors | Contact  │
└──────────────────────────────────────────────────────────────┘
```
Content is left aligned in a centered 1080px column, with an asymmetric hero (text 7/12, photo 5/12).

## Review against defaults
- Cards with shadows: the SaaS default. **Rejected.** Tiles are flat tint with no border.
- Icons in colored circles everywhere: the template look. **Changed** to small rounded-square tiles, and only in
  the highlights and agenda. Buttons and links get inline icons.
- Full publication list on the page: accurate but crowded. **Changed** to a selected list with the full list in a `<details>` element.

## History
- v1: scanpath over the name, navy-ink palette, side rail. v2: live heatmap portrait, agenda and teaching sections.
- v3: this version, after feedback on crowding, dark backgrounds, photo shape and icons.

## Pass 2 critique log (v3: 1440×900 and 375×812, light only)
| # | Gate | Finding (measured) | Fix |
|---|------|--------------------|-----|
| 1 | WCAG 2.5.8 | Nav brand link was 165×17px; 16 DOI links in the full list were 21×32px | Brand is 44px tall; DOI links are at least 32×32px |
| 2 | Type scale | Off-scale sizes: 15.98px ×109, 18.02px ×34, 15.3px ×8 | Added `--t-sm` 16px; now exactly 6 sizes: 13.6, 16, 17, 21.3, 41.5, hero |
| 3 | Alignment | Highlights text at x=296 vs Honors tile text at x=292 (4px seam) | Same padding (24) and gap (12) on both; both now at 288 |
| 4 | Mobile, seen in screenshot | Touch hint wrapped to 2 lines, leaving the eye icon stranded | Shorter copy, now one line (19px) |
| 5 | Mobile measure | Agenda tiles kept the icon column, about 25 characters per line | Icon stacks above text below 760px; text is 279px wide |
| 6 | Rhythm | Publication authors sat flush against the title | 4px gap |

Passing as built: contrast 267/267 (desktop) and 266/266 (mobile); focus ring 5.96:1 at 3px; one h1, no skipped
levels; no duplicate link names; 4 text colors and 3 corner radii, all from tokens; no horizontal page overflow.
Left as-is on purpose: the mobile nav scrolls sideways (the probe lists it as overflow by design), and the type
treatments for link-like controls are deliberate tiers (nav, primary, secondary, text link, DOI).
