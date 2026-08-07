# Store FAQ Bot That Picks an Answer From the Help Center — Audit Blueprint

## What this audits

A store FAQ bot that picks an answer from the help center. Shoppers ask about refunds, but the FAQ bot answers with shipping times because it latched onto the product name. Fix that before the busy sale week.

**Stakes:** Shoppers get the wrong policy and leave the cart

**Pass standard:** The answer matches the shopper's real ask — not a nearby FAQ about the same product

---

## The failing inputs

Source: Store help-desk chat logs

Real usage pattern: Short mobile questions with product names in the middle

### Specimen sentences (verbatim)

```
how long do i have to return the Nova Buds after they ship
Nova Buds delivery says Friday — can i still cancel
refund for wrong size on the Trail Jacket, not a shipping question
```

---

## Five-check audit scores

| Check | Rating | What it measures |
|-------|--------|------------------|
| Unowned | 4 | Does the system have a dedicated owner for refund/return/cancel routing? |
| Copies | 2 | Are there duplicate or conflicting FAQ entries that confuse the matcher? |
| Room | 1 | Does the system have capacity to distinguish intent when product names appear? |
| Stitch | 2 | Do the components (intent detection, FAQ retrieval, answer selection) hand off cleanly? |
| Ablation | 1 | If you remove the product-name signal, does routing improve or break? |

**Top crack:** Unowned (rating 4)

No part of the system currently treats refund/return/cancel words as a priority signal. The FAQ bot latches onto product names ("Nova Buds," "Trail Jacket") and returns shipping content even when the shopper explicitly mentions "return," "cancel," or "refund."

---

## Ship call

**Hold.** No part of the system currently treats refund/return/cancel words as a priority signal — ship engineering lead needs to add a dedicated check before Black Friday. Reopen once the three specimen sentences all route correctly with refund words present.

---

## Tripwire

Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

---

## How a stranger uses this auditor

1. **Paste your failing setup:** Describe your FAQ bot (or similar routing system), what it's supposed to do, and who gets hurt when it fails.

2. **Provide three real failing inputs:** Paste actual customer messages where the bot gave the wrong answer.

3. **Walk the five checks:** The auditor scores each check for your setup, proposes findings, and names the measurement that would confirm each finding.

4. **Get your call and tripwire:** Receive a ship/hold decision with conditions and owners, plus an alarm number that tells you when trouble has returned.

---

## Worked example: This audit

**Setup:** Store FAQ bot that picks an answer from the help center

**Failing input:** "how long do i have to return the Nova Buds after they ship"

**What went wrong:** Bot returned shipping/delivery FAQ instead of return policy because it matched on "Nova Buds" and ignored "return."

**Top crack finding:** Unowned — no dedicated check prioritizes refund/return/cancel words over product-name matches.

**Measurement to confirm:** Run the three specimen sentences through the bot. If any returns shipping content when the message contains refund/return/cancel, the unowned check fails.

**Call:** Hold until engineering lead adds a dedicated refund/return/cancel priority signal.

**Tripwire:** 10+ refund-word tickets answered with shipping content per day during sale week → CX manager escalates to engineering.
