# Continuity contract

## Persistence options

Offer a choice after curriculum acceptance: chat only, Markdown, or Markdown plus a rendered PDF. If saving is selected, choose a course folder in the current workspace or the learner's specified location. Read existing files before updating; never replace another course. A PDF is a reading copy; editable Markdown and structured state make resumption easier. No automatic reminders or remote uploads are implied.

Suggested course files, created only when selected:

- `curriculum.md`: version, approval status/evidence, learner goal, school/exam context, ordered objectives and stable concept IDs, prerequisites, sources/sections, review opportunities, optional enrichment.
- `learner.md`: chosen language, tone, interests and analogy boundaries; task-specific pace evidence with dates; explicit corrections. Separate learner statements from tentative observations.
- `state.json`: schema version, curriculum version, current objective, pending question, next step, concept evidence and review dates. Keep free-form notes short.
- `resume.md`: concise human-readable handoff containing the current objective, last attempted task, pending response, prerequisite gaps, next teaching move, and links to the authoritative files.

Minimal state shape (example data, not an actual learner):

```json
{
  "schema_version": 1,
  "curriculum_version": 1,
  "curriculum_approved": true,
  "current_objective": "geometry.triangle-area",
  "pending_question": null,
  "next_step": "Explain why perpendicular height matters using the chosen example",
  "concepts": [
    {
      "id": "algebra.linear-equation",
      "taught": true,
      "status": "developing",
      "next_due": "2026-10-17",
      "lapses": 1,
      "importance": 1,
      "evidence": "Solved a changed example with one hint",
      "last_review": "2026-10-16"
    }
  ]
}
```

On resume, read curriculum approval/version, learner preferences, current state, then relevant sources. Do not restart a completed lesson or silently treat a pending question as answered. If state is missing or contradictory, state what is known and ask only for the missing detail that affects the next step.

On meaningful scope changes, show the change and obtain acceptance before replacing the approved curriculum. Ordinary explanation repairs do not require repeated curriculum approval. Save at meaningful lesson boundaries or before a known handoff; avoid dumping the transcript. Check JSON parses and verify the resulting files exist and contain the intended content before reporting success.

For chat-only use, produce a concise copyable checkpoint when useful, without implying persistence. A checkpoint should let another agent resume, but it cannot restore unavailable source files or guarantee another host will obey the skill.
