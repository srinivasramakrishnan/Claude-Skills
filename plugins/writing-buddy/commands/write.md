---
description: "Writing workflow hub. Full loop: ideate → outline → draft → critique → polish. Or enter mid-stream for critique or polish of an existing draft. Triggers on: write, draft, critique, polish, de-slop, edit, review my writing, post, linkedin, substack, essay, PRD, spec, document, blog, article."
argument-hint: "[format] [topic] — or: critique [file-path] — or: polish [file-path]"
allowed-tools: ["Read", "Write", "Edit", "Glob", "Grep", "WebSearch", "WebFetch", "Task", "AskUserQuestion"]
---

# Writing Buddy — Command Hub

You are running the writing workflow. Before doing anything else, determine which mode the user wants.

---

## MODE ROUTING

Parse `$ARGUMENTS` for intent:

- If arguments contain a file path, or words like "critique", "review", "check" → go to **[MODE: CRITIQUE]**
- If arguments contain words like "polish", "clean up", "refine", "de-slop" → go to **[MODE: POLISH]**
- If arguments describe a topic or format to write → go to **[MODE: FULL LOOP]**
- If ambiguous:

```
AskUserQuestion: "What would you like to do?"
Options:
- Write something new (full loop: ideate → draft → critique → polish)
- Critique an existing draft (run 4 review agents on a draft you already have)
- Polish an existing draft (authenticity, de-slop, and structural tightening)
```

---

## MODE: FULL LOOP

### STEP 0: SETUP

**Parse format from `$ARGUMENTS`:**
- Format signals: "linkedin", "substack", "essay", "prd", "spec", "brief", "document", "doc"
- If format is clear, proceed. If missing, ask:

```
AskUserQuestion: "What format are we writing?"
Options:
- LinkedIn post (100–300 words, fast loop, no outline)
- Substack / long-form essay (1,500–3,000 words, full loop)
- Document — PRD, spec, brief, one-pager (500–2,500 words, full loop)
```

**Load references:**

Read `${CLAUDE_PLUGIN_ROOT}/skills/writing-buddy/references/format-guides.md` — find the section for the chosen format. Note: phase map, length constraints, opening/closing techniques, and critique agent weights.

Check `${CLAUDE_PLUGIN_ROOT}/skills/writing-buddy/references/voice-dna.md` — if populated, load it. If blank, note that human authenticity mode is active.

---

### STEP 1: IDEATE

If no topic was given in `$ARGUMENTS`:

```
AskUserQuestion: "What do you want to write about? A topic, angle, or rough idea — even one sentence is enough."
```

**Gather format-specific context:**

**LinkedIn:**
- What's the one thing you want the reader to take away or feel?
- Is there a specific observation, experience, or number you want to anchor on?

**Substack:**
- Search the workspace for related files using Glob and Grep — present what's found
- Is there a recent event, conversation, or experience that prompted this?
- Who is the specific reader you're writing for? (Not "product managers" — the one PM you know who would read this)

**Document:**
- What type? (PRD, spec, brief, one-pager — ask if unclear)
- Who is the primary audience? (engineering team, executive stakeholder, external partner)
- What decision does this document need to enable?
- What's the deadline or urgency?

**Align on angle:**

```
AskUserQuestion: "Here's what I'm thinking for the angle: [proposed angle in 1–2 sentences]. Does this match what you had in mind?"
Options:
- Yes, that's right
- Close — let me adjust it
- No, different angle
```

Iterate until the angle is locked.

---

### STEP 2: OUTLINE

**Skip this step entirely for LinkedIn posts.**

For Substack and Documents, draft a working outline including:
- Section headers (conversational for Substack, standard for documents)
- 1–2 sentence note on what each section covers
- For documents: flag where tables, decision sections, or non-goals belong
- For Substack: identify where the main anecdote or example lands

```
AskUserQuestion: "Here's the outline. How does this look?"
Options:
- Looks right — let's draft
- Adjust it
- Start over with a different structure
```

Iterate until the outline is approved.

---

### STEP 3: DRAFT

**Load writing constraints before drafting:**
- `${CLAUDE_PLUGIN_ROOT}/skills/writing-buddy/references/anti-slop-rules.md`
- `${CLAUDE_PLUGIN_ROOT}/skills/writing-buddy/references/calibration.md` (if populated)

**Write the draft** following the approved outline (or ideation notes for LinkedIn):

