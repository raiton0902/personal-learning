# Review selection

## Evidence to record

Use stable subtopic IDs from the approved curriculum. Record what the learner independently did, when, whether hints were used, repeated failures, last review, next due date, and source of the question. Distinguish conceptual confusion, notation difficulty, and forgetting. Asking the same question often is a signal to investigate, not an automatic failing score. Interest is an example preference, not a reason to omit important curriculum material.

## Choosing earlier material

1. Eligibility: previously taught concepts in the approved course, enabled for review. Exclude untaught or removed topics. Current-topic practice is separate. Never make a learner responsible for an untaught prerequisite by labeling it review.
2. Repeated failed retrieval or a persistent misconception triggers explanation/relearning rather than endless random drilling. Keep these items visible in a repair list; if they block the next lesson, repair them first. Do not mark repaired until a meaningful attempt provides evidence.
3. Within the eligible pool, prioritize due items; weight overdue duration, demonstrated fragility, and curricular importance. Retain a nonzero sampling chance for stronger items. Choose without replacement; shuffle selected question positions alongside current-topic questions.
4. A stronger topic earns a longer interval, not permanent removal. A fast initial answer is insufficient evidence of durable learning: test after a delay and with a changed example.
5. After a review, update from the actual response. Success with substantial help is not independent recall. Supply corrective feedback on errors and use a nearby application when useful.

## Prototype heuristic, not a validated scheduler

The helper accepts `concepts` in a JSON object. Required fields: unique `id`, `taught` boolean, `next_due` (ISO date). Optional fields: `review_enabled` (default true), `status` (`unassessed`, `fragile`, `developing`, `secure`, `needs_relearning`), `lapses` (nonnegative integer), and `importance` (positive finite number, default 1). `needs_relearning` or three lapses routes to the repair list. Three is a configurable prototype threshold, not a scientific cutoff.

Among eligible due items, weight is `importance * fragility * (1 + min(days_overdue, 30) / 10)`. Fragility factors: unassessed 1.5, fragile 3, developing 2, secure 1. Positive weights permit secure concepts to be selected. Items not yet due remain scheduled and are not pulled forward by default. No percentage here is a proven optimal review allocation.

Start with a small review budget, such as one earlier concept in a short quiz. Ask more only when the learner wants a review session or evidence warrants it. If the pool repeatedly favors one subject, reserve occasional slots for neglected due units. The helper alone does not enforce a long-term coverage guarantee; retain selection history and check coverage at unit boundaries.

For a first provisional schedule, use a delayed check at the next suitable session/day. After independent delayed success, increase the interval; after failure, repair and shorten it. Record actual dates; several questions in one sitting do not substitute for practice on different days. No universal interval sequence works for every topic or exam horizon. A mature version can integrate a tested scheduler for recall items; broad conceptual and artistic ability still requires task-specific assessment.

Example command (read-only):

```text
python scripts/select_review.py path/to/state.json --today 2026-10-17 --count 2 --seed 42
```

Omit `--seed` for ordinary randomized selection; retain it for reproducible debugging. Use the learner's local calendar date. The script does not save progress, generate questions, certify mastery, or send reminders.
