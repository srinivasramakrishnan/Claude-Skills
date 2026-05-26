---
name: writing-buddy
description: "Multi-phase writing workflow with parallel critique agents, anti-slop detection, and human authenticity checks. Auto-triggers on writing tasks, drafting, editing, polishing, or content generation. Use /write for the full loop, critique, or polish modes. Triggers on: write, draft, post, linkedin, substack, essay, PRD, spec, document, blog, article, polish, critique, de-slop, edit, review my writing."
---

# Writing Buddy

A rigorous writing loop that produces clean, human, specific content across three formats: LinkedIn posts, Substack essays, and structured documents (PRDs, specs, briefs).

## Commands

| Command | What it does |
|---------|-------------|
| `/write [format] [topic]` | Full loop: ideate → outline → draft → critique → polish |
| `/write critique [file]` | Run 4 review agents on an existing draft |
| `/write polish [file]` | Voice alignment + de-slop + structural tightening |

All three modes live in a single command. `/write` routes to the right mode based on your arguments, or asks if ambiguous.

## Supported Formats

| Format | Length | Loop |
|--------|--------|------|
| LinkedIn post | 100–300 words | Ideate → Draft → Critique → Polish |
| Substack essay | 1,500–3,000 words | Full loop with outline |
| Document (PRD/spec/brief) | 500–2,500 words | Full loop with outline |

## How It Works

The `/write` command flows continuously through phases, asking questions at every decision point:

1. **Setup** — pick format, note any voice calibration samples
2. **Ideate** — align on topic, angle, and key points
3. **Outline** — structure the piece (skipped for LinkedIn)
4. **Draft** — write using anti-slop rules and human authenticity principles
5. **Critique** — 4 parallel agents score the draft
6. **Polish** — apply accepted fixes, final cleanup

## Reference Files

- `references/voice-dna.md` — Voice profile (blank until personalization session)
- `references/anti-slop-rules.md` — Banned phrases and structural patterns to avoid
- `references/format-guides.md` — Per-format rules, phase maps, critique weights
- `references/quality-rubric.md` — Scoring dimensions and thresholds
- `references/calibration.md` — Annotated writing samples for voice matching (blank until personalization session)

## Review Agents

Four agents run in parallel during critique:

- **reviewer-authenticity** — Does this read like a real, specific human wrote it?
- **reviewer-slop** — Any AI-isms, banned phrases, or structural patterns to kill?
- **reviewer-structure** — Does the architecture serve the argument?
- **reviewer-facts** — Are all named claims, numbers, and companies verifiable?

## Human Authenticity Principles

Until a personal voice profile is established, writing is evaluated against these principles:

- Every claim is grounded in a specific, named example within 2 sentences
- The writing has a clear point of view — it takes a position, not just a survey
- Sentences vary in length. Short punchy declaratives earn longer unpacks.
- The opening earns the reader's next click. The closing earns a share or a reply.
- Nothing is vague enough to be true of everything. Specificity is the proof.
- No AI-isms, corporate filler, or false drama. Reads like a person thinking out loud.
