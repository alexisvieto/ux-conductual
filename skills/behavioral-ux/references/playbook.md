# Playbook by screen type

For each archetype: the highest-leverage principles, concrete patterns, and
what to avoid. Adapt them to the project's components and tokens.

**Index:** [Form](#form) · [List, inbox, or table](#list-inbox-or-table) ·
[Dashboard](#dashboard) · [Object detail](#object-detail) ·
[Search](#search) · [Checkout and pricing](#checkout-and-pricing) ·
[Permission requests](#permission-requests) · [Destructive actions](#destructive-actions) ·
[Notifications](#notifications) · [Onboarding](#onboarding) ·
[Empty states](#empty-states) · [Login](#login) ·
[AI interfaces](#ai-interfaces) · [Microcopy](#microcopy)

---

## Form

**Principles.** Fitts, Hick, recognition, defaults, error prevention, feedback,
working memory, Tesler.

**Patterns.**
- One submit action, in a comfortable zone (pinned to the bottom on mobile). If
  there's a total or summary, put it next to the button.
- A visible label above each field. The placeholder is a real example
  (`e.g. 555-0100`), never the label.
- Group fields into titled, thematic sections. If most fields are required, mark
  the optional ones ("optional") instead of covering the required ones in
  asterisks.
- Selection instead of free text for known values; prefilled defaults;
  automatic calculations.
- Correct `type`, `inputmode`, and `autocomplete` for the keyboard and autofill.
- Accept flexible formats (Tesler): spaces, dashes, and prefixes in phone and
  card numbers.
- Validate when the user leaves the field; warn about consequences before
  submitting.
- If you block submission, say what's missing. Better yet, allow submission and
  move focus to the first error, with a summary at the top.
- A "Sending…" state and a clear confirmation at the end (peak-end).

**Avoid.** Typed-in totals; free text for catalog values; placeholder as
label; validating as the first character is typed; clearing the user's input
on error.

## List, inbox, or table

**Principles.** Hick (filters), open tasks, Jakob, Gestalt, serial position.

**Patterns.**
- Actionable or urgent items first; sort by real priority.
- A few quick filters (All, Mine, Pending) and search for everything else.
- Scannable rows: key data emphasized, secondary data in a muted color.
- Owner and status visible on every row.
- Mobile: cards. Desktop: a table with a sticky header and aligned columns
  (numbers right-aligned, with tabular figures).
- Minimal per-row actions; the rest in a menu. Bulk actions when several rows
  are selected.
- Badges that clear when the item is resolved, not when it's viewed.

**Avoid.** Walls of identical columns with no hierarchy; counters that lie;
paginating when the user needs to compare.

## Dashboard

**Principles.** Open tasks, attention hierarchy, progress, framing.

**Patterns.**
- "Needs your attention" at the top, with urgent items in a status color and a
  direct link to the action.
- Metrics as progress when there's a goal or limit, not just raw numbers.
- Comparison to a reference (previous period, target) so the number means
  something.
- Content by role: not the same dashboard for everyone.
- A visible context anchor (period, scope).

**Avoid.** A pretty dashboard with no "what do I do now?"; charts that answer
no question.

## Object detail

**Principles.** Progressive disclosure, prevention, reversibility, progress,
feedback.

**Patterns.**
- Actions based on the object's state, not all of them all the time.
- The lifecycle as visible progress (draft → sent → paid).
- History or audit trail in view when it matters (who changed what, and when).
- Inline editing for small changes.

**Avoid.** Showing every action all the time; confirmations without context.

## Search

**Principles.** Recognition, Tesler, feedback, empty states.

**Patterns.**
- A visible field at the top (Jakob), with a keyboard shortcut on desktop (`/` or `Ctrl+K`).
- Suggestions and recent searches on focus; autocomplete while typing.
- Error tolerance: accents, capitalization, plurals, and typos.
- Results with the search term highlighted; filters after searching, not before.
- No results: say what was searched, suggest a correction, and offer to clear
  filters.

**Avoid.** Exact-match search that fails over a single accent; "0 results" with no way out.

## Checkout and pricing

**Principles.** Minimal friction, prevention, honest framing, peak-end, ethics.

**Patterns.**
- Guest checkout; create an account afterward, if the user wants.
- Visible steps with progress; order summary always in view.
- **Total price from the start**: taxes, shipping, and fees included or
  disclosed before the final step.
- Address and card autofill; card type detection.
- For plans: a clear comparison, one highlighted recommended plan (Von Restorff),
  and annual versus monthly pricing without tricks.
- A final confirmation with the order number, what happens next, and when it
  arrives.

**Avoid.** Fees that appear at the end (that's a dark pattern); preselected
insurance or add-ons; mandatory sign-up before payment.

## Permission requests

**Principles.** Fogg (right moment), trust, Jakob.

**Patterns.**
- Ask for the permission **in context**, when the user tries to use the feature
  that needs it (camera on tapping "Scan"), not all at once when the app opens.
- Before the system prompt, show your own screen explaining what the user
  gains. If they decline, don't show the system prompt (it can often be shown
  only once).
- If they deny it, the feature degrades gracefully and explains how to enable it
  later.

**Avoid.** Bombarding users with permissions at launch; blocking the whole app
over a permission only one feature uses.

## Destructive actions

**Principles.** Reversibility, prevention, Fitts (distance), feedback.

**Patterns.**
- Prefer archive or trash with undo.
- If it's irreversible, confirm with context: what gets deleted, how much, and
  what effect it has ("3 invoices and their payments will be deleted. This can't
  be undone.").
- The confirm button names the action ("Delete 3 invoices") and uses the danger
  color; Cancel gets default focus.
- For very serious actions, require typing the resource name to confirm.
- Keep destructive buttons away from frequent ones.

**Avoid.** "Are you sure?" with "OK/Cancel"; a destructive button next to "Save".

## Notifications

**Principles.** Fogg (prompt), open tasks, respect for attention.

**Patterns.**
- Trigger when the action makes sense, and link straight to the exact destination.
- Batch non-urgent items into a digest; give users control (preferences by type).
- Badges that reflect real pending items and clear when resolved.
- The text says what happened and what to do, without needing to open it to
  understand.

**Avoid.** Nagging to force behavior; inflated badges; notifications that
land on the home screen.

## Onboarding

**Principles.** Fogg (lower the barrier), endowed progress, progressive disclosure,
peak-end.

**Patterns.**
- Value in the first minute: let the user accomplish something useful before
  setup.
- Ask for the minimum up front; everything else when it's needed.
- A setup checklist with real progress; celebrate the first win.
- Sample data or templates so users don't start from a blank slate.
- Contextual help instead of long mandatory tours.

**Avoid.** Ten-step tours; asking for everything before showing value.

## Empty states

An empty state teaches; it doesn't just show a blank box.

- **First use:** explain what goes here and offer the first step ("Create your
  first invoice"), with the button right in the empty state.
- **All caught up:** frame it as an achievement ("You're all caught up"), not
  an error.
- **No results for a filter or search:** distinguish it from "no data" and
  offer to clear filters.
- **Loading error:** say so and offer to retry. Never an empty state that's
  actually a failure.

**Avoid.** The silent empty state; an empty state that hides a loading error.

## Login

**Principles.** Jakob, recognition (WCAG 3.3.8), feedback, prevention.

**Patterns.**
- Simple and fast; autofocus on the first field.
- `autocomplete="username"` and `"current-password"`; allow pasting; show or
  hide the password.
- Passkeys, magic links, or sign-in with a provider when available.
- "Verifying…" on submit; helpful errors that don't reveal whether the account
  exists.
- Visible password recovery.

**Avoid.** Blocking paste; captchas on the first attempt; generic
errors.

## AI interfaces

Interfaces built on language models and agents bring new problems:
slow responses, variable output, and actions with consequences.

**Principles.** Response times, feedback, reversibility, prevention,
trust.

**Patterns.**
- **Streaming**: show the response as it's generated. The first token arrives
  in under 1 s, even if the full response takes longer.
- **Work status**: if the agent uses tools, show what it's doing
  ("Searching your invoices…") and let the user stop it.
- **Visible uncertainty**: cite sources, flag what isn't verified, and make it
  easy to check. Never present a guess in the same tone as a fact.
- **Editable output**: the user can correct or regenerate without starting over.
- **Confirm before acting**: if the agent is about to send, pay, delete, or
  publish, show exactly what it will do and ask for confirmation. Reversible
  actions can go straight through with undo.
- **Starter suggestions**: examples of what it can do, to beat the blank page
  (recognition over recall).
- **Honest limits**: say what it can't do instead of making things up.

**Avoid.** 20-second spinners with nothing else; confident answers that are
fabricated; agents that act without showing what they'll do; losing the user's
text when generation fails.

## Microcopy

**Patterns.**
- **Buttons**: verb + object ("Send invoice", "Create account"), not "OK" or a
  bare "Send" when it's ambiguous.
- **Errors**: what happened + how to proceed, in the user's language, without
  blame ("We couldn't find that email. Check the spelling or create an
  account.").
- **States**: present participle (-ing) for the process ("Saving…") and past
  participle for the result ("Saved").
- **Confirmations**: what was done and what comes next.
- **Consistency**: one concept, one word. If it's "customer", don't alternate
  with "user" or "contact".
- **Tone**: match the product's voice and tone; clear beats clever.

**Avoid.** Technical jargon ("Error 500"); humor in serious errors; all caps
to shout.
