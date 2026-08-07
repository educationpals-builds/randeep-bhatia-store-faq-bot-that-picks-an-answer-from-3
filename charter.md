# Store FAQ bot that picks an answer from the help center

## Audit Charter

**Specimen under review:** Store FAQ bot that picks an answer from the help center

**Problem situation:** Shoppers ask about refunds, but the FAQ bot answers with shipping times because it latched onto the product name. Fix that before the busy sale week.

**Stakes if unfixed:** Shoppers get the wrong policy and leave the cart

---

## Standard for success

The answer matches the shopper's real ask — not a nearby FAQ about the same product

---

## Real inputs tested

**Source:** Store help-desk chat logs

**Usage pattern:** Short mobile questions with product names in the middle

### Specimen sentences

```
how long do i have to return the Nova Buds after they ship
Nova Buds delivery says Friday — can i still cancel
refund for wrong size on the Trail Jacket, not a shipping question
```

---

## Five-check findings

| Check | Rating | Notes |
|-------|--------|-------|
| Unowned | 4 | Refund/return/cancel words have no dedicated handler — the bot sees "Nova Buds" and routes to shipping FAQ |
| Copies | 2 | Multiple FAQ entries overlap on product names without distinguishing intent |
| Room | 1 | No space in the routing logic for policy-type signals |
| Stitch | 2 | Product-name match overwrites intent signals instead of combining them |
| Ablation | 1 | Removing the product name changes the answer entirely — the bot depends on it too heavily |

---

## Deciding check

**Top crack:** Unowned

The system has no component that owns refund/return/cancel as a priority signal. When a shopper types "refund for wrong size on the Trail Jacket, not a shipping question," the bot latches onto "Trail Jacket" and serves shipping content. The refund word is present, explicit, and ignored.

---

## Ship call

Hold. No part of the system currently treats refund/return/cancel words as a priority signal — ship engineering lead needs to add a dedicated check before Black Friday. Reopen once the three specimen sentences all route correctly with refund words present.

---

## Tripwire

Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

---

## Summary

This audit found that the store FAQ bot fails on refund questions because no part of the routing logic treats refund/return/cancel words as a priority signal. The product name ("Nova Buds," "Trail Jacket") dominates routing, so shoppers asking about returns get shipping answers instead. The call is **Hold** until engineering adds a dedicated check for policy-intent words. After release, CX manager watches for refund-word tickets answered with shipping content — if that count exceeds 10/day during sale week, engineering gets escalated.
