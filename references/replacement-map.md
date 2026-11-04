# Replacement map (Step 9)

What replaces each Script pattern as of November 2026: a **native setting** the PM can set up (click-by-click), or a **custom Shopify Function** a developer builds (spec), or a **gap**. Source IDs in brackets refer to `sources.md`. Function API version at time of writing: **2026-10** [dev-function-apis]. **Never recommend a third-party app.** Shopify-built apps appear only as "Optional alternative (Shopify-built app)" unless agency policy says otherwise (SKILL.md).

Labels in click paths are from Shopify's Help Center. If a label in the admin differs, tell the developer/PM to follow the live label and note it; re-check the cited page if the whole path differs.

---

## 0. Decision rules (apply in this order, for every LOST or PARTIAL rule)

1. **Plan gate.** Read the plan from Step 3. Custom Functions need **Shopify Plus** [dev-function-apis]. Checkout Blocks features other than Thank you / Order status content blocks need **Plus** [hc-checkout-blocks].
2. **Native first.** If the pattern below has a native fix with fidelity **Exact** or **Close** (after rule 2a), recommend it as the main fix ("PM can do this"). If the pattern's Gaps line names a difference in **money or eligibility** (what a shopper pays, who qualifies, which units are discounted, stacking) and the store is on Plus, also give the developer option, labelled "If the merchant needs the exact old behaviour". If the Gaps line names only a presentation difference (a discount line instead of a lower price, wording), don't add a developer option.
   - **2a. Per-store fidelity check (do it before rule 2).** List what the rule card says the Script **left out**: products (tags, vendors, types, IDs, compare-at), gift cards, customers (tags, guests), carts or codes. If the native fix would give the discount, rate or payment option to anything the Script left out, or you can't confirm from what you saw that it wouldn't, its fidelity **for this store** is **Partial**, whatever the pattern line says. Common case: an order-level native discount (N2) can't leave out lines, so it discounts MAP-protected or `no-discount` products the Script skipped. Where the pattern lists a native variant that keeps exclusions, check that one first; it keeps the pattern's fidelity only if every exclusion becomes one of its conditions. A Partial native fix that still helps shoppers stays in the report as **"Interim (until {D#} is live)"**, with a G# that names what it gets wrong.
3. **Function when native falls short.** If native fidelity is **Partial** or **None** (including Partial from rule 2a), or the native fix would push active automatic discounts past **25** [hc-combinations], and the store is on Plus → main fix = **developer spec** (template in `output-template.md` section 6).
4. **Gap when nothing fits.** If native is Partial/None and the store is not on Plus (or the behaviour is in section 5) → record a **gap** with the closest native option.
5. **Shopify-built apps** (Checkout Blocks, Shopify Bundles): add as an optional line only; never as the main fix under the default policy; never say "install" as an instruction — say "the agency may choose to use…".
6. **Always** attach the store-wide warnings in section 6 that apply to the rule.
7. **"Recommended apps" from the Scripts report or CSV:** never copy a third-party name from that column, anywhere in the report. A Shopify-built app this map lists for the pattern may still appear as a labelled optional alternative (rule 5), even if the CSV also lists it: it comes from this map, not from the report.
8. **Interim for a P1 developer fix.** If a rule is P1 and its main fix is a D#, add one interim option in D# field 14, as a merchant decision. If rule 2a already gave an interim F#, point to it. Use only an existing setting or a click path in this map, labelled "re-check live" if its exact labels aren't in section 2, and say who it affects. Examples: turning off the manual payment method until the payment customization is live (approved accounts lose it at checkout too; staff can still send them draft order invoices); adding "no PO boxes" to the Express and Overnight rate names with N9. If nothing fits, write "No interim option".

Fidelity scale: **Exact** = same price and outcome for the shopper. **Close** = same money, different presentation or edge cases. **Partial** = some logic lost. **None** = can't be reproduced.

---

## 1. Plan gates (quick table)

| Thing | Plan | Source |
|---|---|---|
| Native discounts (amount off, BXGY, free shipping), segments, shipping rates | All plans | [hc-amount-off] [hc-bxgy] [hc-free-shipping] |
| Collections (manual and automated/"smart") | Basic, Grow, Advanced, Plus (**not Starter**) | [hc-smart-collections] |
| Several product discounts on the **same line item** | **Plus** | [hc-combinations] |
| Custom app containing Shopify Functions | **Plus** (built in the Dev Dashboard) | [dev-function-apis] [hc-transition] |
| Cart Transform `lineUpdate` (price/title/image override) | **Plus or development stores** | [dev-cart-transform] |
| Payment Customization: hide specific placements; `paymentTermsSet`; `orderReviewAdd` (B2B) | **Plus** | [dev-payment-customization] |
| Payment customizations on credit-card methods in the US and Canada | Plus (non-Plus: non-credit-card methods only) | [hc-checkout-customization] |
| Function network access (fetch) | Enterprise per the Functions overview; the Discount API page says Plus and Enterprise. Conflicting → treat as **not available** unless Shopify approves it | [dev-function-apis] [dev-discount-api] |
| Checkout Blocks discounts, functions, order limits, address validation | **Plus** | [hc-checkout-blocks] |
| Shopify Bundles | All plans | [hc-bundles] |
| B2B (companies, catalogs, volume pricing, quantity rules, net payment terms) | Basic, Grow, Advanced, Plus (not Starter or Retail). Non-Plus: 3 active catalog assignments across B2B markets, no direct company catalog assignment, no deposits / partial payments. Volume pricing, quantity rules and net terms are on all four plans | [hc-b2b-plan-features] |
| Discount Rollouts (show a discount to a share of shoppers) | **Unverified** — Help Center points to a requirements page that wasn't checked | [hc-rollouts] [cl-discount-rollouts] |

