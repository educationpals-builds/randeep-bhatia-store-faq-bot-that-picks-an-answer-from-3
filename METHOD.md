# The Five-Check Method: PRISM

When a store FAQ bot latches onto product names and ignores what the shopper actually asked, the failure isn't random. It follows a pattern you can audit systematically.

This method walks five checks that reveal where the bot's routing logic breaks down. The acronym is **PRISM**:

---

## P — Partition the Space

Does the system divide the problem into distinct, non-overlapping zones?

For a FAQ bot, this means: are "refund questions," "shipping questions," and "cancellation questions" treated as separate territories — or does everything blur together under "questions about Nova Buds"?

If the bot has no partition for refund/return/cancel intent, it will always collapse to whatever signal is loudest (usually the product name).

---

## R — Run in Parallel

Does the system check multiple signals at the same time, or does it short-circuit on the first match?

A bot that sees "Nova Buds" and immediately routes to shipping info never gets a chance to notice "return" or "refund" in the same sentence. Parallel checks would surface both signals before making a routing decision.

---

## I — Individuate the Pattern

Does the system recognize that the same product name can appear in completely different question types?

"Nova Buds delivery says Friday" and "how long do I have to return the Nova Buds" both mention the same product — but they're asking about different policies. The bot must individuate the pattern: same noun, different intent.

---

## S — Stitch the Spectra

When multiple signals fire, does the system combine them into a coherent answer — or does one signal drown out the others?

A shopper who writes "refund for wrong size on the Trail Jacket, not a shipping question" is explicitly telling you which spectrum matters. If the bot can't stitch that explicit signal into its routing, it will keep answering about shipping.

---

## M — Map What Each Head Sees

Can you trace which part of the system responded to which part of the input?

If you can't map the bot's attention — can't see that it latched onto "Trail Jacket" and ignored "refund" — you can't fix the routing. The map reveals the blind spot.

---

## The Anti-Pattern: Collapse to Monochrome

When a system fails these checks, it collapses to monochrome: every input gets flattened to a single dominant signal, and the nuance disappears.

A FAQ bot that answers every Nova Buds question with shipping times has collapsed to monochrome. It sees "Nova Buds" and nothing else. The refund words, the cancellation words, the explicit "not a shipping question" — all of it vanishes.

The five PRISM checks exist to prevent this collapse. Each one asks: is the system preserving a dimension of the input that matters for getting the right answer?

When you audit a failing setup, score each check. The lowest-scoring check is usually where the collapse happens — and where the fix needs to go.
