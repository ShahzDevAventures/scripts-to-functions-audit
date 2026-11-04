# Output template: the store audit document (Steps 4 and 12)

Two variants. **Variant A** is the short version when Step 0 finds nothing to migrate. **Variant B** is the full audit. Use the headings, order and IDs exactly as written. Write "None" under a heading that has no content; never delete a heading. Every finding carries a confidence label: **Confirmed / Likely / Unverified**.

This file fixes the content and order. The look comes from `report-template.html`, and both follow the same order. Save two files with the same content in the same order: `{admin-handle}-scripts-to-functions-audit-{YYYY-MM-DD}.html` (the report people read) and the same name ending `.md` (for tickets and developers). In the Claude app, show the HTML report in the chat as an artifact; it stays private to the PM. Never publish it, share a link to it, email it or post it. The PM decides who sees it.

ID scheme: scripts **S1…**, rules **S1.R1…**, PM fixes **F1…**, developer specs **D1…**, gaps **G1…**, tests **T1…** (store-wide tests **TW1…**), store-wide warnings **W1…W9** (from `replacement-map.md` section 6), PM checks **C-PM1…**.

---

## Readability rules (both variants; check them before saving)

1. **Lead with the answer.** Order on screen: page head, fix-first banner, summary, then the numbered sections. Store details and the glossary sit in one collapsed block right after the summary.
2. **Visible in five minutes.** In the HTML, the text a reader sees without opening anything is about **1,500 words** or less. Everything long goes inside `<details>` (fold map below). Never cut content to save space; fold it.
3. **Plain name first.** In the fix-first banner, the summary, the top fixes and the priority list, never write an ID alone. Write "Hide Pay by Invoice from non-trade customers (D3)", not "D3".
4. **Short blocks.** Summaries are bullets, one idea each. No paragraph over 3 sentences anywhere in the report.
5. **Markdown copy.** Same sections in the same order, nothing cut. It doesn't fold: what the HTML puts inside `<details>` appears in the Markdown as normal text under the same heading.

**Fold map (HTML)**

| Part | Visible | Inside `<details>` |
|---|---|---|
| Page head | Title, one subline (website · admin handle · plan · date · run mode), status count badges | — |
| Fix-first banner | 1–2 sentences on the top-ranked rule: who is affected and what goes wrong today. Tone: `banner bad` if any P1, `banner warn` if the top is P2, plain `banner` if only P3 / Monitor, `banner ok` if nothing is LOST or PARTIAL | — |
| 1. Summary | Up to 6 bullets and the stat tiles | — |
| Store details and words used | Only the `<summary>` line | Store table, label definitions, glossary |
| 2. Script inventory | The table and a one-line note on the report counts | A longer reconciliation, if needed |
| 3. Priority list | The 6-column table and one line on where the inputs came from | "How the priority was scored": the full rubric table and input notes |
| 4. Findings | Per rule: heading, badges, 1–2 sentences on what it did, "Status today" line, "Fix" line | Who, What, When, Message, Was live, Pattern, Class, Evidence, Gap, Tests, Notes |
| 5. PM can do this | Every F# in full | — |
| 6. Needs a developer | Every D#: title and goal (field 1); the apps line if it applies | Fields 2–14 |
| 7. Gaps | Every G#: title and "Decision needed" | Why, closest option |
| 8. Tests | The one-line reminder "Go up to the payment step and leave. Never pay.", then one line per test: name, what it checks (plain name), expected today | The rules box, Pass / Fail rule and full test cards |
| 9. Store-wide warnings | Per W#: a bold title and a paragraph of 3 sentences at most | — |
| 10. Things the PM must check | The table | — |
| 11. Coverage check, 12. Sources and method | Only the `<summary>` line | Everything |
| Appendix A | Heading and one line | The code, one `<details>` per script |

