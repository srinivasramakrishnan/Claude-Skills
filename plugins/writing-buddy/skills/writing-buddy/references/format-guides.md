# Format Guides

Per-format rules for each content type writing-buddy supports. Each format section defines its phase map, length constraints, opening and closing techniques, structural rules, and critique agent weights.

---

## LinkedIn Post

**Length:** 100–300 words
**Phase map:** Ideate → Draft → Critique → Polish (no outline phase)

### Opening Techniques

**Concrete observation:** Lead with something specific you saw, heard, or did — not a thought about it.
> "I shipped a feature last week that three users asked for and zero used."

**Provocative number:** A real stat or count that reframes something familiar.
> "We ran 40 discovery interviews last quarter. The insight that changed our roadmap came from interview 37."

**Direct admission:** Say the uncomfortable thing upfront.
> "I've been wrong about this for two years."

### Closing Techniques
- **Single-sentence callback:** Circle back to the opening in one sharp line.
- **Genuine question:** A real question for the audience — not rhetorical, not to manufacture engagement.
- **One concrete action:** The specific thing you'd tell a colleague to do tomorrow.

### Structure
- No section headers
- 1–2 sentences per paragraph, separated by line breaks
- One bold phrase maximum, only if it earns it
- No hashtag chains or emoji strings
- The last line should feel like punctuation, not a CTA begging for likes

### Critique Weights
| Dimension | Weight |
|-----------|--------|
| Authenticity | 25% |
| Engagement & craft | 20% |
| Structure & flow | 10% |
| Factual accuracy | 15% |
| Anti-slop | 30% |

Anti-slop is weighted highest: LinkedIn is where AI slop is most concentrated and most legible as AI slop.

---

## Substack / Long-Form Essay

**Length:** 1,500–3,000 words
**Phase map:** Ideate → Outline → Draft → Critique → Polish (full loop)

### Opening Techniques

**Gap thesis:** Acknowledge what the reader already knows, then identify the specific gap nobody is addressing.
> "By now, everyone knows AI can write. What nobody's figured out is how to tell when it's worth publishing."

**Two-sentence pivot:** Short declarative, then a "But" or "Except" that reframes it.
> "Prompts and models get all the attention. The thing that actually determines whether a product works in production is evals."

**Table of contents (how-to posts):** Just list what's coming. No preamble.
> "In this post I'll cover: what I got wrong, what I changed, and what I'd tell myself a year ago."

**Personal hook:** Start with a specific anecdote that earns the thesis.
> "When we launched the feature, 12 people used it in the first hour. Three of them filed support tickets."

### Closing Techniques
- **Action plan:** Week-by-week or step-by-step steps the reader can take this week
- **Dialogue invitation:** Invite the reader to respond, with a specific question
- **Callback:** Return to the opening scene or fact and close the loop
- **Resource list:** Curated links, tools, or next reads for how-to posts

### Structure
- Section headers: conversational, not academic (not "Section 3: Implementation")
- Mix of prose paragraphs and lists where lists are genuinely the right format
- Bold for key phrases within prose — not for decoration
- 3–5 sentences per paragraph, no walls of text
- One clear idea per paragraph

### Technical Explanation Pattern
For complex concepts, use this four-layer structure:
1. **Why it matters** — give the reader a reason to care before the explanation
2. **Intuitive frame** — what it's like, in plain language
3. **Mechanism** — how it actually works
4. **Practical implication** — what to do with this information

### Critique Weights
| Dimension | Weight |
|-----------|--------|
| Authenticity | 30% |
| Engagement & craft | 25% |
| Structure & flow | 25% |
| Factual accuracy | 15% |
| Anti-slop | 5% |

---

## Document (PRD / Spec / Brief)

**Length:** 500–2,500 words
**Phase map:** Ideate → Outline → Draft → Critique → Polish (full loop)

Documents are structured artifacts designed to align a team around a decision, plan, or proposal. The goal is precision and clarity, not voice or style. That said, documents should still be specific, grounded, and free of corporate filler.

### Document Types and Signals
- **PRD (Product Requirements Document):** Problem statement, goals, non-goals, user stories, requirements, success metrics
- **Spec:** Technical or functional specification with precise requirements and edge cases
- **Brief:** Concise framing of a problem or opportunity, typically for stakeholder alignment
- **One-pager:** Executive summary format — context, proposal, ask, impact

Ask the user which type they're writing if not obvious from context.

### Opening Techniques

**Problem statement:** State the problem and why it matters, in the first paragraph.
> "Users drop off at the onboarding step where we ask for payment before they've seen value. This costs us approximately 30% of signups at a step with no technical justification for its placement."

**Context + proposal:** Establish the situation, then state what you're proposing.
> "We've had three separate requests from enterprise customers for SSO in the past quarter. This doc proposes a phased approach to delivering SAML-based SSO before Q3."

### Closing Techniques
- **Decision request:** End with the specific decision the document is asking the reader to make
- **Next steps with owners:** List 3–5 next steps, each with a named owner and date
- **Open questions:** A short list of unresolved questions that need input

### Structure
- Standard section hierarchy: H1 for the title, H2 for major sections, H3 for subsections
- Tables for structured comparisons (options, requirements, metrics)
- Bold for key terms on first use
- Bullet points only for genuinely list-shaped content (not for padding)
- Non-goals section is required for PRDs — it prevents scope creep by documenting what this work will not do

### Critique Weights
| Dimension | Weight |
|-----------|--------|
| Authenticity | 15% |
| Engagement & craft | 15% |
| Structure & flow | 35% |
| Factual accuracy | 30% |
| Anti-slop | 5% |

For documents, structure and accuracy dominate. The goal is a document a team can act on — not a compelling read. Anti-slop is still tracked because corporate filler erodes trust in documents.
