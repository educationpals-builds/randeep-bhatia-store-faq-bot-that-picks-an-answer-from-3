# Verify: Store FAQ bot that picks an answer from the help center

Use this checklist to confirm the auditor surfaces the deciding-check finding and demands a numeric measurement for it.

---

## Stranger verification flow

A stranger describes their own FAQ bot setup — what it's supposed to do, who gets hurt when it fails, and a few real failing inputs. Run their setup through `/play` and confirm:

### 1. The tool walks all five checks

The auditor must score each check for the stranger's specimen, not skip to a verdict.

### 2. The deciding-check finding surfaces

For this build, the deciding check is **unowned** — signals that no part of the system treats as a priority.

When the stranger's setup has a similar gap (e.g., certain keywords or intents that nothing in the pipeline owns), the auditor must name it explicitly:

> "No part of the system currently treats [X] as a priority signal."

If the tool skips this finding or buries it in a generic summary, verification fails.

### 3. A numeric measurement is demanded

The auditor must propose a specific number the stranger can watch. For this build, the measurement is:

> Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

For the stranger's setup, the auditor must demand an equivalent:

- A countable event (not "keep an eye on it")
- A danger line (a number that means trouble)
- A watcher (who escalates when the line is crossed)

If the tripwire is vague or missing a number, verification fails.

---

## Sample verification run

**Stranger input:**  
"My store FAQ bot answers questions from the help center. Shoppers ask about returns but get shipping info because the bot latches onto the product name. Here are three real failures:

- how long do i have to return the Nova Buds after they ship
- Nova Buds delivery says Friday — can i still cancel
- refund for wrong size on the Trail Jacket, not a shipping question"

**Expected auditor output includes:**

1. Scores for all five checks (unowned, copies, room, stitch, ablation)
2. Deciding check identified: **unowned** — refund/return/cancel words have no dedicated handler
3. Call: Hold until engineering adds a dedicated check
4. Tripwire with a number: 10 misrouted refund tickets per day during sale week triggers escalation to engineering

---

## Pass criteria

| Check | Pass |
|-------|------|
| All five checks scored | ☐ |
| Deciding check (unowned) surfaced with specific finding | ☐ |
| Call includes owner on any condition | ☐ |
| Tripwire includes a number, a danger line, and a watcher | ☐ |

If any box is unchecked, the auditor needs revision before it can be used on a stranger's setup.
