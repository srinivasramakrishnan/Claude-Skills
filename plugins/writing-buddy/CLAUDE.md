# Writing Buddy Plugin

This plugin is the source of truth for writing workflow, quality standards, and content generation for this workspace.

## Voice Profile Status

The voice profile at `skills/writing-buddy/references/voice-dna.md` is currently a blank placeholder. Until it is populated, the authenticity reviewer operates in **human authenticity mode**: evaluating writing for genuine human tone, specific grounded claims, and clear point of view — rather than matching against a named voice.

The calibration file at `skills/writing-buddy/references/calibration.md` is also blank pending a personalization session.

## For All Content Creation

Use `/write` for the full writing loop. To review an existing draft, run `/write critique [file]`. To polish an existing draft, run `/write polish [file]`. All three modes are handled by the single `/write` command.

## Anti-Slop

The canonical anti-slop rules are at `skills/writing-buddy/references/anti-slop-rules.md`. Apply them to ALL written content, not just content produced through `/write`.

## Key Principle

**Default to asking, not assuming.** At every decision point — angle, tone, audience, examples — use AskUserQuestion rather than making creative assumptions. The goal is content the user actually wants to publish, not content that approximates what they might want.

## Supported Formats

LinkedIn post, Substack/long-form essay, Document (PRD, spec, brief, etc.)

## Draft Storage

Drafts are saved to `${CLAUDE_PLUGIN_ROOT}/drafts/` using the naming pattern `YYYY-MM-DD-slug.md`.
