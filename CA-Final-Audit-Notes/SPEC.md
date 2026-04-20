# Note-Making Spec v2 — CA Final Paper 3 (May 2026) · HTML Edition

**Single source of truth for every subagent producing chapter notes.**
Scope: ICAI SM Final Paper 3 — Advanced Auditing, Assurance & Professional Ethics (May 2026).
Target reader: CA Final student in revision phase. Not a first-time learner.
Output format: **Single-file HTML** (self-contained, embedded CSS, mermaid.js via CDN only).

---

## 1. Hard rules (do not break)

1. **Grounded in the PDF, not in training knowledge.** Each SA's Objective and one key Definition MUST be lifted verbatim from the ICAI SM PDF located at `/sessions/sweet-eloquent-planck/mnt/megha_icai-ca-testing/CA-Final-Audit-Notes/pdfs/ch-XX.pdf`. Quote the exact ICAI sentence. If the PDF is missing or unreadable, STOP and report — do not fabricate. **Prefer the prose-list Objective statement in the PDF over any diagram-box Objective** (diagram boxes produce extraction artifacts).
1a. **Intermediate-deferred SAs: flag but do not fill.** If the Ch PDF explicitly defers an SA to Intermediate level (e.g., Ch 2 does this for SA 200, 210, 230, 265), include a brief `.sa-card` for that SA containing ONLY: (a) scope line, (b) a `.exception` block stating "SA XXX is deferred to Intermediate level per the ICAI Final SM. Objective and detailed requirements are not reproduced in this chapter's PDF. Refer Intermediate SM for revision.", (c) optional 1-line list of key keywords-to-remember. Do NOT supply Objective/Definitions/Requirements/Exceptions from training knowledge. Do NOT fabricate ICAI-verbatim quotes.
2. **Length cap: equivalent of 20–30% of source length.** Measure in words of visible text (excluding HTML tags). Full HTML note: 2,500–4,500 visible words **(2,500–5,000 for Ch 5, Ch 7, Ch 19)**. One-pager: ≤ 400 visible words **(≤ 500 for Ch 5 and Ch 19)**.
3. **90-second-per-screen rule.** Any single scroll-screen of the rendered HTML should be readable in under 90 seconds.
4. **Keywords, not sentences.** Requirements in bullet triggers. E.g. `Reasonable assurance · material misstatement · professional skepticism`. Never `The auditor shall obtain reasonable assurance...`
5. **Clause numbers mandatory** for CARO and Ethics. Quote the exact clause/paragraph number.
6. **Never copy-paste whole ICAI paragraphs.** >2 consecutive verbatim sentences = violation (except for the 1 objective-quote per SA).
7. **5 exam triggers per chapter**, mandatory in both full and onepager files.

---

## 2. File layout — chapter-wise folders

Each chapter gets its own folder under `chapters/`:

```
chapters/
├── ch-01-quality-control/
│   ├── full.html
│   ├── onepager.html
│   └── diagrams/          (optional: extra PNG/SVG if not inlined)
├── ch-02-general-principles/
│   ├── full.html
│   └── onepager.html
├── ch-03-audit-planning/
├── ch-04-risk-assessment/
├── ch-05-audit-evidence/
├── ch-06-completion-review/
├── ch-07-reporting/
├── ch-07a-caro-2020/
├── ch-08-specialised-areas/
├── ch-09-related-services/
├── ch-10-review-financial-info/
├── ch-11-prospective-financial-info/
└── ch-19-ethics/
```

Plus at the root:
- `index.html` — dashboard with mark-weightage map, links to every chapter, study-order recommendation
- `SPEC.md` — this file
- `pdfs/ch-XX.pdf` — source PDFs
- `diagrams-shared/` — reusable SVGs (e.g., SA-cluster map used in multiple chapters)

---

## 3. HTML shell — mandatory boilerplate

