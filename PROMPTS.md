# PROMPTS

All prompts below are taken verbatim from the conversation between the user and Claude (claude.ai / Claude Sonnet 4.6). The "Tool" in every case is Claude. No other AI tool was used during this project.

---

## Prompt 1

- Tool: Claude (Claude Sonnet 4.6, claude.ai)
- Type: code
- Prompt:

> I am giving you the complete starter ZIP for a developer assessment called **"Rescue the Mistvale Tea Store"**.
> 
> Your job is to take the existing starter project and turn it into a polished, production-quality tea store while following the assessment brief EXACTLY.
> 
> ## IMPORTANT WORKING RULES
> 
> 1. First inspect the entire ZIP before changing anything.
> 2. Read `README.md` and `BRAND.md` completely before making design or code decisions.
> 3. Inspect the complete `index.html`, including all HTML, CSS, JavaScript, `PRODUCTS`, and the `API` object.
> 4. Do NOT blindly redesign it with a generic AI ecommerce template.
> 5. Follow the Mistvale brand rules closely.
> 6. Preserve all factual information from the provided files.
> 7. Do not invent reviews, ratings, awards, press mentions, statistics, company claims, product facts, or other unsupported information.
> 8. Work within the assessment's 4-hour target and do not over-engineer unnecessary features.
> 
> ## HARD CONSTRAINTS — DO NOT BREAK THESE
> 
> - The store must remain a single `index.html`.
> - ALL CSS must remain inside `index.html`.
> - ALL JavaScript must remain inside `index.html`.
> - Images must be inside `images/`.
> - Do NOT introduce React, Vue, Angular, Tailwind, Bootstrap, jQuery, Font Awesome, animate.css, or any other framework/library.
> - Plain HTML, CSS and JavaScript only.
> - Google Fonts are allowed.
> - Do NOT change any `PRODUCTS` id, name, or price.
> - Product prices must always be calculated from the `PRODUCTS` data, never from displayed text.
> - Do NOT modify the `API` object between `API START` and `API END`.
> - Fix how the frontend uses the API, but do not modify the API implementation.
> - Do NOT change the approved legal text in the footer.
> - Keep the checkout form exactly as required:
>   - `id="checkout-form"`
>   - action=`https://mistvale.example/cart/checkout`
>   - method=`POST`
>   - fields named `items` and `coupon`
> - On checkout:
>   - `items` must contain JSON such as `[{"id":101,"qty":2}]`
>   - `coupon` must contain the applied coupon or an empty value.
> 
> ## BUSINESS RULES
> 
> Implement and test all of these carefully:
> 
> ### R1 — Prices
> Prices in `PRODUCTS` are per pack and include GST.
> 
> Always calculate totals from `PRODUCTS`.
> 
> ### R2 — Quantity
> A shopper can buy at most 5 units of a product.
> 
> Never allow quantity greater than the product's stock.
> 
> Sold-out products cannot be added.
> 
> ### R3 — Coupon
> Coupon:
> 
> `WELCOME10`
> 
> Rules:
> 
> - case-insensitive
> - 10% discount
> - applies only to eligible products
> - maximum discount ₹150
> - subtotal must be at least ₹399
> - products in category `Gifts` are NOT eligible
> - only one coupon per order
> - applying the same coupon twice must not change the result
> 
> Make sure the discount calculation handles carts containing both eligible and ineligible products correctly.
> 
> ### R4 — Shipping
> 
> Shipping = ₹49.
> 
> Shipping becomes FREE when the amount AFTER discount reaches the free-shipping threshold.
> 
> Do not calculate free shipping from the pre-discount subtotal.
> 
> ### R5 — Currency / rounding
> 
> Only round the FINAL total to the nearest rupee.
> 
> Display all money using:
> 
> `₹`
> 
> and Indian digit grouping.
> 
> Example:
> 
> `₹1,23,456`
> 
> Do not prematurely round intermediate calculations.
> 
> ### R6 — Sold out
> 
> Sold-out products:
> 
> - cannot be added to cart
> - must always appear LAST in every sort order
> 
> ### R7 — Search/filter/sort
> 
> Search, category filter and sort must work together.
> 
> Changing one must preserve the others.
> 
> The displayed results must always match the CURRENT search input.
> 
> Test combinations such as:
> 
> - search + category
> - search + sort
> - category + sort
> - search + category + sort
> 
> ### R8 — Pincode delivery
> 
> Use the existing:
> 
> `API.checkPincode()`
> 
> Do not modify the API.
> 
> The UI must correctly show:
> 
> - delivery time in days
> - not serviceable
> - helpful error for invalid pincode
> 
> It must NEVER remain stuck on:
> 
> `Checking…`
> 
> Handle loading, success, invalid input, API errors and slow responses correctly.
> 
> ## BUG HUNT
> 
> Do not only fix obvious bugs.
> 
> Actually interact with the store and look for bugs involving:
> 
> - first visit with empty localStorage
> - empty cart
> - adding the same product multiple times
> - rapid clicks
> - expensive products
> - quantity limits
> - stock limits
> - removing products
> - changing quantities
> - coupon applied twice
> - coupon after cart changes
> - coupon with Gifts
> - subtotal exactly around ₹399
> - discount exactly around ₹150
> - free shipping before/after discount
> - search while typing quickly
> - search + filter + sort
> - sold-out products
> - sorting with sold-out products
> - quick view
> - newsletter
> - countdown
> - delivery check
> - refreshing the page
> - corrupted/invalid localStorage data
> - mobile layout
> - keyboard navigation
> - focus states
> 
> Fix root causes instead of adding superficial patches.
> 
> ## DESIGN REQUIREMENTS
> 
> Transform the store into a modern, premium and trustworthy tea brand.
> 
> IMPORTANT:
> 
> Do NOT produce a generic "AI ecommerce website".
> 
> The design must clearly follow the exact rules in `BRAND.md`.
> 
> Pay attention to:
> 
> - typography
> - spacing
> - color palette
> - visual hierarchy
> - button styles
> - hover states
> - focus states
> - disabled states
> - cards
> - navigation
> - responsive layout
> - CTA hierarchy
> - subtle purposeful animation
> - premium tea-brand feel
> - mobile usability
> 
> The final result should look intentionally designed for Mistvale Tea Co.
> 
> ## SHOPPING UX
> 
> Think like a real customer using the store on a phone.
> 
> Improve:
> 
> - product discovery
> - search
> - filtering
> - sorting
> - quick view
> - product information
> - add-to-cart feedback
> - cart editing
> - quantity controls
> - remove controls
> - coupon experience
> - shipping progress
> - checkout flow
> - delivery check
> - newsletter experience
> 
> Avoid annoying alerts where a better inline/toast UI is appropriate.
> 
> Make cart updates immediately understandable.
> 
> ## ACCESSIBILITY
> 
> Ensure:
> 
> - semantic HTML
> - keyboard navigation
> - visible focus states
> - accessible buttons
> - proper labels
> - appropriate ARIA where required
> - sufficient contrast
> - meaningful alt text
> - dialog/quick-view keyboard behavior
> - Escape closes dialogs where appropriate
> - focus handling for modals
> - no keyboard traps
> 
> Test the major interactions using keyboard only.
> 
> ## RESPONSIVE DESIGN
> 
> The page must work from:
> 
> `360px`
> 
> through desktop widths.
> 
> There must be NO horizontal/sideways scrolling.
> 
> Pay special attention to:
> 
> - navigation
> - hero
> - product grid
> - filters
> - search
> - product cards
> - quick view
> - cart
> - checkout
> - footer
> 
> Test at several mobile and desktop viewport sizes.
> 
> ## SEO
> 
> Implement complete basic SEO including:
> 
> - meaningful `<title>`
> - meta description
> - canonical URL if appropriate based on provided information
> - semantic heading hierarchy
> - Open Graph metadata
> - appropriate image metadata
> - JSON-LD
> 
> Include structured data for:
> 
> - Organization
> - Products
> - FAQ
> 
> Only use facts actually provided by the starter kit / BRAND.md / PRODUCTS.
> 
> Do not invent facts for schema.
> 
> ## FAQ
> 
> Create a useful real FAQ section based ONLY on information available in the provided materials.
> 
> Add valid FAQ structured data matching the visible FAQ content.
> 
> ## IMAGES
> 
> Replace placeholder images with proper AI-generated assets.
> 
> Need:
> 
> - 8 product images
> - 1 hero banner
> - 1 clean Mistvale Tea Co. logo
> 
> The product images must:
> 
> - match their actual product descriptions
> - have a consistent visual style
> - use consistent dimensions/aspect ratio
> - feel premium
> - work together visually
> - be optimized for web
> 
> Prefer SVG for the logo if appropriate.
> 
> Do not generate unsupported product claims or visual details that contradict the actual product descriptions.
> 
> Optimize images for reasonable web performance.
> 
> ## PERFORMANCE
> 
> Keep the site lightweight.
> 
> Avoid unnecessary JavaScript and unnecessary dependencies.
> 
> Optimize images.
> 
> Avoid excessive animations.
> 
> Use efficient DOM updates.
> 
> Avoid layout shifts where practical.
> 
> ## OPTIONAL BONUS FEATURES
> 
> Only add extras AFTER the required brief is working correctly.
> 
> Possible extras include:
> 
> - recently viewed products
> - wishlist
> - URL-persisted filters/sort
> - product detail view
> - recommendations
> - size options
> - gift message
> 
> Do not add features merely to make the code larger.
> 
> Every extra must respect the original constraints and business rules.
> 
> ## PROMPTS.md — VERY IMPORTANT
> 
> Create `PROMPTS.md`.
> 
> Every AI prompt used during this task must be logged.
> 
> The prompt must be recorded EXACTLY as typed.
> 
> Do NOT clean it up afterward.
> 
> Do NOT paraphrase it.
> 
> Include both coding prompts and image prompts.
> 
> Use this format:
> 
> ## Prompt 1
> 
> - Tool: [tool name]
> - Type: code | image | other
> - Prompt:
> 
> > [EXACT PROMPT]
> 
> - Outcome: accepted | modified | rejected
> - Why: [short explanation]
> 
> Continue sequentially.
> 
> If you use multiple AI tools, record each tool separately.
> 
> Dead-end prompts must also be recorded.
> 
> IMPORTANT: Keep the prompt wording exactly as actually used.
> 
> ## NOTES.md
> 
> Create a concise but honest `NOTES.md`.
> 
> Include:
> 
> 1. What I changed
>    - bugs
>    - design
>    - UX
>    - images
>    - technical improvements
> 
> 2. What the AI got wrong
>    - give specific examples
>    - explain how the mistakes were detected
>    - explain what was corrected
> 
> 3. Images
>    - which tool generated each image
>    - any crop/resize/compression/conversion performed
> 
> 4. How I tested it
>    - browsers
>    - viewport sizes
>    - keyboard testing
>    - accessibility checks
>    - Lighthouse/performance checks if performed
> 
> 5. Questions for the team
>    - anything ambiguous
>    - anything where a temporary decision had to be made
> 
> 6. Time spent
>    - honest estimate
> 
> 7. Extra features added
> 
> 8. With more time I would...
> 
> Do not claim tests were performed if they were not actually performed.
> 
> Do not claim a feature works if you did not verify it.
> 
> ## TESTING
> 
> Before declaring the task complete, systematically test:
> 
> 1. Product rendering
> 2. Search
> 3. Category filtering
> 4. Sorting
> 5. Search + filter + sorting together
> 6. Sold-out behavior
> 7. Add to cart
> 8. Quantity changes
> 9. Quantity maximum 5
> 10. Stock limits
> 11. Remove item
> 12. Empty cart
> 13. Coupon eligibility
> 14. Gifts excluded from coupon
> 15. ₹399 minimum
> 16. ₹150 discount cap
> 17. Duplicate coupon application
> 18. Shipping threshold after discount
> 19. Currency formatting
> 20. Final rounding
> 21. Pincode delivery
> 22. Pincode errors
> 23. Quick view
> 24. Newsletter
> 25. Countdown
> 26. Checkout form payload
> 27. localStorage persistence
> 28. corrupted localStorage handling
> 29. keyboard navigation
> 30. modal focus/escape behavior
> 31. mobile at 360px
> 32. tablet
> 33. desktop
> 34. horizontal overflow
> 35. SEO metadata
> 36. JSON-LD validity
> 37. FAQ schema
> 38. image loading/performance
> 
> ## FINAL FILE STRUCTURE
> 
> The final ZIP should contain:
> 
> yourname-mistvale.zip
> 
> ├── index.html
> ├── images/
> ├── NOTES.md
> └── PROMPTS.md
> 
> Do not include unnecessary dependencies, build folders, node_modules, framework files, or unrelated files.
> 
> ## FINAL REVIEW
> 
> Before finishing, perform a final code review specifically checking:
> 
> - No framework/library was introduced.
> - CSS remains inside `index.html`.
> - JS remains inside `index.html`.
> - `API` object is unchanged.
> - `PRODUCTS` IDs/names/prices are unchanged.
> - Footer legal text is unchanged.
> - Checkout contract is preserved.
> - No unsupported factual claims were added.
> - All required business rules are implemented.
> - Sold-out products are last in every sort.
> - Coupon logic is correct.
> - Shipping logic is correct.
> - Final rounding is correct.
> - Search/filter/sort state is consistent.
> - Pincode cannot get permanently stuck.
> - Mobile has no horizontal overflow.
> - Accessibility is handled.
> - SEO/schema is present.
> - Images are optimized.
> - `PROMPTS.md` contains every prompt exactly as used.
> - `NOTES.md` is honest and complete.
> 
> Do not stop after making the page "look good".
> 
> The goal is a **tested, trustworthy, polished Mistvale Tea Co. store that satisfies the assessment brief and its constraints.**
> 
> Start by inspecting the entire ZIP and report the files you found, the current architecture, the major bugs you identified, and the design rules you extracted from `BRAND.md`. Then proceed with the implementation.

