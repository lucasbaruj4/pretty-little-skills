---
name: in-english
description: Translates jargon-heavy tech/AI language into plain terms. Use when the user pastes a word, acronym, announcement, or paper and asks what it actually means, or asks to "decode", "de-mystify", or "explain in plain English" something.
---

# In English

Strips hype and jargon down to plain language.

## Principles

1. Reduce first, nuance second: lead with the crude one-liner ("it's just X"), then add one honest caveat only if the reduction loses something real.
2. Name the hype: if a claim is mostly marketing, say so directly.
3. Give credit where due: if there's a genuine advance under the buzzwords, say that too.
4. No jargon in the explanation. If a technical term is unavoidable, define it in a few words inline.
5. Keep it short: a few lines for a single term, one screen for a release or paper.

## Word mode

Input: a word, phrase, or acronym.

Output:
```
**<term>** = <plain one-liner>
Simpler: <even cruder version, or an everyday analogy>
(optional) Caveat: <the one nuance the reduction hides>
```

If it's marketing-speak with no real referent, say so: "this means nothing specific; they mean <best guess>."

## Release / paper mode

Input: a link, announcement, or abstract.

1. Fetch or search it — don't decode from memory alone.
2. Find the actual technical substance under the prose.
3. Output:

```
## <Name of the thing>

**It's literally:** <one sentence — the "it's just X">

**Claim vs. reality:**
- Claim: "<their most inflated phrase, quoted short>"
- Reality: <plain translation>
(2-4 of these max, the worst offenders)

**Is there anything real here?** <genuine advance / incremental / pure marketing, in 1-2 sentences>
```

## Avoid

- Explaining jargon with more jargon
- Hedging every sentence — commit to the reduction
- Being reflexively cynical about everything
- An output longer than the thing it's decoding
