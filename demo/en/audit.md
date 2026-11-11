# Real audit of the demo

We asked Claude, with the skill installed, to audit the invoice screen in **AUDIT mode**. This is its output translated from the original Spanish run ([`../auditoria.md`](../auditoria.md)); the findings and severities are unchanged. Screens: [`before.html`](before.html) and [`after.html`](after.html).

> Prompt: *"Audit this New invoice screen. User: small business owner, on their phone, between other tasks; wants to bill fast and fears sending a wrong invoice."*

---

**Step 0:** plain HTML/CSS, no design system, tokens or components. The fixes use native HTML (`<label>`, `type`, `inputmode`, `<input type="date">`) and don't add raw colors: status tokens (success, danger, primary) should be defined first, since today there are 4 colors with no meaning. The copy mixes formal and informal voice. No icons.

**User:** small business owner. Uses their phone one-handed, between other tasks, and gets interrupted. Wants to bill a client they usually already know, fast. Fears sending an invoice with wrong data or amounts, or sending it twice.

| # | Finding | Principle | Severity | Where | Fix |
|---|---|---|---|---|---|
| 1 | The "Send a copy to our business partners" checkbox comes pre-checked: it shares the client's data with third parties if the user doesn't notice, and a pre-checked box is not valid consent | Ethics: sneaky default / defaults | 4 | `before.html:42` | Remove it. If truly needed, unchecked, explaining what is shared and with whom, with a clickable label |
| 2 | To decline Pro you must read "No thanks, I prefer to keep losing clients", which blames the user. It's also a 9 px `<small>` in #bbb and not even a button: declining costs far more than accepting | Ethics: confirmshaming / leaving as easy as joining | 4 | `before.html:51` | A neutral "Not now" button the same size as "I want Pro", informative copy, no guilt |
| 3 | "Send" fires the invoice immediately, with no preview or summary (to whom, how much, when due) and no warning of consequences, exactly what the user fears | Error prevention / announce consequences first | 3 | `before.html:45` | Show a summary with context before sending and a button that names the action: "Send $X invoice to client@email" |
| 4 | "Delete" sits next to "Save" and "Send", same size, no confirmation or undo. With small targets and one hand, a mis-tap is easy and the work is lost | Reversibility / Fitts (destructive away from frequent) | 3 | `before.html:46` | Move it out of the main row (menu or tertiary link) and offer "Undo" or a confirmation with context |
| 5 | 4 buttons with the same weight and 4 different colors, none primary. Color means nothing (PDF orange matches the ad) and the main action is unclear | Hick / Von Restorff / single primary | 3 | `before.html:43` | One primary ("Review and send"); "Save draft" secondary; "PDF" tertiary or inside the preview |
| 6 | The user types "Sales tax" and "Total" by hand although the system can compute them from quantity × price. A direct source of invoices with wrong amounts | Tesler / don't ask what the system knows / prevention | 3 | `before.html:39` | Compute subtotal, tax (default rate, editable) and total, read-only and live |
| 7 | Client, tax ID, email and phone are typed from memory every time, although the client usually already exists | Recognition over recall / WCAG 3.3.7 | 3 | `before.html:31` | Client picker with search that fills tax ID, email and phone, plus "New client" |
| 8 | Placeholders act as labels: they vanish while typing and, after an interruption, the user doesn't know which field is which. Screen readers get no accessible name | Visible label / working memory | 3 | `before.html:31` | A visible `<label>` per field; placeholder only as an example |
| 9 | "Error: invalid input" appears at the top before the user does anything. It doesn't say which field fails or how to fix it, isn't next to the field and has no `role="alert"` | Useful feedback / prevention over error messages | 3 | `before.html:30` | Validate on blur, message next to the field ("Client tax ID is missing"), `role="alert"` / `aria-describedby` |
| 10 | No "Sending…" state, no success confirmation, no protection against double taps on Save or Send: risk of a duplicate invoice or not knowing if it went out. It's a static mock, but the design doesn't define those states | Immediate feedback / double submit | 3 | `before.html:44` | Disable and show "Sending…"; on completion confirm ("Invoice #123 sent to …") with the next step |
| 11 | Buttons ~28 px tall, inputs ~30 px and a native checkbox without a clickable label, all below 44–48 px for one-handed use | Fitts / touch targets | 2 | `before.html:17` | At least 44–48 px tall for buttons and inputs; checkbox inside a `<label>` |
| 12 | Dates as free text; the issue date doesn't default to today and the due date offers no usual terms | Defaults / recognition over recall | 2 | `before.html:35` | `type="date"` defaulting to today; due date with options (on receipt, 15, 30 days) |
| 13 | Currency has no default ("Currency" as an option) and sits after Total, in an illogical order | Defaults / natural task order | 2 | `before.html:41` | USD by default, next to price or total, or in settings |
| 14 | 11 fields in a single column with no groups or titles (client, dates, details and amounts mixed) | Gestalt / working memory (~4 chunks) | 2 | `before.html:31` | Group into "Client", "Details" and "Totals", with titles and more space between groups than within |
| 15 | Email, phone, quantity and price without `type` or `inputmode`: the phone shows the text keyboard | Jakob / less friction | 2 | `before.html:33` | `type="email"`, `type="tel"`, `inputmode="decimal"` for quantity and price |
| 16 | The Pro ad competes with the task inside the invoicing form | Hick / attention on the main task | 2 | `before.html:50` | Move it out of the flow; at most show it after a successful send, without pressure |
| 17 | The "No data" empty state doesn't say what the list is or what to do | Empty states teach the next step | 2 | `before.html:49` | "You haven't issued invoices yet. Your first one will appear here", or remove it from this screen |
| 18 | Contrast below AA: "help" in #999 at 11 px, the list in #aaa, the decline link in #bbb at 9 px and the checkbox text in #777 (~4.48:1, just under 4.5:1) | AA contrast / aesthetic-usability | 2 | `before.html:13` | Raise secondary text to ≥4.5:1 and at least 13 px |
| 19 | Fixed 390 px width: on 360 px phones there will be horizontal scroll | Mechanics / responsive | 2 | `before.html:10` | `max-width: 390px; width: 100%` |

**The 3 highest-impact fixes**
1. Remove both dark patterns: the pre-checked "business partners" box (unchecked or removed) and the Pro confirmshaming (neutral "Not now" button).
2. Before sending, show a summary (client, total, due date) and a single primary button "Send $X invoice to …", with a "Sending…" state and a success confirmation; "Delete" leaves the row.
3. Let the system do the work: client picker that fills tax ID and email, tax and total computed, today and USD by default, visible labels and errors next to each field.
