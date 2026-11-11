# Ethics of behavioral design

The same techniques that make an app easy to use can be used to manipulate. The
difference is **who they work for**.

## The golden rule

> Use psychology to make the **right, honest action** the easiest one.
> Never to make an action that **harms the user** the easy one, the
> default, or the hard one to avoid.

**Quick test:** if you had to explain out loud to the user why the screen is
designed this way, would you be embarrassed? If the answer is yes, it's a
dark pattern. Remove it.

## Dark patterns (always severity 4 in an audit)

Taxonomy based on Brignull (deceptive.design), Gray et al. (2018), and Mathur et
al. (2019).

| Pattern | What it is | Example |
|---|---|---|
| **Confirmshaming** | Guilting or shaming users for choosing the healthy option | "No thanks, I'd rather pay more" |
| **Sneaky defaults** | Preselecting what benefits the business and harms or surprises the user | Preselected shipping insurance or newsletter |
| **Roach motel (asymmetric friction)** | Easy to get in, hard to get out | Subscribe in one click, cancel only by phone |
| **Fake urgency** | Made-up countdowns or deadlines | "Offer ends in 05:00" that resets |
| **Fake scarcity** | Made-up stock or demand | "Only 2 left" that never changes |
| **Fake social proof** | Made-up activity or reviews | A generated "John from Chicago just bought this" |
| **Inflated badges** | Indicators that represent nothing real | A permanent red dot to attract clicks |
| **Nagging** | Repeated pressure to force a behavior | Asking to enable notifications on every visit |
| **Hidden costs (sneaking)** | Revealing fees at the end | A fee that appears at the last step |
| **Trick questions** | Confusing copy or double negatives | "Uncheck to not stop receiving emails" |
| **Obstruction** | Hiding or disguising what the user wants | "Cancel" in light gray, small text |
| **Privacy zuckering** | Pushing users to share more data than they want | "Accept all" highlighted, "Settings" hidden |
| **Visual interference** | Disguising ads as content, or fake buttons | An ad shaped like a "Download" button |

## UX anti-patterns (honest mistakes, just as harmful)

- **Silent action**: no feedback; the user retries and creates duplicates.
- **Unexplained blocking**: disabling without saying what's missing.
- **Late validation**: everything at the end instead of preventing errors.
- **Choice overload**: one more button every time.
- **Fake or endless progress**: breaks trust.
- **Silent empty state**, or an empty state that hides an error.
- **Breaking Jakob's law**: inventing where a familiar pattern existed.
- **Colors outside the tokens**: breaks consistency.
- **Color alone to communicate**: inaccessible to colorblind users.
- **Unlabeled icons** whose meaning isn't universal.
- **Emojis as icons**: use a consistent icon family.

## Legal landscape (this is not legal advice)

Deceptive design is no longer just an ethical problem; in several jurisdictions
it's illegal:

- **European Union, Digital Services Act (Regulation 2022/2065), Art. 25**:
  prohibits online platforms from designing interfaces that deceive or
  manipulate users, or that distort their ability to make free decisions.
- **GDPR**: consent must be freely given, specific, informed, and
  unambiguous; refusing must be as easy as accepting, and preselected
  checkboxes don't count as consent.
- **Unfair Commercial Practices Directive (EU)**: applies to fake urgency,
  fake scarcity, and hidden costs.
- **United States**: the FTC pursues deceptive design under its authority over
  deceptive practices, and state laws such as California's CPRA treat consent
  obtained through dark patterns as invalid. Check the current status of federal
  rules on subscription cancellation before citing them.
- **Other jurisdictions**: consumer-protection and personal-data laws (for
  example Brazil's LGPD or Panama's Law 81 of 2019) generally require informed
  consent and truthful price information.

If the product operates in these jurisdictions, a dark pattern is also a legal
risk. When in doubt, consult a lawyer.

## Ethics checklist

- [ ] The honest, healthy option is the easiest one and the default.
- [ ] No default surprises or harms the user if accepted without looking.
- [ ] All urgency, scarcity, and social proof is real and verifiable.
- [ ] Every badge or counter represents a real, actionable task.
- [ ] Canceling, leaving, or declining is as easy as joining or accepting.
- [ ] The total price is known before the final step.
- [ ] The copy is clear: no double negatives, no guilt.
- [ ] You could explain the design to the user without embarrassment.

> Trust is the asset. A single dark pattern and people stop believing the
> product. Honest design isn't just the right thing to do: it's what makes the
> product work in the long run.
