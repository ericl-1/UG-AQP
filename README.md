# Assessment Quality Platform (AQP)
**Version 3.0 · Faculty of Medicine, University of Ottawa**  
**Hosted at:** https://ericl-1.github.io/UG-AQP/

---

## What this tool does

The Assessment Quality Platform automates the analysis of multiple-choice exam results and student feedback comments for UGME exam coordinators. Upload a QuestionMark or Scantron export and receive item statistics, score distributions, flagged question reports, student feedback organised by question, and formatted Word documents — all without installation, software licences, or statistical expertise.

Everything runs in your browser. No data leaves your computer.

---

## How to start an analysis

Open the tool and click **Start new session** from the home screen. The setup flow has three steps:

1. **Exam details** — enter the exam title, date, and coordinator name (optional; included in every exported report).
2. **Analysis type** — choose one of three modes:
   - **MCQ Item Analysis** — item statistics, score distributions, flagging, and DIF.
   - **Student Feedback Analysis** — parse and organise student comments by question.
   - **Combined Analysis** — run both in a single session. MCQ is validated first; feedback upload unlocks once MCQ is confirmed.
3. **Upload** — upload the required files for your chosen mode (see below), then click **Run Analysis**.

---

## Supported data sources

| Source | Results file | Answer key |
|---|---|---|
| QuestionMark | Raw data export (.xlsx or .csv) | Answer key export (.xlsx or .csv) |
| Scantron | Scantron .txt export | Not required — key embedded in file |

For feedback analysis, upload a QuestionMark feedback export (.xlsx, one row per student).

---

## MCQ Item Analysis

### Running the analysis

1. Select **MCQ Item Analysis** on the setup screen.
2. Upload your results file and answer key file.
3. If you want a DIF report comparing English and French student performance, enable **DIF Analysis** and confirm the stream codes (default: E / F).
4. Click **Run Analysis**.

### Item Analysis tab

An **MCQ Analysis / DIF Analysis** toggle switches between two tables.

The MCQ Analysis table shows all questions with:

- Difficulty (p-value) and discrimination (point-biserial correlation, rpbis)
- Elentra item ID (when embedded in the QM file)
- Flag reason — Difficult, Poor discrimination, Low discrimination, Check Key, Too easy — with a plain-language recommendation. DIF flags appear alongside other flag types on the same question when applicable.
- Best students chose (for Check Key items)
- Distractor breakdown (expand any row)

Use the **View filter** to show All items, Flagged only, Easy only, Poor disc., or DIF flagged.

### DIF Analysis

DIF (Differential Item Functioning) uses the Swaminathan–Rogers / Zumbo logistic regression method, comparing English and French students' probability of answering correctly after controlling for overall ability. A Nagelkerke R² effect size is reported and questions are flagged when the chi-square difference on 2 degrees of freedom is significant at p < 0.01. Flagging is suppressed when any language × outcome cell has fewer than five responses to avoid false positives on sparse data.

### Flagging thresholds

Default values match the UGME assessment manual. All thresholds can be adjusted in **Settings**.

| Flag | Condition | Default |
|---|---|---|
| Too easy | p-value ≥ | 0.96 |
| Difficult | p-value < | 0.35 |
| Poor discrimination | rpbis < | 0.00 |
| Low discrimination | rpbis < | 0.15 |
| Check Key | p < 0.25 and rpbis < | 0.15 |
| DIF flagged | chi-square p < | 0.01 |
| DIF gap — amber warning | EN vs FR gap ≥ | 8% |
| DIF gap — red warning | EN vs FR gap ≥ | 15% |

### Question Exceptions

Mark individual questions as **Credited** or **Deleted** from the Question Exceptions panel. Excepted questions are excluded from all calculations (scoring, averages, reliability, and DIF) and are clearly marked in all reports. Every exception requires a written reason before it can be saved.

---

## Student Feedback Analysis

### Running the analysis

1. Select **Student Feedback Analysis** on the setup screen.
2. Upload your QuestionMark feedback export (.xlsx, one row per student).
3. Click **Validate feedback**, then **Run Analysis**.

### Feedback tab

Three views for feedback results:

- **By Question** — comments grouped by question number, in ascending order.
- **Most Commented** — same content sorted by comment volume.
- **Frequency** — all questions ranked by number of responses with a volume bar.
- **Flagged Qs** — available in Combined sessions; shows only questions that also carry an MCQ flag.

Use the search bar to filter comments across all views. Bookmark individual comments with ★ and use "Move ★ bookmarked to top" to surface them.

### Comment categorization

Comments are automatically classified as **Content**, **Translation**, or **Other**. Uncategorised comments can be assigned manually in the Feedback tab. Bare question references (e.g. "Q12" with no attached comment) are counted silently and do not appear in the comment list.

### Feedback Overview (KPI zone)

Six metrics summarise the feedback session: Students responded, Questions reached (with a coverage gauge), Total attributions, Most commented question, Students with Q# feedback, and — in Combined sessions — a breakdown of how many flagged questions also received student comments.

---

## Combined Analysis

Select **Combined Analysis** to run both MCQ and feedback in a single session. The setup screen stages the uploads: confirm the MCQ file first ("Looks good"), then the feedback upload zone unlocks. A single **Run Analysis** button sequences both analyses. Results are available across all four tabs — Item Analysis, Feedback, Review Queue, and Reports — and flagged questions are automatically cross-referenced in the Feedback view.

---

## Review Queue

The **Review Queue** tab lists all flagged and excepted questions in one place for efficient item-by-item review. Each question shows its flag reason, statistics, and recommendation.

---

## Reports tab

Four downloadable Word reports are available depending on which analyses were run:

| Report | Contents |
|---|---|
| MCQ Analysis Report | Key findings narrative, flagged questions table, all-questions summary |
| DIF Report | Methodology summary, flagged DIF items table (EN/FR comparison) |
| Full Combined Report | MCQ and DIF in a single document |
| Feedback Report | Student comments organised by question, volume summary, key findings |

Click **Preview** on any report row to review it before downloading. All reports open with a generation line — date and coordinator name — and are addressed to the Director(s) in the letter format used in SPSS-era reports.

A **CSV export** is also available for the MCQ item statistics, with a self-documenting header block and disposition column for audit purposes.

---

## Exam Overview (KPI zone)

After an MCQ analysis runs, a collapsible **Exam Overview** banner appears above the tabs showing four key metrics: Students (EN/FR split), Exam Average (with a Good/Acceptable/Low/Concerning badge), Reliability (Cronbach's α with a gradient gauge), and Question Health (count of flagged, easy, DIF, credited, and deleted questions). A score distribution histogram is displayed below, with an EN/FR toggle when both streams are present.

---

## Settings

Open **Settings** from the menu (top right of the results screen) to adjust:

- All flagging thresholds (with reset buttons for each)
- DIF stream codes
- UI theme — **uOttawa Garnet** or **Elentra Purple**

Changing thresholds after a completed analysis triggers a prompt to re-run.

---

## Requirements and limitations

- Any modern browser (Chrome, Edge, Firefox, Safari)
- No installation required
- All processing happens in your browser — no data is sent to any server
- **Session data is not saved** — refreshing or closing the tab will lose the current session. Export your reports before closing.

---

## Support

For questions or issues, contact **Eric Larouche**, Supervisor Project Management, Faculty of Medicine, University of Ottawa.

---

*Version 3.0 · Build 20260716-01 · July 16, 2026*  
*Faculty of Medicine · University of Ottawa · Intended for internal use only*
