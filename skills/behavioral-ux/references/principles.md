# Behavioral design principles

Each principle covers: **what it is**, **why it works** (the psychology), **how to
apply it** (stack-agnostic patterns), **the trap** and **the rule**. Numbers
marked as a *heuristic* are reasonable starting points, not laws: validate them
with data (see [How to validate](#how-to-validate)). Sources are in
[sources.md](sources.md).

**Contents**
- [A. Perception and mechanics](#a-perception-and-mechanics): Hick, Fitts, working
  memory, Jakob, Gestalt, Von Restorff, serial position
- [B. Cognitive load](#b-cognitive-load): recognition, defaults, progressive
  disclosure, Tesler
- [C. Motivation](#c-motivation): Fogg, open tasks, progress
- [D. Trust and error](#d-trust-and-error): response times, feedback,
  prevention, reversibility, framing, peak-end, aesthetics
- [When two principles collide](#when-two-principles-collide)
- [How to validate](#how-to-validate)

---

## A. Perception and mechanics

### 1. Hick's law: every option costs time

**What it is.** Decision time grows with the number of equally likely options
shown at once (it grows logarithmically, not linearly).

**Why it works.** Every alternative competes for the same limited attention.
Mind the nuance: the effect is strong when options are unfamiliar and must be
compared against each other; it weakens when users already know what they want
and can scan or search. The "choice overload" from the jam studies isn't
universal either: meta-analyses find highly variable effects.

**How to apply it.**
- One primary action per context; everything else is secondary or navigation.
- Show actions based on the object's state, not all of them all the time.
- Break complex decisions into steps (a well-built wizard cuts options per
  screen).
- If a list is long but users know what they want (countries, customers), don't
  trim it: give them search or autocomplete.

**The trap.** "While we're at it, let's add this button." Every new option slows
down the rest. And the opposite trap: hiding options users need just to
"clean up" the screen.

**Rule.** One visible primary button per context. If you need two, the screen
is doing two things: split it.

### 2. Fitts's law: big and close is faster to reach

**What it is.** The time to reach a target depends on its distance and size:
bigger and closer means faster, with fewer errors.

**Why it works.** It's motor. On mobile, most people hold the phone in one hand
or cradle it and use their thumb; the center and bottom of the screen are the
most comfortable, and the top corners the hardest. On desktop, edges and
corners are "infinite": the cursor stops there on its own.

**How to apply it.**
- Make the main action big and place it in the comfort zone: a bottom bar or
  sticky button on mobile; visible without scrolling on desktop.
- Touch target sizes: WCAG 2.2 requires at least 24×24 CSS px (2.5.8, AA) and
  44×44 for AAA; Apple recommends 44 pt and Material 48 dp. On mobile, aim for 44–48.
- Keep destructive actions away from frequent ones to prevent accidental taps.
- Extend the clickable area beyond the visual (padding, a fully clickable row).

**The trap.** Reusing desktop sizes on mobile. An icon that's comfortable with a
mouse is frustrating with a thumb.

**Rule.** The most frequent action is the biggest, most reachable target on the
screen.

### 3. Working memory: in small bites

**What it is.** Working memory holds only a few items at a time. Miller's
famous "7 ± 2" (1956) was about how much we can repeat from memory; the current
estimate is **about 4 chunks** (Cowan, 2001). Grouping turns many items into a
few chunks.

**Important clarification.** This does **not** mean "no more than 7 items on
screen." What's visible doesn't need to be remembered. It applies when users
must **hold on to** something while doing something else: a code across
screens, options in a voice menu, data from a previous step.

**How to apply it.**
- Split long forms into themed sections, each with a title that explains the
  block.
- Group long numbers and codes (`4512 8890 1123`, not `451288901123`).
- Don't make users remember across screens: show the data again where it's
  needed.

**The trap.** Treating "7" as a magic limit for menus or cards. The real test is
whether users have to remember, and whether items form meaningful groups.

**Rule.** Group by topic; never make users memorize something the interface can
show them.

### 4. Jakob's law: use what they already know

**What it is.** Users spend most of their time in other apps and expect yours
to work the same way.

**Why it works.** Prior knowledge transfers. A familiar pattern is used without
learning; a new one forces users to build a mental model from scratch.

**How to apply it.**
- Standard platform patterns: bottom tabs on mobile, search at the top, cart in
  the top right, swipe for list actions.
- Domain conventions: if users live in an ERP, their banking app or a specific
  tool, respect its semantics and vocabulary.
- Icons with established meanings (magnifying glass = search, gear = settings),
  with a label when the meaning isn't universal.

**The trap.** Inventing a "more elegant" interaction that breaks habit. Novelty
isn't improvement if it costs relearning.

**Rule.** Before inventing, ask where this user already lives and how they solve
it there.

### 5. Gestalt: the eye groups on its own

**What it is.** The brain organizes what it sees with automatic rules:
proximity, similarity, common region, continuity and figure-ground.

**Why it works.** It happens before thinking. Used well, structure is
understood without reading.

**How to apply it.**
- **Proximity**: what belongs together sits together; the label hugs its field.
- **Common region**: enclose groups in cards; put a message inside the block
  that triggers it.
- **Similarity**: same meaning, same visual treatment.
- **Spacing contrast**: little space within a group, lots between groups.

**The trap.** Uniform spacing everywhere: if everything is equally far apart,
nothing groups.

**Rule.** Space between groups is always larger than space within a group.

### 6. Von Restorff effect: what's different gets remembered

**What it is.** Among similar items, the one that differs gets noticed and
remembered more.

**Why it works.** Contrast triggers attention.

**How to apply it.**
- The primary action is the **only** one with the strongest treatment (fill,
  action color).
- Highlight the recommended plan or the critical data point, just one.
- Don't rely on color alone: add shape, weight, an icon or text (color
  blindness, screens in sunlight).

**The trap.** Highlighting everything. If five things compete to stand out, none
of them do.

**Rule.** One highlighted element per context, and make it the one that matters.

### 7. Serial position: first and last carry more weight

**What it is.** In a sequence, we remember the first items (primacy) and the
last ones (recency) best.

**How to apply it.**
- In navigation, put key destinations at the start and the end.
- In lists of benefits or options, lead with the most important.
- In onboarding, the first and last steps are the ones people remember.

**The trap.** Burying what matters in the middle of a long list.

**Rule.** Critical items go first or last; never hidden in the middle.

---

## B. Cognitive load

### 8. Recognition over recall

**What it is.** Recognizing an option is far easier than retrieving it from
memory and typing it.

**Why it works.** Recognition uses external cues; recall is pure effort and a
source of errors (typos, inconsistent formats).

**How to apply it.**
- Select, combobox or autocomplete for values from a known set.
- Useful information inside the option (balance, status) so users don't have to
  go to another screen.
- Recents, favorites and history-based suggestions.
- Login without memory tests: allow pasting passwords and using password
  managers (WCAG 3.3.8).

**The trap.** Free text for something with known values: it introduces
inconsistency that later breaks reports and searches.

**Rule.** If the value belongs to a known set, users pick it, they don't type it.

### 9. Smart defaults and less friction

**What it is.** Every extra field, tap and decision loses users. A good default
makes "doing nothing" the right choice in the common case.

**Why it works.** We tend to stick with what's preselected (status quo bias).
The effect is so strong it shifts organ donation rates between countries: a
default is a decision you make on the user's behalf, for better or worse.

**How to apply it.**
- Prefill what the system knows: today's date, the current user, the last
  choice, country from the address.
- Calculate instead of asking (totals, taxes).
- Don't ask again for anything already entered in the same process (WCAG 3.3.7).
- Use the right keyboard and input (`type="email"`, `inputmode="numeric"`,
  `autocomplete`).

**The trap.** Dangerous defaults. The default must be the common case **and the
safe one**: never one that, accepted without looking, causes harm or
overcharges (see [ethics.md](ethics.md)).

**Rule.** For every field: does the system already know it, or can it guess it
safely? If so, make it the default and keep it editable.

### 10. Progressive disclosure: essentials first

**What it is.** Show what most people need up front and reveal advanced options
on demand.

**Why it works.** Visible complexity intimidates and slows people down even when
it goes unused.

**How to apply it.**
- A minimal form with "advanced options" collapsed.
- Actions that appear based on the object's state.
- Contextual help behind an icon, available but out of the way.

**The trap.** Hiding something frequent behind "See more." This is for the
infrequent.

**Rule (heuristic).** Anything used in one out of five visits or more stays in
view. Confirm it with analytics if you have them.

### 11. Tesler's law: complexity is conserved

**What it is.** Every task has complexity that can't be eliminated, only moved:
either the system absorbs it or the user does.

**How to apply it.**
- Let the system absorb formats (accept `+1 555-010-0199`, `5550100199` and
  `555 010 0199`), time zones, calculations and validation.
- Detect instead of asking (card type from its digits, city from the ZIP code).

**The trap.** "Simplifying" by removing options users need: the complexity
doesn't disappear, it turns into an email to support.

**Rule.** For every difficulty, ask who should carry it. Almost always, the
system.

---

## C. Motivation

### 12. Fogg Behavior Model: B = MAP

**What it is.** A behavior happens when **M**otivation, **A**bility (ease) and a
**P**rompt converge at the same moment. Earlier versions of the model called the
prompt a "trigger."

**Why it works.** Wanting to and being able to aren't enough: it takes a nudge
at the right moment. Increasing ease usually pays off more than increasing
motivation, because motivation rises and falls.

**How to apply it.**
- **Ability**: everything in part B (defaults, recognition, fewer steps).
- **Prompt**: notifications or "needs your attention" states **when the action
  makes sense**, leading **straight** to doing it (the push opens the exact
  screen, not the home screen).
- **Motivation**: visible progress, a sense of accomplishment, a clear benefit.

**The trap.** Prompting without enabling: a notification that leads to a
six-step flow dies.

**Rule.** For every action you want to drive: is it easy? Is there a prompt at
the right moment that leads straight to it?

### 13. Open tasks (Ovsiankina effect)

**What it is.** We tend to **resume** interrupted or unfinished tasks.

**A note on the evidence.** For decades, the Zeigarnik effect ("we remember
unfinished things better") was widely cited. Recent reviews find that this
memory advantage doesn't replicate consistently; what does hold up is the
tendency to resume what was left half-done, described by Ovsiankina. For
design, the practical consequence is the same: a visible to-do invites closure.

**How to apply it.**
- A "to-do" or "needs your attention" section at the top, sorted by real
  urgency.
- Counters that **go down when the task is done, not when it's viewed**.
- "Pick up where you left off," with the draft saved.

**The trap (ethics).** Fabricating to-dos or inflating badges to create
anxiety. If the to-do isn't real and actionable, it becomes noise.

**Rule.** Show real to-dos, sorted by real urgency, that only go down when
resolved.

### 14. Endowed progress and goal gradient

**What it is.** We're more likely to complete a goal when we feel we've already
made progress (endowed progress), and we speed up as we get closer to the end
(goal gradient).

**How to apply it.**
- Accurate progress bars: completed steps out of total.
- Setup checklists with what's already done checked off (creating the account
  counts as a step, if it genuinely is one).
- Make it visible how little is left ("1 step to go").

**The trap.** Fake progress, progress that goes backward or never reaches
100%: it kills trust.

**Rule.** Every multi-step goal is shown as visible, truthful progress.

---

## D. Trust and error

### 15. Response times

**What it is.** How we perceive waiting has had stable thresholds since the
1960s:

| Time | Perception | What to show |
|---|---|---|
| ≤ 0.1 s | Instant, direct cause and effect | Nothing extra; the result |
| ~0.1–1 s | Noticeable, but the train of thought holds | A state change on the control |
| ~1–10 s | The sense of flow is lost | A loading indicator or skeleton |
| > 10 s | Attention is lost | Progress with an estimate and the option to cancel or continue in the background |

The Doherty threshold (~400 ms) marks when a system stops "keeping pace" with
the person using it.

**How to apply it.**
- Respond to the tap immediately (pressed state, `:active`) even if the work
  takes longer.
- Optimistic UI for reversible actions that almost always succeed (mark as
  read, like), rolling back if they fail.
- Skeletons shaped like the content for loads of 1 to 10 s.
- Long processes: real progress, an estimate and the option to get notified
  when done.

**The trap.** An endless spinner for everything; or artificial waits (debounces,
long animations) in the input path.

**Rule.** Under 0.1 s, show nothing; over 1 s, show that it's working; over
10 s, show how much is left.

### 16. Immediate feedback: nothing happens silently

**What it is.** Every action produces a perceptible response.

**Why it works.** Without feedback, the brain assumes it failed and **repeats**
(double submission) or gets anxious ("did it save?").

**How to apply it.**
- An "in progress" state with a verb ("Saving…") and the control disabled
  meanwhile.
- Visible success confirmation (toast, state change, checkmark).
- Visible, accessible errors (`role="alert"`, `aria-live`), next to the field
  that caused them.

**The trap.** Silent actions, or feedback that covers the content or disappears
before it can be read.

**Rule.** Anything that triggers work: (1) shows it's in progress, (2) disables
itself, (3) confirms the result. Always all 4 states: loading, empty, populated
and error.

### 17. Error prevention > error messages

**What it is.** Better to make the error impossible or unlikely than to report
it afterward (poka-yoke).

**How to apply it.**
- Constrain instead of allowing and scolding: ranges, masks, valid options.
- Validate inline, but **after** the user leaves the field, not while they type
  the first character.
- Warn about the consequence before acting ("this will send the invoice to the
  customer").
- If you block submission, say what's missing.
- Error messages, as a last resort, have three parts: **what happened**, **why**
  (if it helps) and **what to do**. "Email needs an @" instead of "Invalid
  input."

**The trap.** Validating only at the end with a generic error; scolding in red
while the user is still typing; blocking without explaining.

**Rule.** First, make it impossible; if not, warn inline with the consequence;
the error message always says what happened and how to move forward.

### 18. Reversibility: undo gives people courage

**What it is.** Being able to undo reduces the fear of acting and the need for
heavy confirmations.

**How to apply it.**
- "Undo" in a toast after common actions, instead of "Are you sure?" before.
- Autosaved drafts; trash or archive instead of permanent deletion.
- Intermediate states (draft, pending) with a way back.

**The trap.** Confirming everything: users learn to click yes without reading,
and the confirmation stops protecting them when it matters.

**Rule.** If it's reversible, make it seamless and offer undo. If it's
irreversible and costly, confirm with context and a button that names the
action.

### 19. Framing and loss aversion

**What it is.** How you frame a fact changes the decision even when the number
is the same. Losses tend to weigh more than equivalent gains, although the size
of that effect (the classic "twice as much") is debated and depends on context.

**How to apply it.**
- For quotas and balances, frame around what's available: "3 left" reads better
  than "you've used 7 of 10."
- Warn as a limit approaches, before users hit it.

**The trap (ethics).** Using it to pressure ("You'll lose your discount in 5
minutes!" when it isn't true). It's for informing and caring.

**Rule.** Frame limits around what's available and warn in time; never invent a
loss.

### 20. Peak-end: the ending is what people remember

**What it is.** The memory of an experience is shaped mostly by its most
intense moment and how it ended, not by the average.

**How to apply it.**
- Design the last step with care: confirm the result, show the final state and
  offer the obvious next step.
- Watch the negative peaks (a payment error weighs more than ten smooth steps).

**The trap.** Flows that end abruptly: a redirect without confirmation or an
"OK" without context.

**Rule.** Every flow ends with a clear confirmation and a next step.

### 21. Aesthetic-usability

**What it is.** Interfaces perceived as aesthetically pleasing are judged easier
to use, and minor flaws are more readily forgiven.

**How to apply it.** Respect the project's tokens, spacing scale and
typography; consistency and contrast before ornament.

**The trap.** Confusing beautiful with busy, or using aesthetics to cover up
real problems: the halo breaks at the first serious error.

**Rule.** Order, contrast and consistency before decoration.

---

## When two principles collide

| Conflict | How to decide |
|---|---|
| **Hick** (fewer options) vs. **feature discovery** | Move the infrequent into a menu, but leave a visible path ("More actions"). What's used often doesn't get hidden. |
| **Progressive disclosure** vs. **recognition over recall** | If users need to know an option exists in order to look for it, keep it visible even if it's secondary. Hide settings, not capabilities. |
| **Defaults** vs. **ethics** | The default is what an informed user would choose, not what benefits the business most. When in doubt, leave it unchecked. |
| **Feedback** vs. **noise** | Confirm what users can't see for themselves. If the change is already visible on screen, there's no need for a toast. |
| **Prevention** (confirm) vs. **flow** | Reversible: act and offer undo. Irreversible and costly: confirm with context. |
| **Jakob** (the familiar) vs. **innovation** | Innovate on value, not on controls. If a new pattern is clearly better, test it with users before imposing it. |
| **Fitts** (big, sticky button) vs. **content** | On reading screens, the action can go at the end; on task screens, make it sticky. |
| **Density** (experts) vs. **simplicity** (beginners) | Optimize for whoever uses the screen most. If both coexist, offer keyboard shortcuts and optional dense views for experts. |

## How to validate

Principles are well-grounded hypotheses, not guarantees. To know whether a
change worked, measure before and after:

- **Success rate**: how many people complete the task?
- **Time on task** and **errors** per task.
- **Drop-off per step** in the funnel (where people leave).
- **Support tickets** about that screen.
- **Tests with 5 users** thinking aloud: they surface most of the serious
  problems at very low cost.
- **A/B tests** when there's enough traffic and a clear metric.

If there's no data, say so in the audit and propose what to measure.
