# Priority rubric: rank by revenue impact (Step 10)

Every **LOST** and **PARTIAL** rule gets a priority **P1 / P2 / P3** (or "Monitor"). REPLACED and NOT APPLICABLE rules are not ranked; REPLACED rules still get tests. Show the inputs and the arithmetic in the report so the PM can see why.

---

## 1. Gather inputs (fixed choice)

Pick the first method that works and use it for the whole run. Say which one in the report.

1. **A. Analytics windows.** Analytics > Reports opens (browser mode), or the PM can send the M7 screenshots for both windows (manual mode).
2. **A90. Last 90 days only.** The PM can't get the windows but has last-90-days numbers (the Analytics overview, or reports set to "Last 90 days"). This is what most PMs have.
3. **B. Three questions.** Neither works.

Only exception: if the chosen method gives no number for a particular rule, ask B's question 2 for that rule alone and mark its input **Unverified**.

### A. Analytics, read-only (browser: `intake-browser.md` section 8; manual: step M7)

Use two windows: **Apr 1 – Jun 29, 2026** (Scripts running) and **Jul 1 – Sep 29, 2026** (Scripts off). If the store has 2025 data, also look at the same months of 2025 to see whether a change is just seasonal.

| Rule type | Report(s) | What to read |
|---|---|---|
| Store size (all) | Sales > **Total sales over time** | Average monthly total sales over the last 3 full months (Aug–Oct 2026) |
| Product/order discounts (L-patterns) | Sales > **Sales by discount codes** (column **Non-shipping script discounts**, Plus stores only); Finances > **Total sales breakdown** | The script discount column for Apr 1 – Jun 29, 2026 shows how much money line item Scripts gave away (it proves they were live and gives their cost; it is **not** the share touched). For the share touched: if the report has rows for the Script's discounts (Unverified whether it does; for example rows named after the Script's message), use those rows' sales ÷ total sales in the window (the report counts only the sales of lines the discount affected). Otherwise A gives no share for this rule: use the exception above (B's question 2, Unverified). Don't use **Discounts by order** for this — the Help Center describes it as discount codes and POS discounts, so it may not include Script discounts. |
| Spend thresholds / tiers (L3, L11, S9) | Sales > **Average order value over time** | AOV shift after June 30 near the threshold amounts |
| Shipping discounts (S9–S11) | Sales > **Sales by discount codes** (column **Shipping script discounts**, Plus only); Finances > **Shipping by order** | Shipping script discount money in Apr 1 – Jun 29, 2026, and the share of orders on the affected rates |
| Shipping hide/rename/reorder rules (S1–S8, S12, S13) | Finances > **Shipping by order**; Orders export column "Shipping Method" (PM export) | Share of orders using the affected rate(s) or going to the affected regions |
| Payment rules (P-patterns) | Finances > **Net payments by method** / **Net payments by gateway** (or the Finance summary cards "Payments by method" / "Payments by gateway") | Share of orders on the affected method; a method that should be hidden (e.g. COD on big orders) gaining share after June 30 is evidence the loss matters |

Viewing reports needs the staff **Reports** permission. Never save a report.

### A90. Last 90 days only (the PM's numbers)

Use the same 90 days for every number, and write the dates (for example "Aug 6 – Nov 3, 2026"). Share = orders the rule's condition touches in those 90 days ÷ all orders in the same 90 days.

| Rule type | Number to use |
|---|---|
| Store size | Total sales for the 90 days ÷ 3 = monthly sales |
| Discount rules with a live replacement | Orders using that replacement discount |
| Discount rules with no replacement | No number (the lost discount leaves no trace) → B question 2 for that rule |
| Shipping rules | Orders on the affected rate(s), or to the affected countries |
| Payment rules | Orders on the affected payment method |

Label every A90 input **"stand-in (last 90 days)"** in the report: it shows behaviour after June 30, not before. If the 90 days include days before July 1, say so. A stand-in counts as a measured input for the tie-breaks (section 2).

### B. Three questions to the PM (when Analytics isn't available)

Ask one at a time:

1. "Roughly how much does this store sell per month, and about how many orders? A band is fine: under $10k, $10k–$100k, $100k–$1M, over $1M."
2. "Before June 30, about how many orders out of every 100 did each of these touch? 10 or more, 3 to 9, fewer than 3, or don't know. Just reply next to each:" then list the LOST/PARTIAL rules by short name, e.g. "VIP 15% off — ?", "No COD over $500 — ?".
3. "Are any of these tied to something customers or suppliers were promised (wholesale terms, a VIP program, an advertised offer, a brand's pricing rules), or to a legal, carrier or fraud rule (for example, products you can't ship to some states)?"

**Turning answers into the percentage scale (section 2):**
- A number always wins over a word. Convert counts with the monthly orders from question 1: "15 a month" at 1,400 orders a month = 1.1% → I = 1. "About a third" = 33% → I = 3.
- Words with no number: "most", "many", "a lot", "about half" → 3; "some" → 2; "few", "a handful", "rarely" → 1.
- "Don't know" → 1, and mark the input **Unverified**.

---

## 2. Score each LOST / PARTIAL rule

