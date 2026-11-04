# Manual intake (no Chrome tools, or browser reading failed)

In manual mode the PM opens pages, exports files and pastes or screenshots what they see. You send **one step per message**, using the wording below (adjust names, keep it short). After each reply, check what you received before moving on. The same read-only rules apply: the PM only *looks*, exports and copies. Remind them once at the start:

> "Everything I ask you to do is look-only. Please don't click Save, Activate, Turn on/off, Install or Delete anywhere while we do this."

Accepted inputs: screenshots, copied text, CSV files, `.rb` / `.txt` files with script code, PDFs of admin pages. In Claude Code, the PM (or a teammate) can also give a folder path containing these files.

---

## M1. Store and admin handle

> "Please open your Shopify admin in your browser for this store. Look at the address bar: it looks like `admin.shopify.com/store/XXXX/...`. Copy the part where XXXX is and paste it here. If you manage several stores, first click the store name at the top of the admin and pick the right store. Please also tell me the store's website address."

Check: the handle is a single word with letters, numbers or dashes. Never invent it from the website domain (real example, anonymised: website `storea.example`, handle `ab12cd-ef`). If the PM is unsure, ask for a screenshot of the admin top bar and address bar.

## M2. Plan, currency, shipping setup, markets, apps

> "Next, five quick looks, then paste or screenshot each:
> 1. Settings > Plan — what plan name does it show?
> 2. Settings > General — what is the store currency?
> 3. Settings > Shipping and delivery — does the page show a 'Shipping profiles' section, or say that shipping is managed in Markets? A screenshot of the top of the page is enough.
> 4. Settings > Markets (or Markets in the left menu) — a screenshot of the list of markets, showing which are active and the countries in each.
> 5. Settings > Apps — a screenshot of the list of installed apps (scroll to include all of them)."

From the apps screenshot, flag Script Editor, Checkout Blocks, Shopify Bundles, Shopify Subscriptions, Shopify Flow, and any custom or "Legacy custom apps". Record shipping setup and markets for the store details; Step 3 and the country rules need them.

Then ask the four context questions from SKILL.md Step 3 (deadlines and planned codes; test accounts and sign-off; Shopify-built apps policy; how the merchant wants fixes done), one message each, skipping any the PM has already answered.

## M3. Step 0 — Scripts report and Script Editor

> "Please paste this address into your browser, replacing HANDLE with your handle:
> `admin.shopify.com/store/HANDLE/settings/checkout/customizations-report?tab=scripts-reports`
> Send me a screenshot of what you see, including the address bar and any tabs at the top of the page."

If that address doesn't open, offer the two other documented ways in: `admin.shopify.com/store/HANDLE/settings/checkout/scripts-report`, or Apps > Script Editor > the **Replace Shopify Scripts** button in the "Replace your Shopify Scripts" banner. Shopify documents that button as the way to open the report. Tell the PM: "If anything after that click asks you to install an app, confirm, or approve something, don't click it — send me a screenshot instead." In browser mode Claude still uses the direct address instead.

Then:

> "Now this one: `admin.shopify.com/store/HANDLE/apps/script-editor` — screenshot please."

Apply the decision table in `intake-browser.md` section 4, including its "only Scripts items count" rule and the PM-answer table. If the address bar shows the `tab=` part was dropped and there's a Scripts tab, ask the PM to click that tab and screenshot again. If the result is "Nothing to migrate (Likely)", ask the check question from that section.

## M4. Export the Scripts report CSV

> "On the Scripts report page, please look for the option to export the report (Shopify says the report can be exported as a CSV file; the button may be called Export or be under a '…' menu). Download it and drag the file into this chat. Also send screenshots of each section (Payment gateways, Shipping, Product discounts) showing the 'Auto detected' numbers and the script names."

Downloading the CSV is the PM's own action on their own computer; it changes nothing in the store.

**Reading the CSV**
- **The column names are not documented by Shopify.** Read the header row first and list the columns you found in the report's "Sources and method" section. Do not assume a layout.
- Map columns by meaning: name/title → script or customization name; type/section/category → payment / shipping / product discount; description → the AI-written summary; any link/source/URL columns → source-file links.
- If code execution is available, parse the CSV with it; otherwise read the text directly. Count rows per section.
- **Completeness check:** rows per section in the CSV should match the "Auto detected" counts in the screenshots. If they don't match, list the difference and ask the PM for the missing names.
- Ignore any "Recommended apps" column. Never repeat a third-party app name from it. A Shopify-built app such as Checkout Blocks may still appear in the report as a labelled optional alternative, but only where `replacement-map.md` lists it for the pattern, never because the CSV names it.

