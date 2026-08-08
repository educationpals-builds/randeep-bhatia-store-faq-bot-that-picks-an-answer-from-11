# Five-check auditor

## One-paste spec

A conversational auditor that walks five checks on any failing setup, scores each, identifies the severity driver, makes a call, and sets a tripwire. Paste your failing setup description and real failing inputs—get back a scored audit with actionable findings.

---

## What this auditor does

You describe a setup that's supposed to do something but fails in specific ways. The auditor walks five checks, scores each, names the deciding crack, makes a call, and sets an alarm so drift gets caught early.

**Pass bar:** The answer matches the shopper's real ask, not a nearby FAQ about the product

**Stakes when this fails:** Shoppers get the wrong policy and leave the cart

---

## The five checks

| Check | What it measures | Score (1–5) |
|-------|------------------|-------------|
| **Unowned** | Is there a gap no part of the setup owns? | 4 |
| **Copies** | Are multiple parts doing the same job? | 2 |
| **Room** | Does each part have enough context to do its job? | 1 |
| **Stitch** | Do the parts hand off cleanly to each other? | 2 |
| **Ablation** | If you remove a part, does the setup still work? | 1 |

---

## Worked example

**Setup being audited:** Store FAQ bot that picks an answer from the help center

**Usage reality:** Short mobile questions with product names in the middle

**Source of failing inputs:** Store help-desk chat logs

### Failing inputs

```
how long do i have to return the Nova Buds after they ship
Nova Buds delivery says Friday — can i still cancel
refund for wrong size on the Trail Jacket, not a shipping question
```

### Scored findings

| Check | Score | Finding |
|-------|-------|---------|
| Unowned | 4 | Nothing currently owns catching "refund," "return," or "cancel" as the deciding signal—the bot latches onto product names instead |
| Copies | 2 | Minor overlap between product lookup and FAQ matching |
| Room | 1 | Each part sees enough context |
| Stitch | 2 | Handoff from intent detection to FAQ selection loses the refund signal |
| Ablation | 1 | All parts contribute |

### Severity driver

**Top crack:** Unowned

The unowned check scores highest (4) because nothing in the setup owns the job of recognizing refund/return/cancel intent. When a shopper writes "refund for wrong size on the Trail Jacket, not a shipping question," the bot sees "Trail Jacket" and returns shipping content—because no part owns catching the explicit refund signal.

### Call

Hold. Nothing currently owns catching "refund," "return," or "cancel" as the deciding signal, which is exactly why "Trail Jacket" outscores "refund" in that message.

### Tripwire

Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

---

## Output shape

Every audit returns:

1. **Scored findings** — Each of the five checks with a 1–5 score and a specific finding
2. **Severity driver** — Which check scored highest and why it's the deciding crack
3. **Call** — Hold, shift, or conditional with checkable actions
4. **Tripwire** — A metric, a threshold, a cadence, and an owner who acts when it trips

---

## How to use

Paste a description of your failing setup:
- What it's supposed to do
- What breaks when it fails (stakes)
- Real failing inputs from your logs/queue
- Where those inputs came from

The auditor walks all five checks, scores each with a specific finding, identifies the severity driver, makes a call, and sets a tripwire with an owner.
