# Wisconsin Card Sorting Test — User Manual

A single-file web recreation of the WCST for **teaching, demonstration, and research prototyping**. It runs entirely in a browser; there is nothing to install and no internet connection is required.

> **Scope note.** Scoring is a simplified educational version, not the Heaton clinical algorithm, and the tool carries no clinical norms. Use it to illustrate the paradigm and collect practice data — not to make diagnostic judgements.

---

## Getting started

1. Open `wcst.html` in any modern browser (Chrome, Edge, Firefox, Safari). Double-clicking the file is enough.
2. The tool opens in **Auto** mode. Use the **Auto / Examiner** toggle near the top to switch between the two modes.
3. Everything happens on one screen; no accounts or setup are needed.

To change the examiner password, open `wcst.html` in a text editor and edit the clearly marked line near the top of the script:
`var EXAMINER_PASSWORD = "wcst-2026";`

---

## Auto mode (self-administered)

The computer chooses and enforces the sorting rule, scores automatically, and shifts the rule silently.

- Four **key cards** sit at the top; a **test card** appears below.
- Match the test card to a key card by clicking it, or pressing **1–4**.
- The rule (colour, shape, or number) is hidden. The only feedback is **Correct** or **Incorrect**.
- After **10 correct sorts in a row**, the rule changes silently. Notice that sorting stopped working and switch strategy.
- The session ends after **6 categories** are completed.
- **Reveal current rule** (a teaching aid, Auto mode only) briefly shows the active rule.

---

## Examiner mode (manual administration)

Reproduces the two-person clinical workflow: the examiner sets the rule and delivers feedback by hand while the subject sorts.

Clicking the **Examiner** tab prompts for the password. Once entered it stays unlocked for that browser session.

**Console controls (visible to the examiner, not the subject):**

- **Subject ID** — free-text identifier written into every export.
- **Session start** — captured automatically when the examiner session begins.
- **Enforced rule** — set Colour / Shape / Number. This is your answer key; change it whenever you decide to shift.
- **Shift rule / new category** — moves to the next rule manually.
- **Auto-shift after 10 correct** — optional; when ticked, the rule advances automatically like Auto mode.
- **Correct match for this card** — shows which key is correct under the current rule, so you can score consistently.
- **Hide answer from subject** — blurs the rule and answer hint so you can turn the screen toward the participant.
- **Lock examiner** — re-locks the console and returns to the subject-safe Auto view (useful when handing over the device).

**Delivering feedback:** the subject clicks a key card (or presses 1–4); this becomes a *pending* response showing what they chose and which attributes it shares with the test card. You then click **✓ Correct** or **✗ Incorrect** (or press **C** / **X**) to deliver feedback and record the trial.

---

## Readout and metrics

The **Session readout** strip is always visible and shows: trials administered, categories completed (of 6), perseverative errors, total errors, the current correct streak, and category-completion markers.

---

## Trial log and exports (Examiner mode)

**Trial log — record booklet** lists every trial (number, test card, response key, rule in effect, verdict, and a perseverative flag), newest first.

- **Download trial log** — a CSV of the current session. It opens with a metadata header (subject ID, session start, export time, mode, and totals), followed by one row per trial. Delete the `#` header rows if importing into a strict parser.
- **Clear log** — empties the on-screen log.

---

## Session summary report (Examiner mode)

A live panel showing the standard WCST-style indices for the current session:

| Index | Meaning |
|---|---|
| Trials administered | Total responses given |
| Total correct / errors | Overall accuracy split |
| Perseverative errors | Errors that match the just-abandoned rule (the clinically key measure) |
| Non-perseverative errors | Errors not attributable to perseveration |
| Conceptual-level responses | Responses occurring in runs of 3+ consecutive correct |
| Categories completed | Rules mastered, out of 6 |
| Failure to maintain set | Errors made after 5+ consecutive correct but before completing the category |

**Batch export across subjects:**

- **Add session to batch** — captures the current subject's summary as one row.
- **Download summary CSV** — writes a one-row-per-session file (with the full index set) for analysis in Excel or R. If the batch is empty, it exports the current session as a single row.
- **Clear batch** — empties the queue.

The batch is held in memory for the current browser session, so **export before reloading or closing the tab.**

---

## Keyboard shortcuts

| Key | Action |
|---|---|
| 1–4 | Place the test card on the matching key card |
| C | Deliver **Correct** (Examiner mode, pending response) |
| X or I | Deliver **Incorrect** (Examiner mode, pending response) |

---

## Notes and limitations

- The examiner password is a **client-side soft lock**: it stops the subject from casually opening the console, but anyone who views the file's source can read it. For genuine access control, the tool would need a hosted backend.
- Batch data is not saved to disk automatically; use the export buttons.
- The response deck is generated so each test card matches exactly one key card on each dimension, keeping scoring unambiguous — a simplification relative to the published test.
