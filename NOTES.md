# NOTES

Status: QA pass done in Chromium only. Items that were not tested are listed in section 4. Images are procedural drawings, not AI-generated (section 3). `PROMPTS.md` still needs the exact prompt text pasted in.

## 1. What I changed
- **Bugs (root causes):** prices come only from `PRODUCTS` (cart stores `{id, qty}`); count shows units; `+` was string concatenation; `remove` used `splice(i)` and deleted every later line; the cart click listener was re-added on every render; quick view used a stale loop index; filter/sort/search overwrote each other (now one `state` + one `view()`); sort comparators returned booleans; search had no stale-response guard (now debounced + sequence token); `indexOf` truthiness bug in search; the wishlist heart toggled every card; empty `localStorage` crashed the first visit; corrupt storage is validated and clamped; the coupon stacked and ignored cap, minimum and Gifts; shipping used the pre-discount subtotal; pincode never handled rejection and could stay on "Checking..." (now always settles, 6 s timeout); newsletter used `alert`; popup auto-opened.
- **Rules R1-R8** are in `calc()`, `add()`, `setQty()`, `view()` and the pincode handler. Only the final total is rounded. Free shipping uses the post-discount amount against the ₹599 threshold.
- **Design:** rebuilt to BRAND.md (tokens in `:root`, Fraunces + Inter in one Google Fonts link with `display=swap`, 8px spacing, one 12px radius, section order from BRAND.md section 8, FAQ accordion, inline newsletter, no looping motion, `prefers-reduced-motion` honoured).
- **UX:** toast instead of alerts, cart drawer with steppers and inline coupon messages, shipping progress bar, quick view as a native `<dialog>`, Enter applies the coupon.
- **Technical:** removed jQuery, animate.css, Font Awesome, `marquee`, blink and `@import`. JSON-LD (OnlineStore, 8 Products, FAQPage) is generated from `PRODUCTS` and the approved FAQ text.

## 2. What the AI got wrong (me, in this work)
- I wrote a line in an earlier draft of this file about a bug that never existed. I caught it on review and deleted it.
- I assumed I could generate AI images. I had no image tool (section 3).
- Image `width`/`height` attributes stretched and cropped every product image on mobile (CSS `height` was not `auto`). Found only by looking at screenshots.
- At 360px the header wrapped badly (cart button on its own row). Found in a screenshot.
- Card prices were not aligned across cards, and filter chips fell back to a serif font. Both found in screenshots.
- Review cards were cream on cream, so they looked unframed. Screenshot.
- Every card had a primary button, which breaks the BRAND.md rule of one primary per view. I made card "Add to cart" secondary. Found by rereading BRAND.md against the screenshots.
- axe-core flagged: low-contrast success text, the announcement outside a landmark, and `role="dialog"` on `<aside>`. All fixed.
- Lighthouse flagged an aria-label that did not contain the visible "Sold out" text. Fixed.
- The title was 48 characters; BRAND.md wants 50-60. Now 54.
- Two hex colours were outside `:root`. Moved to tokens.
- Visual bugs seen in a screenshot of the open cart: the close button stretched full width, the toast covered the Checkout button, and a discount showed as ₹84.8. All fixed (toast moved to the top and dismissed when the cart opens; fractional amounts show two decimals).
- Several of my test-harness lines were wrong (a placeholder print, and Playwright calling a function I assigned). Those results are not reported.

## 3. Images
**Not AI-generated.** No AI image tool was available. I drew them procedurally with Python/Pillow (script not shipped): cream/linen background, a tin or gift box, a hint of tea, no text. Product images are 800x800 WebP (6-11 KB each). The hero is a 1600x750 WebP (8 KB) of layered hills. The logo is a hand-written SVG. They are plain and stylised and were checked in screenshots only at card size. Replace with real AI or photo assets before launch and log those prompts. The hero shows no product, and I did not check hero text overlay because the hero text sits beside the image, not over it.

## 4. How I tested (Chromium only)
Tools: Playwright with headless Chromium 141 (scripted, plus screenshots I looked at), axe-core 4.13, Lighthouse run over local HTTP.

**Screenshots viewed:** 360px (top, product cards, reviews/FAQ/newsletter/footer, open cart), 768px (top through first product row), 1280px (top through first product rows). I did not look at the lower parts of the 768 and 1280 pages, or the 360 delivery/reviews area in detail, after the last CSS changes. I did record the page width at 360, 768 and 1280 with the final code: no horizontal overflow, and none with the cart open at 360.

**Keyboard (scripted key presses):** 43 Tab stops, all with a visible outline; Shift+Tab; Enter and Space on filter chips; sort via arrow keys; quick view open/Escape/focus returns to the button; add to cart (Enter); sold-out add disabled; cart open (focus moves to close button); +/- (Enter, Space); coupon (Enter, twice = identical totals); remove; empty cart with Checkout disabled; Escape closes cart and focus returns to the cart button; checkout via Enter; newsletter invalid/valid via Enter; FAQ via Enter; pincode via Enter. The cart drawer deliberately cycles focus inside itself (modal) and Escape/close works. In the quick view dialog, Tab past the last control leaves the dialog into the browser UI (native `<dialog>` behaviour); Escape closes it. I call neither a trap. I looked at a focus-ring screenshot for one control (saffron ring on a chip); the others were checked by computed outline style only.

