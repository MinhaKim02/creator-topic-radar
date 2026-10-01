[English](README.md) | [한국어](README.ko.md)

# Creator Topic Radar

An Agent Skill for researching short-form topics with sources, clear questions, and visible uncertainty.

Find candidates from creator videos, recent events, or your research backlog. Assess audience interest, freshness, factual evidence, duplication, and roughly 60-second fit separately. Built for creators, content marketers, and researchers working on YouTube Shorts, TikTok, Instagram Reels, and similar formats.

**Version:** v0.1.0 · **License:** [MIT](LICENSE)

## When to use it

| You want to… | Start with… | The skill helps you… |
|---|---|---|
| Find topics for the coming week | Creator videos | Identify recurring questions and verify the underlying events |
| Turn a product or company update into a topic | An entity or announcement | Find a specific audience question supported by the evidence |
| Review a research backlog | Your records, notes, or archive | Separate recent developments from old events and unsupported claims |

The workflow ends at topic recommendations. After selecting a topic, you can request a factual handoff. Scripts, scene plans, and publishing belong to a separate workflow.

## Get started

You need an AI agent that can load skills or read their files. Live research also needs web-source access; evaluating a supplied packet can be done offline. This repository contains instructions, not platform APIs or database connectors.

### Install

For **Claude Code**, run this in a terminal from your project directory. You need Node.js/npm and Git:

```sh
npx skills@1.7.0 add MinhaKim02/creator-topic-radar \
  --skill creator-topic-radar --agent claude-code --copy --yes
```

The command copies the skill into your project's `.claude/skills/creator-topic-radar/` folder. The project installation and its supporting files were checked with Skills CLI 1.7.0. See the [Skills CLI documentation](https://github.com/vercel-labs/skills) and [Claude Code skill documentation](https://code.claude.com/docs/en/skills).

For other hosts, use their documented skill location. You can download the repository using **Code → Download ZIP** and keep `SKILL.md` with `references/`. If automatic skill loading is unavailable, ask a file-capable agent to read `SKILL.md` and its linked references.

### Ask for topics

In Claude Code, invoke `/creator-topic-radar` and add your brief. Other hosts may use a different invocation.

```text
/creator-topic-radar
Find up to three topics from the last seven days for consumers interested
in repairing everyday products. Start with creator-led YouTube videos.
Verify the underlying events and compare with my attached past-content list.
Use UTC. Return sources, caveats, and missing evidence. Stop at the shortlist.
```

Provide your audience, subject, time window, platforms, and past-content history when available. Important missing context is clarified or recorded as an assumption. Output follows your language unless you request another. Supply only material you are authorized to use.

## From input to decision

**Fictional examples**, evaluated as of October 1, 2026 for a seven-day research window:

| Supplied input | Resulting decision |
|---|---|
| A record created October 1 describes a May 1 launch, with no later update | Do not call the launch recent; record date and event date differ |
| A May launch has a supplied September 29 replacement-parts announcement | Consider the new announcement; it does not establish lower repair costs |
| Two candidate titles describe the same event, mechanism, and takeaway | Merge the overlap before counting recommendations |

Each recommended candidate includes a working title, one core question, what the video would explain, audience relevance, dates, sources, five separate assessments, caveats, and research gaps. Missing creator evidence leaves interest unassessed; missing content history leaves duplication against past content unassessed.

See a [complete fictional candidate and handoff](examples/en/database-to-topic.md) or the [output template](references/output-template.md). These examples show the format, not live research results.

## Examples and reference

| Document | What you will find |
|---|---|
| Weekly topic research — [EN](examples/en/weekly-topic-research.md) / [KO](examples/ko/weekly-topic-research.md) | A creator-first request and expected behavior |
| Entity to topic — [EN](examples/en/entity-to-topic.md) / [KO](examples/ko/entity-to-topic.md) | Turning a company or product update into a question |
| Database to topic — [EN](examples/en/database-to-topic.md) / [KO](examples/ko/database-to-topic.md) | Backlog review, a full synthetic candidate, and a handoff |
| [Research rubric](references/research-rubric.md) | Factual reliability, semantic duplicates, and short-form fit |
| [Freshness rules](references/freshness-rules.md) | Event dates, material updates, and historical cutoffs |
| [Creator signal guide](references/creator-signal-guide.md) | Video age, metric provenance, and independent observations |
| [Evaluation cases](tests/cases.md) | Synthetic inputs and a review protocol |
| [Changelog](CHANGELOG.md) | Version history |

`SKILL.md` is the canonical English instruction; results follow the user's language. `agents/openai.yaml` provides optional host UI metadata.

## Limits and evaluation

Search coverage and platform metrics depend on available tools. Creator popularity does not verify a claim, and official announcements do not establish audience interest. Offline analysis cannot verify later real-world developments. Duplicate checks are limited to the content history supplied and the candidates inspected.

The shortlist may contain fewer topics than requested, or none. The skill does not predict virality or guarantee views, factual accuracy, or research-time savings.

Skills CLI discovery and project file installation were checked; Claude Code activation and live research were not tested as part of that check. The evaluation cases are specifications, not a claim that every case passed or a performance benchmark. See the [run protocol](tests/cases.md#run-protocol).

## Feedback

[Open an issue](https://github.com/MinhaKim02/creator-topic-radar/issues) with the prompt, public or fictional inputs, and the unexpected result. Keep English/Korean documents aligned when submitting a fix. Do not include private data or credentials.

## License

[MIT](LICENSE). Copyright (c) 2026 Minha Kim.
