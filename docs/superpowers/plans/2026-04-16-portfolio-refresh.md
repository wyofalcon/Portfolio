# Portfolio Refresh Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Execute the full-portfolio refresh defined in `docs/superpowers/specs/2026-04-16-portfolio-refresh-design.md` — rewrite About Me, tighten every section, restructure the projects section into featured-pair + Daemonstrate + secondary-grid zones, update CVstomize and NoteXT featured cards with current product reality, and fix a diagram-modal branch bug discovered during planning.

**Architecture:** Single-file edits to `index.html`. No new files, no new JS, no new CSS classes beyond Tailwind utilities. All existing interactive behavior (scroll header, mobile menu, diagram modal, Lucide icons) preserved. Each task edits a contiguous section of the file so conflicts between tasks are impossible; tasks are ordered top-down in document order so line numbers from earlier tasks don't invalidate later tasks.

**Tech Stack:** Static HTML5, Tailwind CSS v3 (CDN), Lucide icons (CDN), Inter font (Google Fonts), draw.io viewer iframe (existing).

---

## Pre-flight: Branch and verification setup

### Task 0: Confirm working state and verify local preview works

**Files:**
- Read: `index.html`

- [ ] **Step 1: Confirm clean working tree**

Run: `git status`
Expected: `working tree clean` on branch `master`. If not clean, stash or commit current work first.

- [ ] **Step 2: Open the current `index.html` in a browser for before/after reference**

Use VS Code's Live Preview, or open the file directly:
- Windows: `start index.html` (from the repo root)
- Or: drag `index.html` into a browser tab

Expected: Page renders. Placeholder text for images is visible (e.g. "headshot.jpg", "Screenshot: images/noteXT.png"). This is pre-existing and expected.

- [ ] **Step 3: Open browser devtools console; confirm zero errors**

Expected: No errors in the Console tab. Lucide icons render (not as `<i>` tags with data attributes but as inline SVGs).

- [ ] **Step 4: Click "View Architecture" on any featured card**

Expected: Modal opens. The iframe will show a 404-style error from viewer.diagrams.net because the current code references `/main/` branch and your branch is `master`. This is the bug Task 11 fixes. Note it mentally and close the modal.

**Do not commit anything in this task.** This is verification-only.

---

## Part A: Top-of-page copy updates (Hero, About Me, AI Advocacy)

### Task 1: Revise Hero subtext

**Files:**
- Modify: `index.html:139-141`

**Context from spec:** Keep current title ("From Hands-On Hardware to AI-Powered Automation"). Revise the subtext paragraph to lead with self-taught builder identity, 2 sentences, no "relentless curiosity" corporate-speak.

- [ ] **Step 1: Replace the Hero subtext paragraph**

Find in `index.html`:

```html
            <p class="text-lg md:text-xl max-w-3xl mx-auto mb-8">
                Driven by a relentless curiosity to build and improve. I deconstruct complex problems and engineer effective, innovative solutions, whether it's with a wrench or with code. If the tool I need doesn't exist, I build it.
            </p>
```

Replace with:

```html
            <p class="text-lg md:text-xl max-w-3xl mx-auto mb-8">
                Self-taught engineer who learned to ship production systems by using AI as both teacher and collaborator. I deconstruct hard problems and build what I need — whether the tool is a wrench, a PCB, or a multi-agent LLM pipeline.
            </p>
```

- [ ] **Step 2: Reload the browser tab; visually verify**