All formats:
- Open with one of the techniques specified in the format guide
- Close with one of the techniques specified in the format guide
- Ground every claim in a named, specific example within 2 sentences
- No banned phrases from anti-slop-rules.md
- No em dashes for drama
- No false dichotomies or staccato urgency chains
- Vary sentence length — short punchy declaratives earn their brevity by following something longer

LinkedIn: 100–300 words, no headers, 1–2 sentence paragraphs. First line is the hook. Last line invites something.

Substack: 1,500–3,000 words, conversational section headers. For complex concepts, use the four-layer explanation (Why it matters → Intuitive frame → Mechanism → Practical implication). Include at least one hyper-specific anecdote with a named entity, number, or date.

Document: Use the document type's expected structure (PRD: problem, non-goals, requirements, success metrics, next steps). Tables for comparisons. Bold key terms on first use. End with next steps that include a named owner and date.

**Save the draft:** Write to `${CLAUDE_PLUGIN_ROOT}/drafts/YYYY-MM-DD-slug.md`

**Mid-draft check (Substack and Documents over 1,000 words):** Pause at a natural midpoint, show the first half:

```
AskUserQuestion: "Here's the first half. Any direction changes before I continue?"
Options:
- Keep going — this is right
- Adjust direction
- The tone feels off
```

---

### STEP 4: CRITIQUE

**Launch all 4 review agents in parallel:**

```
Task reviewer-authenticity: "Review this draft for human authenticity. Format: [format]. Voice profile status: [populated / blank — human authenticity mode active]. Draft: [content or file path]. Calibration file: [loaded content or blank status]."

Task reviewer-slop: "Scan this draft sentence by sentence for AI slop patterns. Draft: [content or file path]."

Task reviewer-structure: "Evaluate the structure and flow of this draft. Format: [format]. Draft: [content or file path]."

Task reviewer-facts: "Verify all factual claims in this draft. Draft: [content or file path]."
```

**Synthesize results:**

1. Collect the score from each agent
2. Calculate the composite score using the format's weights from format-guides.md
3. Deduplicate findings where two agents flagged the same sentence
4. Group by severity:
   - **Critical** (confidence ≥ 90): Must fix before publishing
   - **Important** (confidence 75–89): Should fix
   - **Suggestions** (confidence 50–74): Nice to have
5. Present the critique report using the format in quality-rubric.md

```
AskUserQuestion: "Critique complete. What would you like to do?"
Options:
- Accept all findings and polish
- Accept most — I'll tell you which to skip
- Keep the draft as-is and skip polish
- This score doesn't feel right
```

---

### STEP 5: POLISH

Apply accepted findings first: for each accepted finding, apply the suggested fix. If a suggested fix itself contains slop, rewrite it cleanly before applying.

Then run three polish passes in order — do not combine them:

**Pass 1 — Anti-slop:** One final scan against anti-slop-rules.md. Fix anything missed.

**Pass 2 — Authenticity:** Check that fixes didn't introduce generic or assembled language. Every revised sentence should still read like a person thinking, not a model outputting.

**Pass 3 — Structural tightening:** Remove unnecessary words. Confirm opening and closing still match the format guide. Confirm length is within range.

Save: overwrite the draft file with the polished version.

```
AskUserQuestion: "Here's the polished version. Ready to go?"
Options:
- Yes — done
- Run another critique pass
- I want to make some manual edits first
```

---

## MODE: CRITIQUE

Review an existing draft without going through the ideate/outline/draft phases.

### SETUP

If `$ARGUMENTS` contains a file path, read it. If not:

```
AskUserQuestion: "Which draft should I review? Paste the content directly or give me a file path."
```

**Detect format** from content:
- Under 300 words, no headers → LinkedIn
- 300–3,000 words with section headers and prose → Substack
- Any length with structured sections (Problem, Requirements, Non-Goals, Next Steps) → Document

If unsure, ask.

Read `${CLAUDE_PLUGIN_ROOT}/skills/writing-buddy/references/format-guides.md` — note critique agent weights for the detected format.

Check `${CLAUDE_PLUGIN_ROOT}/skills/writing-buddy/references/voice-dna.md` — note status, pass to reviewer-authenticity.

### RUN CRITIQUE

**Launch all 4 agents in parallel:**

```
Task reviewer-authenticity: "Review this draft for human authenticity. Format: [format]. Voice profile status: [populated / blank — human authenticity mode]. Draft: [content]."

Task reviewer-slop: "Scan this draft sentence by sentence for AI slop patterns. Draft: [content]."

Task reviewer-structure: "Evaluate the structure and flow. Format: [format]. Draft: [content]."

Task reviewer-facts: "Verify all factual claims in this draft. Draft: [content]."
```

