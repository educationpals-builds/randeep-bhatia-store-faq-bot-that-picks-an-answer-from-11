# Verify: Store FAQ bot that picks an answer from the help center

This verification confirms the Five-check auditor surfaces the deciding-check finding and demands a numeric measurement for it.

---

## Stranger verification steps

### 1. Open /play with the seeded specimen

Paste this failing-setup description:

> **Setup:** Store FAQ bot that picks an answer from the help center  
> **Stakes:** Shoppers get the wrong policy and leave the cart  
> **Standard:** The answer matches the shopper's real ask, not a nearby FAQ about the product  
> **Real inputs:** Short mobile questions with product names in the middle  
> **Sample failing lines:**  
> - how long do i have to return the Nova Buds after they ship  
> - Nova Buds delivery says Friday — can i still cancel  
> - refund for wrong size on the Trail Jacket, not a shipping question  
> **Source:** Store help-desk chat logs

### 2. Confirm the tool surfaces the deciding check

The audit must identify **unowned** as the deciding check — the highest-severity finding.

Expected finding: Nothing currently owns catching "refund," "return," or "cancel" as the deciding signal.

### 3. Confirm the tool demands a numeric measurement

The audit must request a specific, countable measurement for the unowned check — not a vague quality judgment.

Expected measurement demand: Count of tickets containing an explicit refund/return/cancel word that get answered with shipping content.

### 4. Confirm the output includes call and tripwire

**Call:** Hold. Nothing currently owns catching "refund," "return," or "cancel" as the deciding signal, which is exactly why "Trail Jacket" outscores "refund" in that message.

**Tripwire:** Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

---

## Pass criteria

| Check | Pass condition |
|-------|----------------|
| Deciding check surfaced | Tool names "unowned" as the top crack |
| Numeric measurement demanded | Tool asks for count of refund/return/cancel tickets misrouted to shipping answers |
| Call stated | Tool returns a hold/ship/conditional ruling with reasoning |
| Tripwire set | Tool returns an alarm with threshold, cadence, and owner |

If all four pass, the Five-check auditor is working correctly for this specimen domain.
