# Alivio Shareholder Deck Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Produce a verified, print-ready PowerPoint and PDF that make the shareholder case for a $9,950 Alivio installation plus $2,500 monthly maintenance across 20,000 units.

**Architecture:** Build the deck with the bundled Codex Grid presentation layouts and editable native charts/tables through `@oai/artifact-tool`. Keep calculations in one source object inside the deck builder so every chart, metric, and footnote uses the same figures.

**Tech Stack:** JavaScript ES modules, `@oai/artifact-tool`, LibreOffice, Poppler, bundled presentation QA scripts.

## Global Constraints

- Use a 1280 x 720 slide canvas.
- Use Arial as the portable sans-serif font.
- Use $9,950 installation, $2,500 monthly maintenance, and a 36-month initial term.
- Cover up to 20,000 units within the agreed scope.
- Label competitor custom pricing and labor savings as estimates or illustrations.
- Include a `[Sources]` block in speaker notes for every non-trivial external claim.
- Deliver both `.pptx` and `.pdf`.

---

### Task 1: Source and calculation ledger

**Files:**
- Create: `tmp/alivio-shareholder-final/source-notes.txt`
- Create: `tmp/alivio-shareholder-final/calculations.txt`

**Interfaces:**
- Consumes: Approved commercial terms and official competitor pages.
- Produces: Exact inputs and verified outputs used by the deck builder.

- [ ] **Step 1: Record the authoritative source URLs**

Include BoroDesk, Yardi, BuildingLink, AppFolio, EliseAI, Entrata, RealPage, HappyCo, New York SHIELD Act, NYC DOB, and NYC HPD URLs.

- [ ] **Step 2: Verify the cost arithmetic**

Run a JavaScript calculation that confirms:

```text
year_one = 9950 + (2500 * 12) = 39950
three_year = 9950 + (2500 * 36) = 99950
yardi_1_three_year = 20000 * 1 * 36 = 720000
market_2_three_year = 20000 * 2 * 36 = 1440000
market_3_three_year = 20000 * 3 * 36 = 2160000
```

- [ ] **Step 3: Verify the operating scenario**

Confirm:

```text
requests = 20000 * 0.25 = 5000 per month
hours = 5000 * 6 / 60 = 500 per month
admin_cost = 500 * 35 = 17500 per month
gross_savings = 17500 * 0.40 = 7000 per month
annual_gross_savings = 7000 * 12 = 84000
annual_net_after_subscription = 84000 - 30000 = 54000
```

### Task 2: Build the presentation

**Files:**
- Create: `tmp/alivio-shareholder-final/build.mjs`
- Create: `Alivio_Shareholder_Business_Case_2026.pptx`

**Interfaces:**
- Consumes: Source and calculation ledger.
- Produces: A 22-slide editable PowerPoint.

- [ ] **Step 1: Initialize the artifact-tool workspace**

Run:

```bash
node "$SKILL_DIR/container_tools/setup_artifact_tool_workspace.mjs" --workspace "$TMP_DIR"
```

- [ ] **Step 2: Implement shared presentation helpers**

Create helpers for slide titles, footers, notes, native charts, tables, and text blocks. Use stable object names for inspection.

- [ ] **Step 3: Implement the 22-slide narrative**

Follow the approved sequence in `docs/superpowers/specs/2026-07-30-alivio-shareholder-deck-design.md`. Use varied Codex Grid silhouettes and preserve minimum font sizes.

- [ ] **Step 4: Export slide previews and the PowerPoint**

Export all slide PNGs, a montage, layout JSON, and the final `.pptx`.

### Task 3: Presentation QA

**Files:**
- Inspect: `tmp/alivio-shareholder-final/rendered/`
- Inspect: `tmp/alivio-shareholder-final/montage.png`
- Modify: `tmp/alivio-shareholder-final/build.mjs`

**Interfaces:**
- Consumes: Draft PowerPoint.
- Produces: Corrected PowerPoint with no visible defects.

- [ ] **Step 1: Run automated overflow checks**

Run:

```bash
python "$SKILL_DIR/container_tools/slides_test.py" "$FINAL_PPTX"
```

Expected: no overflow errors.

- [ ] **Step 2: Render every slide**

Run:

```bash
python "$SKILL_DIR/container_tools/render_slides.py" "$FINAL_PPTX"
```

- [ ] **Step 3: Inspect the montage and every slide**

Check wrapping, chart labels, table legibility, footnotes, alignment, page markers, and visual consistency.

- [ ] **Step 4: Correct and rerun QA**

Update `build.mjs`, rebuild, rerender, and repeat until there are no material defects.

### Task 4: PDF export and QA

**Files:**
- Create: `Alivio_Shareholder_Business_Case_2026.pdf`
- Inspect: `tmp/alivio-shareholder-final/pdf-render/`

**Interfaces:**
- Consumes: Final verified PowerPoint.
- Produces: Print-ready PDF matching the PowerPoint.

- [ ] **Step 1: Export PDF with LibreOffice**

Use the bundled headless `soffice` binary to export the verified PowerPoint.

- [ ] **Step 2: Verify PDF metadata**

Run `pdfinfo` and confirm 22 pages and landscape page size.

- [ ] **Step 3: Render all PDF pages**

Run `pdftoppm -png` using the bundled Poppler binary.

- [ ] **Step 4: Inspect every rendered page**

Confirm there are no substituted fonts, missing glyphs, clipping, chart defects, or unreadable footnotes.

### Task 5: Final content audit

**Files:**
- Inspect: `Alivio_Shareholder_Business_Case_2026.pptx`
- Inspect: `Alivio_Shareholder_Business_Case_2026.pdf`

**Interfaces:**
- Consumes: Verified deliverables.
- Produces: Final delivery confidence.

- [ ] **Step 1: Search extracted slide text for prohibited ambiguity**

Confirm the deck does not call an estimate a quote, guarantee labor savings, promise unlimited scope, or transfer Alivio's reusable IP.

- [ ] **Step 2: Confirm required shareholder content**

Confirm the deck includes direct cost savings, implementation inclusions, employee-prototype risk, competitor analysis, SWOT, ownership terms, local server/local LLM options, rollout gates, and the precise decision requested.

- [ ] **Step 3: Deliver the PowerPoint and PDF**

Provide each final artifact once with a concise summary of the commercial recommendation and disclosure methodology.
