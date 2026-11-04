# Status verification: LOST / REPLACED / PARTIAL (Step 8)

You decide, for every rule card from Step 7, what shoppers get **today** compared with what the Script did before June 30, 2026. Evidence comes only from read-only admin pages (browser mode, `intake-browser.md` section 7) or the PM's screenshots/files (manual mode, step M6). Never infer a replacement from memory or from what "most stores do".

---

## 1. Status definitions (exact)

| Status | Use when | Typical confidence |
|---|---|---|
| **REPLACED** | An **active** replacement exists and matches the rule on every *material* dimension (section 3). | Confirmed if every dimension was seen; Likely if the replacement's logic isn't visible (e.g. an app/Function discount showing only a title and app badge). |
| **PARTIAL** | An **active** replacement exists but at least one material dimension differs, **or** it covers only some of the rule's tiers/conditions, **or** its app shows "Errors on [n] area". | Confirmed / Likely |
| **LOST** | No replacement exists, **or** the only candidates are draft, scheduled for the future, expired, turned off, inactive (Functions page **Inactive** tab), not activated in Delivery/Payment customizations or Checkout rules, or part of a **Rollout** that hasn't started. | Confirmed if you checked every place in section 2 for that rule type; Likely if one place couldn't be read. |
| **NOT APPLICABLE (never ran)** | The rule did nothing before June 30 (evidence per `script-reading-guide.md` section 7). | Confirmed / Likely |

If "Was live before June 30" is **Unknown**, treat the rule as live (conservative) and say so.

**Material** = changes what a shopper pays, who qualifies, which shipping/payment options they can choose, or the merchant's margin (stacking). **Non-material** = wording of a label or message, or showing a discount line instead of a lower price — record these as notes and as test items, not as PARTIAL.

**Shopper messages (decided once, used everywhere in this skill):** a missing or different custom message is, **on its own**, a noted difference, never PARTIAL. Two exceptions make it material: (1) the message told shoppers a condition or price detail they need to decide, for example "duties may be collected on delivery" or "invoices are due 30 days after shipment"; (2) the rule's effect **is** the new name (rename rules S7 and P6), so the name is the behaviour. Judge everything else on the money, eligibility and options above.

---

## 2. Where to look, by rule type (check every listed place before calling something LOST)

| Rule type (pattern IDs) | Places to check | Replacement looks like |
|---|---|---|
| Product / order discounts, tiers, BXGY, VIP, first order, gifts (L1–L11, L14, L17–L21) | Discounts list (all statuses); each candidate's detail page; **Markets > Rollouts**; Checkout Blocks custom discounts (if installed); Shopify Bundles (if installed); B2B catalogs (if wholesale); every custom/legacy custom app's **Functions** page (Discounts area) | A native discount or an app discount (app badge on hover) with matching value, target and eligibility; or a Function listed as Active in the Discounts area |
| Member price as lower unit price, bundles (L6, L8) | Apps' Functions pages (look for a Cart Transform-type function; there is **no admin list of cart transforms** — Unverified, may need a developer check); Shopify Bundles | A cart transform in an app's Active functions; Bundles products |
| Code rejection (L12) | Discounts (app discounts); combinations on the sale discount and on every active code (planned codes affect the priority and W1, not the status) | An automatic app discount that rejects codes (logic not visible → Likely); or native combinations that stop codes stacking. Judge native combinations on money, not the message: if any active code can be worth more than the sale discount, "best discount wins" lets that code replace the sale where the Script refused it → PARTIAL (margin). If no active code can win, → REPLACED, with Shopify's standard message as a note |
| Stacking (L13) | Combinations on every active discount | Combinations matching the old always-stack behaviour where the merchant wants it |
| Quantity limits / blocking (L22, L24) | Settings > Checkout > Checkout rules (On/Off); Add-to-cart limit; Checkout Blocks order value limits; shipping profiles for restricted products | An On checkout rule from an app; an add-to-cart limit; a profile without the restricted zones |
| Shipping hide / show / rename / reorder (S1–S8, S12, S13) | Shipping profiles, zones and rate names/conditions (or Markets shipping options); **Delivery customizations** section; **Settings > Checkout > Checkout rules** (for PO box, address and destination rules S1, S2, S4: a validation can replace them); Checkout Blocks delivery functions and address validation; apps' Functions pages (Shipping and delivery and Checkout areas) | Rates only in the right zones / with the right conditions / with the new names; an **active** delivery customization; an **On** checkout rule that blocks the same address and rate combination |
| Shipping discounts (S9–S11) | Discounts (free shipping native; app discounts with a shipping class); **Markets > Rollouts**; rates' "Offer free shipping" amounts; Checkout Blocks shipping discounts | A free-shipping discount or rate condition with matching threshold, countries and eligibility |
| Payment hide / rename / reorder / terms (P1–P9) | Settings > Payments method names; **Payment customizations > Manage**; Checkout Blocks payment functions; apps' Functions pages (Payments area); B2B company payment terms | An **active** payment customization; a renamed manual method; company payment terms |

