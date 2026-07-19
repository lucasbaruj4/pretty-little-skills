---
name: handover-webchat
description: Packages the current web chat conversation into a portable handover kit (HANDOVER.md, context-enriched copies of every file touched, and a kickoff prompt) so a new chat can pick the work up cold. For the web version of Claude, which has no file-system access of its own.
disable-model-invocation: true
---

# Handover

A conversation ends; the work doesn't. This skill turns a live thread into a **handover kit**: a set of files that let a fresh agent — with zero memory of this chat — resume without re-deriving anything the user already paid for.

The failure mode to design against is the "summary that reads well and helps no one": tidy prose that says *what was discussed* but not *what was decided, why, what's half-finished, and what to type next*. Write for a competent stranger who is about to be dropped into the middle of the work.

## What a handover kit contains

1. **`HANDOVER.md`** — the entry point. Always produced.
2. **Carry-over files** — every file the chat created, edited, or leaned on, prepared so it stands on its own.
3. **A kickoff prompt** — inside `HANDOVER.md`, a block the user can paste as the first message of the next chat.

## Step 1 — Inventory the session before writing anything

Scan the whole conversation, not just the tail, and note:

- **Artifacts**: files created or edited in the chat, files uploaded by the user, files on disk that were read or referenced, external resources (URLs, docs, tickets).
- **Decisions**: choices that got made, and the reasoning that made them. A decision without its "why" gets re-litigated by the next agent.
- **Insights / breakthroughs**: the things that took effort to figure out — the root cause, the working incantation, the realization that reframed the problem. These are the most expensive items in the thread and the easiest to lose.
- **Dead ends**: approaches tried and abandoned, and why. This is what stops the next agent from wasting an hour repeating them.
- **State**: what is done, what is in progress, what is untouched.
- **Blockers and open questions**: including anything waiting on a third party, a deadline, or a decision the user still owes.
- **Conventions**: naming schemes, jargon, tone, file layout, tool preferences that emerged during the chat.

If the conversation history is long and you have a search-past-chats or file-reading capability, use it rather than trusting recall. Handovers built on vague memory are worse than useless — they're confidently wrong.

## Step 2 — Prepare the carry-over files

For each file the work touched:

- **If it already carries its own context** (clear header, explains its purpose and format) — leave the content alone and just include it in the kit.
- **If it doesn't** — add what's missing, at the top, without disturbing the existing content. Use a comment syntax native to the file (`<!-- -->` for Markdown/HTML, `#` for scripts/YAML, `/* */` for code) so nothing breaks when the file is used.

A context header answers, in a few lines:

```
<!-- CONTEXT (added <YYYY-MM-DD> for handover)
Purpose: what this file is for.
Format/conventions: how it's structured, how to append to it.
Maintained by: who or what updates it, and when.
Related: other files in this kit it depends on or feeds.
-->
```

Rules that keep this trustworthy:

- **Never rewrite, reorder, condense, or "clean up" the user's content** while preparing it. Additive only. If a file genuinely needs restructuring, say so in `HANDOVER.md` and let the user decide.
- If a file is already self-explanatory, don't pad it — presenting it unchanged is the correct outcome, and worth saying out loud.
- If the chat produced content that only ever lived in the conversation (a plan, a schema, a draft), promote it to a real file now. It won't survive otherwise.
- Preserve exact identifiers — paths, commands, IDs, names, versions, deadlines. Paraphrasing these is how handovers break.

## Step 3 — Write HANDOVER.md

Use this structure. Skip a section only when it would be genuinely empty, and say so rather than inventing filler.

```markdown
# Handover — <topic> (<YYYY-MM-DD>)

## TL;DR
Three to five lines. What the work is, where it stands, what happens next.

## Context
What we were doing and why. Enough background that a stranger understands the
goal without reading the original thread. Include constraints that shaped the
work (deadlines, environment, hard requirements, things the user rejected).

## Current state
Done / In progress / Not started. Be concrete — file paths, line numbers,
command names, exact status. "Partially working" means nothing; "the poller
runs but drops the wifi field on suspend" means something.

## Key decisions
| Decision | Why | Alternatives rejected |
Each row is a fight the next agent doesn't have to have again.

## Insights & breakthroughs
The hard-won stuff. Root causes found, gotchas, the specific thing that made
it click. Be specific enough to be actionable — this is the section that
justifies the whole document.

## Dead ends
What was tried and didn't work, and why. Explicitly worth writing down.

## Open questions & blockers
Including anything waiting on someone else, with dates if there are any.

## Next steps
Ordered, concrete, each one startable. Lead with the immediate next action.
1. ...

## Files in this handover
| File | What it is | How to use it |
One row per file in the kit, including this one.

## How to work with these files
How the files relate, which is the source of truth, how to append/update them,
what to update at the end of the *next* session so the chain doesn't break.

## Conventions & vocabulary
Project-specific terms, naming rules, tone, tool choices. Only if any exist.

## Kickoff prompt for the next session
> A paste-ready first message: what to read, in what order, and what to do first.
```

Write it plainly. No hype, no "we successfully leveraged". If something is uncertain, mark it uncertain — a handover that hides its own gaps sends the next agent down a hole with confidence.

## Step 4 — Present

Save everything to the output directory and present the files together, `HANDOVER.md` first. Then, in chat, give a two- or three-line summary of what's in the kit and flag anything you couldn't reconstruct.

## Repeat handovers

If a handover file for this work already exists (from an earlier session), **update it instead of creating a rival**. Fold the new state in, refresh the next-steps list, and keep a short dated log at the bottom so the history of the work stays visible:

```markdown
## Session log
- 2026-07-14 — Registered thesis with SRH; still waiting on UPA committee.
- 2026-07-02 — Mapped the dependency chain; sent solicitud.
```

Two half-true handovers are much worse than one that's current.

## Scaling

Match the kit to the work. A short chat that produced one script needs a one-page `HANDOVER.md` and that script with a header — not a ceremonial ten-section document. A three-week bureaucratic saga with five tracked files needs the full structure. The test is always the same: **could a fresh agent, given only these files, do the next thing correctly?** If yes, stop. If no, that's the gap to fill.
