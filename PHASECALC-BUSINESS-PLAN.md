# Phasecalc.com — Business Plan (North Star)

*This document is the North Star. If it conflicts with Notion task entries, this document wins. It changes rarely — only on genuine strategy shifts, not routine task updates.*

---

## The one-line thesis
A suite of high-quality, static personal-finance calculators that earn organic search traffic and convert it to affiliate revenue — built lean, solo, and in public, with near-zero operating cost and near-zero maintenance burden.

## What success looks like
Modest, durable side income from a low-maintenance asset. Not a startup, not a full-time business, not venture-scale. The win condition is a set of calculators that rank, get linked to, and pay out via affiliate programs (and eventually AdSense) while requiring little ongoing work. Optionality to grow if it takes off — but the base case is a profitable, self-sustaining side project.

---

## Operating principles

1. **Tools over content.** At a zero-authority domain, a genuinely useful, linkable calculator earns backlinks and rankings that a blog post can't. Build calculators first; explainer articles support them, not the reverse.

2. **Distribution over volume.** One good Reddit / Hacker News / r/InternetIsBeautiful launch moves more than weeks of scheduled social posts at current traffic. Ship, then distribute deliberately. Don't confuse a content calendar for growth.

3. **Lean infrastructure, always.** No backend, no accounts, no database. Static single-file HTML/JS on Netlify. Every added moving part is a maintenance tax on a solo builder. Simplicity is a feature, not a limitation.

4. **Affiliate before ads.** At low traffic, affiliate placements pay far better per visitor than AdSense. Apply to AdSense early (approval lag), but defer placement until traffic is meaningful enough to justify the UX cost.

5. **Build in public, honestly.** Post when something real ships, not on a schedule. Social (X, Instagram/Threads, TikTok, YouTube) is a narrative and presence layer that compounds slowly — a claim on the handle and a record of the build, not a primary growth lever yet.

---

## Phased roadmap

Each phase has exit criteria — don't jump ahead until they're met.

### Phase 1 — Foundation *(largely complete)*
Build the core calculator suite and stand up all infrastructure.
- **Exit criteria:** A meaningful suite of calculators live (met: 13+ live); custom domain, hosting, email, Search Console, sitemap all operational; social handles claimed.

### Phase 2 — Indexing & distribution *(current)*
Get every page indexed and run the first real distribution pushes.
- **Exit criteria:** All live pages indexed in Search Console; analytics installed and reporting; first Reddit / Show HN / r/InternetIsBeautiful launches executed; affiliate networks joined and first advertiser programs approved.

### Phase 3 — Traffic & ranking
Earn organic search traffic and start ranking for target calculator keywords.
- **Exit criteria:** Consistent organic impressions/clicks in Search Console across multiple calculators; a handful of calculators ranking on page 1 for their primary keyword; first affiliate conversions recorded.

### Phase 4 — Monetization maturation
Optimize the funnel from traffic to revenue.
- **Exit criteria:** Affiliate revenue is regular (not one-off); AdSense placement decision made based on real traffic data; each high-traffic calculator paired with its best-fit affiliate offer.

### Phase 5 — Compounding & optionality
Let winners compound; decide whether to scale, hold, or expand.
- **Exit criteria:** Revenue covers costs with margin and is stable month-over-month; clear read on which calculators/keywords justify further investment; explicit hold-vs-grow decision made.

---

## Monetization progression

1. **Tip jar (live):** Buy Me a Coffee (buymeacoffee.com/ctong) — low-friction, no approval, minimal expectations.
2. **Referral links (live):** Monarch Money and similar personal-finance referrals where they fit a calculator's audience.
3. **Affiliate networks (in progress):** FlexOffers or CJ Affiliate — no traffic minimum to join, so join early. Target three categories that map to the calculator suite:
   - **Brokerage** (Public / Robinhood / Webull) → compound interest, DCA, DRIP, margin loan calculators
   - **Tax software** (TurboTax / H&R Block / FreeTaxUSA) → Trump Account, capital gains calculators
   - **HELOC / mortgage** advertisers → HELOC, mortgage extra-payment, cash-out refi calculators
4. **AdSense (deferred placement):** Apply early for approval; hold actual placement until traffic is meaningful enough to be worth the UX tradeoff.
5. **Later / lower priority:** Wealth-management referrals (Empower/Personal Capital flat bounties), aggregator affiliates (Credit Karma) — revisit as traffic grows.

**Sequencing logic:** the earlier items require no traffic and no approval, so they go live immediately. Affiliate networks are join-early / place-when-relevant. AdSense is the last lever precisely because it pays worst per visitor at low volume.

---

## Channel / distribution guide

- **Reddit** — r/financialindependence (Wednesday self-promo thread), r/InternetIsBeautiful. Lead with the calculator suite as a useful free tool, not a pitch. Highest-leverage channel at current scale.
- **Hacker News** — Show HN, framed around the suite. One good shot; make it count.
- **X (@phasecalc)** — build-in-public cadence: post when something real ships. Not a scheduled pipeline.
- **Instagram / Threads / TikTok / YouTube (@phasecalc)** — presence claims and narrative layer. Document the build; don't force a content calendar. Deprioritized as a growth lever until there's traffic to amplify.
- **SEO (the long game)** — each calculator + companion explainer + FAQ schema is the durable engine. This is where compounding happens; the social/forum pushes are ignition, not the engine.

---

## Decision framework

When choosing what to do next, in priority order:

1. **Does it serve organic search?** A new calculator, an explainer, better cross-linking, or an indexing fix beats almost anything else at this stage.
2. **Is it distribution with real leverage?** A launch to an engaged community beats scheduled social posting.
3. **Does it reduce future maintenance or cost?** Lean-infrastructure choices compound in a solo project.
4. **Does it unlock revenue with no traffic cost?** Join affiliate networks, get approvals in the pipeline — these have lag, so start them early.
5. **Everything else is Someday.** Premature scaling (full content calendars, "20 pieces per calculator," ad optimization at low traffic) is deferred until the phase that warrants it.

**Anti-patterns to resist:**
- Applying a month-3+ playbook to a zero-authority domain (e.g. the "20-piece content per calculator" formula — premature).
- Adding infrastructure (backend, accounts, framework) for its own sake.
- Treating social posting volume as a proxy for progress.
- Placing ads before traffic justifies the UX cost.

---

## Standard patterns (reference)

- **Every calculator ships with:** the tool (single static HTML file), a companion SEO explainer article, FAQ schema, and cross-links to related calculators in the suite.
- **Brand — "Phases":** ink navy / parchment / amber-slate; IBM Plex Mono + Source Serif 4 / IBM Plex Serif; ledger/passbook aesthetic; phase-block staircase motif.
- **Deploy:** batch related changes into single pushes via GitHub Desktop → Netlify.
- **Tasks live in Notion** (source of truth for day-to-day work); this doc governs strategy above it.
