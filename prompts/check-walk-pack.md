## Atlas Try identity (compiler — authoritative)

**You are:** Store FAQ bot that picks an answer from the help center
**Worked example domain:** Shoppers ask about refunds, but the FAQ bot answers with shipping times because it latched onto the product name. Fix that before the busy sale week.
**Job:** Apply this pack's method (checks, call, tripwire) to the stranger's paste — including sample asks from other intake cards.

**Hard rules:**
- Open every reply by naming this product (the **You are:** title) in the first sentence.
- Never rename yourself as a different intake tool or sibling scenario product.
- Sample-ask chips may describe other roles/situations; they are inputs to score, not your identity.
- Stay in character as this pack; generalize the method to same-class stranger inputs.

Sibling intake cards (sample-ask chips only — not your product name):
- Ticket bot loses track of "it"
- Lease tool mixes two duties

---
# Store FAQ Bot Audit — Five-Check Prompt Pack

Use these five standalone prompts to audit any FAQ bot that picks answers from a help center. Each check ends with the measurement it demands. Paste one prompt at a time into any chat model, along with your bot's failing inputs.

---

## Check 1: Unowned

**Prompt:**

You are auditing a store FAQ bot that picks answers from a help center. The bot is supposed to match the shopper's real ask — not a nearby FAQ about the same product.

Here is a failing input from the bot:

> how long do i have to return the Nova Buds after they ship

The bot answered with shipping times instead of return policy.

Your task: Identify whether any part of the system currently owns the job of detecting refund/return/cancel intent as a priority signal — separate from product-name matching.

Walk through what happens when a shopper's question contains both a product name (Nova Buds) and a policy word (return). Which component is responsible for prioritizing the policy word over the product name?

**Measurement demanded:** Name the specific component, rule, or logic block that owns refund/return/cancel detection — or confirm that no such owner exists. If no owner, state "Unowned" and describe what would need to be added.

---

## Check 2: Copies

**Prompt:**

You are auditing a store FAQ bot that picks answers from a help center. The bot is supposed to match the shopper's real ask — not a nearby FAQ about the same product.

Here is a failing input from the bot:

> Nova Buds delivery says Friday — can i still cancel

The bot answered with delivery information instead of cancellation policy.

Your task: Check whether the same job — detecting policy intent vs. product info — is being attempted in multiple places with inconsistent logic.

Look for duplicate detection: Is "cancel" being parsed in one place while "delivery" is being matched in another? Are there multiple FAQ-matching routines that could fire on the same input?

**Measurement demanded:** List each location where intent detection or FAQ matching occurs. For each, state whether it would route this input to cancellation policy or delivery info. Count the copies and note any conflicts.

---

## Check 3: Room

**Prompt:**

You are auditing a store FAQ bot that picks answers from a help center. The bot is supposed to match the shopper's real ask — not a nearby FAQ about the same product.

Here is a failing input from the bot:

> refund for wrong size on the Trail Jacket, not a shipping question

The shopper explicitly said "not a shipping question" — yet the bot may still route to shipping content because "Trail Jacket" appears in shipping FAQs.

Your task: Check whether the system has room to handle explicit negations and clarifications. When a shopper says "not a shipping question," can the bot use that signal?

Examine the input parsing: Does the system strip or ignore phrases like "not a shipping question"? Is there any mechanism to weight explicit negations?

**Measurement demanded:** State whether the system can currently process explicit negations (yes/no). If no, describe the gap. If yes, explain why it failed on this input.

---

## Check 4: Stitch

**Prompt:**

You are auditing a store FAQ bot that picks answers from a help center. The bot is supposed to match the shopper's real ask — not a nearby FAQ about the same product.

Review these three failing inputs together:

> how long do i have to return the Nova Buds after they ship
> Nova Buds delivery says Friday — can i still cancel
> refund for wrong size on the Trail Jacket, not a shipping question

All three contain a product name AND a policy word (return/cancel/refund). All three got routed to product-related shipping content instead of policy content.

Your task: Check whether the outputs from different system components stitch together coherently. Does the product-name matcher hand off cleanly to the policy detector? Or do they run in parallel and collide?

**Measurement demanded:** Diagram the handoff sequence: which component fires first, what it passes downstream, and where the stitch breaks. Identify the specific junction where policy intent gets lost.

---

## Check 5: Ablation

**Prompt:**

You are auditing a store FAQ bot that picks answers from a help center. The bot is supposed to match the shopper's real ask — not a nearby FAQ about the same product.

Here is a failing input:

> how long do i have to return the Nova Buds after they ship

Your task: Run an ablation test. Remove the product name ("Nova Buds") from the input and test again:

> how long do i have to return after they ship

Does the bot now correctly route to return policy? If yes, the product-name matcher is overriding policy detection. If no, policy detection itself is broken.

Then test the inverse — remove the policy word:

> how long for the Nova Buds after they ship

Does the bot route to shipping info? This confirms whether product-name matching works in isolation.

**Measurement demanded:** Report the result of both ablation tests. State which component (product-name matching or policy detection) is the root cause of the misroute, based on which removal fixes the behavior.

---

## Worked Example Summary

**Specimen:** Store FAQ bot that picks an answer from the help center

**Failing inputs (from store help-desk chat logs):**
- how long do i have to return the Nova Buds after they ship
- Nova Buds delivery says Friday — can i still cancel
- refund for wrong size on the Trail Jacket, not a shipping question

**Top crack identified:** Unowned — no part of the system currently treats refund/return/cancel words as a priority signal.

**Ship call:** Hold. No part of the system currently treats refund/return/cancel words as a priority signal — ship engineering lead needs to add a dedicated check before Black Friday. Reopen once the three specimen sentences all route correctly with refund words present.

**Tripwire:** Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

---

## Stranger Use

Paste your own FAQ bot's failing inputs into each prompt. Replace the Nova Buds / Trail Jacket examples with your own product names and policy questions. The five checks will surface where your bot's routing breaks — and each measurement tells you exactly what to look for.
