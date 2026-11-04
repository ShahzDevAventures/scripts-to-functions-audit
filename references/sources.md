# Sources

**Last verified: 2026-11-04.** Every fact, admin path, API name, limit and plan rule in this skill comes from the pages below. "Re-checked live" marks pages fetched again while the skill was being written, to confirm the facts the skill depends on most. "(review)" marks pages fetched again on 2026-11-04 by an independent review pass, which corrected several facts (see the review log at the end). "(fix pass)" marks facts fetched again on 2026-11-04 after a blind test run. All other pages were read by the research pass the same day. Pages marked *(summary)* were read through a fetch summary because the direct fetch was rate-limited, so they are one step removed from the raw page.

**When to re-check live:** if an admin page, button label, URL, API name, target or limit doesn't match this skill, open the page cited below on help.shopify.com or shopify.dev, follow what it says now, and note the difference in the audit's "Sources and method" section. If you can't re-check, mark the item **Unverified** and add it to the PM's checks. Shopify changed Scripts, Functions, discounts and shipping a lot in 2025–2026, so re-check this whole list every quarter.

---

## Shopify Help Center (help.shopify.com)

| ID | Page | Supports |
|---|---|---|
| hc-transition | https://help.shopify.com/en/manual/checkout-settings/script-editor/transitioning-to-functions (also reached via `/script-editor/migrating`) — **re-checked live (review)** | "As of June 30, 2026, Shopify Scripts has been deprecated"; report click path Apps > Script Editor > "Replace Shopify Scripts" banner; report links `admin.shopify.com/settings/checkout/scripts-report` and `…/customizations-report?tab=scripts-reports`; sections Payment gateways / Shipping / Product discounts; name, description, source file links, recommended apps, tutorials, "Auto detected"; CSV export; custom Functions apps must be created in the Dev Dashboard |
| hc-script-editor | https://help.shopify.com/en/manual/checkout-settings/script-editor — **re-checked live (review, fix pass)** | Script types and when they ran; Scripts still published on June 30, 2026 "have been deactivated and no longer work". The page doesn't show the Script Editor list badges |
| hc-script-limits | https://help.shopify.com/en/manual/checkout-settings/script-editor/limitations — **re-checked live (review)** | One published script per type, 200 scripts, 40,960 characters; no POS / draft orders / Buy Button / Facebook-Instagram; no metafields, time or web requests; couldn't raise prices or add items; multi-currency caveats |
| hc-script-api | https://help.shopify.com/en/manual/checkout-settings/script-editor/shopify-scripts | Script API inputs and effects (change_line_price, split, reject, apply_discount, change_name, delete_if, sort_by!) |
| hc-script-examples | https://help.shopify.com/en/manual/checkout-settings/script-editor/examples (+ `/line-item-scripts`, `/shipping-scripts`, `/payment-gateway-scripts`) | Template names, config constants, placeholders |
| hc-script-multicurrency | https://help.shopify.com/en/manual/checkout-settings/script-editor/scripts-multicurrency | Store-currency amounts, `derived_from_presentment` |
| hc-script-liquid | https://help.shopify.com/en/manual/checkout-settings/script-editor/update-liquid-templates-for-scripts | Theme Liquid fields that showed Script prices |
| hc-checkout-customization | https://help.shopify.com/en/manual/checkout-settings/checkout-customization — **re-checked live (review)** | Paths: Settings > Payments > Payment customizations > Manage (Add customization, Save, Activate); Settings > Shipping and delivery > Delivery customizations; Settings > Checkout > Checkout rules (Add rule, Turn on/off, Remove rule); non-Plus US/Canada limited to non-credit-card methods; hiding accelerated checkout needs a custom app on Plus |
| hc-discounts | https://help.shopify.com/en/manual/discounts | Discount overview, rollouts, sales channel settings |
| hc-amount-off | https://help.shopify.com/en/manual/discounts/discount-types/percentage-fixed-amount — **re-checked live (review)** | Click-by-click steps for Amount off products / orders, including Method, Purchase type, Applies to, Only apply discount once per order, minimum requirement, Eligibility (All customers / Specific customers / Customer segments / Markets), Combinations, Active dates, "Also offer on Point of Sale (POS Pro locations only)", Save. **Re-checked live (fix pass):** Amount off products minimum counts only the selected products or products in selected collections; Amount off orders minimum counts the purchase type excluding purchased gift cards before product discounts, and the cart subtotal including purchased gift cards after them; gift cards used as payment don't count |
| hc-bxgy | https://help.shopify.com/en/manual/discounts/discount-types/buy-x-get-y — **re-checked live (review)** | Buy X get Y steps and labels (Customer buys / Any items from / Customer gets / At a discounted value: Percentage, Amount off each, Free / Set the maximum number of uses per order / Maximum discount uses for codes); "get" item never added automatically; automatic discounts with overlapping buy/get sets discount "the lower-priced item that the customer chooses" |
| hc-free-shipping | https://help.shopify.com/en/manual/discounts/discount-types/free-shipping | Free shipping discount options; minimum uses discounted product prices |
| hc-combinations | https://help.shopify.com/en/manual/discounts/discount-combinations — **re-checked live (review)** | Script discounts applied regardless of combination settings; max 25 active automatic discounts (incl. app); max 5 product/order codes + 1 shipping code; each discount must allow the combination; same-line product discounts need Plus; best discount applies when they can't combine |
| hc-discounts-faq | https://help.shopify.com/en/manual/discounts/discounts-faq — **re-checked live (fix pass)** | Combination message "Some discount codes couldn't be used together. We applied the best combination"; "Most discounts cannot be applied to gift cards", except a product-specific discount whose product is a gift card; product-page display |
| hc-discounts-with-apps | https://help.shopify.com/en/manual/discounts/discount-types/discounts-with-apps — **re-checked live (review)** | App badge and tooltip on app discounts; Type and Combinations columns |
| hc-managing-discounts | https://help.shopify.com/en/manual/discounts/managing-discount-codes | Discounts list filters |
| hc-checkout-blocks | https://help.shopify.com/en/manual/checkout-settings/checkout-blocks — **re-checked live (review)** | "All other features of Checkout Blocks are available only to Shopify Plus" (Basic+ only gets Thank you / Order status content blocks); feature areas; staff permissions |
| hc-cb-custom-discounts | https://help.shopify.com/en/manual/checkout-settings/checkout-blocks/custom-discounts — **re-checked live (review)** | Uninstalling removes its discounts |
| hc-cb-order-discount | https://help.shopify.com/en/manual/checkout-settings/checkout-blocks/custom-discounts/order-discount | Order discount rules; most recently created passing discount applies |
| hc-cb-shipping-discount | https://help.shopify.com/en/manual/checkout-settings/checkout-blocks/custom-discounts/shipping-discount | Percentage / free / fixed / set fixed price; biggest passing shipping discount applies |
| hc-cb-delivery | https://help.shopify.com/en/manual/checkout-settings/checkout-blocks/customizations/delivery-methods — **re-checked live (review)** | Plus only; hide / rename / reorder, **only Hide supports conditional rules** (country, state, zip, shipping address type, customer tags, B2B, cart, product, time); max 25 active across apps; can't hide a whole local delivery or pickup method; carrier name prefixed to renamed rates |
| hc-cb-payment | https://help.shopify.com/en/manual/checkout-settings/checkout-blocks/customizations/payment-methods — **re-checked live (review)** | Plus only; hide / rename / reorder, only Hide supports conditional rules; only methods without a logo can be renamed (PayPal, Klarna named as logo methods); express wallets can be hidden but not reordered; Shop Pay supports only hiding gift cards |
| hc-cb-address-validation | https://help.shopify.com/en/manual/checkout-settings/checkout-blocks/customizations/address-format-validation | Block PO box / military addresses |
| hc-cb-order-limits | https://help.shopify.com/en/manual/checkout-settings/checkout-blocks/order-value-limits | Min/max order value |
| hc-b2b-plan-features | https://help.shopify.com/en/manual/b2b/getting-started/plan-features — **re-checked live (review)** | B2B on Basic, Grow, Advanced, Plus (not Starter/Retail); non-Plus: 3 active catalog assignments, no direct company catalogs, no deposits/partial payments; net terms, quantity rules and volume pricing on all four plans |
| hc-b2b-quantity-pricing | https://help.shopify.com/en/manual/b2b/catalogs/quantity-pricing — **re-checked live (review)** | Markets > Catalogs > catalog > Products and pricing > Manage > Manage products and pricing > Volume pricing / Quantity rules columns > + Add > Save; up to 10 price breaks per product, applied to each variant (page still shows the stale Aug 28, 2025 Scripts date) |
| hc-bundles | https://help.shopify.com/en/manual/products/bundles/shopify-bundles — **re-checked live (review)** | Shopify Bundles: free, first-party, all plans; fixed bundles and multipacks; 30 components (fixed) / 150 (dynamic); 3 options, 100 variants; discounts calculated on the parent bundle; selling-plan compatibility not stated on this page (Cart Transform rejects operations with selling plans [dev-cart-transform]) |
| hc-subscriptions | https://help.shopify.com/en/manual/products/purchase-options/shopify-subscriptions *(summary)* | Subscription discounts |
| hc-price-adjustments | https://help.shopify.com/en/manual/international/pricing/price-adjustments *(summary)* | Market catalogs / price lists |
| hc-add-to-cart-limit | https://help.shopify.com/en/manual/checkout-settings/add-to-cart-limit — **re-checked live (review)** | Settings > Checkout > Advanced preferences > Add-to-cart limit; applies to each variant independently, not the product or cart; plan and shopper message not stated |
| hc-auto-collections | https://help.shopify.com/en/manual/products/collections/automated-collections/auto-select — **re-checked live (review)** | Conditions: Tag includes / does not include; Title, Type, Vendor is equal to / is not equal to / starts with / ends with / contains / does not contain; Compare at price is set / is not set; Match all conditions / Match any condition; max 60 conditions. **Re-checked live (fix pass):** for excluding products only the category, tag, type and vendor conditions apply |
| hc-smart-collections | https://help.shopify.com/en/manual/products/collections/automated-collections (and `/creating-modifying-smart-collections`) — **re-checked live (review)** | "Smart collection" naming; a new collections model is replacing manual/smart collections; Starter plan has no collections. Creation button labels not shown on the page |
| hc-combined-shipping-rates | https://help.shopify.com/en/manual/fulfillment/setup/shipping-profiles/combined-shipping-rates — **checked live (review)** | Rates from different profiles: same name → added together; different names → cheapest of each added and shown as "Shipping"; weight, carrier and app rates combined |
| hc-rollouts | https://help.shopify.com/en/manual/markets/rollouts — **checked live (review)** | "Markets > Rollouts"; rollouts can include theme, checkout and accounts, **discounts**, catalogs; scheduling; plan availability on a separate requirements page (not checked) |
| hc-shipping-zones | https://help.shopify.com/en/manual/shipping/setting-up-and-managing-your-shipping/setting-up-shipping-zones — **re-checked live (review)** | Add shipping option, Name, Rate type Order amount / Weight, Minimum/Maximum, Price, Offer free shipping, Edit shipping option, Done, Save; carrier rates use Handling fee; market-driven shipping changes steps. **Re-checked live (fix pass):** new zone = Shipping zones > Add zone > Zone name > Regions > Done > Save; Horizontal menu > Edit zone; "You must remove a country or region from one shipping zone before adding it to another"; a country must be in an active market (the page gives no explicit "clear a country" step) |
| hc-shipping-rates | https://help.shopify.com/en/manual/shipping/setting-up-and-managing-your-shipping/shipping-rates — **re-checked live** | Profiles and zones; shipping moving gradually to shipping options by market |
| hc-manual-payments | https://help.shopify.com/en/manual/payments/manual-payments — **re-checked live (review)** | Settings > Payments > Manual payment methods > Create custom payment method > Custom payment method name / Additional details / Payment instructions > Activate; reserved names (Bank Deposit, Cash, Cash on Delivery (COD), custom, External Credit, External Debit, Gift Card, Money Order, Store Credit); no conditions described; not for US stores with Shopify-managed sales tax |
| hc-segments | https://help.shopify.com/en/manual/customers/customer-segmentation/create-customer-segments — **re-checked live (review)** | Customers > Segments > Create segment; WHERE dialog (filter, operator, value); Run query; Save |
| hc-custom-apps | https://help.shopify.com/en/manual/apps/app-types/custom-apps — **re-checked live (review)** | Dev Dashboard; legacy custom apps before Jan 1, 2026 |
| hc-working-with-apps | https://help.shopify.com/en/manual/apps/working-with-apps | Settings > Apps; Legacy custom apps; Develop apps |
| hc-extensions-functions | https://help.shopify.com/en/manual/apps/extensions-and-functions — **re-checked live (review)** | Settings > Apps > app > Functions card; Active / Inactive tabs; "Errors on [n] area"; areas Checkout, Discounts, Payments, Shipping and delivery |
| hc-staff-permissions | https://help.shopify.com/en/manual/your-account/staff-accounts/staff-permissions/staff-permissions-descriptions — **re-checked live (review)** | Discounts "View, create, and delete"; Shipping "Manage shipping and delivery"; Checkout and customer accounts "View and edit"; no view-only variants for these; "Reports" permission covers viewing reports; no permission named for the Scripts report |
| hc-sales-reports | https://help.shopify.com/en/manual/reports-and-analytics/shopify-reports/report-types/default-reports/sales-report — **re-checked live (review)** | Sales by discount codes (counts only the sales of lines a discount affected; columns **Non-shipping script discounts** and **Shipping script discounts** display only on Shopify Plus); Average order value over time; Total sales over time |
| hc-finance-reports | https://help.shopify.com/en/manual/reports-and-analytics/shopify-reports/report-types/default-reports/finances-report — **re-checked live (review)** | Total sales breakdown; Discounts by order (discount codes and POS discounts); Shipping by order; payments reports named "Net payments by method" / "Net payments by gateway" (Finance summary cards "Payments by method" / "Payments by gateway") |
| hc-export-orders | https://help.shopify.com/en/manual/fulfillment/managing-orders/exporting-orders | Orders CSV columns (Discount Code, Shipping Method, Payment Method …) |

