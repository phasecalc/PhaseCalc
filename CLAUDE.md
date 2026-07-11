# Phasecalc.com — Project Context

## What this is
Personal finance calculator site (phasecalc.com). Side-income project, SEO-driven organic traffic, monetized via affiliate links (eventually AdSense). Solo builder, build-in-public style. Not a startup — lean and low-maintenance by design.

## Architecture — read before editing
- **No backend, no accounts, no database.** Every calculator is a single static HTML file with inline/embedded JS. No build step, no framework, no bundler.
- **Hosting:** Netlify, static deploy.
- **Deploy workflow:** GitHub Desktop → git → Netlify auto-deploys on push to main.
- **Domain/email:** Porkbun (domain + MX records pointed at Netlify DNS for hello@phasecalc.com forwarding).
- Each calculator is self-contained — don't introduce shared JS/CSS files or a component system unless explicitly asked. Duplication across files is the accepted tradeoff for zero-infra simplicity.

## Brand identity — "Phases"
- **Palette:** ink navy / parchment / amber-slate
- **Type:** IBM Plex Mono (UI/numbers) + Source Serif 4 / IBM Plex Serif (body/explainer copy)
- **Aesthetic:** ledger/passbook — think bank statement, not fintech dashboard
- **Motif:** phase-block staircase (used in logo/OG images and section dividers)
- Match this in any new calculator's HTML/CSS — don't default to generic Tailwind/SaaS look.

## Calculator page pattern
Every calculator ships with:
1. The calculator itself (single HTML file)
2. A companion SEO explainer article
3. FAQ schema (structured data) for the explainer
4. Cross-links to related calculators in the suite (not just back to the original 3)

## Content philosophy
- **Build calculators over articles** at this stage — zero-authority domain gets more from linkable tools than content volume.
- **Distribution over content calendar** — Reddit (r/financialindependence, r/InternetIsBeautiful), Show HN are higher-leverage than scheduled social posts right now.
- **Affiliate over AdSense** while traffic is low. AdSense application goes in early anyway (approval lag), but placement is deferred.
- **X/social cadence:** post when something real shipped, not on a schedule. Social is a narrative/presence layer, not a growth lever yet.
- Skip the "20-piece content per calculator" playbook — that's a month-3+ strategy, premature for a zero-authority domain.

## Working conventions
- **Batch deploys** — group related changes into one push rather than piecemeal commits, to minimize churn.
- Clinton has deep domain knowledge in personal finance/tax treatment — don't oversimplify calculator logic or explainer depth.
- Prefers honest tradeoff assessments over validation when discussing infra/strategy choices.

## Where things actually live (don't duplicate here)
- **Notion** — source of truth for all task tracking (Active/Waiting On/Someday/Done). Check Notion for current work-in-progress before assuming status. TASKS.md is retired — do not reference or update it.
- **PHASECALC-BUSINESS-PLAN.md** — North Star doc: operating principles, phased roadmap, monetization progression, decision framework. This wins if it ever conflicts with Notion task entries.
- Business plan is maintained as a living doc; task status lives entirely in Notion now.

## Tools/stack reference
- Analytics: GA4 (chosen over Plausible — free at pre-revenue stage)
- Monetization: Buy Me a Coffee (buymeacoffee.com/ctong), Monarch Money referral, FlexOffers/CJ Affiliate (pending)
- Image gen: cairosvg (SVG→PNG) + Pillow/truetype for OG images — fonts must be system-registered via `fc-cache -f`, not just `@font-face`, for cairosvg to render them correctly.