Expected: New subtext renders. Title unchanged. CTAs ("View My Work" / "Get In Touch") unchanged. No console errors.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "Refresh Hero subtext to lead with self-taught AI builder identity"
```

---

### Task 2: Rewrite About Me body copy

**Files:**
- Modify: `index.html:160-168`

**Context from spec:** Full rewrite. Own three things: (1) self-taught engineer learning by building with AI as teacher and collaborator, (2) one formal credential — DOL-recognized IBM apprenticeship — earned via the self-driven path rather than validating it, (3) the meta-angle of using AI to learn how to use AI. Drop "results-driven," "expertly combine," "formally validated by." Keep DIRTEE handoff sentence intact (second paragraph).

- [ ] **Step 1: Replace the two `<p>` tags in the About section**

Find in `index.html`:

```html
                <p class="text-lg leading-relaxed">
                    I'm a results-driven AI Automation Specialist with a proven ability to architect, build, and deploy intelligent automation systems from the ground up. I expertly combine full-stack development skills with a deep knowledge of LLM application design to
                    transform complex manual processes into efficient, AI-powered workflows. My journey has been unconventional, rooted in years of self-directed projects that have honed a deep technical expertise—now formally validated by the IBM Systems
                    Support Apprenticeship. This unique blend of intrinsic curiosity and professional training allows me to successfully troubleshoot complex systems, enhance operational efficiency, and collaborate with diverse teams to drive reliability
                    and innovation.
                </p>
                <p class="text-lg leading-relaxed mt-4">
                    I developed the DIRTEE methodology—Design In Real Time, Early Engagement—to capture how I build. It’s a rapid, collaborative approach that turns ideas into working solutions quickly, while ensuring trust, transparency, and alignment from the very first step.
                </p>
```

Replace with:

```html
                <p class="text-lg leading-relaxed">
                    I'm a self-taught engineer. I learned to build production systems by building them — with AI as both teacher and collaborator, not as a shortcut. My one formal credential is the DOL-recognized IBM Systems Support Apprenticeship, earned along that same self-driven path rather than the thing that validates the work it followed.
                </p>
                <p class="text-lg leading-relaxed mt-4">
                    Most of what I do now sits at the meta-angle: using AI to learn how to use AI better, then using both to ship real software — CVstomize, NoteXT, Daemonstrate, a stack of internal tools. Along the way I developed the DIRTEE methodology — Design In Real Time, Early Engagement — to capture how I actually build: rapid, collaborative, transparent from the first step.
                </p>
```

- [ ] **Step 2: Reload browser; visually verify**

Expected:
- Headshot placeholder still visible on the left (unchanged layout)
- Two paragraphs rendered, no "results-driven" / "formally validated by" anywhere
- DIRTEE handoff still present (second paragraph final sentence)
- No console errors

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "Rewrite About Me to own self-taught-with-AI story and drop corporate-speak"
```

---

### Task 3: Tighten AI Advocacy section

**Files:**
- Modify: `index.html:177-183`

**Context from spec:** Light edit. Keep the "why don't we just get Nolan to automate it with AI?" anecdote. Trim redundancy now that About Me names the self-taught + AI angle. Keep section structure unchanged.

- [ ] **Step 1: Replace the AI Advocacy paragraph**

Find in `index.html`:

```html
                <p class="text-lg leading-relaxed">
                    My approach to AI advocacy is hands-on and results-driven. I believe the most effective way to champion new technology is by demonstrating its tangible value, which has successfully converted numerous colleagues, friends, and even my IBM mentor into daily
                    AI users.
                    <br><br> This advocacy often starts with me using AI to streamline my own workflows. When teammates see the efficiency and quality of the output, it naturally leads to impromptu teaching sessions. It reached a point where my team would
                    joke, "why don't we just get Nolan to automate it with AI?"—shorthand for my role as the go-to person for integrating AI. This proves that the most effective teaching comes from showcasing real-world results. It's not about forcing
                    a tool on someone, but about inspiring them by solving their own daily challenges.
                </p>
```

Replace with:

```html
                <p class="text-lg leading-relaxed">
                    The fastest way to convert someone into an AI user is to solve one of their actual problems in front of them. I've had coworkers, friends, and even my IBM mentor go from skeptical to daily users that way — no pitch, no training deck, just "here's the five-minute version of what you spent an hour on."
                    <br><br>
                    At work it reached the point where the team joke became "why don't we just get Nolan to automate it with AI?" — which tracks, because that's roughly my mental default now. Not as a replacement for thinking, but as the way to compress the boring parts of a workflow so the interesting parts get more attention.
                </p>
```

- [ ] **Step 2: Reload browser; visually verify**