## shopify.dev

| ID | Page | Supports |
|---|---|---|
| dev-functions-overview | https://shopify.dev/docs/apps/build/functions | Functions overview (the old Scripts migration guide URL now redirects here) |
| dev-function-apis | https://shopify.dev/docs/api/functions/latest — **re-checked live (review)** | API version 2026-10; "Only stores on a Shopify Plus plan can use custom apps that contain Shopify Function APIs"; limits (11M instructions, 128 kB input, 20 kB output, 256 kB binary, query 3,000 bytes / cost 30, metafields over 10,000 bytes not returned, list arguments ≤ 100); **input query cost table** (metafield field 3; `hasAnyTag` / `hasTags` / `inAnyCollection` / `inCollections` 3; `metaobject` root 1, `field(key:)` 3; other leaf fields 1); checkout execution order; fetch limited to Enterprise per this page |
| dev-discount-api | https://shopify.dev/docs/api/functions/latest/discount — **re-checked live (review)** | Targets `cart.lines.discounts.generate.run`, `cart.delivery-options.discounts.generate.run`; operations `productDiscountsAdd`, `orderDiscountsAdd`, `deliveryDiscountsAdd`, `enteredDiscountCodesAccept`, `enteredDiscountCodesReject`; up to 25 discount functions; rejection only when backed by an automatic discount and code rejectable; surfaces (B2B, Cart, Checkout, POS, Admin, Storefront, accelerated checkout; partial: draft orders, order edit, subscriptions); not re-run on recurring orders (shipping discount becomes 100%); not re-run on order edit; fetch "Shopify Plus and Enterprise" (conflicts with dev-function-apis) |
| dev-cart-transform | https://shopify.dev/docs/api/functions/latest/cart-transform — **re-checked live (review)** | Target `cart.transform.run`; `lineExpand`, `linesMerge`, `lineUpdate`; `lineUpdate` Plus or development stores only; one cart transform function per app per store; operations rejected when a selling plan is present |
| dev-delivery-customization | https://shopify.dev/docs/api/functions/latest/delivery-customization — **re-checked live (review)** | Target `cart.delivery-options.transform.run`; `deliveryOptionHide` / `deliveryOptionMove` / `deliveryOptionRename`; max 25; checkout only (Cart not supported); PO Box hiding only for carrier-service / shipping-app rates; carrier name prefix can't be removed; cheapest option must be selected first; delivery option input fields `code`, `cost`, `deliveryMethodType`, `description`, `handle`, `metafield`, `title` (no `source`) |
| dev-payment-customization | https://shopify.dev/docs/api/functions/latest/payment-customization — **re-checked live (review)** | Target `cart.payment-methods.transform.run`; `paymentMethodHide`, `paymentMethodMove`, `paymentMethodRename`, `paymentTermsSet` (Plus), `orderReviewAdd` (Plus, B2B); placement-specific hiding Plus only; max 25 |
| dev-validation | https://shopify.dev/docs/api/functions/latest/cart-and-checkout-validation — **re-checked live (review)** | Target `cart.validations.generate.run`; operation `validationAdd`; max 25; covers express checkouts (Shop Pay, PayPal, Google Pay, Apple Pay); errors exposed on the cart template and Storefront API cart; "Prevent shipping to PO boxes" example (reads `deliveryGroups.deliveryAddress.address1`); **re-checked live (fix pass):** the input has `cart.deliveryGroups.selectedDeliveryOption` with `title`, `handle`, `code`, `cost`, `deliveryMethodType`, `description`; fetch Enterprise only |
| dev-network-access | https://shopify.dev/docs/apps/build/functions/network-access — **re-checked live (review)** | "available primarily for merchants on Shopify for enterprises"; Discount Functions and Validation: Enterprise with custom apps (conflicts with the Discount API page's "Shopify Plus and Enterprise") |
| dev-discounts-build | https://shopify.dev/docs/apps/build/discounts | Discount Function overview |
| dev-discount-rejections | https://shopify.dev/docs/apps/build/discounts/discount-rejections | Rejecting entered codes |
| dev-build-discount-function | https://shopify.dev/docs/apps/build/discounts/build-discount-function | Function name/description shown in admin |
| dev-bundles | https://shopify.dev/docs/apps/build/product-merchandising/bundles | Bundles via Cart Transform |
| dev-market-shipping | https://shopify.dev/docs/apps/build/orders-fulfillment/market-driven-shipping/feature-preview | Market-driven shipping (collections for product conditions; rates per market) |
| dev-liquid-line-item | https://shopify.dev/docs/api/liquid/objects/line_item — **re-checked live (review)** | Deprecated: `price`, `line_price`, `total_discount` (they include Shopify Scripts discounts but not automatic discounts or codes) → `final_price`, `final_line_price`, `line_level_total_discount`; `discounts` → `discount_allocations`. `message` is **not** deprecated (discount title, or a count when several apply); `error_message` is a separate field |
| dev-script-discount-application | https://shopify.dev/docs/api/admin-graphql/latest/objects/ScriptDiscountApplication — **re-checked live (review)** | How past Script discounts are stored on orders |
| dev-segment-ql | https://shopify.dev/docs/apps/build/shopifyql/segment-query-language-reference | Segment filters (customer tags, number of orders, amount spent, email subscription status) |
| dev-migration-archived | http://web.archive.org/web/20260524112609/https://shopify.dev/docs/apps/build/functions/migrating-from-shopify-scripts (also 2026-06-29 snapshot) | Official mapping: line item → Discount / Cart Transform / Validation; shipping → Delivery Customization + Discount; payment → Payment Customization |

