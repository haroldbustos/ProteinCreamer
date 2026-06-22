# Handoff: Claire Foods — Waitlist / Concept-Validation Landing Page

## Overview
A premium, single-page DTC marketing site for **Claire Foods**, a Canadian food-innovation company. The page promotes a **concept-stage, high-protein, plant-based POWDERED coffee creamer** (powder only — not a liquid). The site's job is **market validation, not sales**: collect email signups, run interactive polls, and gather feedback. Primary KPIs are **email signups and poll/survey participation**.

Key messaging pillars: innovative, optimistic, premium, science-backed, friendly, trustworthy, distinctly Canadian. Avoid earthy/organic health-food clichés — aim for the polish of Apple / NotCo / Oatly / AG1 / Ritual.

## About the Design Files
The files in this bundle are **design references created in HTML** — a working prototype showing intended look, layout, copy, and interactions. They are **not production code to copy directly**. The task is to **recreate this design in the target codebase's environment** (the brief called for React + Tailwind + Framer Motion) using its established patterns, component library, and animation approach. If no environment exists yet, React + Tailwind + Framer Motion is the recommended stack and matches the original intent.

> Implementation note: the prototype is authored as a single "Design Component" HTML file with inline styles and a small vanilla-JS logic class. Treat the inline styles as the source of truth for visual values; re-express them as Tailwind classes / styled components and convert the hand-rolled animations to Framer Motion.

## Fidelity
**High-fidelity (hifi).** Final colors, typography, spacing, copy, and interactions are all specified. Recreate the UI pixel-faithfully, then map values onto the codebase's design system where one exists.

## Design Tokens

### Colors
| Token | Hex | Use |
|---|---|---|
| Claire Magenta (primary) | `#E51C8D` | Dominant accent, all primary CTAs, progress fills, highlights |
| Magenta hover/dark | `#C0107A` | Button hover, gradient end |
| Magenta deep | `#9C0A60` | Final-CTA gradient end |
| Magenta light | `#FF66BC` | Gradient starts, dark-section accents |
| Leaf Green (secondary) | `#7FB935` | Plant-based / sustainability cues, success states, check badges |
| Green light | `#A9DB5A` | Gradient start |
| Green dark | `#6FA82B` | Gradient end, leaf shapes |
| Green deep | `#5C8F22` | Eyebrow text on light |
| Cream White (page bg) | `#FBF8F2` | Default background |
| Warm Beige (alt bg) | `#F3EBDD` | Alternating section background |
| Rich Coffee Brown | `#2A1A12` | Primary text |
| Dark espresso (dark sections) | `#1F140E` | Community section + footer background |
| Body text muted | `#5A4A40` | Paragraph copy |
| Text subtle | `#6A5A50`, `#8A7A6E` | Card descriptions, meta |
| Border subtle | `rgba(42,26,18,0.1)` | Card borders |

### Typography
- **Display / headings:** `'Bricolage Grotesque'` (Google Fonts), weights 400–800. Used at 700–800. Tight tracking on large headings: `letter-spacing:-0.02em` to `-0.03em`; `line-height` 0.98–1.04.
- **Body / UI:** `'Hanken Grotesk'` (Google Fonts), weights 400–700.
- Heading sizes use `clamp()`:
  - H1 hero: `clamp(40px,6vw,76px)`
  - Section H2: `clamp(30px,4.4vw–4.6vw,52–56px)`
  - Body: `clamp(17px,1.5vw,20px)` for lead, 14.5–18px elsewhere.
- `text-wrap:balance` on the hero H1.

### Spacing / Radius / Shadow
- Section vertical padding: `clamp(64px,8vw,110px)`; horizontal `28px`. Hero slightly larger.
- Max content width: `1240px` (nav/hero), `1180px`, `1100px`, `1080px`, `1000px`, `820px` (FAQ) depending on section.
- Border radius: pills `999px`; cards `16–22px`; inputs `11–14px`; chips `14px`.
- Card shadow on hover: `0 14px 30px -14px rgba(42,26,18,0.3)` (varies per card).
- CTA shadow: `0 10px 26px rgba(229,28,141,0.34)`.

## Screens / Views
This is a single long-scroll page. Sections in order:

1. **Sticky Nav** — translucent blurred bar (`backdrop-filter:blur(14px)`, `rgba(251,248,242,0.78)`). Left: logo image (38px) + "Claire Foods" wordmark (Bricolage 800, 20px). Center: links — Concept, Benefits, Survey, Community, FAQ (anchor links `#concept` etc.). Right: magenta pill CTA "Join the Waitlist" (`#waitlist`). **Links hide ≤820px** (no hamburger in current design — add one if desired).