Expected: Anecdote preserved, no "results-driven" duplication with About Me, structure unchanged.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "Tighten AI Advocacy to reduce overlap with rewritten About Me"
```

---

## Part B: DIRTEE, Professional Journey (light audits)

### Task 4: Verify DIRTEE section — no changes expected, but confirm

**Files:**
- Read-only review: `index.html:187-242`

**Context from spec:** DIRTEE is the user's signature work. No structural changes. Audit only: confirm CVstomize and Ainsworth examples still match product reality.

- [ ] **Step 1: Re-read the DIRTEE section in `index.html`**

Read lines 187-242.

- [ ] **Step 2: Decision checkpoint — are the two examples still accurate?**

Check:
- **CVstomize example** (lines 215-224): describes prototyping a customizable resume-portfolio generator with live browser components and peer feedback. This is still accurate to the CVstomize origin story — the product pivoted *later* but the DIRTEE-in-action example is about the *build process*, which is still true.
- **Ainsworth example** (lines 225-234): describes prototyping a privacy-preserving mediation app with ethical safeguards. Still accurate.

Expected: No changes needed. Move on.

- [ ] **Step 3: No commit (no changes made)**

---

### Task 5: Tighten Professional Journey IBM entry

**Files:**
- Modify: `index.html:265-271`

**Context from spec:** IBM entry's prose currently uses apprenticeship-as-validation framing. That framing now lives in About Me, so the IBM timeline entry should describe the work, not re-pitch the credential.

- [ ] **Step 1: Replace the IBM `<p>` description only (keep title/company/dates)**

Find in `index.html`:

```html
                        <p>Completed a DOL-recognized apprenticeship, providing hands-on support for 200+ IBM Power and Intel servers. Diagnosed and resolved critical hardware/software issues, ensuring high reliability and uptime.</p>
```

Replace with:

```html
                        <p>Provided hands-on support for 200+ IBM Power and Intel servers in a production environment. Diagnosed and resolved hardware and software faults, escalated root-cause findings, and built troubleshooting playbooks the team still uses.</p>
```

- [ ] **Step 2: Reload browser; visually verify timeline**

Expected: Three timeline items still render. IBM entry no longer says "DOL-recognized apprenticeship" in the description (that framing is now in About Me). Title, company name, and dates all unchanged.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "Tighten IBM timeline entry; move apprenticeship framing to About Me only"
```

---

## Part C: Projects section — restructure and rewrite (biggest chunk)

The projects section gets the most work. It stays `#projects` with the same outer structure (header + featured + Daemonstrate + grid + GitHub CTA), but the featured pair gets richer cards, and the secondary grid gets tightened.

### Task 6: Rebuild the CVstomize featured card

**Files:**
- Modify: `index.html:322-350`

**Context from spec:** CVstomize card needs new tagline, hook, 3-pillar sub-block (CV Wizard, CVstom Profile, CVstom Portfolio), status badge "MVP in progress", updated tech chips (React 18, Material-UI, Vertex AI Gemini 2.5, GCP Cloud Run, PostgreSQL, Firebase Auth), and TWO CTAs (Live Site to cvstomize.vercel.app + View Architecture).

Order change: The current file has NoteXT first (left), CVstomize second (right). The spec doesn't mandate order, but both get rebuilt so any final order is fine. For this plan we keep NoteXT first to minimize diff noise.

- [ ] **Step 1: Replace the CVstomize featured card**

Find in `index.html` the CVstomize card block (currently the second card in the `<div class="grid md:grid-cols-2 gap-8 mb-8">`):

