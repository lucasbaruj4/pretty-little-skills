---
name: get-started-webchat
description: Cold-starts a new web chat from a handover kit — reads HANDOVER.md and its carry-over files in the right order, then gets straight back to work. Counterpart to handover-webchat.
disable-model-invocation: true
---

# Get Started (Web Chat)

The counterpart to `handover-webchat`. The usual shape of this is that the previous chat ran out of room, `handover-webchat` packed the work into files, and the user pasted those files straight into you — minutes later, mid-stride. Nothing has changed since they were written. **Treat the kit as current and authoritative, and treat the handoff as a continuation, not a fresh start.**

The failure mode to design against is **the confident cold start**: skimming `HANDOVER.md`, latching onto the first "Next steps" bullet, and charging ahead — re-deriving what's already settled, retrying a documented dead end, or reopening a decision the user already made. The other failure mode is the opposite: reciting the handover back to the user as a book report. They wrote it. They know. They typed "continue" because they want the work continued.

## Step 1 — Use only the files in this chat

The kit is whatever the user attached or pasted **into this conversation**. That's the whole search. Don't go looking anywhere else — not cloud storage, not past chats, not memory. The user hands over deliberately; anything they didn't hand you isn't part of the kit.

If the skill was invoked and no files are present, stop and ask for them in one line, then wait. Don't reconstruct the context from memory or past conversations to be helpful — an invented handover is worse than none, because the user will trust it.

## Step 2 — Read in dependency order

`HANDOVER.md` first, all of it. Its **Files in this handover** table is your reading list, and **How to work with these files** says which file is the source of truth. Read every file listed — carefully for the source-of-truth ones, at least enough to know what's in the rest.

Read for the things that actually change your behavior:

- **Current state** — done vs. in progress vs. untouched.
- **Key decisions** — settled. Don't reopen them unprompted; the user already paid for them once.
- **Dead ends** — don't retry these. Most-ignored section, biggest time saver.
- **Insights & breakthroughs** — the expensive stuff. Carry it forward; don't re-derive it.
- **Blockers, deadlines, open questions** — what's actually in the way.
- **Conventions & vocabulary** — match them. The user shouldn't have to re-teach you their jargon, file layout, or tone.
- **Kickoff prompt** — if present, it names the immediate next action. Take it seriously; it was written by an agent that had the full picture.

## Step 3 — Two quick sanity checks, then go

Not a reconciliation ritual — the kit is fresh. Just two things, both cheap:

- **Does the user's message add or override anything?** They may have done something between chats, or changed their mind. The user wins over the file; note the drift in one line so the file gets corrected, and move on.
- **Is the kit actually old for once?** Check the date in `HANDOVER.md` against today. If it's genuinely stale (days or weeks, not minutes), say so plainly, recompute any deadlines, and flag waiting-on-someone items as needing a check. If it's from today, skip all of this and say nothing about it.

Beyond that, don't re-verify what the handover already states. Second-guessing a kit written by an agent that had the full context, in order to reconstruct it worse from fragments, wastes the exact turn the handover was supposed to save.

## Step 4 — Confirm briefly, then work

Give a short in-chat confirmation — enough to prove you landed correctly, not a recap:

```
**Picking up:** <1-3 lines: the work, where it stands, what's next.>
<At most one question, and only if the next action genuinely can't start without the answer.>
```

Then **start on the next action in the same turn.** If the next step is unambiguous — and the kickoff prompt usually makes it so — do it and show the result. Ending your first turn with a summary and a question, when the handover already answered that question, is the main way this skill fails.

## Step 5 — Keep the chain unbroken

The kit only stays worth anything if each session leaves it current. Update the source-of-truth files as you work (append, don't rewrite — same rule as `handover-webchat`). When the user signals they're wrapping up or running low on context, offer to run `handover-webchat` to fold this session in. Two half-true handovers are much worse than one that's current.

## Edge cases

- **No handover, just context files** — the user drops `notes.md` and `tracker.html` and says "continue". Same job: read them, confirm, act. Then offer to build a proper kit with `handover-webchat` so the next handoff is cheaper.
- **Multiple or rival handovers** — most recent is primary; mine the older ones for decisions and dead ends; tell the user rivals exist so they can be merged.
- **A kit that contradicts itself** — or describes a state the files don't match. Say so, don't paper over it, ask.

## Scaling

Match the ceremony to the work. A one-script handover deserves: read it, one line of "here's where we are", then do the thing. A multi-file, deadline-bound project deserves a fuller read and a fuller confirmation. The test is always: **can you now do the next thing correctly, and does the user believe you can?** If yes, stop talking and start working.