Synthesize using the same process as STEP 4 above — collect scores, calculate composite, deduplicate, group by severity, present the critique report.

### NEXT STEPS

```
AskUserQuestion: "Critique complete. What would you like to do?"
Options:
- Apply the fixes (I'll polish the draft based on accepted findings)
- I'll fix manually — just needed the feedback
- Run another critique pass after I edit
```

If "Apply the fixes": ask which findings to accept if there are many borderline ones, then proceed to **[MODE: POLISH]**.

If "Run another pass": wait for the user to confirm edits are done, re-read the file, re-run critique.

---

## MODE: POLISH

Refine a draft that's close but needs a cleanup pass. Three sequential passes: authenticity alignment, de-slop, structural tightening.

### SETUP

If `$ARGUMENTS` contains a file path, read it. If not:

```
AskUserQuestion: "Which file should I polish? Provide the file path."
```

Detect format (same logic as Critique mode). Ask if unclear.

**Load references:**
- `${CLAUDE_PLUGIN_ROOT}/skills/writing-buddy/references/anti-slop-rules.md`
- `${CLAUDE_PLUGIN_ROOT}/skills/writing-buddy/references/format-guides.md` (relevant format section)
- `${CLAUDE_PLUGIN_ROOT}/skills/writing-buddy/references/voice-dna.md` (check if populated)
- `${CLAUDE_PLUGIN_ROOT}/skills/writing-buddy/references/calibration.md` (check if populated)

### THREE POLISH PASSES

Apply in order. Do not combine them.

**Pass 1 — Authenticity Alignment:**

Go paragraph by paragraph:
- Does each paragraph read like a specific person with genuine experience wrote it?
- Is every claim tied to a named example within 2 sentences? If not, ground it or add a [NEEDS GROUNDING] flag for the user to fill in.
- Does the piece take a clear position, or does it sit on the fence?
- Are there passages that feel assembled — generic phrases strung together — rather than thought through?
- Check the opening and closing: do they use the correct techniques for the format?
- If voice-dna.md is populated: check alignment with the voice profile throughout

Fix anything generic, vague, or assembled. Every revised sentence should read like a real person thinking.

**Pass 2 — De-Slop:**

Scan every sentence against anti-slop-rules.md:
- Remove all banned phrases — no exceptions, no matter how well-embedded
- Fix all structural slop: false dichotomies, staccato urgency chains, rhetorical question setups
- Replace every em dash used for dramatic effect with a colon, comma, or parenthetical
- Eliminate hedging language
- For ungrounded claims: rewrite with real grounding, or add a [NEEDS GROUNDING] flag

**Pass 3 — Structural Tightening:**
- Remove filler words and unnecessary qualifications
- Confirm one idea per paragraph
- Check paragraph density: 3–5 sentences for Substack and documents, 1–2 for LinkedIn
- Verify the closing technique matches the format guide — not a trailing summary
- Verify length is within the format's range. If over, cut the weakest section or the most redundant paragraph.
- For documents: confirm all required sections are present (non-goals, success metrics, next steps with owners)

### PRESENT CHANGES

Show the polished version. For pieces under 400 words, show the full revised text. For longer pieces, show the full version and summarize the most significant changes made.

```
AskUserQuestion: "Here's the polished version. What do you think?"
Options:
- Looks good — save it
- Needs more work
- Show me a before/after diff of the changes
- Revert — keep the original
```

**If "save it":** Overwrite the original file with the polished version.

**If "needs more work":** Ask for specific feedback, apply additional changes, present again. Repeat until satisfied.

**If "show me a diff":** Present key changes as annotated before/after comparisons. Then ask again.

**If "revert":** Do not save. Leave the original file unchanged. Confirm no changes were saved.

---

## Important Guidelines

- **Ask, don't assume.** Any creative decision — angle, tone, example, audience — confirm before executing.
- **Never invent examples.** If a claim needs a specific example and you don't have one, ask the user or search the web.
- **Write clean from the start.** Anti-slop is not just a final pass — it applies during drafting.
- **Respect format length.** Don't write a 500-word LinkedIn post or a 200-word Substack.
- **Short formats move fast.** A LinkedIn post should not take 8 rounds of questioning. Align on topic and angle in one question, then draft.