**Impact (I), 0–3** — share of orders or revenue the rule touched before June 30:
- **3** = 10% or more, **or** it carries a named customer program sold to regularly (wholesale, VIP)
- **2** = 3% to under 10%
- **1** = under 3%, or unknown but plausible
- **0** = evidence it touched nothing (e.g. it only referenced products that no longer exist)

**Risk flags (+1 each, at most +2):**
- **Margin leak** — today discounts apply more widely or stack more than intended (e.g. VIP discount now open to all, codes now stacking with a sale or winning over it, excluded products now discounted, two replacements both applying). A **planned** code or sale from Step 3, starting within the next 60 days, that with today's settings would stack with the rule's replacement or win where the Script refused codes also sets this flag.
- **Broken promise** — customers or suppliers were promised this price or term (advertised offer, VIP/wholesale terms, a supplier pricing agreement such as MAP).

**Override — legal, carrier, fraud or safety rule (always P1, whatever the score).** Only these count:
- **Legal:** a law or regulation limits who can buy or where it ships (restricted goods, age limits).
- **Carrier:** the carrier can't deliver what checkout now offers (for example UPS rates to PO boxes).
- **Fraud or credit:** shoppers can now get goods without paying up front or without approval (for example a pay-later or invoice method open to everyone).
- **Safety:** shipping or selling the item is unsafe (hazardous goods to some regions).

Supplier pricing agreements (MAP), finance preferences (an invoice minimum) and marketing promises are **not** overrides: they score through I and the flags.

**Status adjustment:** LOST = 0; PARTIAL = −1 (but never below 1 if any flag is set).

**Score = I + flags + status adjustment.**

| Score | Priority | Meaning for the PM |
|---|---|---|
| 4 or more (or override) | **P1** | Fix this week |
| 2–3 | **P2** | Fix this month |
| 1 | **P3** | Backlog |
| 0 | **Monitor** | No fix needed now; re-check if the merchant relaunches it |

**Deadlines and planned promotions (from Step 3), applied after the score:** a rule whose fix the merchant needs by a date within the next 60 days, or that a planned code or sale starting within the next 60 days interacts with (Margin leak above), is **at least P2**. Write "Needed by {date}" or "Before {code} on {date}" in the Why column. A deadline is a date the merchant needs a fix by; it applies to every rule that fix covers. "It can wait until {month}" is not a deadline.

**Tie-breaks within a band (in this order):**
1. Override rules first (they are P1 because of a risk, not a score).
2. Higher I first.
3. Earlier merchant deadline first. A fix the merchant called urgent counts as due today; no deadline comes last.
4. PM-doable fixes before developer fixes (faster wins).
5. Higher **status** confidence first (Confirmed > Likely > Unverified).
6. Higher **impact-input** confidence first: Analytics windows (A) > last-90-days stand-in (A90) > a PM number > a PM word or "don't know" (Unverified).
7. Lower script number, then lower rule number.

---

## 3. Optional money estimate

Only when you have numbers from A: **estimated monthly revenue touched = share of orders affected × average monthly total sales**. Label it "estimate", round to two significant figures, and never present it as lost revenue (the rule may have been a discount, i.e. it *reduced* revenue per order while helping conversion). Write: "This rule touched about $X of sales per month before June 30 (estimate)." No estimate from A90 or B inputs.

---

## 4. How it appears in the report (section 3)

**Visible table: six key columns.** It matches `report-template.html`. Plain name first, ID after, in the Rule and Fix columns.

| Priority | Rule | What shoppers lost | Orders affected (90 days) | Fix | Owner |
|---|---|---|---|---|---|
| P1 this week | Hide COD over $500 (S1.R2) | COD is offered on any order size again | 180 of 4,000 (Analytics) | Hide COD over $500 (D1) | Developer |
| P2 this month | VIP 15% (S2.R1) | The new VIP discount is open to all customers | Not checked | Limit the VIP discount to the VIP segment (F2) | PM |

"Orders affected (90 days)" is the last-90-days count with its source, "PM: {answer}", or "Not checked". Owner is **PM**, **Developer** or **Merchant decision** (when a G# decision comes first).

**Folded table: "How the priority was scored"** (inside `<details>` in the HTML; a sub-heading in the Markdown). Fixed columns:

| Rank | Rule | Status | I | Flags | Adj. | Score | Priority | Why (one line) | Fix type | Fix ID |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | S1.R2 Hide COD over $500 | LOST | 2 | — | 0 | 2 + override | P1 | Fraud rule; COD share on $500+ orders rose after June 30 | Developer | D1 |
| 2 | S2.R1 VIP 15% | PARTIAL | 3 | margin leak | −1 | 3 | P2 | Replacement open to all customers | PM | F2 |

Under it, the input notes: the method (A / A90 / B) and dates, each rule's input source, Unverified inputs, overrides, deadline and planned-promotion rules applied, and which tie-break decided each tie. Show the one-line input source under the visible table too: "Inputs from Analytics (windows …)", "Inputs from the last 90 days (dates), as a stand-in" or "Inputs from PM answers on {date} (Unverified)".