## Changelogs

| ID | Page | Supports |
|---|---|---|
| cl-scripts-end | https://changelog.shopify.com/posts/shopify-scripts-can-no-longer-be-edited-or-published (2026-03-12) — **re-checked live (review)** | Editing ends April 15; execution ends June 30, 2026; report link with `?tab=scripts-reports` |
| dev-cl-scripts-deprecated | https://shopify.dev/changelog/shopify-scripts-will-be-deprecated-on-june-30-2026 (2026-04-09) — **re-checked live (review)** | "All Shopify Scripts will cease to execute entirely" June 30, 2026 |
| cl-report-launch | https://changelog.shopify.com/posts/shopify-scripts-customizations-report-now-available-to-accelerate-migration (2025-02-04) | Report is "AI-powered" |
| cl-extensions-functions | https://changelog.shopify.com/posts/see-which-apps-use-extensions-and-functions-to-power-your-checkout-online-store-and-more (2026-04-01) | Functions card on app pages |
| dev-cl-multi-product | https://shopify.dev/changelog/multiple-product-discounts-can-apply-on-a-single-cart-line (2026-04-30) | Same-line product discounts (Plus) |
| dev-cl-enhanced-discounts | https://shopify.dev/changelog/enhanced-discounts-support-in-the-shopify-functions-cart (2026-03-02) | Later functions can read discount details |
| dev-cl-2026-04 | https://shopify.dev/changelog/release-notes/2026-04 | BXGY prerequisites in Discount Functions; metaobjects; validation targets |
| dev-cl-2026-07 | https://shopify.dev/changelog/release-notes/2026-07 | `appliesOnSubscription` default; buyer-journey intercept deprecated in favour of code rejection |
| dev-cl-2026-10 | https://shopify.dev/changelog/release-notes/2026-10 — **re-checked live (review)** | Customer `createdAt` in Functions (Jul 30, 2026); segment query syntax `MATCHES` / `NOT MATCHES` (Oct 1, 2026); discounts expose `rollouts`; delivery options expose metafields |
| dev-cl-discount-rollouts | https://shopify.dev/changelog/posts/discounts-can-now-be-included-in-rollouts (Oct 1, 2026) — **checked live (review)** | "When a discount is part of a Rollout, its native dates alone don't describe its availability"; rollouts can test discounts with a share of buyers |
| cl-discount-rollouts | https://changelog.shopify.com/posts/schedule-and-test-discounts-with-rollouts (Oct 2, 2026) — **checked live (review)** | Merchants can launch a discount to a portion of online store traffic, test offers, and launch with theme/checkout changes; plan not stated |
| dev-cl-delivery-option-metafields | https://shopify.dev/changelog/posts/delivery-options-in-shopify-functions-input-now-expose-their-metafields (Sep 15, 2026) — **checked live (review)** | `metafield(namespace:, key:)` on `CartDeliveryOption` in 2026-10 |