```html
                <!-- CVstomize (Featured) -->
                <div class="glassmorphism rounded-2xl flex flex-col group hover:border-sky-500/30 transition-colors overflow-hidden">
                    <div class="w-full h-48 bg-gray-700/50 flex items-center justify-center">
                        <img src="images/cvstomize.png" alt="CVstomize screenshot" class="w-full h-full object-cover hidden" onload="this.classList.remove('hidden')">
                        <span class="text-gray-500 text-sm img-placeholder">Screenshot: images/cvstomize.png</span>
                    </div>
                    <div class="p-6 flex flex-col flex-grow">
                        <div class="flex items-center justify-between mb-3">
                            <h3 class="text-2xl font-bold text-white">CVstomize.com</h3>
                            <span class="bg-yellow-500/20 text-yellow-300 text-xs font-medium px-2.5 py-0.5 rounded-full flex items-center gap-1">
                                <i data-lucide="lock" class="w-3 h-3"></i> Private
                            </span>
                        </div>
                        <p class="text-sky-400 font-semibold mb-3">AI-Powered Resume Platform</p>
                        <p class="flex-grow mb-4 text-sm">
                            Helping you land your dream job, 1 CV at a time. An end-to-end automation platform that parses job descriptions and generates targeted, ATS-optimized resumes from user-provided stories and experience.
                        </p>
                        <div class="flex flex-wrap gap-2 mt-auto">
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">Process Automation</span>
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">Generative AI</span>
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">UI/UX</span>
                            <span class="flex items-center gap-1 text-xs text-gray-400"><span class="w-3 h-3 rounded-full bg-yellow-300 inline-block"></span> HTML</span>
                            <span class="text-xs text-gray-500">&#9733; 1</span>
                        </div>
                        <button type="button" onclick="openDiagram('CVstomize', 'cvstomize.drawio')" class="btn-architecture mt-3">
                            <i data-lucide="git-branch" class="w-3.5 h-3.5"></i> View Architecture
                        </button>
                    </div>
                </div>
```

Replace with:

```html
                <!-- CVstomize (Featured) -->
                <div class="glassmorphism rounded-2xl flex flex-col group hover:border-sky-500/30 transition-colors overflow-hidden">
                    <div class="w-full h-48 bg-gray-700/50 flex items-center justify-center">
                        <img src="images/cvstomize.png" alt="CVstomize screenshot" class="w-full h-full object-cover hidden" onload="this.classList.remove('hidden')">
                        <span class="text-gray-500 text-sm img-placeholder">Screenshot: images/cvstomize.png</span>
                    </div>
                    <div class="p-6 flex flex-col flex-grow">
                        <div class="flex items-center justify-between mb-3">
                            <h3 class="text-2xl font-bold text-white">CVstomize.com</h3>
                            <span class="bg-yellow-500/20 text-yellow-300 text-xs font-medium px-2.5 py-0.5 rounded-full flex items-center gap-1">
                                <i data-lucide="lock" class="w-3 h-3"></i> Private
                            </span>
                        </div>
                        <p class="text-sky-400 font-semibold mb-1">Your professional identity, organized and shareable.</p>
                        <p class="text-sm italic text-gray-400 mb-4">CVstom Portfolios become the next resume.</p>

                        <!-- Three-pillar sub-block -->
                        <div class="space-y-3 mb-4 text-sm">
                            <div class="border-l-2 border-sky-500/60 pl-3">
                                <p class="font-semibold text-white">CV Wizard</p>
                                <p class="text-gray-400">Conversational AI builds your profile through dialogue — no blank-page resume paralysis.</p>
                            </div>
                            <div class="border-l-2 border-sky-500/60 pl-3">
                                <p class="font-semibold text-white">CVstom Profile</p>
                                <p class="text-gray-400">Single source of truth for skills, experience, and projects. Update once, reflect everywhere.</p>
                            </div>
                            <div class="border-l-2 border-sky-500/60 pl-3">
                                <p class="font-semibold text-white">CVstom Portfolio</p>
                                <p class="text-gray-400">Shareable identity at <span class="text-sky-400">cvstomize.com/u/yourname</span> with viewer-toggleable lenses.</p>
                            </div>
                        </div>

                        <div class="mb-3">
                            <span class="bg-blue-500/20 text-blue-300 text-xs font-medium px-2.5 py-0.5 rounded-full inline-flex items-center gap-1">
                                <i data-lucide="drafting-compass" class="w-3 h-3"></i> MVP in progress
                            </span>
                        </div>

                        <div class="flex flex-wrap gap-2 mb-4">
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">React 18</span>
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">Material-UI</span>
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">Vertex AI (Gemini 2.5)</span>
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">GCP Cloud Run</span>
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">PostgreSQL</span>
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">Firebase Auth</span>
                        </div>

                        <div class="flex items-center gap-4 mt-auto">
                            <a href="https://cvstomize.vercel.app" target="_blank" rel="noopener" class="inline-flex items-center gap-1 text-sky-400 hover:text-sky-300 text-sm font-medium">
                                <i data-lucide="external-link" class="w-3.5 h-3.5"></i> Live Site
                            </a>
                            <button type="button" onclick="openDiagram('CVstomize', 'cvstomize.drawio')" class="btn-architecture">
                                <i data-lucide="git-branch" class="w-3.5 h-3.5"></i> View Architecture
                            </button>
                        </div>
                    </div>
                </div>
```

