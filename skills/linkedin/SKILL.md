---
name: linkedin
description: Draft LinkedIn posts, comments, replies, outreach messages, carousels, and weekly plans; improve profiles and analyze supplied inbox messages or post analytics. Use when the user requests LinkedIn writing, content planning, profile improvements, or reviews of their LinkedIn content.
license: MIT
---

# LinkedIn

Eleven LinkedIn workflows adapted from [avi691/linkedin-agent-skill](https://github.com/avi691/linkedin-agent-skill), revision `e4ec4fb6f1b0e227eb9b14b31b735072db5df9cb`. Shared by Avi Grondin; originally created by Jake Schincariol. See [LICENSE](LICENSE).

## Choose the workflow

Read only the guide needed for the user's request. `/li-*` examples in the guides are workflow labels, not required platform commands; route them to these files.

| User request | Guide |
| --- | --- |
| Post or hook options | [li-post](references/li-post/guide.md) |
| Comment on someone else's post | [li-comment](references/li-comment/guide.md) |
| Replies under the user's post | [li-reply](references/li-reply/guide.md) |
| Profile score or rewrite | [li-profile](references/li-profile/guide.md) |
| Weekly content and engagement plan | [li-plan](references/li-plan/guide.md) |
| Humanize a draft | [li-human](references/li-human/guide.md) |
| Carousel or document post | [li-carousel](references/li-carousel/guide.md) |
| Repurpose a transcript or long article | [li-repurpose](references/li-repurpose/guide.md) |
| Connection note or DM sequence | [li-dm](references/li-dm/guide.md) |
| Triage supplied messages | [li-inbox](references/li-inbox/guide.md) |
| Analyze supplied posts and analytics | [li-audit](references/li-audit/guide.md) |

## Voice and state

Use the user's supplied voice profile, if available; otherwise use `work/linkedin/voice.md` in the current workspace. The starting template is [assets/voice.md](assets/voice.md). Ask for past writing or the missing context when it matters, and preserve information already supplied. Do not invent the user's biography, experience, clients, results, or numbers.

Keep the plan and optional history in `work/linkedin/plan.md` and `work/linkedin/log.md`, relative to the current workspace. Write final downloadable deliverables to the workspace's outputs folder when one is specified. Do not put personal voice profiles, private messages, analytics, plans, or logs into the public skill repository.

## Supporting files

File names in a guide resolve relative to its directory. Cross-workflow `li-post/hooks.json` references mean [references/li-post/hooks.json](references/li-post/hooks.json). Profile scoring uses [references/li-profile/rubric.json](references/li-profile/rubric.json).

Before presenting LinkedIn copy, use the humanizer guide and the bundled Python tools. Invoke the scripts by their absolute installed paths, with scratch drafts in the workspace; `slop.json` is loaded beside each script automatically.

```text
python3 <skill-directory>/references/li-human/humanize.py <draft> -o <clean> --report
python3 <skill-directory>/references/li-human/detect.py <draft> <clean> --json
```

Review the cleaned copy to preserve meaning, proper names, terminology, and the user's voice. Scores are local editing heuristics, not proof of authorship or reliable predictions from an external AI detector. Very short replies cannot satisfy every check; report insufficient text where appropriate. Do not add invented details to raise a score. The detector's exit code 1 can mean REVIEW or FLAGGED; inspect its result before treating it as a script failure. Limit iterative scoring to two revision rounds, then present the best accurate draft with any remaining limitations.

## Deliver the result

Provide copy-ready writing in the host's writing blocks when supported. Use the user's requested length and format; guide defaults are starting points. If they request a completed carousel PDF, make the artifact within that authorization without adding a separate copy-approval step.

This skill prepares drafts for manual use on LinkedIn. It does not publish posts, send messages, schedule platform actions, or modify the account. Log an accepted draft as accepted; mark it published only when the user says it was published. Treat platform limits, timing suggestions, and ranking claims in the upstream guides as assumptions to verify when relevant, rather than guarantees.