## Shopify App Store (developer = Shopify; first-party)

| ID | Page | Supports |
|---|---|---|
| app-checkout-blocks | https://apps.shopify.com/checkout-blocks | Developer Shopify, free |
| app-shopify-bundles | https://apps.shopify.com/shopify-bundles | Developer Shopify, free |
| app-subscriptions | https://apps.shopify.com/shopify-subscriptions | Developer Shopify |
| app-flow | https://apps.shopify.com/flow | Built by Shopify |
| app-launchpad | https://apps.shopify.com/launchpad | Plus only; scheduled Scripts in the past |
| app-script-editor | https://apps.shopify.com/script-editor | Script Editor listing ("only available to Shopify Plus customers"; seen via a search snippet only) |

## Community and public code (lower trust; used only to recognise real script styles)

| ID | Page | Supports |
|---|---|---|
| gh-shopify-scripts | https://github.com/Shopify/shopify-scripts (archived; README shows the stale Aug 28, 2025 date) | Hand-written and composable examples; folder ≠ type |
| gh-script-creator | https://github.com/jgodson/shopify-script-creator | Script Creator class signatures |
| gh-disco | https://github.com/discolabs/scripts-examples and https://gist.github.com/gavinballard/dadd4508682b3d72bc58ad47347d21f7 | Composable Campaign / Selector / Partitioner style |
| gh-broken-example | https://github.com/davidleininger/ShopifyScripts/blob/master/Payment-Gateway.rb | Undefined-method crash example |
| gh-billing-address | https://github.com/freakdesign/Shopify-code-snippets/blob/master/Shopify%20Scripts/Payments/remove-gateway-on-billing-country.rb | Undocumented `billing_address` call |
| comm-find-scripts | https://community.shopify.com/t/how-do-we-accurately-find-scripts/565828 | "Auto detected" counts customizations (2 scripts → 6) |
| comm-scripts-ending | https://community.shopify.com/t/shopify-scripts-are-ending-what-is-everyone-using-now/632089 | Claim that Script Editor was read-only until July 30, 2026 (**Unverified** on any Shopify page) |

