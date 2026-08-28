# Affiliate disclosure block — reusable snippet

One copy-paste block that carries **disclosure and tracking together**, so a future placement
can't accidentally ship with one and not the other.

Not a shared JS/CSS file, deliberately — this repo is single-file pages with no build step
(see CLAUDE.md). This is the canonical source; paste it into whichever page needs a placement.

**Why disclosure sits inside the block:** the FTC requires disclosure to be clear and
conspicuous *at the point of click* — adjacent to the link a reader is deciding whether to
click, not in a page footer and not only in the privacy policy. A block that bundles the two
makes the compliant thing the easy thing.

---

## 1. CSS — paste once per page, inside the existing `<style>`

```css
  /* ---- Affiliate placement (disclosure + link, see AFFILIATE-DISCLOSURE-SNIPPET.md) ----
     The disclosure is part of the block by design: never ship the link without it. */
  .affiliate-block {
    background: var(--ink-raised);
    border-left: 2px solid var(--amber-dim);
    padding: 14px 16px;
    margin: 22px 0;
  }
  .affiliate-block p { margin: 0; }
  .affiliate-block .affiliate-offer {
    font-size: 15px;
    color: var(--parchment-dim);
    line-height: 1.6;
  }
  .affiliate-block .affiliate-offer a {
    color: var(--amber);
    text-decoration: none;
    border-bottom: 1px solid var(--amber-dim);
  }
  .affiliate-block .affiliate-offer a:hover { border-bottom-color: var(--amber); }
  .affiliate-block .affiliate-disclosure {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 10.5px;
    line-height: 1.6;
    color: var(--parchment-faint);
    margin-top: 8px;
  }
```

## 2. HTML — paste at the point of click

Place it where the reader is actually deciding, i.e. next to the relevant result or
explanation. Never in `.support-footer`.

```html
<div class="affiliate-block">
  <p class="affiliate-offer">
    [ONE PLAIN SENTENCE: what the product is and why it's relevant *here*.]
    <a href="[AFFILIATE_URL]" data-affiliate="[LINK_ID]" target="_blank" rel="sponsored noopener">[LINK TEXT]</a>.
  </p>
  <p class="affiliate-disclosure">
    [WHAT THE RELATIONSHIP IS AND WHAT THE SITE GETS.] It costs you nothing extra, and it
    doesn't change any number on this page.
  </p>
</div>
```

**`rel="sponsored noopener"`** — `sponsored` is Google's required attribute for paid or
affiliate links. Note this is the opposite of the embed attribution link, which is
deliberately dofollow.

## 3. JS — paste once per page, inside the existing page script

Event delegation, so every current *and future* placement on the page is wired by this one
listener. No per-link setup, nothing to forget.

```js
  // ---- Affiliate click tracking (pairs with .affiliate-block; delegated so future
  // placements need no extra wiring). Fires the standard affiliate_click event. ----
  document.addEventListener('click', function (e) {
    var a = e.target.closest && e.target.closest('a[data-affiliate]');
    if (!a) return;
    window.trackEvent && window.trackEvent('affiliate_click', { link_id: a.dataset.affiliate });
  });
```

`affiliate_click` is already marked as a key event in GA4 admin, so new placements inherit
conversion tracking with no analytics change.

---

## Worked example — tone reference

Modelled on the existing Monarch disclosure, which is the house voice: first person, states
plainly what the link is, says what the site actually gets, and applies no pressure.

> I also use [Monarch](https://monarch.com) to track net worth and spending — that's a
> referral link, so if you sign up I get a discount on my own subscription. No pressure
> either way.

Applied to the block:

```html
<div class="affiliate-block">
  <p class="affiliate-offer">
    If you'd rather not do this by hand, <a href="[AFFILIATE_URL]" data-affiliate="[PROVIDER]"
    target="_blank" rel="sponsored noopener">[Provider]</a> handles this calculation as part
    of its filing flow.
  </p>
  <p class="affiliate-disclosure">
    That's an affiliate link — if you sign up, this site earns a commission. It costs you
    nothing extra, and it doesn't change any number on this page.
  </p>
</div>
```

## Rules for any new placement

1. **Disclosure ships with the link, always.** If you're pasting the `<a>` without the
   `.affiliate-disclosure` line, stop.
2. **Adjacent, not footer.** Point of click.
3. **`data-affiliate` is required** — it's what fires the tracking. Use a short stable id
   (`turbotax`, `freetaxusa`, `monarch`).
4. **`rel="sponsored noopener"`.**
5. **Say what the site gets** — "earns a commission", "gets a discount" — not a vague
   "may be compensated".
6. **Never let it touch the math.** The disclosure claims the numbers are unaffected; that
   has to stay true.

## Not yet applied

No page currently uses this block. First intended placement is the e-file/tax-software link,
held until after this batch is live. The existing Monarch placement in `.support-footer`
retains its own bespoke wiring and was deliberately left untouched.
