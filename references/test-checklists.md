# Test-checkout checklists (Step 11)

The PM (not Claude) runs these on the live store, **now** (to confirm today's status) and **again after each fix**. Claude never adds to cart or checks out. Write every test in plain English with concrete products, amounts, addresses and expected results taken from the rule cards and the products the PM named in Step 11 — no placeholders left in the final report. If the PM named no products, describe them by type and price ("any regular product around USD 60 not tagged `no-discount`").

Use the Step 3 answers: if a development store exists, say "run these on the development store first, then on the live store after the fix"; name the test customer accounts the PM listed; and if the merchant set times when testing is allowed, repeat them in the rules box. If no test account exists, add a PM check asking the person who signs off to have one created.

---

## 1. Rules for the PM (copy this box into the report once)

> **Before you test**
> - Use a computer browser. For "guest" tests use a private/incognito window so you're not logged in.
> - For "logged-in" tests use a **test customer account** the agency or merchant controls that has the tag the test needs. Don't use a real customer's account. (If no test account exists, ask the merchant to set one up — that is a store change the merchant makes, not part of this audit; Claude doesn't create accounts.) If there's no test account, mark logged-in tests "Not run — no test account".
> - If a test shows something you didn't expect, write down what you saw and move on to the next test. Don't try to fix anything in the admin.
> - Go as far as the **payment step** and look. **Never click "Pay now" / "Complete order"**, and never place an order — everything these tests check is visible before paying. When you're done, close the tab. Use your own or the test account's email at checkout: the store may send an abandoned-checkout email to whatever address you enter.
> - For code tests, use codes the merchant has approved for testing. If a code has a usage limit, ask the merchant first.
> - Use a real-format address in the right country/region. For PO Box tests, put "PO Box 123" in the address line.
> - For each test, note what you see: items and prices, discount lines and amounts, shipping options (names, prices, order, which one is pre-selected), payment methods shown, and any message. A screenshot of the order summary is ideal.
> - Tick Pass, Fail or Not run (rule below) and write what was different.

---

## 2. Test card format (use exactly this in the report)

```
T{n}. {short name} — checks {S#.R#}{, S#.R#}
Set-up: {guest | logged in as a test customer tagged "…"} · address: {…} · products: {…}
Steps:
 1. …
 2. …
Expected today: {what should happen if the rule is REPLACED, or what happens because it is LOST}
Expected after the fix: {what should happen once the fix is in place}
Where to look: {cart page | checkout order summary | shipping step | payment step}
Result: [ ] Pass  [ ] Fail  [ ] Not run   Notes: ______
```

**Pass / Fail rule (print it once under the rules box):** Pass = what you see matches the expected result exactly: same amounts (to the cent), same names, same order, same shown/hidden options. Anything different = Fail, and write what you saw. A step you couldn't do (no test account, product sold out) = Not run, with the reason.

For a LOST rule, "Expected today" describes the lost behaviour plainly (e.g. "Full price — no 15% line"), so the PM can confirm the loss. For REPLACED rules, "Expected today" and "after the fix" are the same.

---

## 3. Templates by pattern (fill every {…} from the rule card)

**Discounts on products or orders (L1, L2, L7, L17, L18, L20)**
1. Add {qualifying product} and {a non-qualifying product} to the cart.
2. Cart page: {qualifying product} shows {X% / $X} off with the label "{title}"; {non-qualifying product} shows no discount.
3. Go to checkout: same discount in the order summary.
4. For customer rules (L7/L20): repeat as a **guest** (expected: no discount) and as a **tagged test customer** (expected: discount).
5. For sale exclusions (L17): add a product with a compare-at price (expected: no extra discount).
6. For market rules (L18): repeat with the other country/currency selected (expected: {…}).

**Tiers by spend (L3)**
1. Build a cart just **under** {threshold 1} → no discount.
2. Add an item to go **over** {threshold 1} → {discount 1}.
3. Go over {threshold 2} → {discount 2} only (tiers don't add up).

**Quantity breaks (L4, L9)**
1. Add {product} × {qty just below break} → no discount.
2. Change to {qty at break} → {discount / unit price}.
3. Mix two different qualifying products to reach the break → expected {counts together natively / per line in the Script} (this is where native and Script differ — note it).

**Buy X get Y / BOGO / gifts (L5, L11, L14)**
1. Add {X items}. Then add {Y item} yourself (natively it is **never added automatically**).
2. Expected: {Y} is {free / X% off}; only {N} unit(s) discounted.
3. Gifts: reach {threshold}; if the theme auto-adds the gift, check its price is 0.00 (if it shows full price, that's a fail — the gift is being charged).
4. If the Script picked the cheapest (or most expensive) unit, add two Y items of different prices and note which one is discounted. Expected with a native **automatic** Buy X get Y: the lower-priced one. Expected with a developer-built Function: whichever the spec says.

**Bundles / set prices (L6)** — Add all bundle components (or the bundle product) → expected total {price}; check the line(s) shown.

**First order (L10)** — Guest with a new email → expected {…} (natively, segment-based discounts don't apply to guests; a first-order code does). Logged-in test customer with past orders → no discount.

**Code rejection and stacking (L12, L13)**
1. Add {sale item}; enter code {code}.
2. Expected: {code rejected with message "…" | only the best discount applies (Shopify's standard message) | both apply}.
3. Remove the sale item; enter the code again → code applies.

**Quantity limits / blocked items (L22, L24)** — Add {product} × {limit + 1} (or ship to {restricted region}) → expected {message and checkout blocked | quantity capped | item can't ship}. The old Script silently removed items; the new behaviour shows a message — that is intended.

**Shipping: hide / show / rename / reorder (S1–S8, S12, S13)**
1. Cart with {products}; at checkout enter {address in the affected region}.
2. Shipping step: expected options **exactly** {list with names and prices, in order}; pre-selected option: {cheapest}.
3. Repeat with {address outside the region} → {list}.
4. PO Box (S2): address line "PO Box 123" → expected {rate hidden | message asking for a street address}.
5. Customer-tag rules (S6): repeat as guest and as tagged test customer.

**Shipping discounts and free shipping (S9–S11)**
1. Cart just under {threshold} → {rate} costs {price}.
2. Over {threshold} → {rate} shows {free / discounted price}; other rates {unchanged}.
3. Tagged/code versions: repeat with the tag or code.

**Payment (P1–P9)**
1. Cart {under / over} {amount}, address {…}, {guest / tagged}.
2. Payment step: expected methods **exactly** {list, in order, with names}; {method} {shown / hidden}.
3. Note: express buttons (Shop Pay, Apple Pay, PayPal) appear before checkout and were never affected by payment Scripts.

---

## 4. Store-wide tests (add those whose warning applies)

- **TW1 Stacking (W1):** add a product covered by an automatic discount, then enter {a current active code}. Expected: {both apply | only the best applies}, as the merchant wants. Note what you see. For each planned code from Step 3: once the merchant has created it, open it and read its **Combinations** (look only), then run this test on its first day, as early as possible.
- **TW2 Cart display (W2):** with any discount applying, check the **cart page** (not only checkout) shows the discounted line price/total. If the cart shows full price but checkout shows the discount, the theme needs the developer fix.
- **TW3 Express checkout (optional, careful):** express buttons can pay in one step. Only do this test if you're **not** signed in to Shop Pay in that browser and you are **not** using a device where Apple Pay / Google Pay can pay with a fingerprint, face or double-click. From a cart with a discount, click the Shop Pay button and look at the order summary it shows, then close that window without confirming anything. If you're not sure, skip this test and write "Skipped". Expected: same discounts, shipping options and prices as normal checkout.
- **TW4 Point of Sale / draft orders (W3):** ask the merchant's POS staff whether migrated discounts now appear on in-store sales, and whether that's wanted. (Don't create draft orders or POS sales yourself for this audit.)
- **TW5 Subscriptions (W4):** on a product with a subscription option, choose the subscription and check the first-order discount at checkout. Recurring-order behaviour can't be seen in a test checkout; it's covered in the developer notes.
