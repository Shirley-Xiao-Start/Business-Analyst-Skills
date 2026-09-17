---
name: markdown-mindmap
description: Generates mind maps from natural-language descriptions or topic inputs using Markdown heading hierarchy, producing render-ready .md files. Also teaches Markdown mind-map conventions, VS Code setup, and troubleshooting. Use this whenever the user says "mind map", "mindmap", "organize this into a mind map", "create a mindmap", "give me a .md mindmap", or "draw a mind map in Markdown".
---

# Markdown Mind Map

A mind map in Markdown uses **heading hierarchy** to express the root-topic / sub-topic / detail structure. The output is a `.md` file that renders as a foldable outline in VS Code and as a visual mind map in any Markdown preview that supports it.

## Decide the mode first

- **Mode A: topic -> mind map.** The user gives a topic or a paragraph describing one. Default mode.
- **Mode B: file -> mind map.** The user points at a document and wants the structure extracted. Read the file first.
- **Mode C: teaching mode.** The user says "I'm new to this", "teach me", "step by step". Follow the teaching outline.

## Output conventions

Whichever mode is in play, the `.md` you produce must satisfy these:

- The file **must** be valid Markdown using only `#` through `####` heading levels (no tables, no code fences unless quoting reference material).
- **Line 1** must be a single `# Title` stating the topic.
- Level-2 headings (`##`) are the **main branches** — top-level categories or stages.
- Level-3 headings (`###`) are **sub-branches** — sub-categories or phases within a branch.
- Level-4 headings (`####`) are **leaf nodes** — specific items, tasks, or details.
- **No bullet lists** inside the tree; the heading hierarchy is the structure.
- Use `== Stage name ==` only if the topic is temporal; otherwise keep it purely categorical.
- File name: `<topic>-mindmap.md`, for example `project-management-mindmap.md`, so files sort by topic.

## Mode A: topic -> mind map

### Extract three things

1. **Root**: what is the central topic? This becomes the `#` heading.
2. **Main branches**: the major categories, stages, or dimensions. These become `##` headings. Keep to 5–9 — if you find more, group some into a higher-level branch.
3. **Sub-branches and leaves**: for each main branch, what are the next-level subdivisions and the concrete items?

### Do not invent details the user did not give.

If the user says "project management" with no further description, draw the canonical five stages — Requirements, Design, Development, Testing, Deployment — but stop there. Do not add "Retrospective" or "Maintenance" unless the user mentions them. Ask before filling gaps.

### Example: project management stages

Input: "Leverage Markdown to create a mind map that visually organizes the various stages of project management, including requirements analysis, design, development, testing, and deployment"

```markdown
# Project Management Stages

## Requirements Analysis
### Stakeholder Identification
#### Interview key stakeholders
#### Document stakeholder roles and influence
#### Map stakeholder expectations
### Requirement Gathering
#### Collect functional requirements
#### Collect non-functional requirements
#### Prioritize requirements (MoSCoW)
### Requirement Specification
#### Write requirements document
#### Define acceptance criteria
#### Validate requirements with stakeholders

## Design
### Architecture Design
#### Choose technology stack
#### Define system components
#### Design data model
### UI/UX Design
#### Create wireframes
#### Design user flows
#### Build interactive prototype
### Design Review
#### Conduct design review with team
#### Iterate based on feedback
#### Finalize design documentation

## Development
### Sprint Planning
#### Break features into user stories
#### Estimate effort
#### Define sprint goals
### Implementation
#### Write code following standards
#### Code review process
#### Integrate with existing systems
### Version Control
#### Branch strategy
#### Commit conventions
#### Pull request workflow

## Testing
### Test Planning
#### Define test strategy
#### Identify test cases
#### Prepare test data
### Test Execution
#### Run unit tests
#### Run integration tests
#### Run end-to-end tests
### Bug Management
#### Log and track defects
#### Prioritize bug fixes
#### Verify fixes

## Deployment
### Release Planning
#### Define release criteria
#### Create release notes
#### Plan rollback strategy
### Deployment
#### Deploy to staging environment
#### Run smoke tests
#### Deploy to production
### Post-Deployment
#### Monitor system health
#### Gather user feedback
#### Conduct post-mortem
```

Two things to note. **The branch structure mirrors the canonical project-lifecycle model**, so anyone familiar with the domain can read it without explanation. **Each leaf is a concrete, actionable item** — not an abstract concept — because a mind map is meant to be used as a working reference, not just a picture.

## Mode B: file -> mind map

1. **Read the file** to understand its structure.
2. **Identify the top-level structure** — the highest-level divisions naturally form the `##` branches.
3. **Descend one or two levels deeper** to populate `###` and `####`.
4. **Stop at boundaries that carry meaning.** Do not flatten an entire document into a single branch; stop when the next level would be trivial detail.
5. **One mind map per primary structure.** If the document has two unrelated topics, produce two `.md` files ordered by an index prefix.

When reading files, read only the key nodes. Do not load an entire repository into context — it is slow and it blurs the focus.

## Mode C: teaching mode

Work through in order, giving runnable code and a visible result at each step:

1. **Minimal runnable map** -- a single `# Title` with one `## Branch` and one `### Sub-branch`.
2. **Heading levels and semantics** -- what `#`, `##`, `###`, `####` mean in a mind map, and when to stop descending.
3. **Naming leaf nodes** -- concrete and actionable, not abstract. "Write unit tests" not "Testing".
4. **Branch discipline** -- 5–9 main branches; if more, group them. No mixed categorization (e.g., don't mix "people" and "phases" in the same level).
5. **Getting it running in VS Code** -- see the next section.

Call out the three beginner traps: **using bullet lists instead of headings**, **going deeper than four levels** (it loses readability), and **mixed classification at the same level**.

## VS Code setup

Markdown mind maps render in **any** Markdown preview — they are plain `.md` files. But these extensions make them easier to work with:

- **Markdown Outline** (extension ID `formulahendry.markdown-outline`) -- shows a foldable tree of all headings in a sidebar. Perfect for navigating a large mind map.
- **Markdown Preview Enhanced** (extension ID `shd101wyy.markdown-preview-enhanced`) -- renders a live preview, exports to PDF / PNG / SVG, and supports Mermaid diagrams alongside plain Markdown trees.
- **Headings Outline** (extension ID `johnparks.headings-outline`) -- alternative outline viewer with zoom and search.

Open the `.md` file, then `Ctrl+Shift+P` -> "Markdown: Open Preview" or `Ctrl+Shift+V` to see the rendered tree.

**Fallback with no extension at all**: paste the content into [stackedit.io](https://stackedit.io) or any online Markdown editor. It renders heading trees instantly.

## Troubleshooting checklist

| Symptom | Cause and fix |
|---|---|
| Outline view shows no hierarchy | Headings are not using `#` syntax; check for plain text or bullet lists instead |
| Too many branches at one level | More than 9 `##` items -> group some under a higher-level `###` category |
| Going too deep to read | Deeper than `####` -> collapse some detail into sibling `###` items, or split into a second file |
| Preview does not refresh | Close and reopen the preview (`Ctrl+Shift+V`), or toggle the outline sidebar |
| Non-Latin characters render as boxes | Usually a font issue in the preview extension; switch to a preview that uses the system font |
| File exported as image is clipped | The preview renderer may clip wide trees; export as PDF or use a dedicated mind-map tool with the Markdown input |

## Last step

If the user gave only a topic ("draw a mind map") with no detail, **do not invent branches**. Ask three things first: what scope the map should cover, how many main branches they expect, and whether they want leaf-level detail or just the skeleton. Getting those answers first is far faster than drawing a version and then reworking it.