**If an app's Functions page couldn't be read** (manual mode, or the PM only saw the app's configuration page): a Discount, Delivery Customization, Payment Customization or Validation function only runs once it is switched on in the admin, as an app discount in the Discounts list, an activated Delivery or Payment customization, or an On checkout rule [hc-checkout-customization] [hc-discounts-with-apps]. So if those places were read and are empty, the app holds no active replacement in those areas: the status can stay **Confirmed**. Add a PM check for the app's Functions page. Exception: a Cart Transform (L6, L8) has no admin list, so for those rules the status is **Likely** at best.

Also scan for **clues** that a migration happened: discount titles echoing the Script's message, discounts created after mid-April 2026, app names like the agency's or "functions", Checkout Blocks being installed. Clues are leads, not evidence — confirm on the detail page.

---

## 3. Compare the dimensions (for each candidate replacement)

Write one line per dimension: **Match / Differs (material or not) / Can't see**.

1. **Active now** — status Active; its active dates include today's date (the run date; dates follow the admin's time zone); customization Activated / rule On / Function on the Active tab. **Rollouts:** if the discount is part of a Rollout, a discount's own dates don't tell the whole story. Rollout running and reaching all shoppers → Match. Rollout running but reaching only a share of shoppers (a test) → **Differs (material)** → PARTIAL. Rollout not started → not active → LOST. Share not shown on the page → **Can't see** + PM check "Markets > Rollouts > {name}: does it reach all shoppers?".
2. **Who** — Scripts' customer tag → native segment or Function that uses the **same tag**; guests included or excluded the same way; B2B vs DTC.
3. **What** — same % or amount, same products/collections/rates/gateways (compare names exactly; Scripts matched rate and gateway **display names**), same cap (once per order, max uses, units).
4. **When** — same thresholds (same currency and units), same minimum quantities, same codes, same countries/regions, same date window.
5. **Stacking** — the Script stacked with everything. If the replacement's Combinations stop it from stacking with discounts that active codes or automatic discounts use, that's a **material** difference (PARTIAL) unless the merchant wanted that.
6. **Where** — POS / draft orders / B2B: note differences (W3) but don't change the status for this alone.
7. **Message** — same or similar text: note only, unless one of the two exceptions in section 1 applies.
8. **Health** — any "Errors on [n] area" warning on the app's Functions card → PARTIAL (Likely), priority bump.

Decision (apply in this order; the first that fits wins):
- Any material dimension **Differs**, or only some tiers/conditions exist → PARTIAL.
- Every material dimension **Match** → REPLACED (Confirmed).
- No dimension Differs, some are **Can't see** (logic hidden), **and** the candidate is in the right area (Discounts / Shipping and delivery / Payments / Checkout) **and** its title, function name or message repeats at least one concrete detail of the rule (the same %, amount, tag, rate name, gateway name or the Script's message text) → REPLACED (Likely) and add a test.
- No dimension Differs, some are Can't see, and no concrete detail matches → treat it as no candidate (next bullets) and add a PM check naming the candidate.
- No active candidate after checking every place in section 2 → LOST.
- Couldn't read a place in section 2 (permission, embedded app unreadable) and found nothing elsewhere → LOST (Likely) + PM check naming that place.

---

## 4. Rolling up to the script

| Rules in the script | Script status |
|---|---|
| All REPLACED | REPLACED |
| All LOST | LOST |
| Any mix, or any PARTIAL | PARTIAL |
| All NOT APPLICABLE | NOT APPLICABLE (never ran) |

NOT APPLICABLE rules are ignored in the roll-up unless every rule is NOT APPLICABLE.

---

## 5. Evidence format (copy into the report for every rule)

```
Status: PARTIAL (Likely)
Evidence:
- Discounts > "VIP 15%" — Active since 2026-07-02, Amount off products 15%, Applies to: all products,
  Eligibility: segment "VIP" (filter shows customer tag "vip"), Combinations: order discounts only. (seen 2026-11-04)
- Script S2.R1 gave 15% to tag "VIP" on all products and stacked with codes.
Differences: stacking (material) — product codes no longer combine; POS ticked (note W3).
Checked and found nothing else: Checkout Blocks (not installed), apps' Functions (none in Discounts area).
```

Always list the places you checked that had **nothing**, so a reader can see LOST was earned.

---

## 6. Common traps

- A native discount with the right value but **Eligibility = All customers** replacing a VIP-only Script → PARTIAL (margin leak), not REPLACED.
- A delivery or payment customization that exists but was never **Activated** → LOST.
- A replacement created in an app the merchant later **uninstalled** (Checkout Blocks removes its discounts and customizations on uninstall) → it won't appear; LOST.
- Rate or gateway **renamed** since the Script was written → the old Script may already have stopped matching before June 30 (note it; consider NOT APPLICABLE only with evidence).
- Two replacements for the same rule (e.g. native discount **and** app discount) → check they don't **double-discount**; if both are active and combinable, mark PARTIAL (margin leak).
- Market-driven shipping stores: rates are under Markets; don't call shipping rules LOST until you've read the Markets shipping options.
- A replacement discount that's in a **Rollout test** reaches only some shoppers → PARTIAL, even if the discount itself shows Active.
- A Delivery or Payment customization doesn't run on the **cart page** (checkout only). That matches shipping and payment Scripts, which also ran only in checkout: not a difference.