2. **Hero** (`#top`) — two-column grid (`1.05fr 0.95fr`). Left: status pill ("Concept in validation · Help shape it" with pulsing dot), H1 "What if your coffee creamer actually **added nutrition?**" (word "added nutrition?" in magenta; **animates in word-by-word from a mask on load**), subhead, two CTAs (magnetic hover) "Join the Waitlist →" + "Take the Survey", four trust badges (green check circles): Canadian Innovation, Plant-Based, High-Protein Concept, Customer Driven. Right: **abstract logo-inspired animated stage** — large morphing magenta blob, rotating conic-gradient "coffee swirl" ring, two green leaf shapes (floating), white circular center holding the logo, three floating info chips ("20g protein*", "Plant-based", "Scoopable powder"). Disclaimer line below: target concept attributes illustrative. Background: two large blurred parallax blobs (magenta top-right, green bottom-left).

3. **Problem** (white bg) — H2 "Most creamers add calories. Not much else." + lead. Five fade-up cards: Added sugars, Empty calories, Artificial ingredients, No nutritional value, Dairy concerns. Each has a magenta "✕", title, description.

4. **Concept** (`#concept`, beige bg) — centered H2 "A better morning ritual." Grid of 8 cards (7 benefit + 1 magenta "Shape it with us →" card): High protein, Rich creamy texture (powder dissolves smooth — no clumps), Plant-based, Low sugar, Great taste, Sustainable sourcing, Canadian-made, + convenient powder format messaging. Cards **tilt in 3D toward cursor on hover** (data-tiltgroup). Dashed disclaimer chip: "Final product specifications will be influenced by customer feedback."

5. **Customer Input poll** (`#survey`, white) — H2 "What matters most in a coffee creamer?" 6 selectable cards (More protein, Better taste, Lower sugar, Cleaner ingredients, Sustainability, Dairy-free alternatives). Clicking casts a vote → shows animated % bar + vote count + ✓ badge. **Re-clicking the current choice clears it; clicking another switches.** Votes persist in localStorage. Selected card reserves right padding so % doesn't collide with the ✓ badge.

6. **Flavor poll** (cream bg) — H2 "Which flavor would you try first?" 5 cards each with a color swatch circle: Original Cream, Vanilla, Caramel, Hazelnut, Mocha. Same vote/bar/persist behavior (green fill).

7. **Packaging vote** (white) — H2 "Help us choose." 3 cards with **distinct package silhouettes** (CSS-drawn): **The Tub** (resealable canister, magenta), **The Pouch** (stand-up pouch w/ seal + hang-hole, green), **The Sachets** (3 fanned single-serve sticks, espresso). Vote/bar/persist behavior; selected shows "✓ Your pick" tag.

8. **Benefits** (`#benefits`, beige) — H2 "Why this idea resonates." 6 numbered cards (01–06): More nutrition from existing habits, Convenient protein intake, Plant-based innovation, Better morning routines, Sustainability, Canadian food innovation. 3D tilt group.

9. **Community** (`#community`, dark `#1F140E`) — H2 "Join the early-access community." Three **count-up metric** cards (animate from 0 when scrolled into view): Waitlist members (base 4,218+), Survey responses (9,347+), Feature votes (26,104+). Below: 5 green-check benefit lines. Radial magenta/green glows in corners.

10. **Brand Story** (cream) — two-column. Left: H2 "Proudly Canadian. Built with consumers." + paragraph + 3 tag chips. Right: rounded panel with floating blob + leaf shapes and a `[ brand imagery ]` placeholder (drop a real photo here).

11. **FAQ** (`#faq`, white) — H2 "The honest answers." Accordion, 7 items (one open by default). Q's: Is the product available yet? When will it launch? Is it a powder or liquid? (powder only) How can I influence development? What protein sources? Will it be vegan? Will it dissolve and froth well? How to join testing? "+" icon rotates 45° to "×" on open; body max-height/opacity transition.

12. **Final CTA / Waitlist** (`#waitlist`, magenta gradient bg) — H2 "Help shape the future of coffee creamer." Glassmorphic form: Name + Email (row, stacks ≤560px), optional textarea "What would make you switch to a new coffee creamer?", dark "Join the Waitlist →" button. On submit → swaps to success state ("You're in. Welcome to ClaireFoods." with check). 

