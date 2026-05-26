# Quality Rubric

Scoring framework for evaluating written content across five dimensions. Each critique agent scores its own dimension 1–10. The composite score uses format-specific weights from format-guides.md.

---

## Scoring Dimensions

### Authenticity (default weight: 30%)

Does this read like a specific human wrote it, with genuine experience and a real point of view?

| Score | Description |
|-------|-------------|
| 1–3 | Generic. Could have been written by anyone. No specific details, no clear perspective. |
| 4–5 | Some specificity present, but the overall voice feels assembled rather than experienced. |
| 6–7 | Real person is visible. Minor moments of vagueness or hedging undercut it. |
| 8–9 | Specific, grounded, and confident. Every claim traces to real experience or a verifiable example. |
| 10 | A reader would assume this was written by someone who lived it. No passage reads constructed. |

**What the authenticity reviewer checks:**
- Is every claim tied to a named, specific example within two sentences?
- Does the piece take a position, or does it survey both sides without committing?
- Are sentences varied in length and rhythm, or monotone?
- Are there parenthetical asides, qualifications, or digressions that feel human rather than scripted?
- Would the opening make a real reader want to read the second paragraph?
- Does the closing earn a reply, share, or action — not just a summary?

*Note: When voice-dna.md is populated, this dimension will also check for alignment with the established personal voice profile and calibration sentences.*

### Engagement & Craft (default weight: 25%)

Would a reader finish this? Would they share it or act on it?

| Score | Description |
|-------|-------------|
| 1–3 | Flat. No hook. A reader stops after the first paragraph. |
| 4–5 | Readable but not compelling. Gets the information across without earning attention. |
| 6–7 | Good hook, reasonable pacing. Reader stays but isn't surprised. |
| 8–9 | Compelling. Every paragraph earns the next. Details create vivid, specific imagery. |
| 10 | Hard to stop reading. Opening hooks immediately. Pacing is exact. The ending lands. |

**What to evaluate:**
- Does the first sentence earn the second?
- Is there sentence length variation — does a short punch precede a longer unpack?
- Are there flat passages where a reader would skim?
- Do anecdotes include hyper-specific details (names, numbers, dates, product names)?
- Does the ending do something — invite, challenge, summarize an action — rather than just trail off?

### Structure & Flow (default weight: 20%)

Does the architecture serve the argument?

| Score | Description |
|-------|-------------|
| 1–3 | Disorganized. Sections feel disconnected. No clear arc from opening to close. |
| 4–5 | Logical order but mechanical. Header-paragraph-header without natural flow. |
| 6–7 | Well-structured. Sections build on each other. Transitions work. |
| 8–9 | Architecture is invisible — the reader feels guided without noticing the structure. |
| 10 | The structure is itself an argument. The order the piece unfolds in reinforces the thesis. |

**What to evaluate:**
- Does the opening use one of the correct techniques for the format (per format-guides.md)?
- Does the closing match one of the correct techniques for the format?
- Is there one idea per paragraph?
- Do transitions feel organic or forced?
- Is the piece the right length for the format? Under or over?
- For documents: are all required sections present (problem, non-goals, success metrics, next steps)?
- For Substack: do section headers sound like a person wrote them, not a syllabus?

### Factual Accuracy (default weight: 15%)

Is every checkable claim true and verifiable?

| Score | Description |
|-------|-------------|
| 1–3 | Contains factual errors or fabricated claims. |
| 4–5 | Mostly accurate. Some claims unverified but plausible. |
| 6–7 | All checkable facts verified. Unverifiable claims (personal anecdotes) noted but not penalized. |
| 8–9 | Every named entity, number, date, and statistic verified. Sources available. |
| 10 | Every fact sourced. Every claim attributed. Every number precise and current. |

**Claim classification:**
- **Verified:** Confirmed via web search or local file. Source noted.
- **Unverifiable:** Cannot confirm or deny (e.g., internal experiences, personal anecdotes). Flag but do not penalize.
- **Contradicted:** Evidence exists that contradicts the claim. Flag as CRITICAL with corrected information.
- **Outdated:** Was accurate at some point but is no longer current. Flag with current status.

### Anti-Slop (default weight: 10%)

Is this free of AI-generated patterns, corporate filler, and structural slop?

| Score | Description |
|-------|-------------|
| 1–3 | Riddled with violations. Multiple banned phrases per paragraph. |
| 4–5 | Several violations detected. A structural pattern or two, plus buzzwords. |
| 6–7 | Mostly clean. One or two minor traces. |
| 8–9 | Clean. Zero banned phrases. Natural human rhythm throughout. |
| 10 | Zero slop. A slop detector would classify this as fully human-written. |

*This dimension uses the inverted scale from anti-slop-rules.md. Slop score 0 → quality score 10.*

---

## Composite Score

```
Composite = (Authenticity × W_auth) + (Engagement × W_eng) + (Structure × W_str)
          + (Accuracy × W_acc) + (AntiSlop × W_slop)
```

Weights vary by format — see format-guides.md.

### Thresholds

| Composite | Verdict | What to do |
|-----------|---------|------------|
| 8.0+ | Ready to publish | Proceed — or run one more pass if you want to |
| 6.0–7.9 | Needs revision | Find the weakest dimension and fix it |
| Below 6.0 | Major rewrite | Return to draft with specific direction |

Default publish threshold: **7.0**. User can override.

---

## Critique Report Format

When synthesizing findings from all 4 agents, present results as:

```
## Critique Report

**Composite Score: X.X / 10** — [Ready to publish / Needs revision / Major rewrite]

### Scores by Dimension
| Dimension    | Score | Weight | Weighted |
|--------------|-------|--------|----------|
| Authenticity | X/10  | XX%    | X.X      |
| Engagement   | X/10  | XX%    | X.X      |
| Structure    | X/10  | XX%    | X.X      |
| Accuracy     | X/10  | XX%    | X.X      |
| Anti-Slop    | X/10  | XX%    | X.X      |

### Critical Issues (confidence ≥ 90) — must fix
[Issues with suggested rewrites]

### Important Issues (confidence 75–89) — should fix
[Issues with suggested rewrites]

### Suggestions (confidence 50–74) — nice to have
[Issues with suggested rewrites]
```

Group issues by agent source. Include the quoted text, the problem, and a concrete suggested fix.
