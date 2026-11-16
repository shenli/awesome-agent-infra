# Contributing

Thanks for helping improve Awesome Agent Infra.

This repository is a curated infrastructure list, not a general AI agents directory. Please keep additions tightly scoped to systems used to build, run, secure, observe, evaluate, or publish production agent workflows.

## What Belongs Here

A resource is a good fit if it helps answer at least one of these questions:

- How should an agent runtime manage state?
- How should tools be exposed safely?
- How should workspace changes be isolated and published?
- How should sandboxes execute untrusted or semi-trusted actions?
- How should agent runs be traced, evaluated, and replayed?
- How should secrets, permissions, and policy be enforced?
- How should coding agents integrate with repos, issues, PRs, and CI?

## What Does Not Belong

Please avoid resources that are only:

- Prompt collections
- General AI app directories
- Chatbot UI tools
- Generic RAG tools without direct agent-infra relevance
- Model leaderboards with no infrastructure implications
- End-user products with no reusable infrastructure lesson
- Thin tutorials that only wrap an SDK call

## Entry Style

Prefer concise entries in the existing table format:

```md
| [Resource Name](https://example.com) | Type or layer | One sentence explaining why it matters. |
```

Good entries explain the infrastructure lesson. They should not read like marketing copy.

For papers, include a verified publication year and venue, or label the work as
a preprint. Use the existing type column where available; in two-column tables,
append the metadata to the paper title. Link to the primary paper and describe
the systems contribution, such as state lifetime, scheduling, isolation, or
recovery semantics. Verify metadata against the paper or proceedings rather
than inferring a conference year from an arXiv identifier.

Before submitting:

- Check that the resource is not already listed.
- Put it in the most specific existing section.
- Use the canonical project, docs, paper, or article URL.
- Keep descriptions factual and short.
- Add only resources you have enough context to evaluate.

Entries are periodically re-verified. Stale, archived, deprecated, or unmaintained projects may be removed even if they were useful historically.

## Navigation and Synthesis

Keep the reading guide and table of contents aligned with the sections. Group
resources by the infrastructure problem they address. When a paper section
becomes difficult to scan, group by year within that topic; keep current work
visible and consider collapsible groups for older papers.

Any trend summary should link to the entries that support it and distinguish
editorial interpretation from measured results. For counts or charts, document
the corpus snapshot, inclusion rules, date convention, deduplication, and
reproduction steps. Counts describe this curated collection, not the whole field;
label partial years and avoid treating missing entries as proof of a research gap.

## Pull Requests

Small focused pull requests are easiest to review. If a PR adds many resources, group them by section and explain the curation rationale in the PR body.

Maintainers may decline otherwise useful resources if they do not match the scope of this list.
