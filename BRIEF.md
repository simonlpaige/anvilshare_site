# Anvilshare.ai Frontend - Build Brief (for Claude Code subagent)

You are Claude Code. Build the anvilshare.ai marketing site in the current directory (`~/.openclaw/workspace/anvilshare-site`). This is greenfield - there is no existing frontend to preserve. Deploy target: GitHub Pages (`anvilshare.ai` via CNAME).

## What Anvilshare is

The "transformation" brand in the Groundlayer LLC pipeline. Replaces expensive SaaS (starting with HVAC dispatch software) with AI-native replacements on customer-owned hardware. Charges a % of savings. See `~/.openclaw/workspace/modules/anvilshare/BRAND.md` and `~/.openclaw/workspace/modules/groundlayer/PIPELINE.md` for the full picture. READ THESE BEFORE WRITING ANY CODE.

## Brand authority (READ IN ORDER)

1. `~/.openclaw/workspace/modules/groundlayer/BRAND-FAMILY.md` - family skeleton (global tokens, voice rules, visual anti-patterns). Applies to everything.
2. `~/.openclaw/workspace/modules/anvilshare/BRAND.md` - Anvilshare-specific flavor: palette, voice examples, sample copy. THIS IS THE SOURCE OF TRUTH for tone, component personality, and sample copy. Lift sample copy from here verbatim where it fits.
3. `~/.openclaw/workspace/modules/groundlayer/PIPELINE.md` - pipeline context (how Anvilshare fits into the four-brand machine).
4. `~/.openclaw/workspace/modules/groundlayer/design-systems/SITE-BUILD-PLAN.md` - the overall plan; you own the Anvilshare section.

## Hard constraints (FAMILY LAW - do not violate)

- **Type stack**: Source Serif 4 (display) + Inter (body) + JetBrains Mono (data). Load via Google Fonts (`https://fonts.googleapis.com/css2?family=Source+Serif+4:wght@400;600;700&family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap`). No substitutes.
- **Scale**: 1.250 Major Third. Baseline 8px. Spacing multiples of 4px.
- **Radius**: 4px default, 0px structural. **NEVER above 8px anywhere.**
- **Shadows**: whisper only. `0 1px 2px rgba(0,0,0,0.2)` rest, `0 4px 12px rgba(0,0,0,0.25)` hover on dark ground. Nothing cinematic.
- **NO gradients anywhere.** Background, button, text, icon - if a linear/radial-gradient exists, it fails.
- **NO em dashes anywhere.** Use a regular hyphen or rewrite the sentence. Hard rule.
- **NO banned words** (see voice section below).
- **NO uppercase button labels.** Sentence case for CTAs.
- **NO animations on body text.** No entrance animations, no particle effects, no hero video, no auto-playing anything.
- **NO stock photography** of humans in business casual. NO AI-generated faces. NO generic "tech" abstractions (circuit boards, glowing networks).
- **NO emoji in UI chrome** (buttons, nav items, form labels, badges). Emoji are banned in the interface.
- **Icons**: Lucide 1.5px stroke line icons only, inline SVG. No filled icons. Do not load an icon package at runtime - hand-inline the 3-5 icons you actually use.
- **Layout**: horizontal rhythm. Left-aligned headings. 62ch max body line length. Wright pencil lines (1px horizontal rules) as section dividers.
- **Accessibility**: WCAG AA minimum, AAA body contrast target. 2px focus ring in iron-glow. Real alt text sentences.
- **Weight target**: <500KB initial load per page.
- **No AI-speak**. Read the "Voice examples" section in BRAND.md and match that register.

## Banned words (zero tolerance)

unlock, leverage, seamless, delight, journey, robust, empower, transformative, innovative, best-in-class, synergy, ecosystem (unless literal ecology), streamline, holistic, elevate, cutting-edge, unlock the potential, limited spots, now more than ever, digital transformation, book now, act fast, absolutely, wonderful, great question, of course, dive in, dive deep, deep dive (as noun phrase), revolutionize, empower, game-changer, paradigm shift, next-generation.

Also banned: em dashes (—), en dashes (–) used as sentence punctuation. Use hyphens or rewrite.

## Anvilshare flavor tokens (DO NOT DEVIATE)

```css
--forge-dark: #111009;   /* background */
--steel: #1D2228;         /* surface / card */
--iron-glow: #C4642C;     /* PRIMARY ACTION */
--ember: #E8960E;         /* accent - max 5% of any viewport */
--chalk: #EAE4D8;         /* text */
--ash: #6B6560;           /* muted */
--rule: #2E3238;          /* borders, rules */
--success: #2E7D52;
--error: #B03030;
```

Base rem: `18px` (Anvilshare runs slightly larger than the family default because the dark background carries it). Body tracking: `+1%` on Inter body text on dark ground.

## Voice rules