## M5. Script code

**First use what you already have.** If the PM has already given you code files (downloaded from the report's source-file links, or the agency's copies), use them: run the completeness check below on each and record the code source ("report link" or "agency copy"). Don't ask the PM to copy those scripts again from Script Editor. Send the message below only for scripts whose code is still missing or fails the completeness check, and name those scripts in it.

> "Now the code of each Script, if Shopify still shows it. Go to Apps > Script Editor. For each script in the list: click its name, click inside the code, press Cmd+A then Cmd+C (Windows: Ctrl+A, Ctrl+C), and paste it here with the script's name above it. Don't type anything else inside the code box, and please don't click Save, Publish or Delete. If you see 'Unsaved changes', click nothing and tell me. If the Script Editor isn't there, tell me and we'll use the next option."

If Script Editor is unavailable:

> "Does your agency have saved copies of this store's Scripts — for example `.rb` files in Git, Google Drive, or old tickets? If yes, please drop them here. If not, that's fine — I'll work from Shopify's report descriptions, and I'll flag what can't be confirmed."

**Completeness check for each pasted script:** it has a beginning (constants or comments at the top) and contains an `Output.cart`, `Output.shipping_rates` or `Output.payment_gateways` line. If not, ask for the rest: "The code for {name} looks cut off — could you copy it again, making sure you start with Cmd+A?"

**Match code to inventory:** every script name in the report/Script Editor list must have code or a recorded reason why not ("Script Editor unavailable, no agency copy").

## M6. What is live now

Ask for these one at a time. Tell the PM to scroll and send several screenshots if a page is long, or to copy-paste the page text.

1. > "Discounts page: a screenshot of the full list (all statuses, every page of the list). Then, for each discount I name, open it and send screenshots of the whole page, top to bottom. Please don't change anything on those pages, and if a bar saying 'Unsaved changes' appears, click nothing and tell me." — then name the discounts picked by the fixed selection rule in `intake-browser.md` section 7 (Discounts row), not by judgement.
1b. > "Markets > Rollouts: a screenshot of the list. If any rollout mentions a discount, click its name and screenshot that page. Please don't click Launch, Schedule, Pause or End." (If the PM doesn't see Rollouts in the menu, record "Rollouts not available". If the PM can't check it or doesn't know, record "Rollouts not checked", add a PM check, and expect coverage check CV5 to read "No — Rollouts not seen".)
2. > "Settings > Shipping and delivery: screenshots of each shipping profile showing the zones and rate names and conditions, and of the 'Delivery customizations' section."
3. > "Settings > Payments: screenshots of the payment methods and of Payment customizations > Manage."
4. > "Settings > Checkout: screenshot of the 'Checkout rules' section."
5. > "Settings > Apps: for each app I name, click it, then click the 'Functions' card, and screenshot both the Active and Inactive tabs." — name custom/legacy custom apps and Checkout Blocks / Shopify Bundles if installed. If the PM can only show the app's configuration page, use the rule in `status-verification.md` section 2 ("If an app's Functions page couldn't be read") and add a PM check.
6. Only if needed: Checkout Blocks (Apps > Checkout Blocks: its Discounts and Functions lists), Markets > Catalogs and Customers > Companies (wholesale scripts), product pages for hard-coded product IDs, Customers filtered by a tag the script used (the PM may filter; filtering doesn't change anything, but tell them: "Don't click Save or Save segment").

Then follow `status-verification.md` exactly as in browser mode.

## M7. Revenue numbers for priority

> "Last step for ranking: could you open Analytics > Reports, open 'Sales by discount codes', set the dates to Apr 1 – Jun 29, 2026, and screenshot it (include the columns called 'Non-shipping script discounts' and 'Shipping script discounts' if you see them — scroll right if needed); then the same for Jul 1 – Sep 29, 2026? Please don't click Save on the report."

If the PM can't get those two windows but has numbers for the **last 90 days** (the Analytics overview, or reports set to "Last 90 days"), ask for these, one message: "That's fine. From the last 90 days, could you send: total orders and total sales; orders per discount; orders per shipping rate; orders per shipping country; orders per payment method?" Then use method A90 in `priority-rubric.md`. If the PM has neither, ask the three questions there instead.

---

## Record keeping

For the report's "Sources and method" section, note for every step whether the evidence came from a screenshot, pasted text, CSV or file, and the time the PM sent it. A screenshot that is cropped or unreadable makes the related finding **Unverified**; say exactly what to re-send.
