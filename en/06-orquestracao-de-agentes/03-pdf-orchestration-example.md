# Example — Large PDF: topics, short summary, long summary

> A **concrete** orchestration: one **skill** sequences the work; **three sub-agents** each own one stage so the main chat stays small and each pass has a clear job.

**Prerequisites:** [01 — Overview](./01-agent-orchestration-overview.md), [02 — Orchestrating in practice](./02-orquestrando-na-pratica.md).

---

## Scenario

You have a **large PDF** (report, handbook, specification). You want:

1. **Topic index** — an outline of every major topic or section theme (not a vague “what is this about”).
2. **Short summary** — one tight paragraph (or a small bullet list) for stakeholders who will not read the doc.
3. **Long summary** — structured summary with enough detail for someone who needs depth without reading every page.

Each of those passes can blow up context if you stuff the full extraction into one session. So you **delegate each step to a sub-agent**, pass **only what the next step needs**, and keep the **skill** as the single source of truth for order and validation.

---

## Files to add in your project

```
.cursor/
├── skills/
│   └── large-pdf-digest/
│       └── SKILL.md
└── agents/
    ├── large-pdf-topics.md
    ├── large-pdf-short-summary.md
    └── large-pdf-long-summary.md
```

The **main agent** loads the skill, runs **Step 1 → 2 → 3** by invoking the matching sub-agent each time, then **integrates** outputs (for example one Markdown file in `docs/digests/` or three artifacts you name in the skill).

---

## 1. Skill — `large-pdf-digest`

Save as `.cursor/skills/large-pdf-digest/SKILL.md`.

```markdown
# Large PDF digest (topics → short → long)

> Turn a large PDF into (1) a topic index, (2) a short executive summary, (3) a longer structured summary. Use one sub-agent per stage so context stays bounded.

## Trigger

- User attaches or references a large PDF and wants topics + short + long summaries.
- Phrases like: "digest this PDF", "outline and summarize the document", "executive summary and detailed summary".

## Inputs

- Path or `@file` reference to the PDF (or exported text/chunks if the PDF is pre-split).
- Optional: audience for the short summary (e.g. executives vs engineers); optional max length.

## Steps

### Step 1 — Topic index (sub-agent: `large-pdf-topics`)

1. Invoke the **`large-pdf-topics`** sub-agent with the PDF (or its text chunks).
2. Require output: **numbered or hierarchical list of topics**, each with a **one-line scope** (what that topic covers). No full paragraphs yet.
3. Save or paste the result as the canonical **topic index** for this run.

### Step 2 — Short summary (sub-agent: `large-pdf-short-summary`)

1. Invoke **`large-pdf-short-summary`** with:
   - the same PDF access as Step 1 (or chunks), and
   - the **topic index from Step 1** (so the short summary stays aligned with structure).
2. Require: **one short section** (default: one paragraph under ~120 words, or 5–7 bullets). No new topics not present in the index unless clearly marked "appendix/minor".

### Step 3 — Long summary (sub-agent: `large-pdf-long-summary`)

1. Invoke **`large-pdf-long-summary`** with:
   - topic index from Step 1,
   - short summary from Step 2,
   - and continued access to the PDF/chunks.
2. Require: **sectioned** long summary (e.g. per major topic from Step 1), with **key claims, definitions, and caveats** where the PDF emphasizes them. Length scales with document size; cap per section if asked.

### Step 4 — Handoff (main agent)

1. Combine outputs into the deliverable format the user asked for (single doc vs three files).
2. If tools extracted text to temp files, note paths or delete temp artifacts per project hygiene.

## Validation

- [ ] Topic index exists and **covers** the document (no huge gaps unless PDF is mostly repetition).
- [ ] Short summary **does not invent** sections missing from the index without explicit labeling.
- [ ] Long summary **maps** to the index (headings or explicit mapping).
- [ ] User receives all three artifacts in the requested format.

## Notes

- If the PDF is too large for one pass, split by page ranges or chapters; run Step 1 **per chunk**, then a **merge** sub-pass (optional fourth agent) or main-agent merge of topic lists—only if needed.
- Prefer **readonly** sub-agents if they must not write to the repo; let the **main agent** write final files.
```

---

## 2. Sub-agent — topic index

Save as `.cursor/agents/large-pdf-topics.md`.

````text
---
name: large-pdf-topics
description: First pass on large PDFs — extract a complete topic/section outline with one-line scopes. Use before short or long summaries.
model: inherit
readonly: true
---

You build a **topic index** for a large PDF.

