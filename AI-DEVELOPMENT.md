# An AI-led game-development experiment

Frostwatch was created through human direction and extensive AI implementation. **The AI had substantially more control over day-to-day implementation than the human.** The human set the goal, directed priorities, supplied/acquired library assets, challenged inadequate results, played the game, reported bugs and drove repeated corrections across many iterations. The AI selected and executed most technical approaches, wrote and revised code and scripts, integrated assets, built packages, ran diagnostics and prepared documentation/releases.

This was a practical test of how far an AI agent could take game development under continuing human direction and scrutiny. It was not a one-prompt game, a fully autonomous project without oversight, or a claim that the AI created all the artwork. The human's testing and challenges were central to the bug-fixing cycle. External artists, animators, recordists and engine/tool creators supplied substantial underlying work and receive their own full credits in CREDITS.md.

## Division of work

| Human direction and review | AI implementation and iteration |
| --- | --- |
| Defined the fantasy adventure and desired visual quality | Planned and implemented gameplay, world, UI and authoring systems |
| Requested the Unreal migration and selected priorities | Migrated systems, imported/adapted assets and authored integration scripts |
| Added owned resources to the library | Selected and integrated usable content, resolved technical incompatibilities |
| Challenged flat terrain, bad water, floating objects, dark areas, weak combat and poor audio | Investigated reports, changed code/materials/content, rebuilt and tested |
| Required better laptop performance and careful disk use | Profiled rendering, compared alternatives and managed memory/build budgets |
| Set the no-purchases constraint and requested public release | Prepared runtime-only downloads, credits, checksums and GitHub documentation |

Many results needed multiple attempts. Automated tests missed obvious visual problems; screenshots and human playtesting exposed them. Some experiments were rejected after performance or visual review. The current preview still has documented limitations. No percentage of human versus AI authorship has been measured, so none is invented here.

## Models and tools actually evidenced

| Model / system | Role and evidence |
| --- | --- |
| **OpenAI GPT-6 Astra (`gpt-6-astra`) through Codex** | Development model recorded in the audited local session metadata: code, reasoning, tool orchestration, troubleshooting and documentation. |
| **`codex-auto-review`** | Recorded automatic-review identifier. It is not a confirmed public model name; the underlying routed model is not identified in these records. Its measured usage is separated below. |
| **Kokoro v1.0 / Kokoro-82M** | Current offline dialogue synthesis, using kokoro-onnx and British English voice profiles/blends. Not an in-game live AI service. |
| **Piper `en_GB-northern_english_male-medium`** | Historical native-edition narration. Superseded for current dialogue; original tale audio is not in the 0.4 cooked inventory. |
| **Built-in image-generation tool** | Historical generated spruce-branch texture recorded in the credits. The exact backing image model was not established from the available evidence; no model name is guessed. |
| **Microsoft George / Hazel Desktop** | Earlier system text-to-speech, subsequently replaced for current character dialogue. These are voice-engine names, not Codex development models. |

Codex is the development agent/application. Unreal Engine, Python, PowerShell, Git, ONNX Runtime and the asset libraries are tools or resources, not additional language models. Third-party models and assets are credited independently; their authorship is not attributed to the coding AI.

## Recorded token burn

**Snapshot: 2026-09-16T06:44:06.600734+00:00 (UTC).** The audit found **19 local sessions** and **4,034 unique response-usage records** in the identified creation/development workspaces.

| Metric | Recorded tokens |
| --- | ---: |
| Total input + output | **518,407,678** |
| Input, including cached input | 516,201,488 |
| Cached input — subset of input | 504,491,520 |
| Uncached input — input minus cached input | 11,709,968 |
| Output, including recorded reasoning | 2,206,190 |
| Reasoning output — subset of output | 863,046 |

Cached input represents 97.73% of recorded input. **Do not add cached input or reasoning tokens to the total again.** Long tool-heavy conversations repeatedly submit context; this token volume does not mean that much original text or source code was created. Prompt caching can reuse previously processed input; see [OpenAI's prompt-caching documentation](https://developers.openai.com/api/docs/guides/prompt-caching).

| Recorded model identifier | Input | Cached subset | Output | Total |
| --- | ---: | ---: | ---: | ---: |
| `gpt-6-astra` | 506,705,704 | 495,989,760 | 2,190,476 | 508,896,180 |
| `codex-auto-review` | 9,495,784 | 8,501,760 | 15,714 | 9,511,498 |

These are local telemetry counts, not an invoice, subscription-quota calculation or financial cost estimate. Image-generation and offline speech compute are not separately quantified by this Codex token audit. No API-equivalent price is invented.

## Recorded time spent processing

- **Active task wall time, overlapping intervals merged: 35 hours 21 minutes 55 seconds.**
- Sum of task intervals before merging overlaps: 35 hours 34 minutes 6 seconds.
- Calendar span between the earliest included task start and this snapshot: 130 hours 19 minutes 24 seconds.

“Active task wall time” includes model responses, tool calls, builds, cooking, captures, downloads and waits inside active turns. It excludes gaps between turns, but it is **not pure model inference time, GPU-hours, human working hours or uninterrupted useful computation**. Those quantities cannot be recovered reliably from the available records. The current publishing/documentation turn is counted only up to the snapshot; work after that point is excluded.

## Method, scope and limitations

The audit reads local session metadata, per-response `token_usage_record` entries and task-start/task-complete events. Response IDs are deduplicated across files before summing; cumulative token counters are not repeatedly added. Completed task intervals are merged to avoid double-counting overlapping agent work. The active task is capped at the snapshot. Recorded identifiers are used without guessing hidden model routing.

The selected scope includes Frostwatch working directories and the confirmed original creation workspace. It includes historical subordinate/reviewer activity and preliminary setup or ancillary work inside those sessions. It is therefore a **recorded project-associated total**, not a perfectly isolated game-only meter. Missing, deleted, remote or unrecorded sessions cannot be counted. This is a reproducible local-log snapshot, not an independently audited end-to-end labour/cost study.

Only aggregate, sanitised metrics are published in [DEVELOPMENT-METRICS.json](DEVELOPMENT-METRICS.json). Raw conversation logs, private prompts, account details and local file paths are not published.

## Scope of the 0.5.1 update

The continuing human-directed, AI-led iteration added the connected story, parchment/book interface, castle atmosphere and revised lantern. The human requested and challenged the visual direction; AI implemented, built, tested and documented the changes. The usage figures above and DEVELOPMENT-METRICS.json remain the explicitly dated 2026-09-16 06:44 UTC audit snapshot. They exclude later work, including this release preparation; they are not a current lifetime total. No additional token count, processing duration or model identity is inferred without an audited record.

## 0.5.2 update

The human authorised an economical player-first release programme. AI implemented and tested short humanoid pose transitions, reading preferences and extended performance diagnostics, and prepared the roadmap and playtest forms. Existing animation and font assets were reused; no new model or paid asset was introduced for these features. The token/time figures above remain the dated audit snapshot and exclude this later work. External human playtests have not been fabricated or counted as completed.

## 0.5.3 update

Continuing the human-authorised readiness programme, AI implemented save verification/recovery, failure feedback, compact combat cues and adaptive pause/title spacing. Existing assets were reused. The token and processing-time figures remain the explicitly dated audit above; they do not include this later work. Automated checks and scripted play are not represented as external human playtesting.