- [ ] **Step 2: Reload browser; visually verify CVstomize card**

Expected:
- Card renders taller than before (more content)
- Three pillar sub-blocks each show bold white title + gray description, with a sky-accent left border
- "MVP in progress" blue status badge visible
- Six tech chips in a row (React 18, Material-UI, Vertex AI (Gemini 2.5), GCP Cloud Run, PostgreSQL, Firebase Auth)
- Two CTAs side-by-side: "Live Site" (opens cvstomize.vercel.app) and "View Architecture"
- Lucide icons (drafting-compass, external-link, git-branch) render as SVG
- No console errors

- [ ] **Step 3: Click Live Site CTA; confirm it opens cvstomize.vercel.app in a new tab**

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "Rebuild CVstomize featured card: 3-pillar pitch, live link, accurate tech stack"
```

---

### Task 7: Rebuild the NoteXT featured card

**Files:**
- Modify: `index.html:293-320`

**Context from spec:** NoteXT card needs new tagline, reverse-escalation hook (push → SMS → persistent notif → call), abbreviated "Will/donuts" how-it-works sub-block, status badge "Provisional Patent Drafted · 237/237 server tests passing", updated tech chips (Express 5, React 19 PWA, Expo SDK 55, PostgreSQL 16, Twilio, Gemini, Web Push), and View Architecture CTA.

- [ ] **Step 1: Replace the NoteXT featured card**

Find in `index.html`:

```html
                <!-- NoteXT (Featured) -->
                <div class="glassmorphism rounded-2xl flex flex-col group hover:border-sky-500/30 transition-colors overflow-hidden">
                    <div class="w-full h-48 bg-gray-700/50 flex items-center justify-center">
                        <img src="images/noteXT.png" alt="NoteXT screenshot" class="w-full h-full object-cover hidden" onload="this.classList.remove('hidden')">
                        <span class="text-gray-500 text-sm img-placeholder">Screenshot: images/noteXT.png</span>
                    </div>
                    <div class="p-6 flex flex-col flex-grow">
                        <div class="flex items-center justify-between mb-3">
                            <h3 class="text-2xl font-bold text-white">NoteXT</h3>
                            <span class="bg-yellow-500/20 text-yellow-300 text-xs font-medium px-2.5 py-0.5 rounded-full flex items-center gap-1">
                                <i data-lucide="lock" class="w-3 h-3"></i> Private
                            </span>
                        </div>
                        <p class="text-sky-400 font-semibold mb-3">SMS-First AI Personal Assistant</p>
                        <p class="flex-grow mb-4 text-sm">
                            Text anything to your NoteXT number — the system understands intent, learns your daily routine via passive location context, and delivers perfectly-timed, location-aware reminders. It calculates travel time, store visit duration, and your patterns to tell you exactly when to leave.
                        </p>
                        <div class="flex flex-wrap gap-2 mt-auto">
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">Twilio</span>
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">Vertex AI / Gemini</span>
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">Google Maps API</span>
                            <span class="flex items-center gap-1 text-xs text-gray-400"><span class="w-3 h-3 rounded-full bg-yellow-300 inline-block"></span> JavaScript</span>
                        </div>
                        <button type="button" onclick="openDiagram('NoteXT', 'noteXT.drawio')" class="btn-architecture mt-3">
                            <i data-lucide="git-branch" class="w-3.5 h-3.5"></i> View Architecture
                        </button>
                    </div>
                </div>