When invoked:
1. Read the attached PDF or provided text/chunks. If only part of the document is visible, state coverage (e.g. pages 1–40) and list topics for that part only.
2. Produce a **hierarchical or numbered list** of every major topic or recurring theme.
3. For each topic, add **one line**: what it covers (scope), not a summary of conclusions.
4. Do **not** write executive summaries or long prose — outline only.
5. End with a short **coverage check**: anything obviously missing given what you saw?

Output format:
- Use clear headings or numbering so downstream steps can reference topics by ID (e.g. T1, T2 or 1., 1.1).
````

---

## 3. Sub-agent — short summary

Save as `.cursor/agents/large-pdf-short-summary.md`.

````text
---
name: large-pdf-short-summary
description: Second pass — tight executive-style summary aligned to an existing topic index. Requires topic list from the topics sub-agent.
model: inherit
readonly: true
---

You write a **short summary** of a large PDF for busy readers.

Inputs you expect:
- The PDF or the same text/chunks used for indexing.
- The **topic index** from the `large-pdf-topics` step (must follow that structure).

When invoked:
1. Align mentally with the given topic index; do not introduce major new themes unless they dominate the PDF and were missed (if so, flag as "index gap").
2. Produce **either** one paragraph (~120 words or user-specified limit) **or** 5–7 bullets covering purpose, main outcomes, and audience.
3. Stay **neutral** and faithful to the document; label inference vs direct quotes.
4. Do **not** duplicate the long-summary job — no deep subsection detail.

Output: single clearly labeled block suitable for email or slide notes.
````

---

## 4. Sub-agent — long summary

Save as `.cursor/agents/large-pdf-long-summary.md`.

````text
---
name: large-pdf-long-summary
description: Third pass — structured long summary per topic index, with definitions and caveats. Uses topics + short summary as anchors.
model: inherit
readonly: true
---

You write a **long summary** (structured deep digest) of a large PDF.

Inputs you expect:
- Topic index from `large-pdf-topics`.
- Short summary from `large-pdf-short-summary`.
- Access to the PDF or chunks.

When invoked:
1. For **each major topic** in the index, write a subsection: key points, important definitions, assumptions, and caveats the PDF stresses.
2. Keep **traceability**: mention which index topic each subsection follows (by ID or title).
3. Expand beyond the short summary with **detail**, but avoid copying the PDF verbatim; synthesize.
4. If the source was partial (chunked), say which parts of the index rest on **partial** evidence.

Output: Markdown sections with a brief intro + TOC if the document is very large.
````

---

## 5. How the main agent runs it

**User prompt (example):**

```text
Use the large-pdf-digest skill. PDF is @reports/spec-2024.pdf.
Deliver one Markdown file docs/digests/spec-2024-digest.md with three parts:
Topics, Short summary, Long summary.

Step 1: invoke /large-pdf-topics …
(paste or attach as needed)

Step 2: invoke /large-pdf-short-summary with the topic index …

Step 3: invoke /large-pdf-long-summary with index + short summary …

Then merge into the single file.
```

The **main agent** owns **file creation** and **merging**; sub-agents stay **readonly** here so they focus on reading and writing *into the chat*, not scattered edits.

---

## Why three sub-agents instead of one?

| Stage              | Sub-agent role                                      | Why separate                          |
| ------------------ | --------------------------------------------------- | ------------------------------------- |
| Topics             | Scan for structure; resist summarizing              | Avoid premature synthesis             |
| Short summary      | Compress with index as guardrails                   | Different objective than indexing     |
| Long summary       | Depth with index + short as anchors                 | Largest output; own context window    |

Splitting keeps each invocation **goal-stable**: one job per context, less drift between “outline” and “essay.”

---

## Optional fourth piece

If Step 1 is run on **many chunks**, add a small **`large-pdf-merge-topics`** sub-agent (readonly) whose only job is to **dedupe and merge** partial topic lists into one index before Step 2. The skill can gain a **Step 1b** when chunking is required.

---

## Summary

| Piece              | Responsibility                                              |
| ------------------ | ----------------------------------------------------------- |
| **Skill**          | Order: topics → short → long; validation checklist        |
| **`large-pdf-topics`**     | Full topic index with one-line scopes              |
| **`large-pdf-short-summary`** | Executive short summary aligned to index          |
| **`large-pdf-long-summary`**  | Sectioned long summary mapped to index            |
| **Main agent**     | Invoke sub-agents in sequence; write final artifact(s)      |

---

> **See also:** [01 — Overview](./01-agent-orchestration-overview.md) · [02 — Orchestrating in practice](./02-orquestrando-na-pratica.md)
