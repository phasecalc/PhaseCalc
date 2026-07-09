# Multi-Phase Upgrade Plan — Other Calculators

Ranking the rest of the site's calculators on whether adjustable phases (the growth/lump-sum phase-card pattern used by the compound interest calculator and the retirement backtest calculator) is a real improvement, a nice-to-have, or a mismatch. Goal is to keep "Phases" meaningful rather than bolting the same UI onto everything regardless of fit.

Suggested sequencing: do bucket 1 one at a time, starting with Coast FIRE, and use actual usage/feedback from those before committing to all of bucket 2.

---

## Bucket 1 — Should have phases

These are cases where the calculator's current single-scenario math is arguably describing the wrong shape of the problem, not just missing a nice-to-have feature.

### Coast FIRE Calculator
**Why it fits:** Coast FIRE is definitionally three phases — contribute aggressively, stop and let it compound (“coast”), then retire. If the calculator is currently one blended formula, phase-izing it is an accuracy fix, not decoration.

**Upgrade prompt:**
> Rework the Coast FIRE calculator to use an explicit 3-phase engine instead of a single formula: (1) Contribution phase — years, contribution amount, growth rate; (2) Coast phase — years, growth rate only, zero contribution; (3) Retirement phase — report the ending balance at retirement age in today's-dollars purchasing power (optionally accept a withdrawal amount/years to show a runway view, but this can stay deterministic, no historical backtesting needed). Reuse the phase-card UI pattern already established in the compound interest and retirement backtest calculators for visual and interaction consistency. Add a "solve for coast age" mode: given a savings rate, growth rate, and target retirement age, calculate the earliest age contributions can stop while still reaching the retirement target through compounding alone, and mark that point directly on the phase timeline.

### 529 Superfunding Calculator
**Why it fits:** Superfunding already implies three phases baked into the product itself — a lump-sum event (5-year gift-tax-averaged upfront deposit), a growth period, and a tuition drawdown window.

**Upgrade prompt:**
> Add explicit phases to the 529 superfunding calculator: (1) Superfunding lump-sum event — the upfront deposit spread over 5 years for gift-tax averaging; (2) Growth phase — years until college age, contributions optional; (3) Drawdown phase — a fixed number of years (e.g. 4 for undergrad) withdrawing a specified annual amount for tuition, tracking whether the fund covers the full schedule or is exhausted early. Use the same growth+lumpSum phase-card pattern as the compound interest calculator, with the withdrawal phase styled like the retirement backtest's terminal-phase card (locked to the end, visually distinct) but WITHOUT historical backtesting — straight-line only, since 529 withdrawal windows are short (4-5 years) and sequence-of-returns risk matters far less than in a 30-year retirement.

### Roth vs Traditional Calculator
**Why it fits:** The entire point of the comparison is that contribution-phase and withdrawal-phase tax treatment differ. Modeling both as one blended assumption undersells the actual argument.

**Upgrade prompt:**
> Extend the Roth vs Traditional comparison to model two explicit phases per account: an accumulation phase (years, contribution, growth rate) and a withdrawal phase (retirement years, withdrawal amount, tax treatment specific to the account type — Roth withdrawals tax-free, Traditional withdrawals taxed as ordinary income at a specified rate). Let users set both phases' durations independently (e.g. contribute for 25 years, withdraw over 30) rather than the current single blended-assumption comparison. Keep this deterministic — no historical backtesting needed, since the point is tax-treatment comparison, not sequence-of-returns risk.

### Trump Account Calculator
**Why it fits:** Same lump-sum-then-growth-then-access shape as 529 superfunding — a seeded deposit, a contribution window, and a locked/access point.

**Upgrade prompt:**
> Add explicit phases to the Trump Account calculator: (1) Seed deposit — the one-time government-seeded lump sum at account opening; (2) Contribution phase — years until the access age, with an optional annual contribution amount and growth rate; (3) Access/lock phase — display the balance at the unlock age as the key output, optionally followed by a post-access growth or withdrawal phase for account holders who don't withdraw immediately. Use the standard growth+lumpSum phase-card pattern. Deterministic only.

---

## Bucket 2 — Middle ground

Phases would add real value here but the current single-scenario version isn't wrong, just less complete. Lower priority — worth doing once bucket 1 validates the pattern, or if user feedback specifically asks for it.

### Rental Property Calculator
**Upgrade prompt:**
> Add optional phases to the rental property calculator: (1) Acquisition/renovation phase — a period with no rental income (or negative cash flow from renovation costs) before the property is rented; (2) Rental income phase — years of stabilized income with an optional annual rent-growth rate; (3) Optional sale event — a one-time positive lump sum at a specified year, net of a specified selling-cost percentage. Make this additive/optional: default to the current single-phase rental income model for users who just want a quick cash-flow snapshot, and let advanced users expand into the phase view for the full acquisition-to-exit picture.

### HELOC Payment Calculator
**Upgrade prompt:**
> Model the HELOC's actual contractual structure as two phases instead of one: (1) Draw period — interest-only payments on a variable/adjustable balance as funds are drawn; (2) Repayment period — fully amortizing payments once the draw period ends and the balance converts to principal + interest. Let the user specify draw-period length, repayment-period length, and rate for each (many HELOCs reset the rate at conversion). This reflects the loan's real structure rather than a single flat monthly-payment estimate.

### Savings Goal Calculator
**Upgrade prompt:**
> Allow the savings goal calculator to accept multiple growth phases with different contribution amounts (e.g. save $300/month for 2 years, then $600/month after an expected raise, then solve for when the combined phases cross the goal). Keep the existing solve-for-time / solve-for-contribution modes, but let solve-for-time run across a phase list instead of a single flat contribution rate.

### Mortgage Extra Payment Calculator
**Upgrade prompt:**
> Let the extra-payment strategy vary across phases instead of one constant extra amount — e.g. an aggressive extra-payment phase for the first 5 years, then a reduced or paused phase afterward (reflecting a life change like kids or a job change). Reuse the phase-card pattern for defining each extra-payment period's amount and duration.

---

## Bucket 3 — Likely skip

These are single-decision or point-in-time tools where a sequence of phases isn't really the shape of the question being asked. No prompts drafted — revisit only if a specific user request surfaces a real need.

- **Capital Gains Tax Calculator** — a tax computation on one sale event, not a trajectory over time.
- **Inflation-Adjusted Return Calculator** — a single nominal-to-real conversion, not a multi-period model.
- **Margin Loan Calculator** — short-term/point-in-time cost and maintenance-requirement math.
- **Cash-Out Refinance vs. HELOC Calculator** — a snapshot comparison between two options, not a timeline.
- **DRIP Calculator** — intentionally a simple, single-assumption compounding illustration; part of its value is being the *not*-complicated option next to the compound interest calculator.
- **DCA Calculator** — already has its own distinct segmented structure (deployment window vs. total horizon) purpose-built for the DCA-vs-lump-sum question; phases would blur that identity rather than sharpen it.

---

## Notes / open questions for later

- Consider holding off on bucket 2 until there's real usage data from bucket 1 — no need to commit to four more builds before seeing whether the phase treatment actually moves engagement on Coast FIRE, 529, Roth vs Traditional, or Trump Account.
- Each of these is a real build (phase-card UI, shareable-link array encoding, validation, chart boundary markers), not a quick reskin — budget accordingly per calculator.