```

Replace with:

```html
                <!-- NoteXT (Featured) -->
                <div class="glassmorphism rounded-2xl flex flex-col group hover:border-sky-500/30 transition-colors overflow-hidden">
                    <div class="w-full h-48 bg-gray-700/50 flex items-center justify-center">
                        <img src="images/noteXT.png" alt="NoteXT screenshot" class="w-full h-full object-cover hidden" onload="this.classList.remove('hidden')">
                        <span class="text-gray-500 text-sm img-placeholder">Screenshot: images/noteXT.png</span>
                    </div>
                    <div class="p-6 flex flex-col flex-grow">
                        <div class="flex items-center justify-between mb-3">
                            <h3 class="text-2xl font-bold text-white">NoteXT</h3>
                            <span class="bg-yellow-500/20 text-yellow-300 text-xs font-medium px-2.5 py-0.5 rounded-full flex items-center gap-1">
                                <i data-lucide="lock" class="w-3 h-3"></i> Private
                            </span>
                        </div>
                        <p class="text-sky-400 font-semibold mb-1">An intelligent AI agent that handles logistics. Notes are a byproduct.</p>
                        <p class="text-sm italic text-gray-400 mb-4">Reverse-escalation alerts: push → SMS → persistent notif → call. First ack wins.</p>

                        <!-- How-it-works sub-block (Will/donuts example) -->
                        <div class="space-y-2 mb-4 text-sm border-l-2 border-sky-500/60 pl-3">
                            <p><span class="text-sky-400 font-semibold">You text:</span> "Pick up donuts for Will's birthday Saturday at 9am."</p>
                            <p><span class="text-sky-400 font-semibold">Agent:</span> extracts intent, asks a clarifying SMS if needed, learns the store's typical dwell time.</p>
                            <p><span class="text-sky-400 font-semibold">Saturday morning:</span> calculates "leave by" time from Maps + Places + your routine, then alerts via the escalation chain until you acknowledge.</p>
                        </div>

                        <div class="mb-3">
                            <span class="bg-emerald-500/20 text-emerald-300 text-xs font-medium px-2.5 py-0.5 rounded-full inline-flex items-center gap-1">
                                <i data-lucide="shield-check" class="w-3 h-3"></i> Provisional Patent Drafted · 237/237 server tests passing
                            </span>
                        </div>

                        <div class="flex flex-wrap gap-2 mb-4">
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">Express 5</span>
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">React 19 PWA</span>
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">Expo SDK 55</span>
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">PostgreSQL 16</span>
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">Twilio</span>
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">Gemini</span>
                            <span class="bg-gray-700 text-sky-300 text-xs font-medium px-2.5 py-0.5 rounded-full">Web Push</span>
                        </div>

                        <div class="flex items-center gap-4 mt-auto">
                            <button type="button" onclick="openDiagram('NoteXT', 'noteXT.drawio')" class="btn-architecture">
                                <i data-lucide="git-branch" class="w-3.5 h-3.5"></i> View Architecture
                            </button>
                        </div>
                    </div>
                </div>
```

- [ ] **Step 2: Reload browser; visually verify NoteXT card**

Expected:
- Card renders taller than before (more content)
- Tagline and italic hook visible
- How-it-works sub-block shows 3 lines with sky-accent labels ("You text:", "Agent:", "Saturday morning:")
- Emerald-green "Provisional Patent Drafted · 237/237 server tests passing" status badge
- Seven tech chips
- Single "View Architecture" CTA at bottom
- Featured pair grid still visually balanced (both cards roughly equal height — CSS Grid handles this automatically with `flex-grow` on inner content)
- No console errors

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "Rebuild NoteXT featured card: reverse-escalation hook, patent status, multi-channel stack"
```

---

### Task 8: Tighten secondary grid — AInsworth only (other cards already accurate)

**Files:**
- Modify: `index.html:417-442`

**Context from spec:** Per spec audit, only AInsworth needs trimming — the copy currently reads like two sentences glued together with methodology-call-out and product description competing for attention. Tighten to one clean description that preserves the DIRTEE tie-in. Other secondary cards (HuminLoop, ai-dev-workflow, PathaDex, Atrium-Core, Universal-Desktop-Automator, HoverChair) are copy-verified and remain as-is.

