---
name: step-explainer
description: Builds an interactive, HTML artifact that teaches a technical or abstract concept by simulating one concrete instance of it, step by step, with live-mutating state and a decision point for the user. Use when asked to explain a concept visually, "step by step", or to see how something actually works — e.g. git rebase, OAuth, TCP handshakes, garbage collection, attention mechanisms, event loops, database transactions.
---

# Step Explainer

Teaches a concept by simulating one concrete instance of it, rather than describing it abstractly.

## Core idea

Don't explain the concept — simulate one instance of it and let the user drive, one step at a time. A text explanation gives the abstraction; this artifact makes the invisible thing visible and tactile.

## How to build one

1. **Find the hidden object.** Every teachable concept has something that changes over time — a payload traveling through a pipeline, a shared state in a protocol, the structure itself in a data structure, a resource pool. That object becomes the live panel at the top of the artifact.
2. **Pick one fully concrete scenario.** Real numbers and names, not "a request flows through the system" — "user 8812 requests a refund on order #4471."
3. **User-driven steps, never autoplay.** One "step" button; each tap is one transition. Show progress (e.g. "step 3/9").
4. **Mutate the hidden object visibly.** On each step, diff against the previous state and highlight what changed.
5. **Force a decision at the pivotal moment.** At the step that embodies the concept's core idea, stop and make the user choose (approve/reject, pick a branch, resolve a conflict). Implement both branches for real.
6. **Include one deliberate failure and recovery** (retry, rollback, timeout, fallback) — this is often where the concept's whole reason to exist lives.
7. **Show the paths not taken** as dimmed "ghost" elements with a one-line note.
8. **Annotate each step in plain language**: what just happened, who or what decided it, and what it really is underneath the abstraction.
9. **End with a short recap**: totals plus a one-line honest takeaway.

## Layout by concept type

- Flows/pipelines: vertical cards with connectors between them.
- Protocols/negotiations: actor columns, messages as arrows, shared state tracked centrally.
- Data structures: the structure itself is the canvas; steps highlight/move/insert elements.
- State machines: a ring or list of states, current one lit, transition log below.
- Resource management: a visual pool that fills, drains, or gets collected.

If a concept fits none of these, design the layout around its hidden object rather than forcing a mismatched template.

## Build mechanics

- Single self-contained HTML file, vanilla JS (no framework unless truly needed).
- Model steps as an array of functions; each mutates a `state` object, re-renders, and returns `'wait'` at a decision point (swap controls for choice buttons) or `'end'` when done.
- 7-10 steps — enough to not feel trivial.

Match the visual style and language to whatever's appropriate for the conversation.