If the visible text is still over about 1,500 words, fold more, in this order, until it fits: (1) the test lines (keep one line: "{n} tests. Run them now and after each fix."); (2) the PM checks table (keep the count and the checks that must happen before a P1 fix); (3) the warning paragraphs (keep each bold title); (4) the steps of P3 PM fixes (keep title and "What this sets up").

---

## Variant A — Nothing to migrate

```markdown
# Scripts to Functions audit: {Store name}

{primary domain} · admin handle {handle} · {plan} · {YYYY-MM-DD} · {Browser (Claude in Chrome) / Manual}

> **Result: Nothing to migrate ({Confirmed | Likely}).** Shopify turned off all Shopify Scripts on June 30, 2026. This store has no Scripts on record, so nothing stopped working because of that change.

## What I checked

| Check | Page | What it showed |
|---|---|---|
| Admin handle | {store switcher / address bar} | {handle} |
| Scripts report (Scripts tab) | {final URL after redirects} | "{exact text}" |
| Script Editor app | {URL} | "{exact text}" |
| Installed apps | Settings > Apps | {Script Editor listed / not listed} |
| PM confirmation (only if Likely) | — | {answer} |

## Things the PM may want to check
{None | e.g. "The Scripts tab wasn't visible, only the default tab. If the merchant remembers Scripts from before 2026, ask the previous developer for the .rb files and rerun."}
{If the plan isn't Plus: "Scripts were available only on Shopify Plus. If this store was never on Plus, it could not have had Scripts."}
{If the customizations report listed non-Scripts items: "Other customizations on the report, not covered by this audit: {names}."}
{If the check question was asked: "Asked the PM on {date} whether the store ever had Scripts: {answer / no answer}."}

## Sources and method
Last verified against Shopify documentation: 2026-11-04. Report URL and behaviour: Shopify Help Center "Transitioning from Shopify Scripts to Shopify Functions". Read-only: nothing was changed.
```

In the HTML, Variant A is the page head, a `banner ok` with the result line, the "What I checked" table, "Things the PM may want to check" and "Sources and method". Nothing else.

**Real-world example (anonymised, 2026-11-04):** admin handle `ab12cd-ef`, website `storea.example`. `/settings/checkout/scripts-report` redirected to `/settings/checkout/customizations-report` and showed "You have no existing customizations that require action." `/apps/script-editor` showed "You don't have this app installed". If the `?tab=scripts-reports` view isn't explicitly seen, this is **Nothing to migrate (Likely)**, plus the check question. If the Scripts tab was explicitly seen empty, it's **Confirmed**.

---

## Variant B — Full audit

