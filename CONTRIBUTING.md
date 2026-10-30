# Contributing

Thank you for helping maintain Awesome Agentic Chip Design. Contributions may add a paper, a project, a benchmark, an official industry resource, or a correction.

## Scope

Include resources that directly help readers understand or build agentic chip-design workflows: specifications, architecture, RTL, verification, HLS, synthesis, physical design, analog/RF design, EDA execution infrastructure, or EDA algorithm development.

Focus on LLM agents for chip design and resources directly supporting their model capabilities, tool execution, and evaluation. Standalone traditional machine-learning or reinforcement-learning methods are outside the scope. General agent frameworks belong here only when a concrete chip-design integration is the subject of the entry.

## Inclusion Criteria

- Link to a primary paper page, official project repository, official proceedings record, maintained documentation, or official company technical publication.
- Explain the specific task and mechanism in one or two factual sentences.
- Prefer papers with inspectable methods and evaluation, usable artifacts, or a clear role as a foundational reference. Preprints are eligible and must retain their source status.
- Verify that a code link belongs to the named work. Label independent implementations explicitly.
- Keep one primary entry per publication. Merge duplicate preprint and final versions, and update existing entries for code releases or publication details. Link separately published extensions to the original study and explain their relationship.
- Describe commercial or closed-source resources with their actual access status if they are added. Repository visibility alone does not establish an open-source license.
- Prefer technical descriptions over promotional pages. A company overview may establish a relevant research direction when its limited disclosure is explicit. Exclude unverifiable performance claims, duplicate listings, and resources whose connection to chip design is merely incidental.

Popularity is useful for discovery, but stars are not an inclusion requirement. Self-submissions use the same criteria.

## Entry Format

Place an entry in its most relevant subsection of `README.md`. Section 2 covers design tasks, Section 3 covers cross-task agent mechanisms with domain models and learning in Section 3.1, Section 4 covers EDA software development, and Section 5 covers evaluation. Give each paper one primary home and use cross-references for other relevant views. Sort by the initial paper date when available, otherwise the publication date, newest first; use the identifier in descending order for ties. Prefer the verified formal publication as the primary link and include a preprint link when available. Use an explicit stable anchor so reading paths continue to work if the title changes.

```markdown
<a id="paper-YYMM-NNNNN"></a>

- **[Exact paper title](https://arxiv.org/abs/YYMM.NNNNN)**  
  `arXiv YYYY-MM` · `Agent` · [Code](https://github.com/organization/project)  
  One factual sentence explaining the task, mechanism, and relevant tool feedback.
```

The identifiers above are template notation. Replace them with real, verified identifiers. Omit the code link when no associated public repository has been verified. For a paper without arXiv, use a stable DOI or official proceedings URL and an appropriate source/date label.

Available labels:

| Label | Use for |
| --- | --- |
| `Agent` | A system that selects subsequent actions using tool or environment feedback |
| `Framework` | A system architecture or proposal; describe the demonstrated integration scope |
| `Method` | A design technique without an asserted autonomous execution loop |
| `Model` | A reusable model, training procedure, or generator |
| `Infrastructure` | Tool interfaces, execution services, state management, or harnesses |
| `Benchmark` | Evaluation tasks, datasets, protocols, or suites |
| `Survey` | A structured synthesis of existing research |
| `Perspective` | A viewpoint, roadmap, or reflective case study |

Use a combined label only when both roles are central to the work. Apply the `Agent` label when the source describes how tool or environment feedback determines subsequent actions.

## Industrial Resources

Place official product documentation, technical blogs, whitepapers, announcements, and industry reports in [Section 6 of the README](README.md#industrial-systems-and-reports), grouped by company. Cross-link the relevant research tasks or mechanisms. Industrial entries do not increment the paper count.

```markdown
- **[Resource title](https://company.example/technical-resource)**  
  `Official technical blog YYYY-MM-DD` · `Verification and debugging`  
  One or two factual sentences describing the workflow, tool integration, and relevant access status.
```

- Use the source's publication date for dated materials. Label a live product or company overview `Undated`; do not infer a launch date from a page update.
- Keep dated entries newest first. An undated product overview may precede them to introduce the system.
- Distinguish announced plans, early access, demo access, and released products using the source's wording and date.
- Attribute capabilities and results to the vendor. Avoid unqualified claims such as “first,” “best,” or productivity multipliers without their evaluation setting.
- Link to the official source wherever available. If access restrictions require a vendor-authored press-release reprint, label it explicitly, retain any verified official link, and identify the source used.
- Summarize only inspected material. If only a whitepaper's public introduction is accessible, identify the link as a landing page and limit the description accordingly.
- Separate industry surveys and research directions from agent implementations and benchmark evaluations.

## Before Opening a Pull Request

- Search the list for the title, acronym, and arXiv identifier to avoid duplicates.
- Open each added external link and check the title and artifact identity.
- Read the relevant source before writing a summary. Keep reported results tied to their evaluation setting if numbers are necessary.
- Use an initial arXiv month for an arXiv entry. Add a verified venue separately; do not infer acceptance from a target-venue template.
- Keep paper anchors unique and update affected reading paths and section links.
- Count primary paper entries once; exclude industrial resources from the paper badge.
- Update counts, `Recent Papers`, the update date, and `CHANGELOG.md` when the collection changes.
- Preview the Markdown table, code links, and line breaks on GitHub.

One focused change per PR makes review easier. Link-only fixes may be submitted without rewriting the description.

## Reporting a Correction

Use the correction issue template for broken links, inaccurate summaries, incorrect dates, missing publication information, or mistaken repository associations. Include the current entry and a primary source supporting the correction.

## License

Contributions to the original list text are made under [CC0 1.0](LICENSE). Linked resources retain their own licenses; adding a link does not relicense them.