## Observation on a store (anonymised)

- **Store A, 2026-11-04** (name, domains and IDs changed: website `storea.example`; typo `store-a.example` 301-redirects there; admin handle `ab12cd-ef`; myshopify `a1b2c3`): `admin.shopify.com/store/store-a` gave "There's a problem loading this page"; the right handle came from the admin store switcher. Script Editor was not installed. `/settings/checkout/scripts-report` redirected to `/settings/checkout/customizations-report` showing "You have no existing customizations that require action." `/apps/script-editor` showed "You don't have this app installed".

---

- **Script Editor badges after June 30, 2026** (reported by the agency, 2026-11-04): the list shows **Deactivated** for Scripts that were published when Scripts stopped, and **Unpublished** for drafts. The badge label itself isn't on a Help Center page; the meaning follows hc-script-editor.

---

## Known unverified points (the skill handles each by asking the PM or labelling Unverified)

1. Whether stores that had Scripts can still open Script Editor and read code after June 30 / July 30, 2026 (no Shopify page says either way).
2. The CSV export's button label and column names (read headers at run time).
3. Whether the report's source-file links still open.
4. Whether `/settings/checkout/customizations-report` without `?tab=scripts-reports` shows Scripts items, and whether a store that never had Scripts shows a Scripts tab at all.
5. The exact staff permission needed to view the report (the permissions page names none).
6. Exact admin URL slugs for Settings > Plan, General, Domains, Payments, Shipping, Checkout, Apps, Analytics > Reports and Markets > Rollouts (click paths are verified; slugs are patterns).
7. Whether "Sales by discount codes" has rows that name each Script (the Plus-only columns "Non-shipping script discounts" / "Shipping script discounts" are verified; a per-Script breakdown is not).
8. Network-access plan (Enterprise vs Plus and Enterprise): conflicting pages.
9. Which unit a Buy X get Y **code** discounts when buy and get sets overlap (for automatic discounts the lower-priced item is documented).
10. Whether a guest who types a tagged customer's email gets tag/segment-based discounts.
11. Whether app (Function) discounts honour the native sales-channel settings for discounts (e.g. to keep them off POS).
12. How Cart Transform `lineUpdate` prices appear in discount reports.
13. Where (and whether) the admin shows a Rollout's share of shoppers, and which plans have discount Rollouts.
14. Plan availability of the add-to-cart limit, Shopify Flow and Shopify Subscriptions; whether shoppers see a message at the add-to-cart limit.
15. Absence of "accepts marketing" and card brands in Function inputs (absence of evidence only).
16. How a Delivery Customization can reliably tell carrier-calculated from manual rates (pattern S13): the input has no `source` field.
17. Exact button labels for creating a custom shipping profile and a smart/automated collection (the new collections model is rolling out); follow live labels.
18. Whether the logo-method rename limit documented for Checkout Blocks also applies to custom Payment Customization Functions.
19. Whether a cart transform shows up on an app's Functions page, and under which area.

