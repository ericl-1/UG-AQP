# Exam Results Analysis Tool
**Version 2.0 · Faculty of Medicine, University of Ottawa**
**Hosted at:** https://ericl-1.github.io/exam-results-analysis

---

## What this tool does

The Exam Results Analysis Tool automates the analysis of multiple-choice exam results for UGME exam coordinators. Upload your QuestionMark or Scantron export and receive item statistics, score distributions, flagged question reports, and formatted Word documents — all without installation, software licences, or statistical expertise.

Everything runs in your browser. No data leaves your computer.

---

## What's new in version 2.0

- **Student Feedback module** — upload a QuestionMark feedback export and automatically organise student comments by question number, with a manual review screen for ambiguous entries and a downloadable Feedback Report.
- **Redesigned setup screen** — cleaner layout with prominent upload zones, a sticky Run Analysis button always visible, and template download links inline below each upload zone.
- **Redesigned results screen** — six tabs consolidated into three (Analysis, Reports, Feedback). The Analysis tab includes an MCQ / DIF toggle. The Reports tab has a single preview and one Download button.
- **Modernised interface** — lighter surfaces, consistent controls, frozen table headers, working column resizing, and a unified status colour system across all views and reports.

---

## Supported data sources

| Source | Results file | Answer key file |
|---|---|---|
| QuestionMark | Raw data export (.xlsx or .csv) | Answer key export (.xlsx or .csv) |
| Scantron | Scantron .txt export | Not required — key embedded in file |

Don't have a file in the right format? Download the template from the link below each upload zone.

---

## How to run an MCQ analysis

1. Open the tool in your browser.
2. Enter the **exam title** and **exam date** at the top.
3. Select your **data source** (QuestionMark or Scantron).
4. If you want a DIF report comparing EN and FR student performance, turn **DIF Analysis on** and confirm the stream codes (default: E / F for QM, or enter your course codes for Scantron).
5. Upload your **results file** and **answer key file**.
6. Click **Run Analysis**.

---

## How to run a Feedback analysis

Feedback analysis runs independently — no MCQ analysis is required.

1. Switch to the **Student Feedback** tab on the setup screen.
2. Upload your **QuestionMark feedback export** (.xlsx, one row per student).
3. Click **Parse & Analyse Feedback**.
4. Review any unrecognised comments in the manual review screen — assign each one to a question number, send it to General Feedback, or discard it.
5. View results in the **Feedback** tab: Frequency table, By Question, or Most Commented.

If an MCQ analysis is also loaded in the same session, questions flagged in the MCQ analysis are automatically cross-referenced in the Feedback results.

---

## Analysis results

### Analysis tab
The MCQ Analysis table shows all questions with:
- Difficulty (p-value) and discrimination (point-biserial correlation)
- Flag reason (Difficult, Poor discrimination, Check Key, Too easy)
- Best students chose (for Check Key items)
- Recommendation (Keep, Review, Credit, Delete)

Use the **MCQ / DIF toggle** to switch between the MCQ item table and the DIF table. Use the **View filter** to show All items, Flagged only, Too easy, Poor disc., or DIF flagged.

### Reports tab
Three downloadable Word reports:
- **MCQ Analysis Report** — key findings narrative, flagged questions table, and all-questions summary
- **DIF Report** — EN/FR performance comparison per question (only available when DIF is enabled)
- **Full Combined Report** — MCQ and DIF in a single document

Select a report from the toggle to preview it before downloading.

### Feedback tab
Three views for feedback results:
- **Frequency** — all questions ranked by number of responses, with a volume bar
- **By Question** — comments grouped by question number in order
- **Most Commented** — same as By Question but sorted by volume

Download a formatted **Feedback Report** as a Word document at any time.

---

## Flagging thresholds

The following thresholds determine when questions are flagged. All values match the UGME assessment manual defaults and can be adjusted in **Settings** (hamburger menu → Settings).

| Flag | Condition | Default threshold |
|---|---|---|
| Too easy | p-value ≥ | 0.96 |
| Difficult | p-value < | 0.35 |
| Poor discrimination | rpbis < | 0.00 |
| Check Key | p < 0.25 and rpbis < | 0.15 |
| DIF flagged | p-value < | 0.01 |
| DIF gap — amber warning | EN vs FR gap ≥ | 8% |
| DIF gap — red warning | EN vs FR gap ≥ | 15% |

Changing any threshold after an analysis has already run will show a warning banner prompting you to re-run.

---

## Question Exceptions

You can mark individual questions as **Credited** or **Deleted** before or after running an analysis using the Question Exceptions panel (accessible from the Run Analysis footer when results files are loaded). Credited and Deleted questions are excluded from the analysis calculations and marked clearly in all reports.

---

## Settings

Open **Settings** from the hamburger menu (top right) to adjust:
- Analysis thresholds (all eight, with sliders and reset buttons)
- UI theme (uOttawa garnet or Elentra purple)

---

## Exports

| Export | Format | Contents |
|---|---|---|
| MCQ Analysis Report | Word (.docx) | Letter to directors, flagged questions table, all-questions table |
| DIF Report | Word (.docx) | DIF methodology summary, flagged DIF items table |
| Full Combined Report | Word (.docx) | MCQ + DIF in a single document |
| Feedback Report | Word (.docx) | Student comment summary by question |
| MCQ data | CSV | All item statistics — opens in Excel |
| DIF data | CSV | Full DIF statistics including chi-square values |

---

## Requirements

- Any modern browser (Chrome, Edge, Firefox, Safari)
- No installation required
- No internet connection required after the page loads
- No data is sent to any server — all processing happens in your browser

---

## Support

For questions or issues, contact **Eric Larouche**, Supervisor Project Management, Faculty of Medicine, University of Ottawa.

---

*Version 2.0 · Build 20260629-01 · June 29, 2026*
*Faculty of Medicine · University of Ottawa · Intended for internal use only*