- [ ] **Step 1: Replace only the AInsworth `<p>` description**

Find in `index.html`:

```html
                        <p class="text-sm flex-grow mb-4">A rapid prototype built using my DIRTEE methodology — a recorded conversation between engineer and client was annotated, summarized, and built with Canvas using Gemini Pro. Worked flawlessly on the first try. AI-powered relationship mediator inspired by Mary Ainsworth.</p>
```

Replace with:

```html
                        <p class="text-sm flex-grow mb-4">AI-powered relationship mediator inspired by Mary Ainsworth. Built as a DIRTEE-methodology proof-of-concept: a recorded engineer-client conversation annotated, summarized, and shipped via Canvas + Gemini Pro. Worked first try.</p>
```

- [ ] **Step 2: Reload browser; visually verify**

Expected: AInsworth card now leads with what the product *is*, then explains how it was built. DIRTEE tie-in preserved. No layout shift.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "Tighten AInsworth card to lead with product, then build methodology"
```

---

### Task 9: Confirm Atrium-Core display name and verify remaining secondary cards need no changes

**Files:**
- Read-only review: `index.html:387-414` (HuminLoop), `index.html:444-471` (ai-dev-workflow), `index.html:473-494` (PathaDex), `index.html:496-517` (Atrium-Core), `index.html:519-542` (Universal-Desktop-Automator), `index.html:544-572` (HoverChair)

**Context from spec:** Spec explicitly calls out that Atrium-Core uses display name "Atrium-Core" even though the actual private repo slug is `Atrium-Core---Master-Jewler`. This is intentional readability over strict accuracy. No external link since the repo is private.

- [ ] **Step 1: Verify Atrium-Core card has no external link and shows clean display name**

Read `index.html:496-517` and confirm:
- Display title is `Atrium-Core` (not the repo slug)
- No `<a href="https://github.com/...">View</a>` link in the card (since it's private)
- Privacy badge shows "Private" with lock icon
- "View Architecture" button present

Expected: All four conditions already true in the current file. No changes needed.

- [ ] **Step 2: Skim the other five secondary cards for obvious staleness**

Read each card's description paragraph and confirm it matches current product reality. Per the spec audit, all five are already accurate.

- [ ] **Step 3: No commit (no changes made)**

---

## Part D: Hands-On Engineering, Skills, Contact (light audits)

### Task 10: Verify Hands-On Engineering, Skills, Contact sections — no copy changes

**Files:**
- Read-only review: `index.html:584-613` (Hands-On Engineering), `index.html:617-651` (Skills), `index.html:654-671` (Contact)

**Context from spec:** Hands-On Engineering reinforces self-taught-builder identity nicely and stays. Skills section keeps its 3-column structure. Contact unchanged. The spec also explicitly leaves the door open for dropping stale skills bullets, but on re-reading the current list, every bullet still reflects ongoing work (LLM Application Architecture, Agentic AI & Workflows, Advanced Prompt Engineering, API Integration, Conversational AI Workflows — all current; Process & Workflow Automation column all current; Full-Stack & Operations column all current).

- [ ] **Step 1: Skim all three sections; confirm no changes needed**

Expected: All three sections pass the audit. No commit.

---

## Part E: Bug fix discovered during planning

### Task 11: Fix diagram modal `main` → `master` branch reference

**Files:**
- Modify: `index.html:726`

**Context:** The `openDiagram()` JS function fetches raw diagram files from `raw.githubusercontent.com/wyofalcon/Portfolio/main/diagrams/...` but this repo's default branch is `master`, not `main`. Currently every "View Architecture" click results in a 404 in the draw.io viewer iframe. Discovered during Task 0 verification; spec did not mention this bug but it's blocking a success criterion ("no broken existing functionality").

- [ ] **Step 1: Replace `main` with `master` in the raw URL**

Find in `index.html`:

```js
            const rawUrl = `https://raw.githubusercontent.com/wyofalcon/Portfolio/main/diagrams/${diagramFile}`;
```

Replace with:

```js
            const rawUrl = `https://raw.githubusercontent.com/wyofalcon/Portfolio/master/diagrams/${diagramFile}`;
