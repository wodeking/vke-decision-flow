# VKE Decision Workflow Skill

`vke-decision-workflow` turns an ambiguous VKE knowledge request into an evidence-led decision package. It is designed for OpenClaw/Codex-style skill runners that can load a `SKILL.md` file and optional references.

## What This Skill Does

This skill guides an agent through the full VKE decision workflow:

1. Capture the original request.
2. Frame the decision problem.
3. Build a research plan.
4. Create an evidence ledger.
5. Write analysis notes.
6. Perform red-team review.
7. Produce a commercial decision report.
8. Create monitoring indicators.
9. Write a retrospective.

The workflow emphasizes:

- separating facts, judgments, and assumptions
- citing evidence IDs
- marking confidence for each core judgment
- testing alternative explanations
- avoiding unsupported claims

## Folder Structure

```text
vke-decision-workflow/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
└── references/
    └── artifact-templates.md
```

## Typical Usage

### 1. Start a New VKE Case Without Web Search

```text
Use $vke-decision-workflow to create a VKE decision workflow for this request:

我需要判断“化工领域 MES 系统是否值得个人开发者投入”。

Please generate the initial case artifacts:
- 00_request.md
- 01_problem-brief.md
- 02_research-plan.md
- 03_evidence-ledger.csv as an empty evidence ledger template

Do not search the web. Only use the information I provide.
```

### 2. Research Public Evidence and Build the Full Package

```text
Use $vke-decision-workflow to evaluate whether chemical-industry MES systems are worth entering.

Please follow the VKE workflow:
1. Create 01_problem-brief.md and 02_research-plan.md.
2. Search public sources for evidence.
3. Write all evidence into 03_evidence-ledger.csv.
4. Generate 04_analysis-notes.md.
5. Generate 05_red-team-review.md.
6. Generate 06_knowledge-product.md as a commercial decision report.
7. Generate 07_watchlist.md and 08_retrospective.md.

Requirements:
- Every evidence item must have a traceable source.
- Do not fabricate amounts, dates, organizations, or cases.
- Separate facts, judgments, and assumptions.
- Mark confidence for each core judgment.
```

### 3. Work Only From User-Provided Evidence

```text
Use $vke-decision-workflow to build a decision package from the attached files.

Constraints:
- Do not search the web.
- Do not add facts outside the attached PDFs, screenshots, notes, or existing evidence ledger.
- Create or update 03_evidence-ledger.csv, 04_analysis-notes.md, and 06_knowledge-product.md.
```

### 4. Update an Existing VKE Case

```text
Use $vke-decision-workflow to update this existing VKE case:

C:\path\to\CASE-YYYY-NNN_topic

Please read the existing:
- 03_evidence-ledger.csv
- 04_analysis-notes.md
- 05_red-team-review.md

Then regenerate:
- 06_knowledge-product.md
- 07_watchlist.md
- 08_retrospective.md

Do not modify 00_request.md, 01_problem-brief.md, or 02_research-plan.md.
```

### 5. Red-Team an Existing Analysis

```text
Use $vke-decision-workflow as a red-team reviewer.

Based on:
- 03_evidence-ledger.csv
- 04_analysis-notes.md

Update 05_red-team-review.md and focus on:
1. Whether the main judgments are sufficiently supported.
2. Whether there is selective evidence.
3. Whether reverse evidence was ignored.
4. Whether stronger alternative explanations exist.
5. Which assumption is most fragile.
6. Whether confidence should be lowered.
7. What evidence would improve judgment quality.
```

### 6. Generate Only the Commercial Decision Report

```text
Use $vke-decision-workflow to generate a commercial decision report.

Based on:
- 03_evidence-ledger.csv
- 04_analysis-notes.md
- 05_red-team-review.md

Generate 06_knowledge-product.md with this structure:
1. Executive Summary
2. Evidence & Confidence
3. Analysis & Counter-Arguments
4. Impact Assessment
5. Action Plan

Do not add facts outside the evidence ledger.
```

## Network Access

The skill itself does not require network access. Network access is only needed when the user asks the agent to collect new evidence from public sources.

Use offline mode when the user provides all source material:

```text
Do not search the web. Only use the files and evidence I provide.
```

Use online research mode when the agent should collect new evidence:

```text
Search public sources and write every new source into 03_evidence-ledger.csv.
```

## Evidence Rule

The evidence ledger must not be generated from model memory alone. Every row in `03_evidence-ledger.csv` must come from one of:

- user-provided files
- user-provided links
- searched public sources
- existing evidence records

If evidence is missing and search is not allowed, create an empty ledger template or mark the evidence as pending.
