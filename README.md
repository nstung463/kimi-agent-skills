# Kimi Agent Core Skills

> A curated collection of 261 reusable skills for writing, research, finance, software development, documents, media, and planning workflows.

## Overview

This repository packages the complete core skill collection supplied with the Kimi Agent setup. Each skill is self-contained and includes a `SKILL.md` instruction file, with supporting scripts, references, assets, templates, or configuration where required.

The collection contains 261 skill directories and more than 2,600 supporting files. It is designed to make specialized agent workflows easier to discover, install, reuse, and maintain in a standard repository structure.

## Skill areas

| Area | Representative capabilities |
| --- | --- |
| Writing and content | Copywriting, SEO, email, newsletters, reports, speeches, translation, and social content |
| Research and finance | Deep research, academic review, equity research, valuation, earnings, commodities, funds, and risk analysis |
| Product and planning | PRDs, campaigns, OKRs, pricing, roadmaps, sprints, Gantt planning, and SaaS analysis |
| Engineering and data | Backend, APIs, databases, SQL, testing, Git, Kubernetes, Terraform, security, and data visualization |
| Documents and media | DOCX, PDF, XLSX, PPTX, slide design, design systems, infographics, video, and podcast workflows |
| Personal productivity and learning | Flashcards, quizzes, tutoring, interview practice, resumes, meeting recaps, and work planning |

## Notable entry points

- `docx`, `pdf`, `xlsx`, and `pptx` for document and presentation workflows
- `kimi-find-skills`, `kimi-skills-finder`, and `kimi-help-center` for skill discovery
- `webapp-building`, `backend-building`, `api-doc-gen`, and `database-inspector` for software projects
- `deep-research`, `research-writer`, and `academic-paper-reviewer` for research workflows
- `seo-audit`, `campaign-planner`, and `brand-naming-lab` for marketing workflows

The complete inventory is available under [`skills/`](skills/). Each skill's `SKILL.md` is the authoritative guide for its triggers, workflow, dependencies, and usage requirements.

Browse the [skill catalog](docs/), [changelog](CHANGELOG.md), [contribution guide](CONTRIBUTING.md), and [security policy](SECURITY.md) for additional project documentation.

## Installation

Install the complete collection with:

```bash
npx skills add nstung463/kimi-agent-skills
```

To use a single skill, copy its directory from `skills/` into the skills directory of your agent environment. Keep the skill's supporting files together with `SKILL.md`.

## Repository structure

```text
kimi-agent-skills/
|-- skills/
|   |-- docx/
|   |-- pdf/
|   |-- pptx/
|   |-- xlsx/
|   |-- kimi-find-skills/
|   `-- ... 261 skill directories
|-- .gitignore
|-- docs/
|-- CHANGELOG.md
|-- CONTRIBUTING.md
|-- SECURITY.md
`-- README.md
```

## Usage guidance

1. Select the skill that matches the task.
2. Read its `SKILL.md` before starting the workflow.
3. Install or verify the dependencies documented by that skill.
4. Keep scripts, references, assets, and templates in their original relative locations.

## Attribution and scope

This repository is a community-oriented packaging of the supplied Kimi Agent core skill collection. It is not an official Kimi or Moonshot AI product and does not represent the original authors or organizations.

The files in individual skill directories may have different authorship and licensing terms. Preserve the attribution and license information included with each skill, and review the relevant `LICENSE`, `LICENSE.txt`, or documentation before modifying, redistributing, or using a skill commercially.

## Credits

- Core skill collection: supplied Kimi Agent skill library
