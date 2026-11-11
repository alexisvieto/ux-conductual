---
name: behavioral-ux
description: >-
  Behavioral design for any interface: user psychology applied to screens,
  forms, flows, states (empty, loading, error), notifications, microcopy, visual
  hierarchy and AI interfaces, in any stack and design system. Two modes: DESIGN
  (build applying the principles) and AUDIT (findings table with principle,
  severity, location and fix). Turns Hick, Fitts, cognitive load, Jakob,
  Gestalt, recognition over recall, defaults, progressive disclosure, Fogg
  (B=MAP), response-time limits, error prevention, reversibility, framing,
  peak-end and anti dark patterns ethics into concrete patterns with cited
  research. Use it to design, review or improve a UI: "review this form", "this
  feels hard to use", "make it more intuitive", "reduce friction", "empty
  state", "onboarding", "microcopy", "UX review", "UX audit", "dark patterns",
  "usability". Do not use it for pure aesthetics (palette, typography, brand
  motion) or for code without an interface. Spanish version: ux-conductual.
license: CC-BY-4.0
metadata:
  author: "Alexis Vieto · Senior Software Engineer · Nexera (nexerai.io)"
  version: "2.0.0"
---

# Behavioral UX

Designing an interface is not placing controls on a screen: it is **making the
right action the easiest, the most visible and the hardest to get wrong**, using
how human attention, memory and motivation actually work. Always in the user's
favor, never against them.

## Guiding principle

> The screen answers three questions, in this order, without making the user
> think: **(1) What needs my attention now? (2) What is the one main action?
> (3) How do I know it worked?**

Golden rule: if the user has to *think* about where to tap, what to type or
whether something was saved, the screen is not ready yet.

## Step 0: Adapt to the project (always, before proposing anything)

The principles are universal; the parts belong to the project.

1. **Stack and platform**: web (React, Vue, Svelte, Angular…), native mobile
   (SwiftUI, Compose), Flutter. Use their idiomatic conventions.
2. **Design system and tokens**: look for `globals.css`, `theme`,
   `tailwind.config`, tokens, the component library. Use its status colors,
   spacing and radii. **Never invent a palette or hard-code raw colors.**
3. **Existing components**: reuse buttons, inputs, modals and toasts before
   creating new ones.
4. **Conventions**: copy language and voice, a single icon family (never emojis
   as icons), accessibility patterns already in use.
5. **Design document**: if there is a `DESIGN.md` or brand guide, it is the
   source of truth. This skill says **which** principles to apply and **why**;
   the project says **with which parts**.

## Profile the user

Before designing or auditing, answer each in one line:

- **Who?** Role, experience, frequency of use.
- **Where and how?** Device, one hand or two, rushed or calm.
- **What do they want to achieve?** The real task, not "use the app".
- **What do they fear?** Making a mistake, losing work, not knowing if it saved.

Optimize each screen for **the role that uses it most, at the moment they use
it**, not for the edge case.

## Pick the mode

### DESIGN mode (new screen, flow or component)

1. Step 0 and user profile.
2. Answer the three guiding questions for this screen.
3. Open the archetype in [references/playbook.md](references/playbook.md)
   (form, list, dashboard, detail, search, checkout, permissions, onboarding,
   empty states, login, destructive actions, AI interfaces).