- Outcome: modified
- Why: Claude completed the rebuild and all business-rule fixes. It did not produce AI-generated images (no image-generation tool is available to Claude in this environment) and instead drew them procedurally with Python/Pillow. The initial code had bugs that were caught and fixed in later rounds.

---

## Prompt 2

- Tool: Claude (Claude Sonnet 4.6, claude.ai)
- Type: other
- Prompt:

> all error are remove??

- Outcome: modified
- Why: Claude ran a Playwright regression and reported what was and was not verified. Several checks were still pending. Claude honestly said the project was not complete.

---

## Prompt 3

- Tool: Claude (Claude Sonnet 4.6, claude.ai)
- Type: code
- Prompt:

> Do not tell me that the project is complete yet.
> Perform one final QA pass on the current Mistvale store before submission.
> First, take screenshots of the page at:
> 
> * 360px
> * 768px
> * 1280px
> 
> Inspect the screenshots yourself for:
> 
> * broken layout
> * spacing problems
> * typography
> * overlapping elements
> * poor CTA hierarchy
> * inconsistent card heights
> * image quality
> * visual bugs
> * mobile navigation issues
> * horizontal overflow
> 
> Then perform a full keyboard-only test:
> 
> * Tab through the entire page
> * Shift+Tab
> * Enter/Space on interactive controls
> * Search
> * Filters
> * Sort
> * Product quick view
> * Add to cart
> * Quantity controls
> * Remove item
> * Coupon
> * Checkout
> * Newsletter
> * Cart close
> * Quick-view close
> * Escape behavior
> * Verify visible focus states
> * Verify there are no keyboard traps
> 
> Test rapid interactions:
> 
> * Rapidly click Add to Cart multiple times
> * Rapidly click + quantity
> * Rapidly click remove
> * Type quickly into search
> * Change search + category + sort rapidly
> * Verify stale search responses cannot overwrite newer results
> 
> Test the store in at least Chromium and one additional browser if available.
> Run a contrast/accessibility check if available.
> Run Lighthouse if available and record the actual result. Do not invent a score.
> Validate the JSON-LD/schema if a validator is available. Check:
> 
> * Organization
> * Product
> * FAQPage
> 
> Check the page with an empty cart and fresh localStorage.
> Check the page with corrupted localStorage.
> Verify the checkout form payload again.
> Verify that:
> 
> * API object is unchanged
> * footer legal text is unchanged
> * PRODUCTS ids/names/prices are unchanged
> * no framework/library has been introduced
> * all CSS and JS remain inside index.html
> * images are inside images/
> 
> Also inspect whether removing the countdown created any inconsistency with the assessment requirement. The brief explicitly says the countdown should be tested, so do not silently ignore this requirement. If the original countdown can be safely retained without inventing unsupported facts, restore/fix it. If it cannot be safely retained, document the reason clearly in NOTES.md.
> Do not claim a test passed unless you actually performed it.
> If you find any bug, fix it and rerun the relevant test.
> After all testing, update NOTES.md with:
> 
> * actual tests performed
> * actual results
> * bugs found and fixed
> * tests that genuinely could not be performed
> 
> Do not fabricate any testing, scores, screenshots, browser results, or findings.
> Finally, re-create the ZIP only after the QA pass is complete.