```

- [ ] **Step 2: Reload browser; click any "View Architecture" button**

Expected: Modal opens. The iframe still won't render an actual diagram because the `diagrams/` folder is empty in the repo (pre-existing condition, called out in the spec's Risks section), but it no longer 404s on the branch name — it will instead return the expected "file not found" from raw.githubusercontent.com for the missing file. This is a step forward, not a regression.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "Fix diagram modal branch reference from main to master"
```

---

## Part F: Final verification and push

### Task 12: End-to-end page verification

**Files:**
- Read-only: `index.html`

- [ ] **Step 1: Hard-refresh the browser tab (Ctrl+Shift+R)**

Expected: Page loads fully. No console errors.

- [ ] **Step 2: Walk every section top-to-bottom; visually confirm**

Checklist:
- [ ] Hero: new subtext reads "Self-taught engineer who learned to ship production systems..."
- [ ] About Me: no "results-driven" / "expertly combine" / "formally validated by" anywhere. Three-point story present.
- [ ] AI Advocacy: "why don't we just get Nolan to automate it with AI?" anecdote still there
- [ ] DIRTEE: section renders identically to before
- [ ] Professional Journey: three timeline items, IBM entry no longer says "DOL-recognized apprenticeship" in description
- [ ] Projects — Featured pair: NoteXT on left (reverse-escalation hook, emerald status badge, 7 chips, architecture CTA), CVstomize on right (3 pillars, MVP-in-progress badge, 6 chips, Live Site + Architecture CTAs)
- [ ] Projects — Daemonstrate: unchanged standalone card
- [ ] Projects — Secondary grid: 7 cards, AInsworth reads cleanly, Atrium-Core uses display name with no external link
- [ ] Hands-On Engineering: 5 cards unchanged
- [ ] Skills: 3 columns unchanged
- [ ] Contact: email/LinkedIn/GitHub icons unchanged
- [ ] Footer: copyright unchanged

- [ ] **Step 3: Test interactive behavior**

- [ ] Scroll: header gains glassmorphism background after scrolling down
- [ ] Nav links (About, Experience, Projects, Skills, Contact): all scroll to the correct section
- [ ] Mobile menu (resize browser narrow or use devtools device mode): hamburger opens/closes menu, links close menu on click
- [ ] Architecture modal: opens on button click, closes on X, closes on Escape, closes on backdrop click
- [ ] Lucide icons: all render as SVG (no raw `<i data-lucide="...">` tags visible)
- [ ] CVstomize Live Site link: opens cvstomize.vercel.app in a new tab

- [ ] **Step 4: Push to origin**

```bash
git push
```

Expected: Push succeeds. Since Pages is now configured for branch-based deploy (`build_type: legacy`, master:/), the live site at https://wyofalcon.github.io/Portfolio/ will rebuild automatically within ~1 minute — no Actions workflow involved.

- [ ] **Step 5: Verify live deploy**

After waiting ~60 seconds, hard-refresh https://wyofalcon.github.io/Portfolio/ (Ctrl+Shift+R to bypass cache).

Expected: Live site now reflects all changes. If it still shows old content, check `gh api repos/wyofalcon/Portfolio/pages` — `status` should be `built`, not `building` or `errored`.

---

## Success Criteria (from spec)

- [x] Featured cards (CVstomize, NoteXT) visually distinct from secondary grid (taller, richer content blocks, more CTAs) — Tasks 6 & 7
- [x] All copy in both featured cards traceable to either the repo README or the user's 2026-04-16 state summary — Tasks 6 & 7
- [x] About Me no longer contains "results-driven," "expertly combine," or "formally validated by" phrasing — Task 2
- [x] CVstomize live site link works (opens cvstomize.vercel.app in a new tab) — Task 6
- [x] All other sections audited and copy-tightened where stale; no structural changes outside `#projects` — Tasks 1, 3, 5, 8; Tasks 4, 9, 10 are read-only audits
- [x] No broken existing functionality: scroll, mobile menu, architecture modal, lucide icons — Task 12 verification; diagram modal bug fix Task 11
- [x] Page renders without console errors — Task 12 verification
