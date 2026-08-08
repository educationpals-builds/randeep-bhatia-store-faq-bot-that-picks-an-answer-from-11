# Five-check auditor

## Audit charter

This document records the full audit of a setup that splits work across parts. The worked example is a **Store FAQ bot that picks an answer from the help center**.

---

## Standard committed

> The answer matches the shopper's real ask, not a nearby FAQ about the product

---

## Usage reality

Short mobile questions with product names in the middle

---

## Inputs audited

**Source:** Store help-desk chat logs

**Lines tested:**

```
how long do i have to return the Nova Buds after they ship
Nova Buds delivery says Friday — can i still cancel
refund for wrong size on the Trail Jacket, not a shipping question
```

---

## Check findings

| Check | Score | Notes |
|-------|-------|-------|
| Unowned | 4 | Critical gap — no part owns refund/return/cancel signals |
| Copies | 2 | Minor duplication in product-name matching |
| Room | 1 | Adequate separation between FAQ categories |
| Stitch | 2 | Handoff between product lookup and policy lookup unclear |
| Ablation | 1 | Removing shipping head doesn't break refund answers |

---

## Deciding check

**Top crack:** Unowned

The "unowned" check scores highest because nothing currently owns catching "refund," "return," or "cancel" as the deciding signal. When a shopper writes "refund for wrong size on the Trail Jacket, not a shipping question," the bot latches onto "Trail Jacket" and returns shipping content — because "Trail Jacket" outscores "refund" in the current weighting. The shopper gets the wrong policy and leaves the cart.

---

## Call

Hold. Nothing currently owns catching "refund," "return," or "cancel" as the deciding signal, which is exactly why "Trail Jacket" outscores "refund" in that message.

---

## Tripwire

Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

---

## Pressure response

Hold my rating — I'll defend it

---

## What this audit delivers

A stranger with a failing setup pastes their description, stakes, and sample inputs. The Five-check auditor walks all five checks conversationally, proposes findings with the measurement that would confirm each, and returns a scored audit with a severity story, a call, and a tripwire — the same discipline applied here to the Store FAQ bot.