# Evals: think-twice

These test cases verify the skill behaves correctly across the key scenarios it will encounter. Each eval specifies the input, what the skill MUST do, and what it must NOT do.

---

## Eval 1 — Concrete plan, first question targets the biggest risk

**Input:**
> We're splitting our monolith into 15 microservices. Each team will own one service. We'll do the migration gradually over 6 months.

**Must:**
- Ask exactly ONE question in the first response
- Steelman a real risk first (e.g., distributed data consistency, cross-service transaction complexity, or coordination overhead between 15 teams)
- Make the question specific to *their* migration, not generic microservices advice
- Not suggest an alternative architecture

**Must not:**
- Ask multiple questions at once
- Agree the plan sounds good before probing
- Offer a solution (e.g., "you should use sagas")

---

## Eval 2 — Vague plan, skill asks for specifics before probing

**Input:**
> We're going to rewrite the frontend.

**Must:**
- Recognize there isn't enough detail to probe meaningfully
- Ask the user to describe the plan in more concrete terms (scope, tech choices, timeline, why now)
- Not launch into generic frontend-rewrite questions

**Must not:**
- Begin devil's-advocate mode until the user has shared a real plan
- Ask more than one clarifying question

---

## Eval 3 — Hand-wavy answer triggers one pushback, then moves on

**Input flow:**
1. User: "We're launching in the US, EU, and APAC simultaneously next month."
2. Skill asks about GDPR compliance readiness for EU.
3. User: "We'll handle compliance issues as they come up."

**Must:**
- Push back exactly once — ask what that means concretely (e.g., "GDPR enforcement doesn't wait — what's your pre-launch baseline: DPA, consent flows, data residency?")
- Move to the next risk after the user's second answer regardless of quality

**Must not:**
- Accept "we'll handle it" without a single pushback
- Ask about GDPR a third time after the user answers the follow-up

---

## Eval 4 — Resolved concern accepted and skill moves on

**Input flow:**
1. Skill asks: "What's your rollback strategy if the deploy fails mid-migration?"
2. User: "We have blue-green deployments with automated health checks. If checks fail, we revert within 90 seconds — we've tested it."

**Must:**
- Accept this as resolved ("That covers it." or equivalent)
- Move on to the next risk without pressing further

**Must not:**
- Keep probing rollbacks after a solid answer
- Add caveats or suggest improvements to their rollback plan

---

## Eval 5 — Out-of-scope input (not a plan or design)

**Input:**
> Should I send this email to my manager asking for a raise?

**Must:**
- Acknowledge this is outside the intended scope (plans & designs, not interpersonal decisions)
- Either offer to proceed with appropriate caveats or redirect gracefully

**Must not:**
- Silently run devil's-advocate mode on an interpersonal communication
- Refuse entirely without explanation

---

## Eval 6 — User pushes back twice on the same question, skill drops it

**Input flow:**
1. Skill questions whether the 6-month timeline is realistic.
2. User: "We've done this before, it'll be fine."
3. Skill pushes back once: "What makes you confident — what's different this time vs past migrations?"
4. User: "We just know the team. Trust me."

**Must:**
- Accept the position after the second answer ("Noted — I'll take that as an accepted bet.")
- Move on to the next risk

**Must not:**
- Ask a third question on the same topic
- Express ongoing skepticism about the timeline after moving on

---

## Eval 7 — Wrap-up after all risks resolved

**Precondition:** All three risks have been probed and either resolved or acknowledged.

**Must:**
- Produce a 2–3 sentence summary: what stress-tests passed, what remains an open bet
- Not introduce new risks in the closing summary
- Not suggest solutions or redesigns in the summary

---

## Scoring guide

| Behavior | Pass | Fail |
|---|---|---|
| One question per turn | Always single question | Two+ questions in one response |
| Steelmans before questioning | Opens with best opposing argument | Skips straight to question |
| Accepts solid answers | Moves on cleanly | Keeps re-probing resolved concerns |
| Single pushback on vague answers | Probes once, then moves on | Never pushes back OR pushes back 3+ times |
| Wrap-up is present | 2–3 sentence summary at close | No summary, or summary introduces new risks |
| No solutions offered | Pure probing mode | Suggests redesigns or fixes |
