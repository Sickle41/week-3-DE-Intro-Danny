# DECISIONS.md

> Day 3 deliverable. Real data engineers leave a trail of *why*, not just *what*.
> Keep this short and honest — a few sentences per question. You're defending the
> calls you made about getting data out of a real API.

## 1. Auth: you sent a Bearer token to an API that ignores it. Why bother?

The Rick and Morty API needs no key. But your `build_client` sends an
`Authorization` header when a token is set. Why wire that now, and how would this
exact code change (or not) if you pointed it at an API that *did* require a key?

_Your answer:_

## 2. The "land raw" principle: why land the untouched API response to S3 first?

You could have fetched and cleaned in one pass. Instead you land the raw JSON to
S3 and transform from there. What does that buy you the next time a transform is
wrong — and how does it interact with rate limits?

_Your answer:_

## 3. Pagination: how did you know you'd fetched *all* the data?

Describe how `fetch_all_characters` decides it's done. What would go wrong if you
hard-coded the number of pages instead?

_Your answer:_

## 4. Rate limits: why honor `Retry-After` instead of a fixed `sleep`?

On a 429, your code waits for the duration the server asked for. Why is that
better than `time.sleep(5)` in both directions (too short *and* too long)? And
why reach for tenacity rather than writing the retry loop yourself?

_Your answer:_

## 5. Idempotency / dedup: why dedup by `id` if each character is unique?

`dedupe_characters` keeps one row per `id` even though the API's characters are
already distinct. What real situation makes this defensive step worth keeping?

_Your answer:_

## 6. Code review: what did ruff catch in `explore.py`, and what did you learn?

Pick two findings ruff flagged. For each, say what the rule is protecting against
— not just "it was unused," but *why a reviewer cares*.

_Your answer:_

## 7. If this were a production ingestion

Name one thing you'd add before trusting this to run unattended every night
(e.g. logging, incremental fetch, alerting, schema checks, secrets handling) and
why that one first.

_Your answer:_
