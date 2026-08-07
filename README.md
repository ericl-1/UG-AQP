# AQP — Assessment Quality Platform

**Version 3.0 · Build 20260728-10**  
Undergraduate Medical Education

A browser-based tool for analyzing multiple-choice exam results and student feedback, replacing a former SPSS-based workflow for UGME exam coordinators.

🔗 **Live app:** https://ericl-1.github.io/UG-AQP/

---

## What it does

AQP guides coordinators through a step-by-step wizard to upload exam data, run psychometric analysis, review results, and generate formatted Word reports — all without leaving the browser.

**MCQ item analysis**
- Per-question difficulty (p-value) and discrimination (point-biserial correlation)
- Cronbach's alpha (reliability) for the exam as a whole
- Automatic flagging: Too easy · Difficult · Poor discrimination · Low discrimination · Check key
- Plain-language recommendations: RETAIN / CREDIT / DELETE / CHANGE THE KEY
- Distractor analysis (answer distribution per question)

**Differential Item Functioning (DIF)**
- Swaminathan–Rogers logistic-regression method (published standard)
- Compares EN and FR stream performance per question after controlling for overall ability
- Nagelkerke R² effect size with sparse-data guards (minimum 5 students per cell)
- Supports QuestionMark stream codes and Scantron course codes

**Student feedback analysis**
- Parses free-text QM feedback exports and auto-maps comments to question numbers
- Inline comment resolver for unmatched comments
- Categorizes comments: Content · Translation · Other
- Cross-references flagged MCQ questions in the feedback report

**Combined analysis**
- Runs MCQ item analysis and feedback parsing in a single session
- Results cross-reference automatically across both analyses

---

## Key features

- **5-step wizard** — Exam details → Analysis type → Configure → MCQ upload → Feedback upload (combined)
- **Question exceptions** — Delete, credit, or alternate-key individual questions with a required justification; exceptions applied at analysis time
- **Elentra ID support** — Item bank IDs parsed from QM exports and surfaced in item table, DIF table, Review Queue, CSV, and all Word reports
- **Review Queue** — Checklist of flagged items with coordinator review tracking
- **Reports** — Word (.docx) exports for MCQ, DIF, MCQ+DIF, and Feedback; PDF via browser print; CSV and JSON session data exports
- **Session status strip** — Live indicator of what's loaded and which reports are available
- **Configurable thresholds** — All flagging thresholds adjustable in Settings; changes prompt re-analysis
- **Two themes** — uOttawa garnet and Elentra purple

---

## Data and privacy

**No data ever leaves your browser.** AQP runs entirely client-side with no server, no database, and no authentication. Uploaded files are processed in memory and discarded when the tab is closed. The only item persisted to local storage is the selected colour theme.

---

## Supported data sources

| Source | Results file | Answer key |
|---|---|---|
| QuestionMark (QM) | `.xlsx` raw export | `.xlsx` key export |
| Scantron | `.txt` export (key embedded in MASTER row) | _(embedded)_ |

---

## Technical overview

| Property | Detail |
|---|---|
| Architecture | Single-file HTML application (HTML + CSS + JS, no build step) |
| Deployment | GitHub Pages — zero server infrastructure |
| Dependencies | JSZip · docx-js (Word export, in-browser) · html2canvas |
| Statistics | Pure JS — no external stats library |
| Browser support | Any modern browser (Chrome, Edge, Firefox, Safari) |
| Data model | `ExamSession` envelope wrapping `G` (MCQ) and `FB` (feedback) globals; JSON-serializable for future backend |

The psychometric core (Cronbach's alpha, logistic-regression DIF, item statistics) is implemented as pure functions that are DOM-free and portable to any future backend or shared module.

---

## Roadmap

The current version is production-grade for single-session analysis. The following capabilities are planned for future releases, gated on backend infrastructure:

**Near-term**
- Session autosave and resume (currently, closing the tab clears the session)
- Coordinator flag — manual question flagging with reason and recommended action, alongside stat-driven flags
- Exception rationale surfaced in Word report documents

**Backend-enabled (requires server + auth)**
- Session history and longitudinal item tracking (keyed to Elentra item IDs)
- Multi-user access and committee workflow
- SharePoint integration — session storage, Word export pipeline, institutional document archiving
- Elentra integration — item performance data fed back to the item bank
- Backend-rendered PDF matching Word export fidelity

**Platform vision**
- Evidence Score — a converging-evidence signal per question synthesizing all flag types into a single weighted indicator
- Historical item performance dashboard across exam cycles
- Power BI reporting integration

---

## Usage

1. Open https://ericl-1.github.io/UG-AQP/ in any modern browser
2. Click **New Analysis Session**
3. Follow the setup wizard (4 steps for MCQ or feedback-only; 5 steps for combined)
4. Review results and export reports from the **Reports** tab

For full instructions, see the [User Guide](AQP_User_Guide.docx) (included in this repository).

---

## Contact

**Eric Larouche**  
Supervisor, Project Management · Undergraduate Medical Education  
[elarouch@uottawa.ca](mailto:elarouch@uottawa.ca)

To report a bug, request a feature, or ask about the analysis methodology, please reach out by email. Include the exam name and a description of the issue.

---

*AQP — Assessment Quality Platform · Undergraduate Medical Education · v3.0*
