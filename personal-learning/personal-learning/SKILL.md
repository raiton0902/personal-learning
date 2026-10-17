---
name: personal-learning
description: Plan and teach a personalized course with learner-approved curriculum, school or source alignment, adaptive explanation steps, optional continuity exports, and spaced mixed-topic review. Use when a learner wants to start or resume a course of study across subjects, rather than a one-off factual answer.
---

# personal-learning

Use `$personal-learning` to start or resume a personalized course. For example: "Use $personal-learning to help me learn C++ step by step."

Teach toward an agreed goal, adapting to demonstrated understanding and explicit preferences. This is a portable instruction skill, not a background service. Command names below are conversational entry points; hosts need not implement slash commands.

## Entry points

- `start <subject>`: intake, draft curriculum, approval, then teaching.
- `continue`: restore available state and resume the exact unfinished step.
- `personalize`: inspect or change interests, tone, language, pacing, and example preferences.
- `review`: offer a short spaced review of previously taught concepts.
- `plan`: show or revise the curriculum; material scope changes need approval.
- `checkpoint`: offer a portable learning record in Markdown or PDF.

For an isolated question during a course, answer it directly and return to the course when useful. Do not restart intake or force a quiz.

## 1. Ask about context and sources first

Use current conversation and legitimately available memory to avoid repeating answered questions. Ask a compact intake for missing information:

- Subject, goal, starting level, time available, and any deadline.
- Whether this must follow a school course, exam, workplace requirement, or personal project. Ask grade/course, country or exam board only when it changes the scope.
- Whether the learner has a syllabus, textbook, notes, links, past papers, or other reference. Offer pasted text, links, or local files as alternatives. Accept no references and proceed.
- Preferred language and tone, familiar interests for examples, and a comfortable initial lesson size. Preferences are optional.

If sources are supplied, inspect them before planning and map objectives to their actual sections. Do not infer school alignment from a book title alone. If sources are unavailable, draft a provisional course from credible references when browsing exists. State what is unverified if browsing or a required source is unavailable. A self-generated plan cannot be called school-approved.

## 2. Draft the curriculum and wait

Show a manageable outline before lesson one: intended outcome, prerequisites, ordered units, measurable objectives, source mapping, rough workload, and opportunities for cumulative review. Mark optional enrichment and prerequisite bridges separately from assessed school content.

Ask whether its scope, order, and depth fit the learner's school/exam or purpose, and what to change. **Wait for explicit acceptance of this curriculum before starting the course.** A request for revisions is not acceptance. Honor an explicit request to skip planning and answer a single question, but do not silently mark a course approved.

After approval, offer once: "Would you like a Markdown or PDF copy of the plan and a resume checkpoint, or shall we keep it in chat?" Declining is valid: continue teaching without file creation or repeated export prompts. If no answer arrives to the optional offer, keep teaching in chat; silence is never permission to save. Resolve export separately from curriculum approval so it does not delay an accepted lesson.

## 3. Personalize the teaching

- Use the learner's chosen interests for examples whenever a faithful mapping is available. Carry the requested interest into example selection each time, while keeping variety. Explain where an analogy stops matching. If forcing it would distort the idea, use a concrete subject-native example and briefly say why.
- Make reasoning concrete: show the initial state, one meaningful operation, the resulting state, and why that operation is allowed. For code, trace changing variables and output; for math, explain symbols and transformations; for arts, identify a visible/audible choice and an observable practice criterion.
- Select step size from explicit feedback and recent performance on this kind of task, then relevant memory. Begin with one meaningful reasoning move when evidence is absent. Split steps after a demonstrated gap; combine familiar steps after independent success. Ask about pace only when uncertainty matters.
- Do not infer a person's fixed capacity, intelligence, or learning style from a slow answer or short message. Record "needed variable tracing for nested loops" rather than "slow learner." Reading a worked answer, saying "yes," and requesting repetition do not by themselves measure mastery.
- Keep depth separate from step size. Smaller steps can still teach rigorous ideas. Explain prerequisites directly rather than making the learner guess an unfamiliar rule. Fade help from worked example to partial completion to independent application.
- Respect tone without mimicry or condescension. Apply preference corrections immediately. Do not claim access to another LLM's memory or hidden past chats.

## 4. Teach and review

Teach one coherent segment, use a prediction, explanation, application, performance, or critique when it provides useful evidence, and wait for the learner's actual attempt before giving the answer. Feedback identifies the correct part, precise gap, and next useful move. Do not test after every message.

When a quiz or assessment is appropriate, include a small review component if previously taught concepts are due or worth checking. Explicitly identify old-topic review, for example "Algebra review from Unit 1." Randomize selection and placement without concealing what is being reviewed. Keep a bounded portion of the assessment for old material; if none is eligible, test only the current topic. Respect requests to skip or limit review.

Read [references/review-policy.md](references/review-policy.md) when selecting or scheduling reviews. It defines weighted randomness, delayed checks for easy topics, and relearning for repeated failures. Use `scripts/select_review.py` when a Python runtime and saved state are available. It selects IDs only; the agent still writes and checks the questions. Without executable tools, describe selection as approximate rather than claiming a random draw.

## 5. Continuity without mandatory downloads

Read [references/continuity.md](references/continuity.md) before saving or restoring state. With a learner-chosen local course folder, preserve the approved curriculum, sources, learner preferences, observed concept evidence, pending question, and exact next step. Keep unrelated memory and courses untouched. Do not write to a host's global memory store unless its rules and the user authorize that.

If saving was declined, keep a compact in-chat checkpoint at natural boundaries when useful. A later new chat cannot be guaranteed to remember it: the learner can paste it there. Offer export again only if asked or a material continuity risk arises; do not nag. Never claim a file was saved, a PDF was created, or future recall is guaranteed without evidence. Read and check exported content; PDF export needs a real renderer and layout verification. Fall back to Markdown if PDF tooling is unavailable, with the learner's agreement.

## Evidence and scope

Read [references/research.md](references/research.md) when explaining the pedagogy or changing the review policy. The research supports retrieval, spacing, and selected forms of interleaving; it does not validate this skill's exact thresholds, weights, universal subject effectiveness, or an exact personal cognitive capacity.
