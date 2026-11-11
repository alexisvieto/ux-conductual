# Before and after

Patterns in generic HTML and React. Translate them to the project's components
and tokens: here `btn`, `field`, and the colors are illustrative.

## 1. Button that triggers work (feedback + double submit)

**Before.** No loading state: the user taps twice and creates two orders.

```tsx
<button onClick={save}>Save</button>
```

**After.** Shows it's working, disables itself, and confirms.

```tsx
const [status, setStatus] = useState<"idle" | "saving" | "ok" | "error">("idle");

async function onSave() {
  setStatus("saving");
  try { await save(); setStatus("ok"); toast("Invoice saved"); }
  catch { setStatus("error"); }
}

<button onClick={onSave} disabled={status === "saving"} aria-busy={status === "saving"}>
  {status === "saving" ? "Saving…" : "Save invoice"}
</button>
{status === "error" && <p role="alert">We couldn't save. Check your connection and try again.</p>}
```

Principles: immediate feedback, error prevention, microcopy (verb + object).

## 2. Form field (label, example, keyboard, helpful error)

**Before.**

```html
<input placeholder="Phone">
<span class="error">Invalid input</span>
```

**After.**

```html
<label for="tel">Phone</label>
<input id="tel" type="tel" inputmode="tel" autocomplete="tel"
       placeholder="e.g. 555-0100" aria-describedby="tel-error" aria-invalid="true">
<p id="tel-error" role="alert">Some digits are missing: enter a 10-digit phone number.</p>
```

Principles: visible label (the placeholder is an example), correct keyboard,
autofill, an error that says what happened and how to proceed. Accept `555 0100`
and `5550100` on the server (Tesler).

## 3. Destructive confirmation (context + button that names the action)

**Before.**

```text
Are you sure?       [Cancel] [OK]
```

**After.**

```text
Delete 3 invoices
Invoices 104, 105, and 106 and their recorded payments will be deleted.
This can't be undone.
                    [Cancel]  [Delete 3 invoices]  ← danger color; initial focus on Cancel
```

Even better, if possible: move to trash and show a toast
"3 invoices moved to trash · Undo".

Principles: reversibility, prevention, microcopy.

## 4. Empty state (teaches the next step)

**Before.**

```text
No data.
```

**After (first use).**

```text
Your invoices will show up here
Create your first one and we'll let you know when the customer opens it.
[Create invoice]
```

**After (filter with no results).**

```text
No invoices match "overdue · March"
[Clear filters]
```

Principles: empty states, Fogg (prompt + ability), recognition.

## 5. Quota or limit (honest framing)

**Before.** `You've used 47 of 50 sends`

**After.** `3 sends left this month · Resets December 1`

Principles: framing, warning before the limit, no false pressure.

## 6. AI agent about to act (confirm before sending)

**Before.** The agent sends the email right after drafting it.

**After.**

```text
I'm about to send this email to ana@customer.com:
  Subject: Reminder for invoice 104
  [editable text preview]
[Edit]  [Send email]
```

Principles: prevention, trust, editable output.

## 7. Cookie consent (ethics)

**Before.** `[Accept all]` highlighted; "Settings" as a gray link.

**After.** `[Reject]` and `[Accept]` with equal visual weight, and
"Choose what to allow" as a clear third option.

Principles: ethics, GDPR (rejecting as easy as accepting).
