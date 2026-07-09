# Retirement Backtest Calculator — Manual QA Checklist

Working file for pressure-testing `/retirement-backtest-calculator` before treating it as production-solid. Automated tests (Node unit tests + jsdom interaction tests) already passed on the engine and basic UI wiring — this checklist is for the things only a human eyeballing the live page will catch.

---

## 1. Math / logic correctness

- [ ] Default scenario ($20,000 start, 20yr @ 7% + $12,000/yr contribution, -$40,000 lump sum at year 8, then 30yr retirement at $20,000/yr withdrawal, 60% stock, 0.2% fee drag) — confirm "balance entering retirement" and success rate look sane on the live page, not just in the test harness.
- [ ] Change starting balance up/down — confirm balance entering retirement scales proportionally (upstream math is linear in starting balance when there are no clipped lump sums).
- [ ] Add a growth phase, remove a growth phase — confirm the "years" cap on remaining phases updates live (max years per card should shrink as other phases use up the 80-year budget).
- [ ] Add a lump-sum event at year 0 (before any growth) — confirm it applies immediately.
- [ ] Add a lump-sum event exactly at the boundary between two growth phases — confirm it applies once, not twice, and lands at the correct point.
- [ ] Add a lump-sum event with a year beyond total upstream years (e.g. upstream is 20 years, lump sum year = 25) — confirm it applies at the very end, right before retirement starts.
- [ ] Add a withdrawal lump sum (negative amount) larger than the balance at that point — confirm it clips to zero (never goes negative) and the warning banner shows the requested vs. applied amount.
- [ ] Try to push total growth-phase years past 80 — confirm the horizon note flips to the "over" warning color and/or the add-phase button disables.
- [ ] Set stock allocation to 100% — confirm terminal returns match the pure stock column behavior (spot check 2-3 individual historical years against the raw data).
- [ ] Set stock allocation to 0% — same check against the pure bond column.
- [ ] Compare 0% fee drag vs. 1% fee drag on an identical scenario — confirm success rate and percentile balances are strictly worse with the fee drag on.
- [ ] Pick a known high-inflation historical start year (1973 or 1979) and eyeball that cycle's row in the results table — withdrawal should visibly outpace a low-inflation start year (1955 or 1961) by the same point in the cycle.
- [ ] Cross-check cycle count: for a given retirement length N, the table should show exactly `98 - N + 1` rows (98 = years of data currently loaded, 1928–2025).
- [ ] Sort/scan the results table by ending balance and confirm the printed 10th/50th/90th percentile stats roughly match what you'd read off manually from the sorted column.
- [ ] Confirm the known rough failure years for a 100%-stock/4%-withdrawal Trinity-style scenario (1929, 1930, 1966, 1968, 1969 starts) show up as "depleted" in the table when you dial the calculator to match that scenario.

## 2. UI / interaction

- [ ] Remove every growth phase (down to zero upstream phases) — confirm retirement starts directly from the starting balance with no crash.
- [ ] Remove every lump-sum event — confirm no orphaned markers remain on the timeline bar.
- [ ] Rename a phase label to include a quote character (`"`), an ampersand (`&`), or an emoji — confirm it doesn't break the card re-render or the shareable link.
- [ ] Enter letters, blank, or a negative number in every numeric field one at a time — confirm graceful clamping on blur, no crash, no `NaN` displayed anywhere.
- [ ] Enter an extremely large number (e.g. starting balance = 1 followed by 15 zeros) — confirm it clamps to the defined max rather than breaking the chart's y-axis.
- [ ] Hover and keyboard-focus every "?" tooltip icon — confirm the help text shows and is legible on both light-colored and dark backgrounds of the tooltip box.
- [ ] Resize the browser to a narrow mobile width — confirm the field grids collapse to two columns, the stat row stacks vertically, and nothing overflows horizontally.
- [ ] Scroll the historical-cycle results table — confirm the header row stays pinned (sticky) and scrolling is smooth even with ~90 rows.
- [ ] Set retirement length very short (1-2 years) — confirm the chart isn't overwhelmed by near-100 spaghetti lines to the point of being unreadable; consider whether a cap/opacity adjustment is needed at high cycle counts.
- [ ] Set retirement length near the max (70 years) — confirm the now-small number of spaghetti lines (~29) still reads clearly and the percentile bands don't look jagged/broken with so few samples.
- [ ] Hover over the chart — confirm Chart.js tooltips aren't a garbled mess given ~70+ overlapping datasets (may want tooltips disabled or limited to the percentile/projection lines only if this is noisy).

## 3. Shareable link / persistence

- [ ] Click "copy shareable link," open the copied URL in a new incognito window — confirm every field (starting balance, each phase, terminal phase settings) restores exactly.
- [ ] Manually corrupt the `?d=` parameter in the URL (delete a few characters) — confirm the page falls back to defaults instead of crashing.
- [ ] Build a scenario with the maximum allowed phases and years, generate the link, reload — confirm the 80-year cap is still enforced on reload and nothing silently exceeds it.
- [ ] Type quickly in a few fields in a row — confirm the URL update is debounced (doesn't spam browser history) but still ends up correct after typing stops.

## 4. Content / copy accuracy

- [ ] Confirm the FAQ and article text reference "1928–[latest year]" dynamically correct and not a stale hardcoded year if the dataset is ever extended.
- [ ] Re-read the FAQ's methodology claims (Trinity-study framing, sequence-of-returns explanation, inflation-adjustment description) against what the engine actually does — confirm no drift between what's coded and what's described.
- [ ] Confirm "Projection" is the only label used for upstream output and "Historical success rate" is the only label used for terminal output, consistently, per the original spec.
- [ ] Click every outbound link (buy me a coffee, Monarch referral, nav links) — confirm none are dead or mistyped.

## 5. Accessibility / cross-browser

- [ ] Tab through the entire page using only the keyboard — confirm a sensible focus order through phase cards, add buttons, and the terminal card.
- [ ] Run a screen reader pass (VoiceOver/NVDA) over the chart's `aria-label` and the phase-card inputs — confirm labels are meaningful without seeing the visuals.
- [ ] Load the page in Safari, Chrome, and Firefox — confirm the chart renders identically and no CSS quirks appear (flexbox wrapping, sticky table header, tooltip positioning).

## 6. Performance

- [ ] With ~90 spaghetti lines rendered (short retirement length), confirm chart redraw on input change isn't noticeably laggy.
- [ ] Rapidly change a slider/number field several times in under a second — confirm no visible jank or duplicate chart instances (check the `chart.destroy()` call is actually preventing leaks — inspect memory/dev tools if unsure).

## 7. Data integrity

- [ ] Spot-check 5-10 individual years' stock return, bond return, and inflation figures in the embedded `HIST` array against the original Damodaran and BLS sources directly, to catch any transcription slip.
- [ ] Confirm deflationary years (negative inflation, e.g. 1930-1933, 2009) correctly *decrease* the withdrawal amount in the following year rather than being floored at zero or skipped.
- [ ] Confirm the most recent year in the dataset stays current — flag when it's time to add the newly-completed calendar year's data (should be an annual, low-effort update once Damodaran/BLS publish it).

---

**Not yet decided — flag for a product call, not a bug:**
- Whether the chart should cap the number of spaghetti lines drawn (e.g. sample every Nth cycle) once cycle count gets very high, purely for visual clarity.
- Whether Chart.js tooltips should be disabled entirely for the spaghetti dataset layer (leaving them only on the projection/percentile lines) to avoid tooltip clutter.