13. **Footer** (dark `#1F140E`) — two-column. Left: logo + wordmark, blurb, (social links were removed). Right: "Stay in the loop" newsletter email form with its **own inline success state** ("You're on the list. Talk soon!"), quick links (Concept, Survey, FAQ, Contact → opens a contact modal), legal row (© + Privacy Policy + Terms of Use). 

## Interactions & Behavior
- **Hero headline:** word-by-word mask reveal on load via `revealUp` keyframe, staggered ~70ms.
- **Scroll reveals:** elements tagged `data-reveal` fade up (opacity 0→1, translateY 28px→0) via IntersectionObserver (threshold 0.12). Staggered `transition-delay` per card. Safety timeout reveals all after 2.8s.
- **Parallax:** `data-parallax="0.06|0.12"` blobs translate on scroll.
- **3D tilt:** cards in `data-tiltgroup` (and `data-tilt`) rotateX/Y toward cursor (`perspective(820px)`, max ~6.5°/8.5°), lift + scale 1.015; smooth spring-back on leave. **Only on `(hover:hover) and (pointer:fine)`** — disabled on touch.
- **Magnetic buttons:** `data-magnetic` CTAs translate toward cursor (×0.32 / ×0.42). Touch-disabled.
- **Polls:** click to vote; re-click current = clear; click other = switch. Bars animate width `0.9s cubic-bezier(.22,1,.36,1)`. Percentages computed from seeded base counts + the user's vote. Persist to `localStorage['claire_votes'] = {choices:{matters,flavor,pack}}`.
- **Count-up metrics:** trigger once on scroll into view, 1.7s ease-out cubic.
- **FAQ accordion:** single-open; toggle max-height + opacity; icon rotate.
- **Waitlist + footer forms:** on submit, optionally POST to a Google Apps Script endpoint (see below), then show success state. `localStorage['claire_joined']='1'`.
- **Contact modal:** footer "Contact" opens an accessible modal (overlay + Escape/backdrop close).
- **Reduce-motion:** a `reduceMotion` flag disables reveals, parallax, tilt, magnetic, count-up, and the headline animation — render everything static. Honor `prefers-reduced-motion` in the real build.

## State Management
- `choices: {matters, flavor, pack}` — each null or an option key. Persisted.
- `joined: boolean` — persisted; gates form success vs. form.
- `faqOpen: number` — index of open FAQ item (-1 = none).
- `name, email, why` — controlled form fields.
- `metric: 0→1` — count-up progress.
- Poll counts: seeded base maps (e.g. matters: protein 1342, taste 1521, sugar 898, clean 1087, sustain 756, dairy 1231; flavors: original 1412, vanilla 2587, caramel 1498, hazelnut 1376, mocha 1334; packs: a 1445, b 1392, c 987). The user's current choice adds +1 to that option for display.

### Configurable props (tweakables)
- `sheetEndpoint` (string) — Google Apps Script Web App `/exec` URL. Empty = demo mode (success state only, nothing sent). See `google-sheet-setup.md` (included) for the full Sheet + Apps Script setup. Form sends `name, email, reason, source, timestamp` as `FormData` via `fetch(..., {mode:'no-cors'})` (fire-and-forget; can't read response).
- `proteinGrams` (int, default 20) — drives the hero "20g protein*" chip.
- `waitlistMembers` (int, default 4218) — base for the count-up metric.
- `reduceMotion` (boolean) — static render.

## Responsive Behavior
- ≤820px: nav links hidden; hero / brand-story / footer grids collapse to 1 column; community metrics stack; hero stage caps at 380px.
- ≤560px: waitlist Name/Email row stacks; hero stage caps at 300px.
- Recommend adding a mobile hamburger menu for the hidden nav links in the production build.
- Minimum tap target 44px for mobile.

## Assets
- `assets/claire-logo.png` — Claire Foods logo (magenta seed cradled by two green leaves; white-safe version). Included in this bundle. Used in nav, hero center, package mocks, footer.
- All other visuals (blobs, leaves, swirl, package silhouettes, steam) are **CSS/markup-drawn** — no image files. Re-create with CSS/SVG or Framer Motion.
- `[ brand imagery ]` placeholder in Brand Story — needs a real lifestyle/product photo.
- Fonts: Bricolage Grotesque + Hanken Grotesk via Google Fonts.

## Files
- `Claire Foods.dc.html` — the full design prototype (all sections, styles, and logic). **Primary reference.**
- `google-sheet-setup.md` — step-by-step to wire the forms to a Google Sheet.
- `assets/claire-logo.png` — logo asset.