4. Pick the **3–4 highest-leverage principles** for this context. If two
   collide, use the conflicts section in
   [references/principles.md](references/principles.md#when-two-principles-collide).
5. Build with the real tokens and components. For code patterns, see
   [examples/before-after.md](examples/before-after.md).
6. Design the **4 states**: loading, empty, with data and error.
7. Run the master checklist and the ethics checklist before delivering.

### AUDIT mode (review something that exists)

1. Step 0 and user profile.
2. Walk the screen with the master checklist and the ethics checklist.
3. **Always** deliver this table, sorted from highest to lowest severity:

| # | Finding | Principle | Severity | Where | Fix |
|---|---|---|---|---|---|
| 1 | The "Save" button shows no loading state and allows double submit | Immediate feedback | 3 | `CheckoutForm.tsx:84` | Disable while submitting and show "Saving…" |

**Severity** (Nielsen's scale): **0** not a problem · **1** cosmetic ·
**2** minor, fix if there is time · **3** major, high priority ·
**4** catastrophe, fix before release. A dark pattern is always 4.

4. Close with **the 3 highest-impact fixes**, one line each.
5. If you can edit the code, offer to apply the fixes; do not apply them unless
   asked.

Evidence, not opinion: every finding names its principle and location. If
something depends on data you do not have (how many users drop off, what they
search for), say so and propose how to measure it (see
[references/principles.md](references/principles.md#how-to-validate)).

## The principles at a glance

Full detail, psychology, traps and sources in
[references/principles.md](references/principles.md).

**Perception and mechanics**
- **Hick**: more options at once, slower decisions. One primary action per
  context.
- **Fitts**: big and close is faster to reach. The most frequent action is the
  biggest, most reachable target.
- **Working memory (Miller, Cowan)**: we hold about 4 chunks. Group by topic.
- **Jakob**: users expect your app to work like the ones they already use.
- **Gestalt**: what belongs together looks together. More space between groups
  than within them.
- **Von Restorff**: what differs stands out. The primary action is the only one
  with that treatment.
- **Serial position**: first and last items are remembered best.

**Cognitive load**
- **Recognition over recall**: pick from a list, do not type from memory.
- **Defaults and less friction**: what the system knows, it does not ask.
- **Progressive disclosure**: essentials visible, advanced on demand.
- **Tesler**: complexity does not disappear; let the system absorb it, not the
  user.

**Motivation**
- **Fogg (B = MAP)**: behavior = Motivation × Ability × Prompt at the same
  moment. Making things easier pays off more than motivating.
- **Open tasks (Ovsiankina)**: we tend to resume what was left unfinished. Make
  real pending items visible.
- **Endowed progress and goal gradient**: visible progress gets finished, and
  speeds up near the end.

**Trust and error**
- **Response times**: 0.1 s feels instant, 1 s keeps the flow, 10 s is the limit
  of attention.
- **Immediate feedback**: nothing happens silently.
- **Prevention over error messages**: make the error impossible before
  reporting it.
- **Reversibility**: undo gives courage; confirm only the irreversible.
- **Framing and loss aversion**: how you frame changes behavior. Use it to
  inform, never to pressure.
- **Peak-end**: the end of the flow is what people remember.
- **Aesthetic-usability**: orderly feels more usable.

## Master checklist

**Attention and hierarchy**
- [ ] Within 2 seconds it is clear what needs attention and what the main
      action is.
- [ ] A single primary button per context; the rest secondary or tertiary.
- [ ] Status color reflects real urgency, uses the project's tokens, and is
      never the only signal (pair it with text or an icon).

**Cognitive load**
- [ ] Nothing the system already knows is requested, and nothing already
      entered is requested again (WCAG 3.3.7).
- [ ] Known values are picked from a list, not typed.
- [ ] Fields grouped by topic; each group has a title that explains it.
- [ ] Every field has a visible label; the placeholder is an example, never the
      label.

**Mechanics**
- [ ] The main action sits in the comfort zone (thumb on mobile, above the fold
      on desktop).
- [ ] Touch targets at least 24×24 px (WCAG 2.5.8) and 44–48 px on mobile
      (Apple 44 pt, Material 48 dp). Destructive actions away from frequent ones.
- [ ] The same data uses the right pattern per size (table on desktop, cards on
      mobile).

**Feedback and states**
- [ ] Every response takes under 0.1 s or shows something: a loading state from
      ~1 s, progress with an estimate from ~10 s.
- [ ] Every button that triggers work shows "in progress" and disables itself to
      prevent double submit.
- [ ] Success is confirmed; errors are visible and accessible (`role="alert"` or
      equivalent), and say what happened and how to continue.
- [ ] All 4 states exist: loading, empty, with data and error. Empty teaches the
      next step.

**Error prevention**
- [ ] Submission is blocked if the minimum is missing, saying **what** is
      missing.
- [ ] Consequences are announced **before** acting ("this will be public").
- [ ] Irreversible actions ask for confirmation with context (what, how much,
      to whom), and the button names the action ("Delete 3 invoices"), not "OK".

**Accessibility and consistency**
- [ ] Visible focus and a logical tab order; everything works with a keyboard.
- [ ] AA contrast (4.5:1 text, 3:1 components); respects
      `prefers-reduced-motion`.
- [ ] Only the project's tokens and components; one icon family; consistent
      copy voice.

**Ending**
- [ ] The flow ends with a clear confirmation and an obvious next step.

## Ethics checklist

Detail, dark patterns and legal framework in [references/ethics.md](references/ethics.md).

- [ ] The honest, healthy option is the easiest and the default.
- [ ] No default surprises or harms the user if accepted without looking.
- [ ] All urgency, scarcity and social proof shown is **real**.
- [ ] Every badge or counter represents a real, actionable task.
- [ ] Leaving, canceling or declining is as easy as joining or accepting.
- [ ] You could explain the design out loud to the user **without shame**.

## References

- [references/principles.md](references/principles.md): each principle in
  depth, conflicts between principles and how to validate.
- [references/playbook.md](references/playbook.md): patterns by screen type.
- [references/ethics.md](references/ethics.md): dark patterns, anti-patterns and
  legal framework.
- [references/sources.md](references/sources.md): studies and sources cited.
- [examples/before-after.md](examples/before-after.md): before and after code
  examples.
