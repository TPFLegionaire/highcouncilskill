# High Council — Artifact Templates

Structures for every mandated artifact (Iron Law 7). Filenames use the session timestamp.

---

## § Council Verdict (the Chairman's output — Markdown, embedded in both files)

```markdown
# Council Verdict — {SHORT_TITLE}

**Session:** {YYYY-MM-DD HH:MM} · **Mode:** DELIBERATE|QUICK|DUO|TRIBUNAL · **Surface:**
subagent | SINGLE-CONTEXT · **Panel:** {members} · **Domain-weight seat:** {member + 1.5× |
none (ambiguous)} · **Chairman:** {name/provider | coordinator fallback}

## The Question
> {FRAMED_QUESTION}

## Where the Council Agrees
{Independent convergence points — high-confidence signals.}

## Where the Council Clashes
{Genuine disagreements, both sides explained, why reasonable lenses diverge.}

## Blind Spots the Council Caught
{ONLY insights that emerged in cross-examination — "What Everyone Missed" items and
enforcement-provoked reversals. Not a rehash of Round 1.}

## The Recommendation
{A direct answer, not "it depends." Cites the tally. If overriding: "CHAIRMAN OVERRIDE —
the defeating minority argument: {verbatim}". If split: present both options + tallies and
hand the decision back.}

## Acceptable Compromises
{What this verdict gives up, named. One bullet each, ≤2 sentences. If nothing — say why.}

## Pre-Mortem
{Mandatory (Iron Law 8), never N/A. "It is {date + 12 months}. {Recommended option} was
taken and failed." 2–3 narratives, ≤80 words each, format per narrative:
**{Mechanism name}** — {causal chain, past tense, built from members' PRE-MORTEM lines +
Minority Report; name the members whose lines it joins}. *First signal:* {earliest
observable}.
At least one narrative titled "Succeeded at the wrong thing". On a split: one block per
surviving option.}

## Kill Criteria
{Observable falsifiers, one per Pre-Mortem narrative minimum. Format per line: "If {X,
observable without re-convening} by {date} → verdict invalid → {do Y}. [detects: {narrative
name}]". No orphan criteria, no undetected narratives.}

## The One Thing to Do First
{Exactly one artifact-producing action: "{verb} {object} by {date}". Not a list. Verbs that
produce artifacts: write, push, run, file, measure, send.}

## Unresolved Questions
{Lead with what the council does NOT know. Inputs needed from the user.}

## Minority Report
{Every DEALBREAKER: yes dissent, even when outvoted — the member, their stance, their
strongest argument. "None" if none.}

## Vote Tally
{One line per option: `{option} — {weight} ({backers with confidence factors})`. Mark the
1.5× seat. State W_total, the ⅔ threshold, and cleared / not cleared. Abstentions listed.}

## Epistemic Diversity Scorecard
- Perspective spread (1–5): {orthogonality of viewpoints; cap at 3 in SINGLE-CONTEXT}
- Provider spread (1–5): {1 if single-family — the honest default}
- Evidence mix: {% empirical / mechanistic / strategic / ethical / heuristic; flag >80%
  monoculture}
- Convergence risk: {Low/Med/High + reason}

---
### Session Metadata
mode: … · panel_size: … · rounds_run: … · surface: subagent|single-context ·
enforcement_fired: {list|none} · fallbacks: {list|none} · weight_seat: … · chairman: …
```

