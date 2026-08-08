# The PRISM Framework

When a setup splits work across multiple heads—retrieval, classification, generation—each head must own a distinct slice of the problem. The five checks below audit whether that split is real or illusory.

---

## P — Partition the Space

Every input must land in exactly one head's territory. If two heads could plausibly claim the same input, the partition leaks. A store FAQ bot that routes "refund for wrong size on the Trail Jacket" to both a product-info head and a returns-policy head has failed to partition.

**Check:** Given any input, can you name the single head responsible before seeing the output?

---

## R — Run in Parallel

Heads that depend on each other's outputs aren't splitting work—they're sequencing it. True parallel heads can process the same input simultaneously without waiting. If your returns-policy head needs to know what the product-info head found first, you have a pipeline, not a partition.

**Check:** Could you run all heads at once and merge results, or must one finish before another starts?

---

## I — Individuate the Pattern

Each head must recognize a pattern the others ignore. If two heads both fire on "Nova Buds," they're seeing the same signal. The split is cosmetic. One head should own product names; another should own action verbs like "return" or "cancel."

**Check:** Name the specific token, phrase type, or structure each head uniquely detects.

---

## S — Stitch the Spectra

When heads return competing answers, something must adjudicate. That stitching logic needs explicit rules—not just "pick the highest confidence." If "Trail Jacket" outscores "refund" because product names always win, the stitch is broken for policy questions.

**Check:** What happens when two heads both return high-confidence answers? Who wins and why?

---

## M — Map What Each Head Sees

You can't audit what you can't observe. Each head should expose what it matched and why. If the FAQ bot says "Here's your shipping info" without showing that it matched on "Nova Buds" and ignored "return," you're flying blind.

**Check:** Can you see the exact tokens or patterns each head activated on for a given input?

---

## The Collapse-to-Monochrome Anti-Pattern

When one signal dominates all others, the multi-head setup collapses into a single-head system wearing a disguise. Product names like "Nova Buds" or "Trail Jacket" become so salient that action words ("refund," "return," "cancel") never get their turn.

**Symptom:** Every input routes to the same head regardless of the user's actual intent.

**Cause:** One feature (often a named entity) carries disproportionate weight in the routing logic.

**Fix:** Audit the unowned space. If nothing currently owns catching "refund," "return," or "cancel" as the deciding signal, that gap explains why "Trail Jacket" outscores "refund" in a returns question.

---

The five checks spell PRISM because they reveal how your setup refracts a single input into distinct processing paths. If the light comes out monochrome, the prism isn't working.
