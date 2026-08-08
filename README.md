# Five-check auditor

Walk five checks on any setup that's supposed to split work across heads—then surface the one that's actually failing, score it, and set a tripwire so drift doesn't sneak back.

---

## Verdict

**Hold.** Nothing currently owns catching "refund," "return," or "cancel" as the deciding signal, which is exactly why "Trail Jacket" outscores "refund" in that message.

---

## Tripwire

Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

---

## Worked example

**Setup audited:** Store FAQ bot that picks an answer from the help center

**What breaks if the parts aren't really splitting the work:** Shoppers get the wrong policy and leave the cart

**Pass bar committed:** The answer matches the shopper's real ask, not a nearby FAQ about the product

**Deciding check:** unowned (scored 4/5 severity)

**Real inputs from store help-desk chat logs:**
- how long do i have to return the Nova Buds after they ship
- Nova Buds delivery says Friday — can i still cancel
- refund for wrong size on the Trail Jacket, not a shipping question

---

## One-paste rebuild

Paste a failing setup you rely on—what it's supposed to do, who gets hurt when it fails, and a few real failing inputs. The auditor walks five checks conversationally, proposes findings with the measurement that would confirm each, and returns a scored audit with a severity story, a call, and a tripwire.

---

## Files

- [charter.md](charter.md) — Full audit: standard, inputs, check scores, severity story, call, tripwire
- [METHOD.md](METHOD.md) — The five-check framework (PRISM) and the collapse-to-monochrome anti-pattern
- [VERIFY.md](VERIFY.md) — Stranger verification steps

---

## Sample asks

1. "My ticket-routing bot is supposed to send billing questions to finance and feature requests to product, but half the billing tickets end up in product's queue. Here are three examples that went wrong…"

2. "We have a lead-scoring system that's supposed to separate enterprise prospects from SMB, but enterprise reps keep getting SMB leads. The system looks at company size and domain, but something's misfiring…"

3. "Our content moderation pipeline splits posts into 'needs human review' vs 'auto-approve' but obvious spam is getting auto-approved while safe posts get flagged. Here are five posts that were misrouted…"

<!-- educationpals-build-verified -->