---

## Review log (2026-11-04, independent re-check against live pages)

Corrected in this skill after re-reading the live pages:
- **Liquid `line_item`** (W2): `message` is not an error field (it shows the discount title or count); `error_message` is separate; `total_discount` is replaced by `line_level_total_discount`, and `discounts` by `discount_allocations` [dev-liquid-line-item].
- **Buy X get Y overlap** (L5): documented for automatic discounts — the lower-priced item is discounted [hc-bxgy].
- **Manual payment methods** (N11): exact path, the Activate button and the full reserved-name list [hc-manual-payments].
- **Automated collections** (N6): "Tag includes", "Compare at price is not set", "Match all / any condition"; smart-collection naming; new collections model; no collections on Starter [hc-auto-collections] [hc-smart-collections].
- **B2B volume pricing** (N12, plan table): path and plan limits now verified live [hc-b2b-quantity-pricing] [hc-b2b-plan-features].
- **Input query cost**: other leaf fields cost 1, metaobject root 1, `field(key:)` 3 [dev-function-apis].
- **Delivery option inputs** (S13): no `source` field; metafields added in 2026-10 [dev-delivery-customization] [dev-cl-delivery-option-metafields].
- **Checkout Blocks rename/reorder** (S7, S8, P6, P7): only Hide supports conditional rules [hc-cb-delivery] [hc-cb-payment].
- **Combined shipping rates** (N10, S4): same-name rates added together; different names → cheapest of each, shown as "Shipping" [hc-combined-shipping-rates].
- **Payment terms** (P8): not supported in accelerated checkouts or with subscription items [dev-payment-customization].
- **Discount Rollouts** (new since Oct 2026): a discount can reach only a share of shoppers; added to status checks [hc-rollouts] [dev-cl-discount-rollouts] [cl-discount-rollouts].
- **Sales by discount codes**: Plus-only script discount columns added to the priority inputs [hc-sales-reports].
- **Finance report names**: "Net payments by method / by gateway" [hc-finance-reports].
- **Discount code usage label**: "Limit to one per customer" [hc-amount-off].
- **Staff permissions wording**: exact permission names [hc-staff-permissions].