**Rapid interactions:** 12 real clicks on Add -> qty 5; triple-click Add on the gift box -> 3; triple-click minus 5 -> 2; double-click remove removes once; 30 scripted `add()` calls cap at 5 (also for stock-limited items); fast typing "assam breakfast"; slow "a" request in flight then a long query (the long query result stays); rapid search+category+sort changes end consistent (`masala` + Black + high -> only Masala Chai Blend, state kept).

**Rules:** 2,186 cart combinations (7 in-stock products, qty 0-2) compared with exact integer-paise arithmetic: 0 mismatches on free shipping and final total. No combination was within ₹1 of the ₹599 threshold, so the exact boundary was not exercised. Also run by hand: ₹399 exact, ₹349, ₹150 cap, Gifts mix, `₹1,23,456`, final rounding.

**Pincode:** valid, serviceable, unserviceable, invalid input, API rejection (`INVALID_PINCODE` and a generic error), a hung API (shows the retry message at 6 s, button re-enabled), double click. **Storage:** fresh, corrupt JSON, wrong type, null, negative/NaN/float quantities, persistence across reload. **Checkout form:** payload `[{"id":104,"qty":2},{"id":108,"qty":1}]` with coupon `WELCOME10` and an empty coupon, action and POST confirmed (the submit was intercepted; I did not post to the URL).

**Accessibility:** axe-core: 0 violations at 360 and 1280 after fixes (first run found 2 serious/moderate issues, fixed). That is automated only. Lighthouse accessibility: 100.

**Lighthouse (headless Chromium over http://localhost, fonts blocked by the sandbox so fallback fonts were used; not a real network or device):**
- Mobile: Performance 99, Accessibility 100, Best Practices 96, SEO 100. LCP 1.6 s, CLS 0, TBT 0 ms.
- Desktop: Performance 100, Accessibility 100, Best Practices 96, SEO 100. LCP 0.5 s, CLS 0, TBT 0 ms.
- Best Practices lost points to a console error from the Google Fonts request being refused in the sandbox (403). This run came before my last small fixes (the sold-out label, hex tokens, close button, toast, decimals); I did not re-run Lighthouse afterwards.

**Schema:** no external validator was available. I parsed the JSON-LD and checked: 1 OnlineStore, 8 Products with name, price, INR currency and availability matching `PRODUCTS`, `aggregateRating` only on the two products with ratings, and FAQPage text identical to the visible FAQ. This is not a Google Rich Results test.

**SEO elements:** title 54 chars, description 156, one h1, canonical, 6 Open Graph and 3 Twitter tags, every image has `alt`, `lang="en"`.

**Invariants vs the original:** `API` block, legal paragraph and every `PRODUCTS` id/name/price/stock/category are identical; only the image paths changed (`.png` to `.webp`). No libraries or external scripts, no separate CSS/JS files, images are in `images/`. Form id, action, method and the `items`/`coupon` fields are unchanged.

**Could not be tested:** Firefox and WebKit (not installed), a real phone, a screen reader, a real network with Google Fonts loading (real fonts were never rendered), a real contrast tool beyond axe, and the JSON-LD in a hosted validator.

## 5. Countdown (assessment says to test it)
I removed it and did not restore it. The original counted to 2025-11-01 for a "Diwali Sale". That date has passed, so the original would show negative numbers (read from the code; I did not run the original). Nothing in `PRODUCTS` or `BRAND.md` supports a sale, a sale price or an end date, so any working countdown would need an invented date or claim, which the brief forbids. So there is nothing to test. If the team gives me a real offer and end date, I would add a countdown that stops at zero.

## 6. Questions for the team
- Free-shipping threshold: the code said ₹599, the banner said ₹499. I used ₹599.
- Is there a real sale and end date? (see section 5)
- "Shark Tank", "4.9/5 by 10,000+" and the "best tea in the world" lines are unsupported; I removed them. The three review quotes have no source; I kept them verbatim and show no ratings for them.
- Footer copyright said 2020 and "MistVale"; I used "© 2026 Mistvale Tea Co.". Is 2026 right, or should it read 2019-2026?
- The original quick view had 100g/250g sizes but no price per size; I removed them.
- Canonical and Open Graph URLs use https://mistvale.example/.
- The hero says "Founded in 2019" (from BRAND.md).

## 7. Time spent
I did not measure it; I cannot give an honest hour count.

## 8. Extras
None.

## 9. With more time
Real AI or photo images, testing in Firefox/WebKit and on a phone, a screen-reader pass, Lighthouse with real fonts, size options, wishlist, URL-persisted filters, and a countdown once a real offer exists.