QUICK verdict = sections: header, Question, Recommendation, Pre-Mortem (1–2 narratives),
Kill Criteria (≥1 per narrative), One Thing First, Vote Tally, Minority Report, Metadata.
DUO verdict = header, Question, both positions, Where They Agree, The Core Tension,
Pre-Mortem (one narrative per position, from the members' PRE-MORTEM lines), One Thing First,
Kill Criteria (mandatory, one per narrative), Metadata. Pre-Mortem is never omitted in any
compact variant (Iron Law 8).

---

## § HTML Report — `council-report-[YYYYMMDD-HHMM].html`

Self-contained, inline CSS, no external assets. Open/present it after generation.

**Design tokens**
```
Font:        -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif
Background:  #ffffff   Text: #1a1a2e   Border: #e0e0e0   Panel bg: #f8f9fa
Member accents:
  Contrarian #e74c3c · First-Principles #3498db · Expansionist #2ecc71 ·
  Outsider #9b59b6 · Executor #f39c12 · Bias Auditor #e67e22 ·
  Tail-Risk #c0392b · Systems #16a085 · Realpolitik #34495e
```

**Structure**
```html
<header>  title, timestamp, mode badge (+ visible SINGLE-CONTEXT badge when degraded)
<section.question>   blockquote of the framed question
<section.verdict>    the full Council Verdict above; left-border accent; Pre-Mortem as
                     one card per narrative (mechanism name as card title, first signal in
                     italics); Kill Criteria in a bordered callout, each line tagged with the
                     narrative it detects; Minority Report in a muted callout
<section.tally>      horizontal bar per option, width ∝ weight, ⅔ threshold as a dashed
                     vertical line; 1.5× seat marked ★
<section.alignment>  one row per member: accent dot · lens · STANCE · confidence · DEALBREAKER flag
<section.rounds>     collapsible <details> per member per round (accent left border);
                     Round 2 shown de-anonymised with the label mapping noted
<section.scorecard>  the four scorecard lines
<footer>             metadata line, muted
```
Print-friendly: `details[open]` forced in `@media print`. Collapsibles default closed except
the verdict.

---

## § Transcript — `council-transcript-[YYYYMMDD-HHMM].md`

Order, no omissions: original user question → framed question → panel/seat/chairman checkpoint
→ all restatements → Round 1 (named) → anonymisation mapping (letter → lens) → Round 2 (as
seen: anonymised) → enforcement log (which checks fired, prompts sent, replies) → Round 3 +
raw PRE-MORTEM and STANCE lines (and any line-only re-prompts) → tally computation →
Chairman verdict verbatim. This file is the persistent
cache (Pattern 44); future sessions read it instead of re-deliberating.

---

## § UU Scan — `uu-scan-[YYYYMMDD].md`

```markdown
# UU Scan — {PROJECT} — {D Month YYYY}

**Mode:** deep ({N} domain subagents) | single-pass (marked) · **Not specialist advice** —
domains {list} need real professionals.

## Snapshot
{≤120 words: what was scanned, who operates it, constraints that matter (solo, hours budget,
spend ceiling, employer nexus), context actually read.}

**Out of scope (already covered):** {exclusion list from the council/prior scan — Iron Law 5.
"None — no prior council/scan found" if empty.}

## Domain Map
| # | Domain | Call | One-line rationale |
|---|--------|------|--------------------|
| 1 | Security & Threat Model | ✓ APPLIES / ~ PARTIAL / ✗ N/A | … |
| … | (all 16, every row filled; PARTIAL names its flip condition) | | |

## Findings
### {Domain N — name}
**The question the missing expert asks:** {one sentence}
**Exposure here:** {concrete, this project} [VERIFIED|INFERRED|ASSUMED]
**Cheapest verification/mitigation:** {one step}
{1–3 blocks per APPLIES domain}

## Failure Projections
{2–3 compound pre-mortems crossing domain boundaries, 12-month horizon; include one
"it succeeded at the wrong thing" narrative.}

## The Meta-Question
{Which expert would say you missed their entire field — name the role, write their one
sentence. The scan's headline.}

## Top 3 Priority Actions
1. … 2. … 3. {cross-domain, ordered, concrete}

## Scan Limits
{Mode honesty (single-pass ≠ independent corroboration), model count, what needs a real
specialist, which PARTIALs to revisit and on what trigger, what was deliberately excluded.}
```

---

## § UU-REGISTER — append-only

Locate the existing `UU-REGISTER.md` first (workspace → prior outputs); create only if truly
absent, with this header:

```markdown
# UU Register
A living, project-agnostic knowledge base of unknown-unknowns discovered across builds. Each
entry is a reusable insight for the NEXT project, not a note about one project. Append; never
rewrite.
```

Entry format — one line, dated, generalised:
```
- [YYYY-MM-DD · project] {insight phrased for the next project}
```
Gate: if the line only makes sense for this project, rephrase or drop it.

---

## § Tribunal Report — `tribunal-report-[YYYYMMDD-HHMM].html`

Same design tokens. Order: header (TRIBUNAL badge) → Council Verdict (full § structure) →
divider → UU Scan (rendered, Domain Map as a table with call chips ✓/~/✗) → closing section
**"Do These Three Things"** — reconcile the council's One Thing First with the scan's Top 3
into one ranked list; if they conflict, show the conflict and rank anyway with one line of
reasoning. Companion transcript + register append still required.

---

## § Status Blocks (Pattern 72)

During execution: `[COUNCIL] {step} → {result}` / `[SCAN] {step} → {result}` per step.
Closing block, always:
```
[COUNCIL] framed → restated → R1×{n} → R2 anonymised → enforcement {fired|clean} → stances
tallied → pre-mortems ×{n} → chairman synthesised
[SCAN] framed → exclusions {n} → domain map 16 → findings {n} → meta-question → register +{n}
[OUTPUT] {each artifact filename on its own line}
```
(Omit whichever engine didn't run.)
