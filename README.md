[English](README.md) | [한국어](README.ko.md)

# Creator Topic Radar

Research short-form topics and see the evidence behind each recommendation.

Creator Topic Radar is an Agent Skill for creators, content marketers, and researchers working on YouTube Shorts, TikTok, Instagram Reels, and similar formats. It turns creator videos, recent events, or your research backlog into a shortlist with separate assessments of interest, freshness, factual reliability, duplication, and roughly 60-second fit.

**Version:** v0.1.0 · **License:** [MIT](LICENSE)

## Get started

This is a folder of Markdown instructions for an AI agent, rather than a standalone application. You need an agent that can read the folder; live research also requires access to web sources. There is no bundled platform API or database connector.

1. Get the complete `creator-topic-radar` folder from [the repository](https://github.com/MinhaKim02/creator-topic-radar). You can use GitHub’s **Code → Download ZIP**.
2. Install it in your host's configured Agent Skills directory, keeping `SKILL.md` and `references/` together. Follow that host's discovery instructions. If your agent can read files but does not load skills automatically, ask it to read `SKILL.md` and the linked references explicitly.
3. Provide your audience, subject, research window, target platforms, and any past-content list. Ask for a shortlist:

```text
Use $creator-topic-radar to find up to three topics from the last seven
days for consumers interested in repairing everyday products.
Start with creator-led YouTube videos, verify the underlying events,
and compare with the past-content list I provide. Use UTC.
Return a shortlist with sources and uncertainties; do not write scripts.
```

`$creator-topic-radar` invocation depends on your host. Automatic installation and discovery have not been validated per host. Provide only data the agent is authorized to access. If important context is missing, the skill asks for it or states its assumptions. Results follow your language unless you request another.

## What you get

Each candidate includes a working title, one core question, what the video would explain, why the audience may care, an event/update timeline, sources, five separate assessments, caveats, research gaps, and a recommendation. A relevant backlog record can be linked when it supports the question.

**Illustrative result:** A fictional maker launched a toaster in May and announced replacement parts in September. A candidate might ask, “What does the new parts announcement change for owners?”

| Assessment | Example judgment |
|---|---|
| Audience Interest | Unassessed: no creator evidence supplied |
| Freshness | Old event + new development: date the launch and parts announcement separately |
| Factual Reliability | Supported announcement: availability remains a company claim and does not establish lower repair costs |
| Duplicate Risk | Unassessed: no past-content list supplied |
| Short-form Suitability | Strong for the announcement's scope; cost savings require more evidence |

This invented example shows the format, not a completed investigation. The [full output template](references/output-template.md) includes citation requirements and the selected-topic handoff.

The workflow ends at topic selection. After you choose a topic, you can request a factual handoff with sources, caveats, and open questions. Scripts, scene design, production prompts, and publishing belong to a separate workflow.

## Discovery modes

| Mode | Start with | What the skill investigates |
|---|---|---|
| Creator-first | Creator videos | Channels and accessible adjacent creators, recurring questions, underlying events, and factual sources |
| Entity-first | A company, product, person, industry, or technology | Concrete recent changes, an audience question, creator interest, and evidence |
| User-database-first | Your records, notes, spreadsheet, or archive | The actual claim, event date, current status, evidence, and audience relevance |

Modes can be combined. A company name is a starting point, not a topic; a newly created record is not necessarily a recent event.

## Why this approach?

Repeated research can confuse visibility with truth, article dates with event dates, or a different company name with a different story. Creator Topic Radar translates those failure modes into reusable rules and evaluation cases. Its judgments are intended to be explainable, not reduced to an arbitrary weighted score.

The sequence is: establish the brief → discover candidates → identify events and updates → investigate interest and facts separately → assess duplication and fit → recommend with evidence.

| Judgment | Rule that matters |
|---|---|
| Creator interest | Creator videos show attention; compare age, reach, and metric provenance. Treat new uploads as early when performance is not yet judgeable. |
| Freshness | Separate event, publication, record, claim, and material-update dates. A new article may be commentary on an old event. Historical research uses evidence available by the cutoff. |
| Factual evidence | Check appropriate direct sources. Separate verified facts from company claims, reports, interpretation, and predictions; show material conflicts. |
| Duplicates | Compare the question, mechanism, conclusion, and viewer takeaway, not just names. Compare within the shortlist too, and qualify judgments against the history actually supplied. |
| Short-form fit | Keep one question and its essential caveats. Narrow the scope instead of overstating facts to fit 60 seconds. |

Official evidence does not demonstrate audience interest, and creator popularity does not verify a claim. A business/investment angle is used only when a supported mechanism connects it to the story.

## Examples

| Example | English | Korean |
|---|---|---|
| Weekly creator-first research | [Prompt and behavior](examples/en/weekly-topic-research.md) | [요청과 기대 행동](examples/ko/weekly-topic-research.md) |
| Entity to topic | [Prompt and behavior](examples/en/entity-to-topic.md) | [요청과 기대 행동](examples/ko/entity-to-topic.md) |
| Database to topic | [Prompt and sample result](examples/en/database-to-topic.md) | [요청과 기대 행동](examples/ko/database-to-topic.md) |

All example records and creators are fictional. Real runs require current source verification.

## Repository map

| Path | Role |
|---|---|
| `SKILL.md` | Single canonical English execution instruction; output follows user language |
| `references/` | Detailed rubric, freshness rules, creator signal guide, and output template |
| `README.md`, `README.ko.md` | Matched English/Korean user-facing documentation |
| `examples/en/`, `examples/ko/` | Paired prompts and clearly fictional demonstration fixtures |
| `tests/cases.md` | Behavioral evaluation cases and review criteria |
| `agents/openai.yaml` | Optional host UI metadata |
| `CHANGELOG.md` | Version history and draft publication status |

## Limits and evaluation

Search coverage, platform metrics, same-age comparisons, and recommendation-graph access depend on available tools. Missing metrics do not establish lack of interest; missing content history leaves duplicate risk unassessed. Offline work can evaluate supplied evidence, but cannot establish later real-world developments.

The skill returns fewer candidates, or none, when evidence is insufficient. It does not predict virality or guarantee factual accuracy, views, or research-time savings. Cross-host compatibility has not been broadly tested.

[Evaluation cases](tests/cases.md) provide synthetic inputs and a review protocol, not benchmark results. Test in your own environment before relying on the workflow.

## Versioning

v0.1.0 is the initial draft. Use patch releases such as 0.1.1 for small fixes, minor releases such as 0.2.0 for substantive workflow changes, and 1.0.0 after sufficient practical testing. See [CHANGELOG.md](CHANGELOG.md).

## Roadmap

Potential improvements include age-adjusted comparisons, cross-platform signals, stronger duplicate tests, and repeated-run evaluation with accepted/rejected recommendation records, datasets, and benchmarks. These are planned directions, not completed results.

## Feedback

Report problems in an issue with the prompt, public or fictional inputs, and the unexpected result. If you submit a fix, keep the English/Korean documents aligned. Do not include private data or credentials.

## License

Released under the [MIT License](LICENSE). Copyright (c) 2026 Minha Kim.
