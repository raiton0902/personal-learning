# Personal-Learning

An AI tutoring skill that plans a course around your goals and materials, teaches step by step, and revisits earlier topics.

Use it to study a subject over several lessons. It asks what you already know and what you want to learn, then proposes a curriculum. Lessons begin after you approve the plan. You can keep the course in chat or save a checkpoint to resume later.

## Installation and first use

Follow [INSTALL.md](INSTALL.md), then ask:

```text
Use $personal-learning to help me learn C++ step by step.
I know variables and basic loops. Ask about my goals and course materials
before proposing a curriculum, and wait for my approval before teaching.
```

Other examples:

```text
Use $personal-learning to study geometry using my attached syllabus.
Teach in Indonesian and use small worked examples.
```

```text
Use $personal-learning to continue my course from this resume.md file.
```

## What it does

- Builds a plan from your goals, syllabus, and reference materials, including prerequisites you need to cover.
- Waits for your approval before starting lessons.
- Adjusts explanations based on your answers and feedback.
- Uses examples from your interests when they fit the concept.
- Brings back earlier topics for review and mixes problems that use methods you have already learned.
- Saves Markdown checkpoints if you choose, with PDF reading copies when your AI tool can render them.

In chat, ask for `start <subject>`, `continue`, `personalize`, `review`, `plan`, or `checkpoint`. Your AI tool does not need to support slash commands.

## Requirements and limits

Your AI tool must be able to load skill instructions or read Markdown files. Teaching does not require Python. The optional review-selection script needs Python 3.10+ and uses only the standard library. Your AI tool may require an account or subscription; the skill needs no separate API key.

The skill provides instructions for your AI tool to follow. Progress across chats depends on the tool's memory or a checkpoint you supply. It cannot send reminders by itself. Check explanations against your course sources, and use a tool with a PDF renderer if you want PDF exports.

Save your course records outside this repository so they stay separate from files you share. The skill asks before saving them.

## Research basis

| Design choice | Citation | Evidence boundary |
| --- | --- | --- |
| Revisit material after a correct answer | Karpicke & Roediger (2008) [1] | Vocabulary retrieval study; does not establish effects for every subject. |
| Check understanding again in later sessions | Rawson & Dunlosky (2011) [2] | Retrieval and relearning experiments; no universal schedule follows. |
| Mix previously taught mathematical methods | Rohrer et al. (2015, 2020) [3, 4] | Classroom mathematics evidence; not proof of optimal mixing across all subjects. |

These studies support parts of the teaching approach. The skill itself has not been validated with learners. Its review weights, three-lapse relearning trigger, use of interests in examples, and rules for lesson size are prototype choices. The [research notes](personal-learning/references/research.md) and [review policy](personal-learning/references/review-policy.md) explain those choices and their limits.

## Repository layout

```text
README.md
INSTALL.md
CITATION.cff
personal-learning/
  SKILL.md
  agents/openai.yaml
  references/
    research.md
    review-policy.md
    continuity.md
  scripts/select_review.py
```

`select_review.py` reads saved progress and returns the IDs of concepts due for review. The AI tool then writes questions and evaluates your answers. The script leaves your records unchanged. See the [command and fields](personal-learning/references/review-policy.md) and [state example](personal-learning/references/continuity.md).

## References

1. Karpicke, J. D., & Roediger, H. L., III. (2008). The critical importance of retrieval for learning. *Science, 319*(5865), 966–968. [DOI: 10.1126/science.1152408](https://doi.org/10.1126/science.1152408).
2. Rawson, K. A., & Dunlosky, J. (2011). Optimizing schedules of retrieval practice for durable and efficient learning: How much is enough? *Journal of Experimental Psychology: General, 140*(3), 283–302. [DOI: 10.1037/a0023956](https://doi.org/10.1037/a0023956).
3. Rohrer, D., Dedrick, R. F., & Stershic, S. (2015). Interleaved practice improves mathematics learning. *Journal of Educational Psychology, 107*(3), 900–908. [DOI: 10.1037/edu0000001](https://doi.org/10.1037/edu0000001). [Author manuscript](https://files.eric.ed.gov/fulltext/ED557355.pdf).
4. Rohrer, D., Dedrick, R. F., Hartwig, M. K., & Cheung, C.-N. (2020). A randomized controlled trial of interleaved mathematics practice. *Journal of Educational Psychology, 112*(1), 40–52. [DOI: 10.1037/edu0000367](https://doi.org/10.1037/edu0000367).

## Cite this project

> personal-learning contributors. (n.d.). *personal-learning* [AI tutoring skill].

[CITATION.cff](CITATION.cff) contains citation metadata for tools that support it. When publishing, add the repository URL. Include a version or commit when citing a particular release, and cite the original studies when discussing their findings.

## Related projects

Other learning skills found during the initial research include [SugarMGP/study.skill](https://github.com/SugarMGP/study.skill), [derwells/learn-skill](https://github.com/derwells/learn-skill), and [human-aware-teaching-skill](https://github.com/yuanmingze2008/human-aware-teaching-skill). Their inclusion does not imply endorsement. The research claims above rely on the cited studies.

## Publication and reuse

No license has been selected yet. Before inviting others to modify or redistribute the project, add a license that states the permissions you want to grant. The linked papers are not included in this repository and retain their own rights.
