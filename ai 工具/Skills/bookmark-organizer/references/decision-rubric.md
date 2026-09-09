# Classification Decision Rubric

Use this rubric when the bookmark's destination is ambiguous.

## Evidence hierarchy

1. Page title / page semantics
2. URL path and site context
3. Existing folder
4. Likely future retrieval purpose
5. Source website

Existing folder is a weak prior, not ground truth.

## Primary-use test

Ask:

> If the user remembers this bookmark six months from now, what phrase are they most likely to search for?

Use that phrase/topic to guide placement.

## Confidence

### HIGH

The bookmark has an obvious semantic home.

Example:

`Redis 官方文档` -> `Development / Redis`

### MEDIUM

Two plausible homes exist.

Example:

`OpenAI Agents SDK GitHub repository` -> `AI / Agent` vs `Development / SDK`

Prefer one primary location and record the ambiguity.

### LOW

There is insufficient evidence from title and URL.

Place in Inbox/review instead of guessing.

## Duplicate preference

When two exact-URL duplicates must eventually be reduced, prefer the survivor with:

1. clearer title
2. more appropriate folder
3. canonical/stable URL
4. better recognizable context

Do not claim page quality without evidence.
