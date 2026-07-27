# AQP — Assessment Quality Platform

**University of Ottawa · Faculty of Medicine · Undergraduate Medical Education**

AQP is a browser-based exam analysis tool that replaces a legacy SPSS workflow for MCQ item analysis, DIF (Differential Item Functioning) analysis, and student feedback review. It runs entirely client-side — no server, no accounts, no installation — and is deployed on GitHub Pages as a single HTML file.

[![Version](https://img.shields.io/badge/version-3.0-garnet)](https://ericl-1.github.io/UG-AQP/)
[![Build](https://img.shields.io/badge/build-20260727--03-lightgrey)](https://ericl-1.github.io/UG-AQP/)
[![Deploy](https://img.shields.io/badge/deployed-GitHub%20Pages-brightgreen)](https://ericl-1.github.io/UG-AQP/)

---

## What it does

Upload a QuestionMark (or Scantron) results export and an answer key. AQP computes:

- **Item statistics** — difficulty (p-value) and discrimination (point-biserial correlation) for every question
- **Cronbach's alpha** — standard k/(k−1) formula, excluding deleted items from the item set
- **DIF analysis** — Swaminathan–Rogers logistic regression method comparing EN and FR student performance, with Nagelkerke R² effect size and sparse-data guards
- **Score distribution** — by language stream, with visual chart
- **Flag cascade** — Too Easy → Difficult → Poor Discrimination → Check Key, with plain-language recommendations (RETAIN / CREDIT / DELETE / CHANGE THE KEY)

Optionally pair with a QuestionMark feedback export to review, categorise, and export student comments by question.

All results are exportable as formatted **Word (.docx)** reports, **PDF** (via browser print), a structured **CSV** session record, and a **JSON** session data file for longitudinal tracking.

---

## Features

| Area | Detail |
|---|---|
| **MCQ Analysis** | Per-question difficulty, discrimination, flag type, recommendation, EN/FR breakdown |
| **DIF Analysis** | Logistic regression per item; EN vs FR performance gap; p < 0.01 significance threshold |
| **Feedback** | Parse, attribute, categorise, and review student free-text comments by question |
| **Reports** | Word exports: MCQ, DIF, MCQ+DIF combined, Feedback — each also printable to PDF |
| **Session exports** | CSV (question stats + feedback summary) and JSON (full structured session record) |
| **Question Exceptions** | Delete, credit, or assign alternate answer keys with written justification required |
| **Review Queue** | Collaborative review workflow for flagged items |
| **Thresholds** | All 8 analysis thresholds configurable; UGME Standard defaults pre-loaded |

---

## Deployment

The app is a single self-contained HTML file deployed on GitHub Pages.

```
https://ericl-1.github.io/UG-AQP/
```

No build step. No dependencies to install. No server. To update: replace `ugme_mcq_tool.html` and push. Changes are live within minutes.

---

## Data sources

| Source | Format | Notes |
|---|---|---|
| QuestionMark results | `.xlsx` | Primary source — raw export from QM, one row per student |
| QuestionMark answer key | `.xlsx` or `.csv` | Separate key export from QM |
| QuestionMark feedback | `.xlsx` | One row per student, free-text comment column |
| Scantron | `.txt` tab-delimited | Secondary source — MASTER row required for answer key |

---

## Architecture

AQP is intentionally a single-file client-side application:

- **~14,000 lines** of HTML, CSS, and JavaScript in one file
- **Zero server dependencies** — runs on any static host including GitHub Pages, SharePoint, local file system
- **Zero npm/build pipeline** — drop the file anywhere and it works
- **Session state in memory only** — no cookies, no localStorage (theme preference excepted)

The psychometric engine (`cronbach`, `doDIF`, `logReg`, parsers) is effectively pure — it reads inputs and returns results with no DOM dependency. These are the durable assets for any future backend integration.

### Why single-file?

For a single-analyst, single-session tool this removes an entire class of deployment and versioning problems. The ceiling is hard — no session history, no multi-user access, no longitudinal tracking — but the core analysis is production-grade today.

---

## Roadmap

The platform is designed to grow. The single-file architecture is the right scaffold to deliberately grow out of.

**Near-term (v3.x)**
- PDF exports matching the Word report format (requires a small server-side component)
- Session history and longitudinal item tracking (requires backend persistence)
- Scantron end-to-end validation

**Medium-term**
- SharePoint integration for institutional persistence and AD authentication
- Multi-session JSON comparison — load multiple session exports and track item performance across exam cycles
- Elentra item ID linking for stable cross-exam question identification

**Longer-term**
- SPFx web part for SharePoint-native embedding
- Elentra integration — enhancing the existing item analysis report
- Committee workflow and multi-user access

---

## Session data schema

Each exported JSON file follows a consistent schema designed for longitudinal comparison:

```json
{
  "meta":      { "examTitle", "examDate", "coordinator", "source", "version", "build", "exportedAt" },
  "summary":   { "totalStudents", "enStudents", "frStudents", "examAvgPct", "cronbachAlpha", ... },
  "thresholds": { "difficult", "easy", "disc", "difPValue", ... },
  "dif":       { "enabled", "enCode", "frCode", "flaggedCount" },
  "questions": [ { "number", "elentraId", "difficulty", "discrimination", "flag", "disposition", "dif": { ... } } ],
  "feedback":  { "totalComments", "attributedComments", "generalComments", "questionsTouched" },
  "session":   { "createdAt", "lastMcqRunAt", "lastFeedbackAt" }
}
```

Multiple JSON exports can be combined to track question performance over time. The `elentraId` field is included for future Elentra ID linking once that integration is resolved.

---

## Development

All changes are made to `ugme_mcq_tool.html` directly. Version constants are at the top of the script block:

```javascript
var APP_VERSION     = '3.0';
var APP_BUILD       = '20260727-03';
var APP_FAQ_VERSION = '3.2';
```

**Syntax check** (requires Node.js):
```bash
python3 -c "
import re, subprocess
content = open('ugme_mcq_tool.html').read()
scripts = re.findall(r'<script[^>]*>(.*?)</script>', content, re.DOTALL)
open('/tmp/check.js','w').write('\n'.join(scripts))
r = subprocess.run(['node','--check','/tmp/check.js'], capture_output=True, text=True)
print('RC:', r.returncode, r.stderr or 'clean')
"
```

**Build numbering:** `YYYYMMDD-NN`, incrementing within a date. Five version constants must be updated on every close: `APP_VERSION`, `APP_BUILD`, `APP_FAQ_VERSION` (only when coordinator-facing FAQ content changes), `APP_FAQ_DATE` (same), `APP_RN_DATE` (every close).

---

## Institutional context

- **Faculty:** Faculty of Medicine, University of Ottawa
- **Program:** Undergraduate Medical Education (UGME)
- **Purpose:** Internal use only — not for distribution
- **Replaces:** SPSS-based exam analysis workflow
- **Primary users:** Exam coordinators and assistant-dean of assessments

---

*© 2026 Faculty of Medicine, University of Ottawa. All rights reserved. Intended for internal use only — not meant for distribution.*