```markdown
# Scripts to Functions audit: {Store name}

{primary domain} · admin handle {handle} · {plan} · {YYYY-MM-DD} · {run mode} · **{a} lost · {b} partial · {c} replaced**

> **Fix first:** {the top-ranked rule in plain words: who is affected and what goes wrong today, then the fix by plain name, e.g. "Anyone, including guests, can choose Pay by Invoice at checkout. Build the invoice rule (D3) this week."}

## 1. Summary
- Shopify turned off all Scripts on June 30, 2026. This store had **{n} Scripts** ({x} line item, {y} shipping, {z} payment), containing **{r} rules**.
- Today: **{a} LOST**, **{b} PARTIAL**, **{c} REPLACED**, **{d} never ran**.
- Do first: 1) {plain fix name} ({F#/D#}, {owner}, {P#}) 2) {…} 3) {…}
- Biggest risk: {one line, plain names, e.g. "Codes now stack differently from before (W1)."}
- {Only if a deadline or planned code was named: "Before {code or event} on {date}: {the decision or fix it needs}."}
- Work split: **{f} fixes the PM can do in the admin**, **{g} developer specs**, **{h} gaps** that need a merchant decision.

## Store details and words used in this report
| | |
|---|---|
| Store | {store name} |
| Admin handle | {handle} (found via {store switcher / address bar}) |
| Website | {primary domain} · myshopify: {…} |
| Plan | {plan} {— "not Plus: custom Functions unavailable" if so} |
| Store currency | {code} |
| Shipping setup | {shipping profiles / market-driven} |
| Markets | {each active market and its countries} |
| Audit date | {YYYY-MM-DD} |
| Run mode | {Browser / Manual / mixed — which steps} |
| Shopify-built apps policy | {Default: optional alternatives only / Agency allows as main fixes} (asked the PM on {date}: {answer}) |
| Deadlines and planned promotions | {e.g. "Black Friday Nov 27; code BFCM26, 20% off, Nov 27–30, combinations not decided" / none named} |
| Test checkouts | {test customer accounts or development store: … / none known} · Sign-off: {who signs off on discounts, shipping, payments} |

Confidence labels: **Confirmed** = seen directly · **Likely** = strong indirect evidence · **Unverified** = not checked; see section 10.
Status labels: **LOST** = shoppers no longer get it · **REPLACED** = an active replacement does the same · **PARTIAL** = a replacement exists but differs · **NOT APPLICABLE** = never ran.

> **Words used in this report**
> **Shopify Script**: a small program that changed prices, shipping or payment options at checkout; all were turned off on June 30, 2026. **Deactivated / Unpublished**: Script Editor badges; Deactivated = it was running when Scripts were switched off, Unpublished = a draft that wasn't. **Rule**: one thing a Script did (one condition, one effect). **Shopify Function**: Shopify's replacement for Scripts; a developer builds it as a custom app (Shopify Plus only). **Native setting**: something set up in the Shopify admin without any app. **Combinations**: the setting on each discount that says which other discounts it can stack with. **Customer segment**: a saved group of customers (for example "tagged VIP") a discount can be limited to. **Rollout**: Shopify's way to launch or test a change for some shoppers (Markets > Rollouts). **Test checkout**: going through checkout up to the payment step, looking, and leaving without paying. **P1 / P2 / P3**: fix this week / this month / backlog.

## 2. Script inventory
| ID | Script name | Type | Published before June 30? | Code source | Rules | Script status | Confidence |
|---|---|---|---|---|---|---|---|
| S1 | {name} | {line item / shipping / payment} | {Yes (badge Deactivated) / No (badge Unpublished) / Unknown} | {Script Editor / report link / agency copy / description only} | {S1.R1–S1.R3} | {status} | {…} |

Report sections and "Auto detected" counts: Payment gateways {n}, Shipping {n}, Product discounts {n}. Reconciliation: {how the counts map to the rules above}.

## 3. Priority list (LOST and PARTIAL only, ranked by revenue impact)
| Priority | Rule | What shoppers lost | Orders affected (90 days) | Fix | Owner |
|---|---|---|---|---|---|
| {P1 this week / P2 this month / P3 backlog / Monitor} | {plain rule name} ({S#.R#}) | {one line} | {n of N orders (source) / "PM: few" / Not checked} | {plain fix name} ({F#/D#/G#}) | {PM / Developer / Merchant decision} |

Inputs: {one line: method and windows, e.g. "Last 90 days of Analytics (Aug 6 – Nov 3, 2026) as a stand-in"}

### How the priority was scored
{full rubric table exactly as in priority-rubric.md section 4, then the input notes: sources per rule, Unverified inputs, overrides, deadline and planned-promotion rules applied, tie-breaks used}

## 4. Script-by-script findings
### S1. {Script name} — {type} — {Script status}
**What it did, in plain English:** {one or two sentences}

#### S1.R1 {short name}
- **What it did:** {1–2 plain sentences; visible in the HTML}
- **Status today:** {LOST / REPLACED / PARTIAL / NOT APPLICABLE} ({confidence}) — {one line}
- **Fix:** {plain fix name (F#) (PM) / plain fix name (D#) (developer) / none — REPLACED / none — never ran}
- **Who:** {…}
- **What:** {…}
- **When:** {…}
- **Message shoppers saw:** "{…}" / none
- **Was live before June 30:** {Yes / No (reason) / Unknown} ({confidence})
- **Pattern:** {ID — name} (runners-up: {IDs / none})
- **Class:** {product / product + order / product + order + shipping / shipping / none} (from `script-reading-guide.md` section 1)
- **Evidence:** {pages checked and what was seen, incl. places with nothing — format from status-verification.md section 5}
- **Gap:** {G# / none}
- **Tests:** {T#}
- **Notes:** {report vs code disagreements, bugs, units, hard-coded references and whether they still exist}

{repeat for every rule, then every script}

## 5. PM can do this (click-by-click)
> Make these changes only after the merchant approves. Claude made no changes during this audit. If a button or label in the admin looks different from these steps, stop and check with your agency lead before saving anything; don't guess.

### F1. {plain name} — fixes {S#.R#} — {P#} — {confidence}
- **What this sets up:** {one line} {If rule 2a made it an interim: "Interim until {plain name} ({D#}) is live."}
- **Before you start:** {prerequisites, e.g. "do F2 first (create the collection)"} · Plan: {all plans}
- **Steps:**
  1. {exact admin path and labels from replacement-map.md, filled in with this store's values}
  2. …
- **Check it worked:** run {T#}.
- **How close this is to the old Script:** {Exact / Close / Partial (interim)} — {difference}
- **Optional alternative (Shopify-built app):** {… / none} {only if allowed by policy, and only where replacement-map.md lists one}

## 6. Needs a developer
> Specs only, no code. A custom Shopify Function needs a custom app created in the Dev Dashboard, and it works only on Shopify Plus.
{Only if the PM said the merchant prefers apps or named an app budget, add exactly one line: "The merchant prefers apps where possible. Your agency evaluates third-party apps separately; this audit doesn't."}

### D1. {plain name} — replaces {S#.R#} — {P#} — {confidence}
1. **Goal (plain English):** {…}
2. **Function API and target:** {API} → `{target}` · operation(s): `{…}` · API version at audit: 2026-10 (developer uses current stable)
3. **Plan and turning it on:** Shopify Plus required. Merchant activates it at {path from replacement-map.md N14}.
4. **Inputs needed:** {cart lines: quantity, cost, product tags/vendor/type/collections · buyer: customer tags, number of orders · delivery address · selected delivery option · cart/line attributes · metafields} · estimated input-query cost {n}/30 (costs per `replacement-map.md` section 4: tag, collection and metafield checks 3 each, other leaf fields 1 each; show the sum)
5. **Configuration (editable without code):** {e.g. JSON in a metafield on the discount/customization with keys …} · values from the old Script: {…}
6. **Logic (plain steps; pseudocode at most):**
   1. {…}
   2. {…}
7. **Output and messages:** {operation; exact shopper message "{…}"}
8. **Discount combinations (Discount Functions only):** {classes} — old Script stacked with everything; desired now: {…}
9. **Where it will run:** {cart / checkout / accelerated checkout / POS / draft orders / B2B} — wanted? {…}
10. **Edge cases to handle:** {rule-specific} + guests (no customer), multiple currencies/markets, gift cards, subscriptions/selling plans, mixed carts, very large carts, other discounts or codes present (including planned codes from the store details), address not yet entered
11. **Limits to respect:** max 25 active functions of this type ({current count}); 11M instructions; 20 kB output; 128 kB input; query cost 30
12. **How close this is to the old Script:** {Exact / Close / Partial} — {differences}
13. **How to test (acceptance):** {T# list} plus checking the app's Functions page shows no "Errors on [n] area"
14. **Open questions for the merchant:** {…} {For a P1 spec: the interim option from replacement-map.md rule 8, as a merchant decision}

## 7. Gaps (can't be reproduced exactly)
### G1. {what can't be reproduced} — affects {S#.R#}
- **Decision needed from the merchant:** {who decides} — {accept the closest option / choose another / drop it}
- **Why:** {reason} [{source ID}]
- **Closest option:** {plain name (F# / D#)} — {what shoppers will see differently}

## 8. Test-checkout checklist
Go up to the payment step and leave. Never pay.
{one line per test: "T1. {short name}: checks {plain rule name} ({S#.R#}). Expected today: {…}."}
{rules box from test-checklists.md section 1, then the Pass / Fail rule from section 2}
{T1… cards, then TW… store-wide tests, in the format from test-checklists.md section 2}

## 9. Store-wide warnings
{each applicable W# from replacement-map.md section 6: a bold title line, then one short paragraph (3 sentences at most) on why it applies to this store; W1 names every active and planned code}

## 10. Things the PM must check
| ID | What to check | Where / how | Why it matters | Related |
|---|---|---|---|---|
| C-PM1 | {…} | {click path} | {…} | {S#.R# / F# / D#} |

## 11. Coverage check
{the table below, filled with results}

## 12. Sources and method
- Run mode and pages read: {list with URLs/click paths; for manual mode, files and screenshots received}
- CSV columns found (manual mode): {header names exactly}
- Stop-and-ask events: {none / list}
- Facts and paths: `sources.md` of this skill — last verified against Shopify documentation 2026-11-04. Key pages: {cite the source IDs used}
- Read-only statement: "No settings, discounts, apps, carts or orders were changed during this audit."

## Appendix A. Original Script code (reference only — these Scripts no longer run)
{Script name, code source, and the code as obtained. If a script is longer than 200 lines, include the configuration part and say where the full file is. The 15-word quote limit doesn't apply here.}
```