---

## 2. Native building blocks (click-by-click; the PM does these later, after approval)

**N1. Amount off products** [hc-amount-off]
1. Discounts > **Create discount** > select **Amount off products**.
2. Method: **Automatic discount** (or **Discount code** if shoppers had to type a code).
3. **Title** (shoppers see it on automatic discounts).
4. **Discount value**: percentage or fixed amount.
5. **Purchase type** (if the store sells subscriptions): One-time purchase / Subscription / Both.
6. **Applies to**: Specific collections or Specific products → add them.
7. Fixed amount only: tick **Only apply discount once per order** if the Script discounted once per order.
8. Minimum requirement: **Minimum purchase amount** or **Minimum quantity of items** (if any).
9. **Eligibility**: All customers / Specific customers / Customer segments / Markets.
10. **Combinations**: tick the classes it must stack with (see N5).
11. Leave **Also offer on Point of Sale (POS Pro locations only)** unticked unless the merchant wants it on POS (Scripts never ran on POS).
12. **Active dates**; optional end date.
13. Click **Save**.

**N2. Amount off orders** [hc-amount-off] — same as N1 but choose **Amount off orders** in step 1 (no "Applies to"), so it can't leave out any line (rule 2a). The minimum purchase is checked twice: before product discounts it counts the selected purchase type **excluding** purchased gift cards; after product discounts it counts the cart subtotal **including** purchased gift cards. Gift cards used as payment don't count [hc-amount-off]. Shopify says most discounts can't apply to gift cards; the exception is a product discount whose product is a gift card [hc-discounts-faq].
- **Minimum for N1 (Amount off products):** only the selected products, or products in the selected collections, count toward its minimum purchase amount [hc-amount-off].

**N3. Buy X get Y** [hc-bxgy]
1. Discounts > **Create discount** > select **Buy X get Y**.
2. **Method**: **Automatic discount** (enter a **Title**) or **Discount code** (enter the code).
3. **Customer buys**: **Minimum quantity of items** or **Minimum purchase amount** → the threshold → **Any items from**: **Specific products** or **Specific collections** → add them.
4. **Customer gets**: quantity → **Any items from** → add the products or collections.
5. **At a discounted value**: **Percentage**, **Amount off each** or **Free**. Tick **Set the maximum number of uses per order** and enter the number if the Script capped it.
6. **Eligibility** (all customers / specific customers / customer segments / markets).
7. Codes only: **Maximum discount uses** if the Script limited uses.
8. **Combinations** (see N5). Leave the Point of Sale option off unless the merchant wants it on POS.
9. **Active dates** > **Save**.
The "get" item is **never added to the cart automatically**. For automatic discounts where the same products are in both "Customer buys" and "Customer gets", "the lower-priced item that the customer chooses" is the one discounted [hc-bxgy].

**N4. Free shipping** [hc-free-shipping]
Discounts > Create discount > **Free shipping** > Method > countries (all or selected) > optionally **Exclude shipping rates over a certain amount** > minimum requirement > Eligibility > Combinations > Active dates > **Save**. Free shipping only (100%); there is no native partial shipping discount.

**N5. Fix combinations** [hc-combinations]
For each discount involved: Discounts > click the discount > **Combinations** > tick the classes (product / order / shipping) it should combine with > **Save**. **Both** discounts must allow the combination. Limits: 25 active automatic discounts (including app discounts); 5 product/order codes + 1 shipping code per order; same-line product + product stacking needs Plus.

**N6. Automated ("smart") collection (to target by tag, vendor, type, compare-at price)** [hc-auto-collections] [hc-smart-collections]
Products > **Collections** > create a collection that picks products by **conditions** (Shopify calls it a smart or automated collection) > add conditions, for example **Tag** **includes** X; **Tag** **does not include** X; **Vendor** **is equal to** X / **is not equal to** X; **Type** **is equal to** X / **is not equal to** X; **Compare at price** **is not set** > choose **Match all conditions** or **Match any condition** > **Save**. Up to 60 conditions. Not available on the Starter plan.
- **To leave products out** (the Script's exclusions): use **Tag does not include**, or **is not equal to** on Type or Vendor, with **Match all conditions**. Shopify says only the category, tag, type and vendor conditions can exclude products [hc-auto-collections]. To leave out a gift card, add a condition on its product type, vendor or a tag that only the gift card has (read it from the gift card's product page); if none exists, the exclusion is **Unverified** → rule 2a.
- The condition names and operators are verified (re-checked 2026-11-04); the button names for creating the collection are **Unverified**, and Shopify says a **new collections model** is replacing manual/smart collections — follow the live labels.

