# Portfolio Refresh — Design Spec

**Date:** 2026-04-16
**File touched:** `index.html` (single-page portfolio)
**Status:** Draft for review

---

## Problem

The portfolio (`index.html`) has drifted from current reality on multiple fronts:

1. **CVstomize** copy describes an ATS-optimized resume generator. The product has pivoted to a 3-pillar shareable identity platform — "CVstom Portfolios become the next resume."
2. **NoteXT** copy describes an SMS-first reminder system. The product is now a multi-channel agent (PWA + native + SMS) with a distinguishing **reverse-escalation alert chain** (push → SMS → persistent notification → call) that has a provisional patent draft.
3. **About Me** uses corporate-speak ("results-driven AI Automation Specialist," "formally validated by") that obscures the actual story: a self-taught engineer who learned AI by using AI to build production systems. The DOL-recognized IBM apprenticeship is one credential earned via that path, not the validator of the underlying work.
4. **Visual hierarchy** treats the two showcased projects (CVstomize, NoteXT) the same as 8 other repos. The "showcased" framing isn't honored.
5. **Atrium-Core** display name doesn't match the actual repo slug (`Atrium-Core---Master-Jewler`).
6. **CVstomize live site** (`cvstomize.vercel.app` → cvstomize.com) is not linked.
7. **Other secondary cards** (HuminLoop, AInsworth, ai-dev-workflow, PathaDex, Universal-Desktop-Automator, HoverChair) need a quick copy audit against current GitHub state.
8. Other sections (Hero, AI Advocacy, DIRTEE, Professional Journey, Hands-On Engineering, Skills, Contact) need a light audit pass for accuracy and tonal consistency with the reframed About Me.

## Goals

1. Refresh CVstomize and NoteXT featured cards with authoritative content from the current READMEs and the user's most recent state summary for NoteXT.
2. Visually elevate the two featured cards above the secondary project grid.
3. Reframe About Me to honestly own the self-taught-with-AI story without adding new sections or restructuring the page.
4. Lightly audit every remaining section for accuracy and tone consistency.
5. Sync stale metadata (Atrium-Core repo slug acknowledged in spec; CVstomize live link added).
6. Preserve the existing visual design language (dark glassmorphism + sky accent, Inter font, Lucide icons, Tailwind CDN) and all working interactive behavior (header scroll effect, mobile menu, architecture diagram modal).

## Non-Goals

- No new sections added. No sections removed.
- No image or diagram assets created or sourced. The `images/` and `diagrams/` folders remain empty; the existing placeholder text fallbacks continue to work as designed.
- No changes to Daemonstrate (user is updating it separately).
- No changes to dotfiles or desktop-tutorial repo coverage (intentionally not surfaced).
- No live GitHub API integration for stars/last-updated metadata. Static copy is acceptable.
- No changes to the Jekyll workflow or any GitHub Actions.
- No new color tokens, fonts, or libraries.
- No "How I Learn" or self-taught-themed dedicated section. The reframe is tonal, contained to existing sections.

## Design — Section-by-Section

### Hero (`#home`)

- **Title** stays: "From Hands-On Hardware to AI-Powered Automation."
- **Subtext** lightly revised to lead with the self-taught builder identity rather than generic curiosity. Replace the existing single paragraph with a 2-sentence version that names the self-taught path explicitly without apology.
- CTAs unchanged ("View My Work," "Get In Touch").
- Background image and gradient unchanged.

### About Me (`#about`)

Full rewrite of the body copy. The new version owns three things explicitly:

1. **Self-taught engineer** who learned by building, with AI as both teacher and collaborator.
2. **One formal credential**: the DOL-recognized IBM Systems Support Apprenticeship — earned through a self-driven path, not a substitute for the work it followed.
3. **The meta-angle**: using AI to learn how to use AI, then using both to ship production systems.

