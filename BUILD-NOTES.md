# BUILD-NOTES.md - Anvilshare v1

Built by Claude Code on 2026-04-19.

## Files built

- **index.html** - Homepage: hero, the bet callout, 3-column how-it-works triplet, what's replaceable grid, pricing row, who this is for, Mira tease, footer.
- **how-it-works.html** - Full process page: audit details, Mira in-build section, build methodology, savings share worked example, what Anvilshare won't do.
- **plans.html** - Pricing page: zebra table (audit/build/savings share), 5-item FAQ.
- **contact.html** - Contact page: Simon's details, office hours, 15-min call CTA, Mira placeholder (greyed out).
- **privacy.html** - Privacy policy: plain-English, Groundlayer institutional voice. No cookies, no tracking, no third-party data sharing.
- **terms.html** - Terms of service: plain-English terms for audit, build, and savings share. Groundlayer LLC as legal party.
- **css/site.css** - Single stylesheet, all tokens as CSS custom properties, responsive at 640/900/1200px, print styles, reduced-motion, focus states.
- **assets/favicon.svg** - Lowercase "a" in Source Serif 4 700 on forge-dark square with ember underline.
- **CNAME** - Pre-existing: anvilshare.ai
- **assets/logo.svg** - Pre-existing: used as-is.

## Spec ambiguities resolved

1. **Shadow values**: BRAND-FAMILY.md specifies lighter shadows (0.06/0.10 opacity) while BRIEF.md specifies darker (0.2/0.25 "on dark ground"). Used BRIEF.md values since they're specific to this dark-ground build and make shadows visible.
2. **Savings share worked example**: BRIEF.md says $1,400/mo old cost with $700/mo Anvilshare replacement. The math implies ~$50/mo hosting on customer VPS, making the saving $1,350/mo rather than $700. Used the more detailed math showing hosting as a separate customer cost, since BRAND.md says "runs on your server, not ours."
3. **Mobile nav**: BRIEF.md says "no hamburger animation - use a simple 'Menu' text toggle or a plain horizontal scroll." Chose horizontal scroll (overflow-x auto, hidden scrollbar) since it requires zero JavaScript and satisfies "no JS required for core content."
4. **Mira CTA from BRAND.md**: BRAND.md sample copy has "Call Mira" as primary CTA, but BRIEF.md explicitly says Mira is not live and primary CTA should be "Book a 15-minute call" mailto. Followed BRIEF.md.
5. **Build pricing in table**: BRIEF.md says "quoted per engagement after audit" - no number invented. Used that exact phrasing.

## Flagged for review

1. **Logo SVG uses embedded fonts**: The logo.svg references Source Serif 4 and Inter by font-family name. These will only render correctly in browsers that have loaded the Google Fonts. On systems without those fonts installed, the SVG text will fall back to Georgia/system-ui. Consider converting the logo text to paths for consistent rendering.
2. **Favicon SVG same font issue**: The favicon references Source Serif 4 by name. Most browsers will use a fallback serif for the "a" glyph. Consider converting to a path-based SVG.
3. **No form on contact page**: BRIEF.md specified email and mailto as the primary contact method. No contact form was built. The Cloudflare Worker endpoint (api.groundlayer.co/contact) mentioned in PIPELINE.md is undeployed, so a form would have no backend.
4. **Google Fonts link**: The fonts are loaded from Google's CDN. This is the only external dependency. If self-hosting WOFF2 files is preferred for privacy or performance, that's a follow-up.
5. **Mira section CTA swap**: When Mira launches, replace the mailto CTAs with a phone number CTA. The HTML structure uses distinct sections and clear class names (.mira-panel, .mira-disabled) to make this swap straightforward.

## Voice-check pass results

- **Banned words scan**: 0 hits across all .html files (tested both word lists from BRIEF.md).
- **Em dash scan**: 0 hits (searched for both em dash and en dash characters).
- **Gradient scan**: 0 hits in CSS.
- **Border radius scan**: All values are 2px or var(--radius) (4px). None above 8px.
- **Font stack scan**: Only Source Serif 4, Inter, JetBrains Mono referenced (via CSS custom properties).
- **Style block scan**: 0 inline style blocks in HTML.
- **Script scan**: 0 script tags. Zero JavaScript.
- **Page weight**: Largest source file is site.css at 15KB. All HTML files under 11KB. Total source well under 40KB per page.