Fix pass (2026-11-04, after a blind test run): re-checked live and added **Tag does not include** and the exclusion rule for automated collections [hc-auto-collections]; the Amount off products and Amount off orders minimum-purchase basis, including gift cards [hc-amount-off]; gift cards and discounts, and the exact combination message [hc-discounts-faq]; the Add zone / Edit zone steps [hc-shipping-zones]; `selectedDeliveryOption` in the Validation input [dev-validation].

Confirmed unchanged: June 30, 2026 deactivation wording and report URLs [hc-transition] [cl-scripts-end] [dev-cl-scripts-deprecated]; Plus-only custom Function apps, API version 2026-10, resource limits and execution order [dev-function-apis]; Discount, Cart Transform, Delivery, Payment and Validation targets, operations and 25-function limits; `lineUpdate` Plus/dev-store only; one cart transform per app; selling plans rejected [dev-discount-api] [dev-cart-transform] [dev-payment-customization] [dev-validation]; combination limits [hc-combinations]; checkout customization click paths [hc-checkout-customization]; Functions card, Active/Inactive tabs and "Errors on [number] area" [hc-extensions-functions]; Checkout Blocks Plus-only scope [hc-checkout-blocks]; amount-off steps [hc-amount-off]; shipping zone steps [hc-shipping-zones]; segment steps [hc-segments]; one published Script per type, no POS/draft orders/Buy Button [hc-script-limits]; add-to-cart limit path [hc-add-to-cart-limit].
