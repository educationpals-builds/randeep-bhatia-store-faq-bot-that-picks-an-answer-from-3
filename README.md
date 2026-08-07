# Store FAQ bot that picks an answer from the help center

**Specimen:** Store FAQ bot that picks an answer from the help center

**Problem:** Shoppers ask about refunds, but the FAQ bot answers with shipping times because it latched onto the product name. Fix that before the busy sale week.

**Stakes:** Shoppers get the wrong policy and leave the cart

---

## Verdict

**Hold.** No part of the system currently treats refund/return/cancel words as a priority signal — ship engineering lead needs to add a dedicated check before Black Friday. Reopen once the three specimen sentences all route correctly with refund words present.

---

## Tripwire

Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

---

## Deciding check

The audit found **unowned** as the deciding check (scored 4/5 severity). The bot has no dedicated signal for refund/return/cancel intent — product names dominate routing, so "Nova Buds" triggers shipping FAQs even when the shopper explicitly asks about returns.

---

## One-paste rebuild block

```
Specimen: Store FAQ bot that picks an answer from the help center
Standard: The answer matches the shopper's real ask — not a nearby FAQ about the same product
Deciding check: unowned (4/5)
Call: Hold — engineering lead adds dedicated refund/return/cancel check before Black Friday
Tripwire: >10 refund-misroutes/day during sale week → CX manager escalates to engineering
```

See [charter.md](charter.md) for the full audit with all five check ratings, specimen sentences, and severity story.

---

## How this audit works

This audit walks five checks to determine whether the FAQ bot's routing logic actually splits work correctly. The method is documented in [METHOD.md](METHOD.md). To verify the audit against your own FAQ bot setup, see [VERIFY.md](VERIFY.md).

<!-- educationpals-build-verified -->