---

## Coverage check (run before the audit is final; put the filled table in section 11)

| # | Check | Pass when |
|---|---|---|
| CV1 | Script count | Every script in the Scripts report's Auto detected lists and in Script Editor is in the inventory (state N = N) |
| CV2 | Customization count | Each section's Auto detected count is reconciled with the rules found |
| CV3 | Code source | Every script has a code source recorded, or "description only" |
| CV4 | Rule cards | Every rule has Who, What, When, Message, Was live, Pattern, Class, Confidence |
| CV5 | Status evidence | Every rule has a status and evidence that lists the places checked (from `status-verification.md` section 2, including Markets > Rollouts for discount rules), including the empty ones; discounts were opened by the fixed selection rule in `intake-browser.md` section 7. A place the PM was asked for but couldn't show counts as not checked: write "No — {place} not seen" and add its PM check. That is normal in manual mode and doesn't block the report |
| CV6 | Fix or gap | Every LOST/PARTIAL rule has a priority and at least one F#, D# or G# |
| CV7 | PM steps | Every F# uses paths from replacement-map.md, filled with store values, or is flagged "re-check live" |
| CV8 | Developer specs | Every D# has all 14 fields and contains no deployable code |
| CV9 | Tests | Every LOST/PARTIAL/REPLACED rule has at least one test, and no {placeholders} are left anywhere |
| CV10 | No third-party apps | No app built by anyone other than Shopify is named as a fix; no third-party name from the report's "Recommended apps" appears anywhere; Shopify-built apps appear only where `replacement-map.md` lists them, as labelled optional alternatives (or per the recorded policy) |
| CV11 | Unverified items | Every Unverified label has a matching row in section 10 |
| CV12 | Warnings | Every applicable W# is included, and W1 names the planned codes from Step 3 |
| CV13 | Plan | The plan was read; if it isn't Plus, every D# and Checkout Blocks option is flagged and gaps are added |
| CV14 | Safety log | No forbidden click, typing or script was used in the admin; stop-and-ask events are listed |
| CV15 | File and readability | Saved as `{handle}-scripts-to-functions-audit-{date}.html` and `.md` in the same order, or the failure is stated. HTML structural checks: style block identical to report-template.html, example banner and guide comment removed, tags balanced, only the template's classes (no inline styles). Readability: about 1,500 visible words or less, no ID alone in banner / summary / top fixes / priority list, no paragraph over 3 sentences |

If any check fails and can't be fixed in this run, write **"No — {reason}"** in the table and add a row in section 10. Never mark a check "Yes" without doing it.
