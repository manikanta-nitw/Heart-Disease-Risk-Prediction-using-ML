<div align="center">

```
   _____              _ _       _____
  / ____|            | (_)     |_   _|
 | |     __ _ _ __ __| |_  ___   | |_ __ __ _  ___ ___
 | |    / _` | '__/ _` | |/ _ \  | | '__/ _` |/ __/ _ \
 | |___| (_| | | | (_| | | (_) |_| | | | (_| | (_|  __/
  \_____\__,_|_|  \__,_|_|\___/|_____|_|  \__,_|\___\___|

        ── heart disease risk, read off the strip ──
```

#### `~/~/~/\~/~/~/\~/~/~/\~/~/~/\~/~/~/\~/~/~/\~/~/~/\~/~/~/\~/~/~/\~/~/~/`

A bedside-style risk assessor trained on **538 real patient records**
from a March 2025 clinic dataset — runs entirely in the browser,
no server, no upload, no tracking.

### ▸ [Live Demo →](https://heartdiseaseriskprediction121.netlify.app/)

</div>

<br>

## ▸ What this is

CardioTrace turns a doctor's intake notes into an instant cardiovascular
risk reading. Fill in a patient's age, history, and symptoms; press the
button; get a printed-style verdict — **Low / Moderate / High Risk** —
along with a live ECG-style trace, a breakdown of the leading risk
factors, and a recommended clinical pathway.

It is built as a **single self-contained HTML file**. Open it in a
browser and it works — on a clinic laptop with no internet connection,
on a tablet at the bedside, anywhere.

```
┌──────────────────────────────────────────┐
│  CardioTrace  // risk assessor            │
│  WHS MAR 2025 · 538 RECORDS               │
│  RF · 30 TREES · AUC 0.794                │
│  ╱╲    ╱╲    ╱╲    ╱╲    ╱╲    ╱╲         │
│ ╱  ╲__╱  ╲__╱  ╲__╱  ╲__╱  ╲__╱  ╲__      │
├┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┤
│  CH·01  Patient Particulars               │
│  CH·02  History & Risk Factors            │
│  CH·03  Presenting Symptoms               │
│  CH·04  Lipid Panel  (optional)           │
│  CH·05  Clinical Notes                    │
│                                            │
│           [ ▸ Print Reading ]             │
└──────────────────────────────────────────┘
```

## ▸ Why it looks like this

Most clinical ML demos look like SaaS admin panels — sidebar, cards,
gradients. CardioTrace doesn't. The whole page is styled as a strip of
**pink ECG graph paper** tearing out of a monitor, because that's the
one visual every cardiology ward already recognises at a glance.

- **Typewriter checkboxes** (`[ ]` → `[×]`) instead of toggle switches
- **ASCII block meters** (`███████░░░░░░░░`) instead of progress bars
- A **stamped verdict** — rotated, ink-bordered — instead of a toast
- A **live heartbeat trace** whose spike height and colour track the
  computed risk score, in the header and on the printout

> Form should follow the chart. A heart-risk tool printed like a lab
> ticket is easier to trust than one that looks like a dashboard for
> tracking ad spend.

## ▸ How the model works

| | |
|---|---|
| **Source data** | 538 patient records, WHS clinic, March 2025 |
| **Labelled subset** | 209 records with a confirmed diagnosis |
| **Algorithm** | Random Forest · 30 trees · max depth 8 |
| **Validation** | 5-fold cross-validation |
| **AUC-ROC** | **0.794** |
| **Inference** | Logistic approximation of the forest, embedded directly in JavaScript — no server, no API calls |

**Features used:**

```
AGE · SEX · LOCALITY (urban/rural) · SLEEP QUALITY
HYPERTENSION · DIABETES · HIGH LIPIDS · SMOKING · FAMILY HISTORY · HYPOTHYROID
CHEST PAIN · BREATHLESSNESS · PALPITATIONS
```

Age and chest pain are, by a wide margin, the strongest predictors in
this cohort — consistent with established cardiovascular risk literature.

## ▸ Running it

**Try it instantly →** [heartdiseaseriskprediction121.netlify.app](https://heartdiseaseriskprediction121.netlify.app/)

No build step, no dependencies, no installation — or run it locally:

```bash
# clone or download, then just open the file
open cardiotrace_printout.html        # macOS
start cardiotrace_printout.html       # Windows
xdg-open cardiotrace_printout.html    # Linux
```

Or in **VS Code**: right-click the file → *Open with Live Server*.

## ▸ Reading a result

| Score | Band | Pathway |
|---|---|---|
| `< 40%` | 🟢 **Low Risk** | Routine annual review |
| `40–64%` | 🟡 **Moderate Risk** | ECG + echo, reassess in 1–3 months |
| `≥ 65%` | 🔴 **High Risk** | Cardiology referral, TMT / angiography |

Each reading is added to the on-page **session log** — nothing is saved
to disk or sent anywhere; refreshing the page clears it.

## ▸ A note on use

```
┌──────────────────────────────────────────────────────────┐
│  ⚠  DECISION SUPPORT ONLY — NOT A DIAGNOSIS                │
│                                                            │
│  This tool assists clinical judgement. It does not        │
│  replace it. Every reading should be reviewed by a        │
│  qualified physician before any action is taken.          │
│                                                            │
│  All patient data stays in the browser. Nothing is        │
│  uploaded, logged, or transmitted.                        │
└──────────────────────────────────────────────────────────┘
```

## ▸ Roadmap

- [ ] Export a single reading as a printable PDF / image
- [ ] Expand the training set as more diagnoses are confirmed
- [ ] Add cholesterol-aware risk weighting once lipid data is more complete
- [ ] Optional dark "night shift" theme for the printout

<br>

<div align="center">

#### `~/~/~/\~/~/~/\~/~/~/\~/~/~/\~/~/~/\~/~/~/\~/~/~/\~/~/~/\~/~/~/\~/~/~/`

*Built for a clinic, not a boardroom.*

</div>