Tone: confident, specific, no LinkedIn-speak. No words like "results-driven," "expertly combine," "formally validated." Keep DIRTEE mention in the second paragraph (it's a hand-off into the next section).

Headshot block (left column) unchanged structurally.

### AI Advocacy (`#advocacy`)

Light edit. The "why don't we just get Nolan to automate it with AI?" anecdote is good and stays. Trim any redundancy with the new About Me. Tighten the "this advocacy often starts with me using AI to streamline my own workflows" passage to avoid restating what About Me now says.

### DIRTEE Methodology (`#dirtee`)

No structural changes. This section is the user's signature work. Light audit only:
- Verify CVstomize and Ainsworth examples match current product reality.
- Confirm tone is consistent with reframed About Me.

### Professional Journey (`#experience`)

Timeline content stays. Light copy tightening only. Three items remain:
- Test Technician — Benchmark Electronics (Sep 2025–Present)
- System Support Specialist — IBM Apprenticeship (Feb 2024–Feb 2025)
- Server Trainer — Texas Roadhouse & Red Lobster (2015–2024)

The IBM entry's prose can drop the apprenticeship-as-validation framing (which now lives in About Me).

### GitHub Repositories (`#projects`)

Restructured into three vertical zones:

1. **Featured pair** — CVstomize and NoteXT in a 2-column grid (stacks on mobile). Each card is taller than the existing featured cards, with structured sub-blocks for tagline, hook, mini "pillars/how-it-works," tech chips, status badge, and a CTA row.
2. **Daemonstrate standalone** — unchanged from the current standalone slot below the featured pair. (User is updating separately.)
3. **Secondary projects grid** — 3 columns on desktop, denser cards, single CTA per card. Contains: HuminLoop, AInsworth, ai-dev-workflow, PathaDex, Atrium-Core, Universal-Desktop-Automator, HoverChair.

#### Featured Card: CVstomize.com

| Element | Content |
|---|---|
| Tagline | Your professional identity, organized and shareable. |
| Hook | CVstom Portfolios become the next resume. |
| Pillars block | Three sub-rows: **CV Wizard** (conversational AI builds your profile through dialogue), **CVstom Profile** (single source of truth for skills/experience/projects), **CVstom Portfolio** (shareable identity at cvstomize.com/u/yourname with viewer-toggleable lenses) |
| Status badge | "MVP in progress" |
| Tech chips | React 18 · Material-UI · Vertex AI (Gemini 2.5) · GCP Cloud Run · PostgreSQL · Firebase Auth |
| CTAs | **Live Site** (cvstomize.vercel.app, opens new tab) · **View Architecture** (opens existing modal with `cvstomize.drawio`) |
| Privacy badge | Private (existing yellow lock badge) |

#### Featured Card: NoteXT

| Element | Content |
|---|---|
| Tagline | An intelligent AI agent that handles logistics. Notes are a byproduct. |
| Hook | Reverse-escalation alerts: push → SMS → persistent notif → call. First ack wins. |
| How-it-works block | Abbreviated Will/donuts example (3 short lines): user texts a task → system extracts intent + asks clarifying SMS → calculates "leave by" time from Maps + Places + learned routine, alerts via the escalation chain |
| Status badge | "Provisional Patent Drafted · 237/237 server tests passing" |
| Tech chips | Express 5 · React 19 PWA · Expo SDK 55 · PostgreSQL 16 · Twilio · Gemini · Web Push |
| CTAs | **View Architecture** (opens existing modal with `noteXT.drawio`) |
| Privacy badge | Private (existing yellow lock badge) |

#### Secondary Grid

Each secondary card uses the existing compact card pattern but tightened:
- Image area at the top (existing placeholder fallback)
- Title + privacy badge row
- 1-line description (truncate any longer to keep grid uniform)
- Single CTA: **View** for public repos (links to GitHub), **Architecture** for private repos (opens diagram modal)

Specific copy notes within secondary cards:
- **HuminLoop**: copy verified; description matches current GitHub state. No change beyond layout tightening.
- **AInsworth**: keep DIRTEE-method mention since it ties back to the methodology section. Trim verbose passages.
- **ai-dev-workflow**: copy verified; matches GitHub state.
- **PathaDex**: copy verified.
- **Atrium-Core**: keep readable display name "Atrium-Core" (the actual repo is `Atrium-Core---Master-Jewler` with the typo "Jewler"). No external link added since the repo is private. Spec acknowledges the actual repo slug for any future linking.
- **Universal-Desktop-Automator**: copy verified.
- **HoverChair**: copy verified; ESP32 + Raspberry Pi + AI-Assisted chips stay.

### Hands-On Engineering (`#engineering`)

Light audit. Five existing cards (Gas-Powered Air Compressor, PCB Controller Rebuild, Network-Wide Ad Blocker, Integrated Fume Extractor, Home Lab Renovation) all stay. These reinforce the self-taught-builder identity nicely. Light copy tightening only.

### Skills (`#skills`)

Three-column structure stays (AI & LLM Development, Process & Workflow Automation, Full-Stack & Operations). Light audit:
- Review each bullet for currency.
- Drop or replace anything stale.
- Do not restructure into different categories.

### Contact (`#contact`)

No changes. Email, LinkedIn, GitHub links all current.

### Footer

No changes.

## What Does Not Change (global)

- Header, navigation, mobile menu, scroll-effect, footer.
- Color tokens (`#38bdf8` sky accent, `#111827` body bg, `#1f2937` glassmorphism).
- Tailwind CDN, Lucide icons, Inter font.
- All existing JavaScript: `lucide.createIcons()`, header scroll effect, mobile menu toggle, architecture diagram modal (`openDiagram`/`closeDiagram` and Escape-key handler).
- Architecture diagram modal markup.
- Image placeholder fallback pattern (`img:not(.hidden) + .img-placeholder`).

## Technical Approach

This is a single-file change to `index.html`. The bulk of the work is HTML/Tailwind class restructuring and copy rewrites. No new JS, no new CSS classes beyond what Tailwind provides. The existing `.glassmorphism` class, `openDiagram()` function, and Lucide icon library are reused.

### Component Boundaries (within the single file)

- **Featured card pattern** — a repeatable HTML block: image area, header (title + privacy badge), tagline, hook, structured sub-block (pillars or how-it-works), tech chips, status badge, CTA row.
- **Secondary card pattern** — a tighter HTML block: image area, header, 1-line description, single CTA.
- **Section copy blocks** — straight HTML/text edits in About Me, AI Advocacy, Hero, etc. No structural changes.

The two card patterns are not extracted into anything reusable (this is a static HTML page); they are repeated inline. Tailwind utility classes carry the structural styling.

## Risks & Trade-offs

- **Empty image/diagram folders mean placeholder text shows in production.** Pre-existing condition; not introduced or fixed by this change. User is aware.
- **Static metadata (stars, last-updated) will drift from GitHub reality.** Acceptable trade-off — chosen against live API integration to avoid auth complexity for private repos.
- **Atrium-Core display name vs. actual repo slug differ.** Readability prioritized over strict accuracy. Spec acknowledges the discrepancy explicitly.
- **No tests.** A static HTML portfolio is verified by visual inspection. No test infrastructure exists or is added.
- **About Me reframe is subjective.** The new wording will need user review. Spec captures intent (own self-taught path, drop corporate-speak, name AI as teacher and collaborator) but final wording is a content decision the user should sign off on during implementation.

## Success Criteria

- Featured cards (CVstomize, NoteXT) visually distinct from secondary grid (taller, richer content blocks, more CTAs).
- All copy in both featured cards traceable to either the repo README or the user's 2026-04-16 state summary.
- About Me no longer contains "results-driven," "expertly combine," or "formally validated by" phrasing. New copy explicitly names the self-taught path and AI's role as teacher and collaborator.
- CVstomize live site link works (opens cvstomize.vercel.app in a new tab).
- All other sections audited and copy-tightened where stale; no structural changes outside `#projects`.
- No broken existing functionality: scroll behavior, mobile menu, architecture diagram modal, lucide icons all still work.
- Page renders without console errors in a modern browser.

## Out of Scope (explicitly deferred)

- Daemonstrate updates (user-managed, separate session).
- Image/diagram asset creation or sourcing.
- Live GitHub metadata fetching.
- Any new sections (e.g., "How I Learn," "AI Learning Journey") — explicitly deferred per user choice of lighter-touch reframe.
- Any backend, build, or deploy changes.
- Restructuring of DIRTEE, Skills, Hands-On Engineering, or Professional Journey sections.
