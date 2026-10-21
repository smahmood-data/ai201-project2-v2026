# Acceptance criteria — FitFindr

Five criteria that say what "working" means for this agent, written in unit 3
**before** any results existed.

An acceptance criterion names a target: a number, a count, a rate, or something
a person could plainly observe. *"The agent handles errors"* is an opinion.
*"When search returns nothing, the agent stops before calling the second tool,
in 5 of 5 tries"* is a criterion.

Under each one, write a sentence or two on **why that target** and not a
stricter one. A reason that says something about your tools, your loop, or the
data earns credit; *"80% seemed reasonable"* does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

**Two are written for you. You write three.**

---

## 1. A matching query completes all three tools

Given a query that matches at least one listing, the agent completes all three
tool calls and returns a fit card — in at least 4 of 5 tries.

**Why this target:**
I picked 4 of 5 because the search is a plain keyword match and an otherwise
reasonable phrasing may miss the listing, but a matching query should usually
make it through the loop.

---

## 2. An impossible query stops before the second tool

Given a query that matches no listings, the agent stops before calling
`suggest_outfit` and returns a message naming what to change — 5 of 5 tries.

**Why this target:**
I picked 5 of 5 because this path depends only on the deterministic empty-list
branch, not on model wording or fuzzy matching, so it should never call the
next tool with no item.

---

## 3. Something about state

For 5 of 5 matching runs, `session["selected_item"]["id"]` equals the
`new_item["id"]` received by `suggest_outfit`, and that id is the first result's
id from `session["search_results"]`.



**Why this target:**
I picked 5 of 5 because copying one selected dictionary through the session is
deterministic and is the core state handoff the loop controls.


---

## 4. Something about the fit card

For 4 of 5 fit-card calls, the result is a 2-to-4-sentence caption that names
the selected item, price, platform, and outfit vibe; the exact wording may
vary between calls.



**Why this target:**
I picked 4 of 5 because model output is variable, so one occasional formatting
miss is tolerable, while omitting the item or price makes the card unusable.


---

## 5. Your choice

For 5 of 5 searches given a `max_price`, every returned listing has a numeric
`price` less than or equal to that ceiling, including when the ceiling is zero.



**Why this target:**
I picked 5 of 5 because the price filter is a direct comparison in local data,
and returning an item over budget would violate the user's clearest constraint.


---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 4 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 4. Something about the fit card

         The fit card is different every time.

         **Why this target:** ...

         > **Revised in unit 4:** For 5 different items, the 5 fit cards share
         > no opening sentence.
         >
         > **Why revised:** "different" wasn't checkable — two cards that
         > differed by one word still counted. The new version is something I
         > can actually score.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "I said the empty search stops it 5 of 5 times, but I got 3 of 5,
            so 3 of 5 is more realistic."

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