**N7. Customer segment (for tag / order count / spend / marketing rules)** [hc-segments]
Customers > **Segments** > **Create segment** > click in the query editor > in the **WHERE** dialog choose a filter, then an operator, then a value (pick from the list — don't type syntax) > **Run query** to check who matches > **Save**. Then use it in a discount's **Eligibility > Customer segments**.

**N8. Shipping rate with conditions** [hc-shipping-zones]
Settings > Shipping and delivery > **Shipping profiles** > click the profile > in **Shipping zones**, **Add shipping option** for the zone > **Name** (shown at checkout) > **Rate type**: **Order amount** or **Weight** > **Minimum** / **Maximum** per range > **Price** (0 = free) > optional **Offer free shipping** with a minimum order amount > **Done** > **Save**. (Rate types are **Flat**, **Order amount**, **Weight** and **Carrier or app calculated**. Flat rates have no conditions. Carrier or app calculated rates use **Choose carrier and apps** and an optional handling fee; the optional **Offer free shipping** minimum appears for rates too. A country must also be in an active market before shoppers there can order.)

**N9. Rename a rate / free over an amount** [hc-shipping-zones]
Same profile > **Horizontal menu** (…) next to the option > **Edit shipping option** > change **Name**, or tick **Offer free shipping** and enter the minimum > **Done** > **Save**.
Market-driven shipping stores: rates live under Markets and these steps may differ — follow the live labels [hc-shipping-rates] [dev-market-shipping].

**N15. Separate zone for some countries (so a rate can have its own name or price there)** [hc-shipping-zones]
1. Settings > Shipping and delivery > **Shipping profiles** > click the profile.
2. Next to the zone that holds the country now: **Horizontal menu** (…) > **Edit zone** > in **Regions**, clear the country > **Done** > **Save**. Shopify requires removing a country from one zone before adding it to another.
3. In **Shipping zones**, click **Add zone** > **Zone name** > in **Regions**, select the country > **Done** > **Save**.
4. For the new zone, **Add shipping option** for every rate the country should still have (N8), with the new name where needed.
Do steps 2 to 4 in one sitting: between steps 2 and 4 that country has no rates. The country must stay in an active market. Clearing a country in step 2 is the inverse of the documented selection step; follow the live labels.

**N10. Separate shipping profile for some products** [hc-shipping-rates] [hc-combined-shipping-rates]
Settings > Shipping and delivery > Shipping profiles > create a new custom profile > add the products > add zones and only the allowed rates > **Save**. (Exact button labels **Unverified**; follow the live labels. Up to 99 custom profiles.) When one cart has products from several profiles, Shopify **combines** the rates: rates with the **same name** are added together; if names differ, the cheapest option from each profile is added together and shown as one rate named **"Shipping"**. Weight-based, carrier-calculated and app rates are combined too [hc-combined-shipping-rates].

**N11. Custom manual payment method** [hc-manual-payments]
Settings > Payments > in the **Manual payment methods** section, select **Create custom payment method** > **Custom payment method name** > optional **Additional details** (shown at checkout) and **Payment instructions** (shown on the order confirmation) > **Activate**. Reserved names that can't be used include "Cash on Delivery (COD)", "Bank Deposit", "Cash", "Money Order", "Gift Card" and "Store Credit". The Help Center describes **no** country, order total, product or customer conditions for manual methods (so any such rule needs a Payment Customization). US stores whose sales tax is managed by Shopify can't use manual payments until US sales tax is set to self-directed.

**N12. B2B volume pricing / quantity rules** [hc-b2b-quantity-pricing]
**Markets > Catalogs** > open the catalog > **Products and pricing** section > **Manage** > **Manage products and pricing** > hover over the product (or click the variant link) > in the **Volume pricing** column click **+ Add** (quantity rules: the **Quantity rules** column) > **Save**. Up to 10 price breaks per product, applied to each variant. Customers must be set up as **companies** (Customers > Companies). (That Help Center page also shows the stale "August 28, 2025" Scripts date — never repeat it.)

**N13. Add-to-cart limit** [hc-add-to-cart-limit]
Settings > Checkout > **Advanced preferences** > **Add-to-cart limit** (per-variant cart cap; anti-bot tool). Plan availability Unverified.

**N14. Turning on what a developer built** (for the PM, after the developer delivers) [hc-checkout-customization] [hc-discounts-with-apps]
- Delivery: Settings > Shipping and delivery > **Delivery customizations** > **Add delivery customization** > **Add customization** > choose it > configure > **Save** > select it > **Activate**.
- Payment: Settings > Payments > **Payment customizations** > **Manage** > **Add customization** > configure > **Save** > **Activate**.
- Checkout rule (validation): Settings > Checkout > **Checkout rules** > **Add rule** > choose > **Save** > **Turn on**.
- App discount (Discount Function): Discounts > **Create discount** > in the **Select discount type** dialog, choose the discount type from the app > configure > **Save** [hc-discounts-with-apps]. (Some apps make you create the discount inside the app instead; the developer says which.)

---

## 3. Patterns

Format per pattern: **Native** (main PM fix, if any) · **Developer** (Function API → target → operation, key inputs) · **Optional Shopify-built** · **Fidelity** · **Gaps / watch-outs**.

### Line item patterns

**L1. % or $ off products by tag / vendor / type / collection / IDs**
- Native: N6 (automated collection for the tag/vendor/type, or use existing collections / specific products) → N1 with Applies to = that collection → N5.
- Developer: Discount Function API → `cart.lines.discounts.generate.run` → `productDiscountsAdd` (percentage or fixedAmount with `appliesToEachItem`). Inputs: line `merchandise.product` `hasAnyTag` / `vendor` / `productType` / `inAnyCollection` (tag and collection checks cost 3 each of the 30-point query budget) [dev-discount-api] [dev-function-apis].
- Fidelity: Close, if every product the Script left out can be left out with an N6 condition (rule 2a).
- Gaps: shows as a labelled discount, not a lower line price (W2); same-line stacking with another product discount needs Plus (W1).

**L2. Store-wide or scheduled sale** — Native: N1 or N2 automatic with **Active dates**. Fidelity: Close; if the Script left products out, N2 is Partial (rule 2a) and N1 with an N6 collection keeps the exclusions. Gaps: product/collection pages never showed Script prices either; showing sale prices before the cart needs theme work.

**L3. Tiered spend (spend X → Y off)**
- Native A (the Script discounted the whole cart and left nothing out): one N2 automatic discount per tier with **Minimum purchase amount**; do **not** let these tiers combine with each other (order + order off) — when discounts can't combine, the best one for the cart applies [hc-combinations]. Each tier uses one of the 25 automatic slots. Fidelity: Close.
- Native B (the Script left products or gift cards out, for example MAP brands tagged `no-discount`): N6 collection that leaves them out (**Tag does not include** …, plus a condition for the gift card) → one **N1** automatic discount per tier, **Applies to** = that collection, **Minimum purchase amount** = the tier, tiers not combinable with each other. Only products in the collection count toward an N1 minimum [hc-amount-off], so the threshold matches the Script's "eligible items" spend. When it goes live, end any older order-level tier discount (its **Active dates**), or the bigger one keeps winning and still discounts the excluded products. Fidelity: Close only if every exclusion became a confirmed N6 condition; otherwise Partial (rule 2a).
- Native A on a Script that left products out is **Partial for this store** (rule 2a): it discounts the excluded products and counts them toward the minimum. If Native B is Close, B is the main fix. If B is Partial too, on Plus the developer spec is the main fix, and B (or A, if B can't be built) is the interim F#.
- Developer: Discount Function → `cart.lines.discounts.generate.run` → `orderDiscountsAdd` with one candidate per tier, `conditions` `orderMinimumSubtotal`, selection strategy `MAXIMUM`; or `productDiscountsAdd` on the eligible lines when the Script left lines out [dev-discount-api]. Tier table and excluded tags in a discount metafield (JSON) so the merchant can edit them.
- Optional Shopify-built: Checkout Blocks order discounts (Plus) — "most recently created" passing discount applies, so tiers need care [hc-cb-order-discount].
- Gaps: Script "spread across items" vs a native order-level discount line (A) or per-line product discounts (B); the N2 minimum counts gift cards after product discounts (see N2).

**L4. Quantity / volume breaks**
- Native (DTC): one N1 per break with **Minimum quantity of items**, not combinable with each other. **Gap:** native minimum quantity counts all eligible items across products, not per line.
- Native (B2B): N12 volume pricing — changes the unit price (closest to `change_line_price`), but needs companies.
- Developer: Discount Function → `productDiscountsAdd` with `conditions` `cartLineMinimumQuantity`, or per-line logic; tiers in a metafield [dev-discount-api].
- Fidelity: Close (DTC) / Exact for B2B volume pricing.

**L5. BOGO / Buy X get Y / cheapest free**
- Native: N3.
- Developer: Discount Function with `prerequisites` (added 2026-04) and line targets with a `quantity` to discount exactly N units [dev-discount-api] [dev-cl-2026-04].
- Fidelity: Close. Gaps: "get" item never auto-added; for **automatic** BXGY with overlapping buy/get sets the **lower-priced** item is discounted [hc-bxgy] — so a Script that made the cheapest unit free matches, but a Script that discounted the **most expensive** unit (high-to-low sort) needs the Function; for BXGY **codes** the overlap rule is **Unverified**; on non-Plus, BXGY items can't take further product discounts.

**L6. Bundle / fixed price for a set / "2 for $20"**
- Native: none exact (N1 with minimum quantity gives a % or $ off, not a set price).
- Developer: Cart Transform → `cart.transform.run` → `linesMerge` (components → one bundle line with a price adjustment) or `lineExpand` [dev-cart-transform]. One cart transform per app; rejected if a selling plan is present.
- Optional Shopify-built: **Shopify Bundles** (all plans; fixed bundles and multipacks) [hc-bundles].
- Fidelity: Close (shopper sees a bundle line). Gaps: bundles can't be sold with selling plans.

**L7. Customer-tag (VIP) discount**
- Native: N7 segment on the customer tag → N1/N2 with Eligibility = **Customer segments**.
- Developer: Discount Function with `buyerIdentity.customer.hasAnyTag` (max 100 tags per list) [dev-discount-api] [dev-function-apis].
- Fidelity: Close; Partial for this store if the Script left out customers (another tag) or products the native fix would still discount (rule 2a). Gaps: shopper must be logged in/identified (same as Scripts); whether a guest typing a tagged customer's email gets it is **Unverified**; shown as a discount, not a lower price.

**L8. Member price shown as a lower unit price (no visible discount)**
- Native: none for DTC.
- Developer (Plus only): Cart Transform → `lineUpdate` with a fixed price per unit (optionally a title) [dev-cart-transform]. Not with selling plans; can't target lines also expanded/merged; 20 kB output limit means it can't reprice every line of a big cart [dev-function-apis].
- Fidelity: Close on Plus; otherwise fall back to L7 (Partial). Gaps: how `lineUpdate` prices show in discount reports is **Unverified**.

**L9. Wholesale pricing by tag** — Native: B2B companies + catalog (N12) with % adjustment or fixed prices, quantity rules, volume pricing. Fidelity: Close, but customers must be **moved from tags to companies** (process change). If refused → L7 or L8.

**L10. First-order discount**
- Native: N7 segment "number of orders = 0" (pick in the editor) → N1/N2 with that segment; for a code, also tick **Maximum discount uses > Limit to one per customer** [hc-amount-off] [dev-segment-ql].
- Developer: Discount Function using customer `numberOfOrders` [dev-discount-api].
- Fidelity: Close. Gaps: guests aren't identified as customers — if the Script **included guests** (`customer.nil? ||`), native segment eligibility excludes them; a first-order **code** with "limit to one use per customer" is the closest.

**L11. Free gift with purchase**
- Native: N3 with Customer buys = minimum purchase amount, Customer gets = gift, value **Free**, max 1 use per order.
- Developer: Discount Function (gift line 100% off when the threshold is met); auto-adding the gift needs theme code or Cart Transform `lineExpand` [dev-cart-transform].
- Fidelity: Close. Gaps: gift never auto-added natively; a theme or app that still auto-adds the gift may now add it **at full price** if no discount replaced the Script — check in the test.

**L12. Reject discount codes ("no codes on sale items" / "no codes during promo")**
- Native: set Combinations so codes don't combine with the sale discount (best discount wins). No custom message — checkout shows Shopify's own text, "Some discount codes couldn't be used together. We applied the best combination" [hc-discounts-faq] [hc-combinations]. The missing custom message alone isn't a fidelity loss (`status-verification.md` section 1); a code worth more than the sale now wins where the Script refused it, which is. Check every active **and planned** code (Step 3) against the sale.
- Developer: Discount Function **backed by an automatic discount**, reading entered codes and returning `enteredDiscountCodesReject` with a message; only codes marked rejectable can be rejected [dev-discount-api] [dev-discount-rejections].
- Fidelity: Close with Function / Partial with native.

**L13. Stacking control** — Scripts **always applied regardless of combination settings** [hc-combinations]. Native: N5 on every discount involved. Fidelity: Partial (can't bypass combination rules; same-line product stacking needs Plus). Always raise W1.

**L14. Once per order / max N units** — Native: N1 "Only apply discount once per order" (fixed amount) or N3 max uses per order. Developer: line target `quantity` [dev-discount-api]. Fidelity: Close.

**L15. Line item property or cart attribute logic** — Native: none. Developer: Discount Function reading line `attribute(key)` or `cart.attribute(key)` [dev-discount-api]. Fidelity: Exact.

**L16. Line splitting (`split(take:)`)** — Native: none. Developer: Discount Function discounting part of a line's quantity. Fidelity: Partial — money matches, but the shopper sees one line with a partial discount, not two lines. Cart Transform cannot split a line into two of the same variant [dev-cart-transform]. Record as a gap.

**L17. Exclude sale (compare-at) items** — Native: N6 collection "Compare-at price is not set" used as N1's Applies to (product discounts only; native order discounts can't exclude lines, so N2 here is Partial by rule 2a). Developer: line `cost.compareAtAmountPerQuantity`; order discounts can exclude line IDs [dev-discount-api]. Fidelity: Close.

**L18. Country / market / currency promo** — Native: Eligibility = **Markets** (N1/N2); market catalogs for price differences [hc-price-adjustments]. Developer: `localization.market`, delivery address country [dev-discount-api]. Fidelity: Close (market ≠ shipping address). Scripts were unreliable in other currencies, so the replacement may be more accurate.

**L19. Subscription-only / one-time-only pricing** — Native: Purchase type in N1/N2. Developer: line `sellingPlanAllocation`. Fidelity: Partial — see W4.

**L20. Lifetime spend / order count / accepts marketing** — Native: N7 segment (amount spent, number of orders, email subscription status — pick in the editor) → Eligibility. Developer: `amountSpent`, `numberOfOrders` (no accepts-marketing input found — Unverified absence). Fidelity: Close.

**L21. Many tiers/conditions in one Script** — Native only if it fits under 25 automatic discounts and the combination rules work out. Otherwise Developer: one Discount Function with its configuration in a discount metafield (JSON) or app-owned metaobject; watch the 30-point query cost and 11M instruction limit [dev-function-apis]. Fidelity: Close.

**L22. Quantity limits / anti-reseller (Scripts silently removed excess units)** — Native: N13 add-to-cart limit (per variant). Developer: Cart and Checkout Validation → `cart.validations.generate.run` → validation errors (blocks checkout with a message, including express checkouts; does **not** remove items) [dev-validation]. Optional Shopify-built: Checkout Blocks order value limits (Plus). Fidelity: Close (blocks instead of silently removing).

**L23. Surcharge / add-on fee** — Scripts couldn't raise prices, so this is never a migration item. If requested: Cart Transform `lineExpand` with a priced add-on component [dev-cart-transform].

**L24. Remove or block items for some destinations** (Scripts deleted lines silently) — Native: N10 profile for those products without the restricted zones, so checkout can't offer delivery there (shopper sees that the items can't ship — **Likely**; confirm in the test). Developer: Validation function blocking checkout with a clear message for those destinations [dev-validation]. Fidelity: Close (blocks with a message instead of silent removal).

### Shipping patterns

**S1. Hide/show rates by country / province / ZIP** — Native: N8 — put the rate only in the zones where it should show (ZIP-level zones aren't native). Developer: Delivery Customization → `cart.delivery-options.transform.run` → `deliveryOptionHide`, using delivery address country/province/zip [dev-delivery-customization]. Optional Shopify-built: Checkout Blocks Hide with country/state/zip rules (Plus) [hc-cb-delivery]. Fidelity: Exact (ZIP rules need the Function).

**S2. Hide rates for PO Box / military** — Native: none. Developer: prefer **Validation** (block the PO Box address with a message; Shopify's Validation API page has a "Prevent shipping to PO boxes" example reading `deliveryGroups.deliveryAddress.address1`) [dev-validation]. If the Script hid only **some** rates, the validation must also read the shopper's chosen rate: the validation input has `cart.deliveryGroups.selectedDeliveryOption` with `title` and `handle` [dev-validation], so it can block only those rates (for example names starting "Express" or "Overnight") and let the others through. Turned on at Settings > Checkout > **Checkout rules** (N14). Hiding rates for PO Boxes with a Delivery Customization is supported only for carrier-service or shipping-app rates; with Shopify's built-in rates the address data needed may not reach the function [dev-delivery-customization]. Optional Shopify-built: Checkout Blocks "Shipping address type" hide rule or address format validation (Plus) [hc-cb-delivery] [hc-cb-address-validation]. Fidelity: Close (validation stops checkout instead of hiding some rates).

**S3. Hide/show rates by cart total** — Native: N8 Rate type **Order amount** with min/max (merchant-created rates). Developer: Delivery Customization using cart subtotal. Fidelity: Exact for merchant rates; carrier-calculated rates have no min/max → Function.

**S4. Hide rates by product type / tag / collection** — Native: N10 separate profile with only the allowed rates. Developer: Delivery Customization reading line products. Fidelity: Close. Gaps: mixed carts across profiles get **combined** rates (same-name rates added together; different names → cheapest of each added and shown as "Shipping") [hc-combined-shipping-rates], whereas the Script only hid rates.

**S5. Hide rates by weight** — Native: N8 Rate type **Weight**. Fidelity: Exact.

**S6. Hide/show rates by customer tag or B2B** — Native: none for rates (free shipping for a tag → S9). Developer: Delivery Customization with customer `hasAnyTag` / purchasing company [dev-delivery-customization]. Optional Shopify-built: Checkout Blocks customer tag / B2B rules (Plus). Fidelity: Exact.

**S7. Rename rates** — Native: N9 for merchant-created rates; if the rename applied only to some countries that share a zone with others, first give those countries their own zone (N15), then name the rate there. Developer: `deliveryOptionRename`. Optional Shopify-built: Checkout Blocks Rename (Plus; **no conditions** — in Checkout Blocks only Hide supports rules, so a rename that applied only to some regions or carts needs the Function) [hc-cb-delivery]. Fidelity: Close. Gaps: for carrier rates the **carrier name is always shown first** and can't be removed [dev-delivery-customization].

**S8. Reorder rates** — Native: none. Developer: `deliveryOptionMove`. Optional Shopify-built: Checkout Blocks Reorder (Plus; no conditions) [hc-cb-delivery]. Fidelity: Partial — apps may not pre-select a more expensive option; the **cheapest must stay selected by default** [dev-delivery-customization].

**S9. Free shipping (tag / threshold / country)** — Native: N4 (countries, minimum, segment eligibility, exclude rates over an amount) or N8/N9 "Offer free shipping" over an amount. Fidelity: Exact/Close (the free-shipping minimum counts products at their discounted price [hc-free-shipping]); Partial for this store if the Script left out products, customers or countries the native fix would include (rule 2a).

**S10. Partial shipping discount (% / $ off / "Express for $5")** — Native: none (free shipping only). Developer: Discount Function → `cart.delivery-options.discounts.generate.run` → `deliveryDiscountsAdd` [dev-discount-api]. Optional Shopify-built: Checkout Blocks Amount off shipping (percentage / free / fixed / set fixed price; Plus) [hc-cb-shipping-discount]. Fidelity: Close (shows as a shipping discount instead of a cheaper rate). Code-triggered versions: the Function is backed by a discount code.

**S11. Discount only one specific rate** — Developer: target that delivery option's handle in `deliveryDiscountsAdd`. Optional Shopify-built: Checkout Blocks shipping discount by delivery option title/price/type. Fidelity: Close.

**S12. Hide local delivery / pickup** — Developer: Delivery Customization hiding individual options. Optional Shopify-built: Checkout Blocks can hide individual local delivery options or pickup locations, but not the whole method [hc-cb-delivery]. Fidelity: Partial.

**S13. Show only carrier-calculated rates (hide Shopify manual rates when carrier rates exist)** — Native: none (removing manual rates from zones also removes them when carriers fail). Developer: Delivery Customization hiding manual options when carrier options exist. A delivery option in the 2026-10 input has `handle`, `title`, `code`, `description`, `cost`, `deliveryMethodType` and (since 2026-10) `metafield` — there is **no `source` field** like Scripts had [dev-delivery-customization] [dev-cl-delivery-option-metafields]. So the function must tell carrier rates apart some other way (for example by the merchant's manual rate names, a known carrier `code` pattern, or a metafield the carrier service attaches) — **Unverified** which works; the developer must confirm on a development store. Fidelity: Close if a reliable signal exists; otherwise gap.

### Payment patterns
Common: Payment Customization → `cart.payment-methods.transform.run` → `paymentMethodHide` / `paymentMethodRename` / `paymentMethodMove`; max **25** active; runs in checkout only (not on the cart page, not on POS); activation N14 [dev-payment-customization]. Non-Plus US/CA: credit-card methods can't be customized [hc-checkout-customization]. Optional Shopify-built for P1–P7: Checkout Blocks payment Hide / Rename / Reorder (Plus). In Checkout Blocks only **Hide** supports conditional rules; Rename and Reorder apply to everyone [hc-cb-payment].

**P1. Hide COD/manual methods by cart total** — Native: none (manual methods have no conditions). Developer: hide by cart subtotal. Fidelity: Exact.
**P2. Hide gateways by country / province** — Developer: delivery address country/province, or market when no address yet. Fidelity: Close (address-based rules don't match until checkout has an address; Scripts ran after the address step).
**P3. Show/hide by customer tag or B2B** — Developer: customer `hasAnyTag` / purchasing company. Native for B2B: payment terms per company. Fidelity: Exact.
**P4. Hide by product / collection / vendor / gift card / subscription** — Developer: line product data, gift card flag, selling plan. Fidelity: Exact.
**P5. Hide express wallets** (Scripts couldn't) — Developer: `paymentMethodHide` (hiding a specific placement such as accelerated checkout is Plus only). Shopify warns this may lower conversion [hc-checkout-customization]. New capability, not a migration item.
**P6. Rename a gateway** — Native: name a custom manual method (N11). Developer: `paymentMethodRename`. Checkout Blocks documents that only methods **without a logo** can be renamed (it names PayPal and Klarna as logo methods) and that Shop Pay can't be renamed [hc-cb-payment]; whether the same limit applies to a custom Function is **Unverified** — the developer confirms on a development store. Fidelity: Close (Scripts also couldn't rename logo methods).
**P7. Reorder gateways / change the default** — Developer: `paymentMethodMove`. Fidelity: Partial (express wallets can be hidden but not reordered; Shop Pay supports only hiding gift cards, not renaming or reordering) [hc-cb-payment].
**P8. Payment terms / invoice / deposits** — Native: B2B net payment terms per company (deposits Plus only). Developer (Plus): `paymentTermsSet`; `orderReviewAdd` for B2B review [dev-payment-customization]. Fidelity: Close. Gaps: payment terms aren't supported in accelerated checkouts, and can't be set when the cart has subscription items [dev-payment-customization].
**P9. Gift card field** — Developer: Payment Customization hide/disable gift cards by cart contents or country. Fidelity: Exact.

---

## 4. Function API facts for developer specs (version 2026-10)

| API | Target(s) | Operations | Max active | Plus-only parts | Source |
|---|---|---|---|---|---|
| Discount | `cart.lines.discounts.generate.run`; `cart.delivery-options.discounts.generate.run` (+ `.fetch` variants, network access) | `productDiscountsAdd`, `orderDiscountsAdd`, `deliveryDiscountsAdd`, `enteredDiscountCodesReject`, `enteredDiscountCodesAccept` | 25 discount functions | fetch: see plan table | [dev-discount-api] |
| Cart Transform | `cart.transform.run` | `lineExpand`, `linesMerge`, `lineUpdate` | 1 per app per store | `lineUpdate`: Plus / dev stores | [dev-cart-transform] |
| Delivery Customization | `cart.delivery-options.transform.run` | `deliveryOptionHide`, `deliveryOptionMove`, `deliveryOptionRename` | 25 | — | [dev-delivery-customization] |
| Payment Customization | `cart.payment-methods.transform.run` | `paymentMethodHide`, `paymentMethodMove`, `paymentMethodRename`, `paymentTermsSet`, `orderReviewAdd` | 25 | placements, `paymentTermsSet`, `orderReviewAdd` (B2B) | [dev-payment-customization] |
| Cart and Checkout Validation | `cart.validations.generate.run` (+ `.fetch`) | `validationAdd` (errors on checkout fields or the cart; shown in checkout and on the cart template) | 25 | fetch: Enterprise | [dev-validation] |

- **Execution order in checkout:** Cart Transform → Discount (cart lines) → Fulfillment constraints / order routing → delivery options → Delivery Customization → Discount (delivery) → Payment Customization → Validation. Discount functions run concurrently and don't know about each other; functions after discounts can read discount details (2026-04) [dev-function-apis] [dev-cl-enhanced-discounts].
- **Resource limits:** 11 million instructions (carts up to 200 lines); input 128 kB; output 20 kB; binary 256 kB; input query 3,000 bytes and max cost 30; metafield values over 10,000 bytes not returned; list arguments up to 100 items [dev-function-apis].
- **Input query cost (for the spec's estimate):** any field returning a metafield = 3; `hasAnyTag` / `hasTags` / `inAnyCollection` / `inCollections` = 3 each; `metaobject(...)` root = 1 and each `field(key:)` on it = 3; `__typename` and fields inside a metafield / tag / collection result = 0; **every other leaf field = 1** (for example `id`, `quantity`, `sku`). Each selected field counts once however many lines the cart has [dev-function-apis].
- **Surfaces (Discount Functions):** supported on B2B, Cart, Checkout, POS, Shopify Admin, Storefront, accelerated checkout; partially on draft orders, order edit (checkout) and subscriptions; not on Create Order API, admin order edit, pre-order/try-before-you-buy [dev-discount-api].
- **Code rejection** works only when the function is backed by an **automatic** discount and the code is rejectable [dev-discount-api].
- **Useful inputs Scripts lacked:** cart attributes, metafields and app-owned metaobjects (configuration), `shop.localTime` (time-of-day rules), market, customer `createdAt` [dev-discount-api] [dev-cl-2026-04] [dev-cl-2026-10].
- **Build and ownership:** custom app created in the **Dev Dashboard**; works only on Plus [hc-transition] [dev-function-apis].

---

## 5. Cannot be reproduced exactly (use for gap entries)

| # | Old behaviour | Closest option | Source |
|---|---|---|---|
| G1 | Discounts stacking regardless of combination settings | Set combinations on every discount (N5); same-line product stacking on Plus | [hc-combinations] |
| G2 | Splitting a line into two lines at different prices | Partial-quantity discount on one line (Function) | [dev-cart-transform] [dev-discount-api] |
| G3 | Lower unit price with no discount line, on non-Plus | Labelled discount (L1) | [dev-cart-transform] |
| G4 | Repricing every line of a large cart via Cart Transform | Discount Function or B2B catalog | [dev-function-apis] |
| G5 | Pre-selecting a more expensive shipping option | Reorder only; cheapest stays default | [dev-delivery-customization] |
| G6 | Removing the carrier name from a renamed carrier rate | Rename the rest of the label | [dev-delivery-customization] |
| G7 | Renaming logo payment methods, reordering wallets, customizing Shop Pay beyond the gift-card field | Reorder/rename non-logo methods | [hc-cb-payment] [dev-payment-customization] |
| G8 | Hiding a whole local delivery or pickup method (Checkout Blocks) | Hide individual options/locations | [hc-cb-delivery] |
| G9 | Reading "accepts marketing" or card brands in a Function (absence Unverified) | Segment on email subscription status | [dev-segment-ql] |
| G10 | Network calls from Functions on normal Plus stores | Store configuration in metafields | [dev-function-apis] |
| G11 | Auto-adding a free gift natively | BXGY "Free" + theme auto-add, or Cart Transform `lineExpand` | [hc-bxgy] [dev-cart-transform] |
| G12 | Restricting a custom Function to the Online Store only | Accept POS/draft-order behaviour, or add conditions the developer can detect (Unverified whether app discounts honour sales-channel settings) | [dev-discount-api] |
| G13 | Discounted prices on product/collection pages without theme work | Theme change (Scripts never did this either) | [hc-discounts-faq] |
| G14 | Any Function or Checkout Blocks fix on a store no longer on Plus | Native settings and Shopify Bundles only | [dev-function-apis] [hc-checkout-blocks] |
| G15 | Silently removing cart items | Validation message that blocks checkout | [dev-validation] |
| G16 | A custom rejection message with native settings only | Shopify's standard combination message | [hc-discounts-faq] |

---

## 6. Store-wide warnings (add every one that applies to the "Store-wide warnings" section)

- **W1 Combinations.** Script discounts always stacked; native and Function discounts only stack when **both** sides allow it, and when they can't combine the best one wins. Applies when any line item or shipping Script discounted anything. Name every active code and every **planned** code or sale from Step 3 (with its dates), and say what happens with today's settings: stacks, doesn't stack, or wins over a replacement discount. If a planned code's combinations aren't decided, say who must decide and by when (before its start date). PM action: review Combinations on every active code and automatic discount (N5), and set them on each planned code before it goes live. [hc-combinations]
- **W2 Theme cart display.** The Liquid fields `line_item.price`, `line_item.line_price` and `line_item.total_discount` are deprecated: they included Shopify Script discounts but **not** automatic discounts or discount codes. Themes built for Scripts may therefore show full prices in the cart even when a new discount applies. Developer check: replace them with `final_price`, `final_line_price` and `line_level_total_discount`, and `line_item.discounts` with `discount_allocations`; also show cart-level discount applications. `line_item.message` still exists (it shows the discount title, or a count when several apply); `line_item.error_message` is a separate field. Applies when any line item Script existed. [dev-liquid-line-item] [hc-script-liquid]
- **W3 New surfaces.** Scripts never ran on POS or draft orders. Discount Functions run on POS, B2B, accelerated checkout and partially on draft orders; native discounts have an "Also offer on Point of Sale" option. Decide per discount where it should apply. [dev-discount-api] [hc-amount-off]
- **W4 Subscriptions.** Discount Functions don't re-run on recurring orders, and a shipping discount on the first order becomes 100% off shipping on recurring orders; Cart Transform operations are rejected when a selling plan is present. Applies if the store sells subscriptions. [dev-discount-api] [dev-cart-transform]
- **W5 Reporting break.** Past orders store Script discounts as Script discount applications (titled with the Script message); new discounts appear under their own names, so discount reports won't line up across June 30, 2026. [dev-script-discount-application]
- **W6 Capacity.** Max 25 active automatic discounts (including app discounts) and 25 active functions per Function type; count what is live before adding more. [hc-combinations] [dev-discount-api]
- **W7 Plan.** Custom Functions and most Checkout Blocks features need Plus; re-check if the merchant plans to change plan. [dev-function-apis] [hc-checkout-blocks]
- **W8 Order edits.** Discount Functions aren't re-run when an order is edited in checkout. [dev-discount-api]
- **W9 US/Canada credit cards.** On non-Plus stores in the US and Canada, payment customizations only apply to non-credit-card methods. [hc-checkout-customization]