- **Feynman voice**: explain the real mechanism. Concrete nouns, dollar amounts, specific hours.
- **Heavy, precise, low-register**: says things once, doesn't soften, doesn't hedge.
- **Third person, not first person.** Anvilshare (not Simon) is speaking. "Anvilshare audits your stack." Not "I'll audit your stack."
- **Dollar-specific.** "$1,400 a month" is better than "a lot of money." "$500 audit" is better than "our affordable assessment."
- **Name specific software categories** (dispatch, POS, inventory, scheduling). Do NOT name specific competitor products in marketing copy (per BRAND.md - the enemy is the pattern, not ServiceTitan).
- **No filler words in CTAs.** "Book a 15-minute call." "See how it works." "Read the audit sample." Not "Learn more" or "Get started on your journey."
- Lift sample copy from BRAND.md verbatim where it fits.

## Mira status (IMPORTANT)

Mira (the voice agent phone intake) is NOT live yet. Build plan says 38-50 hours to ship. For THIS v1:
- **Primary CTA**: "Book a 15-minute call" linking to `mailto:simon@anvilshare.ai?subject=Anvilshare%20intro%20call&body=Hi%20Simon,%20I%27d%20like%20to%20set%20up%20a%2015-minute%20call%20to%20talk%20about...` (no Calendly yet; a plain mailto is honest).
- **Mira tease**: Include a small section on the homepage AND the how-it-works page titled "Soon: call Mira" explaining the 10-minute intake is coming. Do not claim it's live. Frame as "in build."
- When Mira launches, the phone CTA will replace the mailto. Keep the markup easy to swap.

## Site structure (filesystem layout)

```
anvilshare-site/
  index.html                # homepage
  how-it-works.html         # the process
  plans.html                # pricing
  contact.html              # reach Simon
  privacy.html              # shared Groundlayer policy (anvilshare-scoped copy)
  terms.html                # shared Groundlayer terms (anvilshare-scoped copy)
  css/
    site.css                # single stylesheet, no inline style blocks except critical <head> tokens
  assets/
    logo.svg                # already placed - use as-is
    favicon.svg             # generate: lowercase "a" in Source Serif 4 700 on forge-dark square, ember underline
  CNAME                     # already placed - anvilshare.ai
  BUILD-NOTES.md            # you write this last
```

## Per-page content requirements

### index.html
- **Hero**
  - Headline (from BRAND.md): "Your dispatch software costs $1,400 a month. We'll replace it for less - and you keep the code." (Use a regular hyphen. NOT an em dash.)
  - Subhead (from BRAND.md): "Anvilshare audits your software stack, builds an AI-native replacement, and charges you half of what you save. If you don't save money, you don't pay for the build."
  - Primary CTA: "Book a 15-minute call" -> mailto
  - Secondary CTA: "See how it works" -> /how-it-works.html
  - Left-aligned, left-weighted, horizontal. Not centered. Not tall. Hero does not take full viewport height; it takes the space it needs.
- **The bet** (1-column callout)
  - "If you don't save money, you don't pay for the build." Explain in 2-3 sentences how the savings-share pricing actually works. Show the mechanism.
- **How it works** (3-column Wright triplet)
  - 1. Audit ($500): a blunt review of your software stack. You get the report regardless of what you decide next.
  - 2. Build: Anvilshare writes the replacement. Runs on your server, not Anvilshare's.
  - 3. Split: Anvilshare takes half of your monthly savings for 36 months. Then it's free.
  - Each column has a Lucide line icon (hand-inlined, 1.5 stroke): "search", "hammer", "divide" or similar.
- **What's replaceable** (horizontal rule separator + 2-column list)
  - Dispatch software, scheduling, invoicing, field service management, POS, inventory, basic CRM. One-line descriptions. Plain prose, not bullet-bait.
- **Pricing row** (from BRAND.md sample copy)
  - "The audit costs $500. If we find nothing worth replacing, you pay $500 and learn something about your stack. That's the deal."
  - Build: quoted per engagement after audit.
  - Split: 50% of verified monthly savings for 36 months, after which the system is yours free.
- **Who this is for**
  - "KC HVAC shops with 2-15 technicians who signed up for dispatch software that hasn't paid for itself." (Lift from BRAND.md target customer section.)
- **Mira tease** (small section, not the main CTA)
  - Short paragraph: a voice agent for 10-minute intake is in build; for now, email Simon. Link to how-it-works page for the full pipeline explanation.
- **Footer**
  - "Anvilshare is a brand of Groundlayer LLC, a Missouri holding company." Link to groundlayer.co. Link to privacy + terms. simon@anvilshare.ai.

### how-it-works.html
- **Hero**: "How the replacement actually works." Subhead: one clear sentence about the 3-step pipeline.
- **Audit section**: describe the $500 audit. What Simon does. What the report contains. When you get it. What happens if nothing is replaceable.
- **Mira section (in-build framing)**: explain what Mira will do when she launches. Frame as "the next step." Be honest about current status.
- **Build section**: explain the engineering. Runs on customer hardware (or rented VPS they own). Open code. Documented. Customer can fire Anvilshare and keep running the software. This is the key differentiator.
- **Savings share math worked example**: use the BRAND.md dispatch example - $1,400/mo becomes $700/mo on the Anvilshare replacement. Savings = $700/mo. Anvilshare gets $350/mo for 36 months. Customer nets $350/mo for 36 months, then full $700/mo savings after. Net 36-month savings to customer: $12,600. Net Anvilshare revenue: $12,600.
- **What Anvilshare won't do**: no lock-in, no proprietary format, no hidden fees, no "we own the data" clauses. Short bullet list.
- **CTA footer**: same primary CTA.