Every HTML file starts from this shell. Do not modify `<style>` — shared design system.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Ch XX — <Title> · CA Final Audit</title>
<script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>
<style>
:root {
  --bg: #faf8f3;
  --ink: #1a1a1a;
  --muted: #5b5b5b;
  --accent: #0a4a8f;       /* ICAI-ish navy */
  --keyword-bg: #fff3d4;   /* soft yellow highlight */
  --exception-bg: #ffe4e4; /* soft red for ⚠ */
  --exception-border: #c33;
  --clause-bg: #e8f2ff;    /* soft blue for clause numbers */
  --table-stripe: #f5f2ea;
  --rule: #d8d3c4;
  --quote-bar: #0a4a8f;
}
* { box-sizing: border-box; }
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Georgia, serif;
  background: var(--bg); color: var(--ink);
  max-width: 820px; margin: 2rem auto; padding: 0 1.25rem;
  line-height: 1.55; font-size: 16px;
}
h1 { font-size: 1.9rem; color: var(--accent); border-bottom: 2px solid var(--accent); padding-bottom: 0.4rem; }
h2 { font-size: 1.4rem; color: var(--accent); margin-top: 2rem; border-left: 4px solid var(--accent); padding-left: 0.6rem; }
h3 { font-size: 1.15rem; color: var(--ink); margin-top: 1.5rem; }
h4 { font-size: 1rem; color: var(--muted); text-transform: uppercase; letter-spacing: 0.05em; margin-top: 1.2rem; margin-bottom: 0.3rem; }
.meta { color: var(--muted); font-style: italic; font-size: 0.9rem; margin-top: -0.5rem; }
.keyword { background: var(--keyword-bg); padding: 0 0.2em; border-radius: 2px; font-weight: 600; }
.exception {
  background: var(--exception-bg);
  border-left: 4px solid var(--exception-border);
  padding: 0.5rem 0.8rem; margin: 0.5rem 0; border-radius: 3px;
}
.exception::before { content: "⚠ "; font-weight: bold; color: var(--exception-border); }
.clause {
  background: var(--clause-bg); padding: 0.1rem 0.4rem;
  border-radius: 3px; font-family: ui-monospace, monospace;
  font-size: 0.9em;
}
blockquote.icai {
  border-left: 4px solid var(--quote-bar);
  background: #fff; margin: 0.8rem 0; padding: 0.6rem 1rem;
  font-style: italic; color: #333;
}
blockquote.icai::before { content: "ICAI verbatim · "; font-style: normal; font-weight: 600; color: var(--accent); font-size: 0.8em; text-transform: uppercase; letter-spacing: 0.05em; }
table { border-collapse: collapse; width: 100%; margin: 1rem 0; font-size: 0.95rem; }
th, td { padding: 0.5rem 0.7rem; text-align: left; border: 1px solid var(--rule); vertical-align: top; }
th { background: var(--accent); color: #fff; font-weight: 600; }
tr:nth-child(even) td { background: var(--table-stripe); }
.sa-card {
  border: 1px solid var(--rule); border-radius: 6px;
  padding: 1rem 1.2rem; margin: 1.5rem 0; background: #fff;
}
.sa-card h3 { margin-top: 0; color: var(--accent); }
.triggers {
  background: #fff; border: 1px dashed var(--accent);
  padding: 1rem; border-radius: 6px; margin: 1.5rem 0;
}
.triggers h3 { margin-top: 0; color: var(--accent); }
.triggers ol { margin: 0; padding-left: 1.2rem; }
.triggers li { margin: 0.4rem 0; }
.mermaid { background: #fff; padding: 1rem; border-radius: 6px; margin: 1rem 0; text-align: center; }
svg.diagram { max-width: 100%; height: auto; display: block; margin: 1rem auto; background: #fff; border-radius: 6px; padding: 0.5rem; }
ul, ol { padding-left: 1.3rem; }
li { margin: 0.2rem 0; }
.chip { display: inline-block; padding: 0.1rem 0.5rem; border-radius: 12px; font-size: 0.75rem; font-weight: 600; margin-right: 0.3rem; }
.chip-sa { background: var(--accent); color: #fff; }
.chip-marks { background: #2a7c3a; color: #fff; }
.nav { margin: 1rem 0; font-size: 0.9rem; }
.nav a { color: var(--accent); text-decoration: none; margin-right: 1rem; }
.nav a:hover { text-decoration: underline; }
</style>
</head>
<body>
<div class="nav">← <a href="../../index.html">All chapters</a> · <a href="onepager.html">One-pager</a></div>
<h1>Chapter XX — <Chapter Title></h1>
<p class="meta">ICAI SM Final P3 May 2026 · <span class="chip chip-marks">~N marks</span> Covers SA <range></p>

<!-- content -->

<script>mermaid.initialize({startOnLoad:true, theme:'neutral'});</script>
</body>
</html>
```

---

## 4. Full-note content structure (SA chapters)

Inside the body, after the H1 and meta:

### 4.1 Chapter map (opening)
Short paragraph (3–5 lines) positioning the chapter.

### 4.2 SA cluster diagram (mandatory, 1 per chapter)
An inline SVG or mermaid diagram showing the SAs in the chapter and their relationships. Example: for Ch 2, a boxes-and-arrows diagram grouping SA 200 (umbrella), SA 210 (before engagement), SA 230 (during), SA 240/250 (fraud/laws), SA 260/265 (TCWG communication), SA 299 (joint audits).

### 4.3 Each SA as a `.sa-card`
```html
<section class="sa-card">
  <h3>SA 200 — Overall Objectives of the Independent Auditor</h3>
  <p><strong>Scope</strong>: 1 line. <strong>Effective:</strong> periods beginning on/after…</p>

  <h4>Objective</h4>
  <blockquote class="icai">"<verbatim ICAI sentence from PDF>"</blockquote>

  <h4>Key Definitions</h4>
  <ul>
    <li><span class="keyword">Material misstatement</span> — trigger definition ≤15 words</li>
    …
  </ul>

  <h4>Key Requirements</h4>
  <ul>
    <li><span class="keyword">Reasonable assurance</span> · professional skepticism · professional judgment</li>
    …
  </ul>

  <h4>Exceptions / Conditions</h4>
  <div class="exception">Inherent limitations: nature of FR, nature of audit procedures, timeliness & cost</div>

  <h4>Auditor's Responsibilities</h4>
  <ul><li>…</li></ul>

  <h4>Conclusion / Reporting</h4>
  <p>1 line — what the auditor ultimately does or reports.</p>

  <!-- optional diagram for whitelisted SAs (§8) -->
</section>
```

### 4.4 End-of-chapter: 5 Exam Triggers
```html
<div class="triggers">
  <h3>📌 5 Exam Triggers — spot these phrasings, invoke these SAs</h3>
  <ol>
    <li>"Auditor discovered unrecorded related-party loans only during review" → <strong>SA 550</strong>, focus on procedures for identifying related parties</li>
    …
  </ol>
</div>
```

---

## 5. One-pager structure

Same shell, body contains ONLY:
1. H1 (same title + "· One-Pager")
2. Meta line
3. **SAs at a glance** table (SA number | name | 5–7 word core trigger | ⚠ key exception)
4. **Must-remember keywords** — one line per SA, keyword list
5. **5 exam triggers** (can be same as full note)
6. **Reporting bottom-lines** — one line per SA

Word cap: ≤ 400 visible words. One A4 page when printed.

---

## 6. Ethics template (Ch 19) — DIFFERENT

The full HTML for Ch 19 uses the same shell but content structured as:

1. Framework map (opening SVG) — CA Act 1949 → Schedules → Parts → Clauses + Council Guidelines + Code of Ethics + Liabilities
2. **Case-study answer skeleton** (reusable, called out in a highlighted box): Provision → Content → Exception → Analysis → Conclusion
3. **First Schedule** — Part I, II, III, IV, each as a `<table>` with columns: Clause # · Prohibition · ⚠ Exception · Fact-pattern trigger
4. **Second Schedule** — Part I, II, III, same tabular format
5. **Council Guidelines** — separate table
6. **Code of Ethics highlights** — only ICAI-tested portions
7. **Liabilities of Auditors** — Civil · Criminal · Companies Act s.147 · IT Act · Professional misconduct
8. 5 exam triggers at the end

---

## 7. CARO 2020 template (Ch 7a)

Standalone HTML file. Content:
1. SVG diagram showing applicability tree (company types → applies / exempt)
2. Reporting-duty-under-s.143(11) 1-para context
3. Big table of all 21 clauses — #, heading, auditor's 1-line reporting duty, ⚠ common trigger
4. Per-clause drill-downs only for exam-favorite clauses: (i) title deeds, (ii) inventory, (iii) loans to related parties, (vii) statutory dues, (ix) default in repayment, (xvii) cash losses, (xxi) subsidiary CARO remarks
5. 5 exam triggers

---

## 8. Diagrams — when and how

Every chapter must include **at minimum**:
- 1 opening SA-cluster/overview diagram (SVG or mermaid)
- 1 diagram per whitelisted SA (see §9 below)
- Optional: 1 concept infographic per chapter if it clarifies a tricky mechanic

### Diagram format preference order:
1. **Inline SVG** — preferred. Self-contained, always renders, prints well.
2. **Mermaid** — OK for flowcharts and decision trees. Uses the CDN already loaded in the shell. Use `<div class="mermaid">...</div>`.
3. **External PNG** — only if SVG or mermaid can't capture it (rare).

### Visual style for diagrams:
- Boxes: rounded corners, navy border (`#0a4a8f`), white fill
- Decision nodes: diamond shape, amber fill (`#fff3d4`)
- Exception/warning nodes: red border (`#c33`)
- Arrows: navy, 1.5px stroke
- Font: system sans-serif, 12–14px
- Keep total diagram width ≤ 780px to fit the body

---

## 9. Flowchart whitelist (diagrams required)

Build a flowchart/decision-tree specifically for:
- **SA 299** — Joint auditors: division-of-work + several-and-joint-liability flow
- **SA 315 → 330** — Risk identification → response
- **SA 450** — Misstatement evaluation → communication decision
- **SA 570** — Going concern: events → procedures → conclusion → reporting branches (4 possible reports)
- **SA 600 (Revised)** — Group audits: principal auditor decision tree for component scoping
- **SA 705 / SA 706** — Modification decision tree (qualified vs adverse vs disclaimer)
- **SA 710** — Corresponding figures vs comparative FS paths
- **SA 720** — Other Information: identification → consideration → reporting
- **CARO 2020** — Applicability tree (companies → exempt vs applies)
- **Ch 19 Ethics** — Schedule/Part/Clause structural map + "Which schedule does this fact pattern fit?" decision diagram

All other SAs: bullets only, no diagram (unless the chapter opener needs one).

---

## 10. Content rules recap (from v1, unchanged)

- **2 emphasis markers only:** `.keyword` class and `.exception` class. No inline `style="color:..."`, no `<mark>`, no `<b>`.
- `.clause` class for clause/section/paragraph numbers.
- No "Introduction" paragraphs. No historical background.
- No plain-English explanation when ICAI has a technical phrasing — use the ICAI phrasing.
- Do not exceed 6 Requirements bullets per SA.
- Do not repeat an SA across chapters (primary coverage only; cross-reference otherwise).

---

## 11. SA → Chapter map (authoritative)

| Chapter | SAs/SQCs covered (primary) |
|---|---|
| Ch 1 Quality Control | SQC 1, SA 220 |
| Ch 2 General Auditing Principles | SA 200, 210, 230, 240, 250, 260, 265, 299, **402** (moved here per PDF) |
| Ch 3 Audit Planning | SA 300 (primary); intro/linkage to 315, 320; **SA 600, 610, 620** (full body — per ch-03.pdf §4.5.1/4.5.2/4.5.3) |
| Ch 4 Materiality, Risk, Internal Control | SA 315, 320, 330, 450 (SA 402 moved to Ch 2) |
| Ch 5 Audit Evidence | SA 500, 501, 505, 510, 520, 530, 540, 550, 560, 570, 580 |
| Ch 6 Completion & Review | SA 260 revisit, 450 revisit, 560, 570 revisit, 580 revisit, 710, 720 |
| Ch 7 Reporting | SA 700, 701, 705, 706, 710, 720 + CARO overview |
| Ch 7a CARO 2020 | 21 clauses, applicability, sec 143(11) |
| Ch 8 Specialised Areas | **SA 800, 805, 810** (special-purpose frameworks / single FS element / summary FS — matches ch-08.pdf) |
| Ch 9 Related Services | SRS 4400, 4410 |
| Ch 10 Review of FI | SRE 2400, 2410 |
| Ch 11 Prospective FI & Other Assurance | SAE 3400, 3402, 3410, 3420 |
| Ch 19 Ethics | CA Act Schedules + Council Guidelines + Code of Ethics + Liabilities |

---

## 12. Validator-agent protocol

**After every batch** (pilot, batch A, batch B, CARO+Ethics, batch C), a validator agent runs with the following procedure:

1. **Reads SPEC.md** (this file) and **every HTML file** produced in the batch.
2. **For each file**, runs the sanity checklist (§13) and reports pass/fail per item.
3. **Spot-checks PDF alignment**: opens the source PDF via the `pdf` skill, samples 3 random SAs, and verifies the Objective blockquote matches the ICAI SM wording (substring match on core phrasing, not character-exact).
4. **Spot-checks length**: counts visible words using a small bash/python helper (`python3 -c "from bs4 import BeautifulSoup; ..."`).
5. **Spot-checks rendering**: validates the HTML parses (xmllint or Python html.parser), no unclosed tags, no broken mermaid syntax.
6. **Returns a report** with per-file grade: PASS / NEEDS-FIX / FAIL, and an explicit list of fix-tasks.

If any file is NEEDS-FIX or FAIL, the main orchestrator (me) spawns **parallel fix-agents**, one per failing file, each given:
- Path to the failing HTML file
- Path to the source PDF
- The specific validator findings to address
- SPEC.md reference

Fix-agents edit in place (using Edit tool), then the same validator re-runs on the fixed files. Loop until clean.

---

## 13. Sanity checklist (every subagent runs before returning)

- [ ] PDF actually opened and read (cite 1 verbatim Objective line per SA in `<blockquote class="icai">`)
- [ ] Full HTML visible word count between 2,500 and 4,500 (Ch 19 up to 5,500)
- [ ] One-pager ≤ 400 visible words
- [ ] 5 exam triggers section present in both files (`.triggers` class div)
- [ ] No paragraph >4 sentences anywhere
- [ ] Clause numbers quoted where required (CARO, Ethics) using `.clause` class
- [ ] No unauthorized flowcharts (only whitelisted SAs per §9)
- [ ] HTML is a valid standalone file — opens in browser, renders correctly
- [ ] mermaid diagrams (if any) parse without error
- [ ] Two files written: `chapters/ch-XX-slug/full.html` and `chapters/ch-XX-slug/onepager.html`
- [ ] Did not cover SAs outside the chapter's primary scope (§11)
- [ ] No `<style>` blocks added beyond the shared one in the shell
- [ ] No inline `style="..."` attributes except on `<svg>` where necessary
- [ ] Uses `.keyword` / `.exception` / `.clause` classes instead of bold/color hacks

---

## 14. What NOT to do

- ❌ Do not copy-paste full paragraphs from the ICAI SM (except 1 Objective per SA)
- ❌ Do not add JavaScript beyond the mermaid.js import in the shell
- ❌ Do not add external CSS or fonts (self-contained HTML only)
- ❌ Do not add decorative AI-generated imagery (information diagrams only)
- ❌ Do not produce PDFs, markdown, or docx — HTML only
- ❌ Do not skip the 5 exam triggers
- ❌ Do not use emoji beyond the ⚠ prefix on `.exception` divs (CSS handles this automatically)
- ❌ Do not cover SAs outside the chapter assignment in §11