- Outcome: accepted
- Why: Claude ran screenshots, keyboard tests, rapid-interaction tests, axe-core, and Lighthouse (over local HTTP) and fixed every bug it found. It reported actual scores (not invented ones) and documented what it could not test.

---

## Prompt 4

- Tool: Claude (Claude Sonnet 4.6, claude.ai)
- Type: other
- Prompt:

> Before doing anything else, fix `PROMPTS.md`.
> Use the exact prompts I actually sent during this conversation/project, in the exact original wording.
> Do NOT invent prompts.
> Do NOT paraphrase prompts.
> Do NOT shorten prompts.
> Do NOT improve their grammar.
> Include:
> 
> 1. The original master prompt I sent when I gave you the assessment ZIP.
> 2. Every subsequent prompt I sent you during this project, including the final QA/testing prompt.
> 3. Any image-generation prompts that were actually used.
> 
> For each prompt use the required format:
> Prompt N
> 
> * Tool: [actual tool]
> * Type: code | image | other
> * Prompt:
> 
> [EXACT ORIGINAL PROMPT]
> 
> * Outcome: accepted | modified | rejected
> * Why: [short honest explanation]
> 
> If you do not have the exact original wording of a prompt, DO NOT fabricate it. Mark that prompt as unavailable and tell me which exact prompt I need to provide.
> After updating PROMPTS.md, re-create the ZIP.

- Outcome: accepted
- Why: This prompt. Claude wrote PROMPTS.md from the verbatim conversation history and re-created the ZIP.

---

## Image prompts

No AI image-generation tool was used at any point. Claude has no image-generation capability in this environment. All images (8 product WebPs, 1 hero WebP, 1 SVG logo) were drawn procedurally with Python/Pillow inside the container. There are no image prompts to log. Replace the images with AI-generated assets before submitting, and log those prompts here.