### plans.html
- One zebra table (steel/forge alternating rows) with three rows: Audit / Build / Savings share. Columns: What it is / What it costs / How it's paid.
- Mono numerics for dollar amounts (JetBrains Mono, iron-glow color for the dollar figures).
- Below the table, FAQ-style block: 4-5 honest Q&As. ("Can I cancel?" "What if I don't want to share savings?" etc.) Written in the Anvilshare voice.
- Same CTA.

### contact.html
- Simon's contact details: simon@anvilshare.ai, KC-based, response time target 1 business day.
- "Book a 15-minute call" mailto button as primary.
- Mira placeholder section: a quiet panel that says "Call Mira: (coming soon)". Grey it out visually but leave the structure.
- Office-hours honesty: say "I answer emails between 9am and 6pm CT. Nights and weekends are for building."

### privacy.html & terms.html
- Standard privacy policy and terms, scoped to anvilshare.ai. You can write plain-English versions that cover:
  - Data collected: contact form submissions, email exchanges, audit reports.
  - Data NOT collected: customer software data during audits stays on customer hardware by design; Anvilshare never touches it in any form that persists.
  - Contract terms point to Groundlayer LLC as the legal party.
  - Last updated 2026-04-19.
- Voice: Groundlayer's sparse, institutional register (read `~/.openclaw/workspace/modules/groundlayer/BRAND.md` for tone).

## CSS requirements (`css/site.css`)

- Single stylesheet. No `<style>` blocks in HTML except critical-path tokens in `<head>` (optional).
- Define all tokens as `:root` CSS custom properties.
- Include responsive breakpoints at 640px, 900px, 1200px (mobile / tablet / desktop / wide).
- Use CSS Grid for triplets; Flexbox for navigation + card headers.
- Focus ring: `outline: 2px solid var(--iron-glow); outline-offset: 2px;`
- All interactive elements must have keyboard-visible focus states.
- Respect `prefers-reduced-motion` (kill the few transitions you do have).
- Print styles: preserve text, strip surfaces, black on white.
- No external font CDN beyond Google Fonts for the three faces.
- No framework (no Tailwind, no Bootstrap). Hand-written CSS that a human can read.

## Things to verify before committing

Run through this checklist manually before the final commit:

1. **Grep for banned words** in all .html files. Zero hits.
2. **Grep for em dashes (—)** and en dashes (–). Zero hits. Regular hyphens only.
3. **Grep for "gradient"** in CSS. Zero hits.
4. **Grep for "border-radius"** values above 8px. Zero hits.
5. **Font stack**: only Source Serif 4, Inter, JetBrains Mono. No others.
6. **Page weight**: each HTML+CSS page should be <40KB of source (Google Fonts + logo SVG will add load but stay under 500KB total initial paint).
7. **Alt text**: every `<img>` has a real sentence, not a filename.
8. **Lucide icons**: hand-inlined SVGs, stroke="1.5", stroke-linecap="round", stroke-linejoin="round". No icon font.
9. **Nav is horizontal**, left-aligned, no hamburger animation on mobile (use a simple "Menu" text toggle or a plain horizontal scroll).
10. **No JavaScript required** for core content visibility. Progressive enhancement only.

## Deliverables (what you hand back)

1. All HTML files listed above, production-ready.
2. `css/site.css` complete.
3. `assets/favicon.svg` generated from the logo.
4. `BUILD-NOTES.md` in the site root containing:
   - What you built (one-line summary per file)
   - Any spec ambiguities you resolved and how
   - Any flagged concerns for Simon/Larry's review
   - Voice-check pass results (zero banned-word hits confirmed)
   - Gradient/em-dash/radius scan results
5. A single git commit on the local `main` branch with message: `anvilshare.ai v1 - Prairie Clarity forge flavor, 6 pages, Mira-pending CTA`

## Do not

- Push to any remote. Do not run `git push`.
- Deploy to GitHub Pages or anywhere else. Simon owns deploy.
- Create a GitHub repo or call `gh`. Do not run any GitHub operations.
- Touch any file outside `~/.openclaw/workspace/anvilshare-site/`.
- Load any font beyond the three specified.
- Inline stock photos, AI-generated images, or any human imagery. Use the logo and typography only. Add plain colored rectangles as image placeholders if layout demands it, with a comment `<!-- placeholder: real photography TK -->` above each.
- Add tracking pixels, analytics, or any third-party scripts.
- Invent pricing Simon didn't approve. Stick to $500 audit + 50% savings share for 36 months. If you need a build price, say "quoted per engagement after audit."
- Claim Mira is live.

## When you finish

Run this command last to wake Larry:

```
openclaw system event --text "Done: anvilshare.ai v1 site built locally (6 pages, single CSS, Forge Dark flavor). Ready for review." --mode now
```

Go.
