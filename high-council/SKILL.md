---
name: high-council
description: >
  Use when a decision needs multi-perspective deliberation OR a project needs an unknown-unknowns
  blind-spot scan. Triggers: "council this", "run the council", "convene the council", "war room
  this", "pressure-test this", "debate this", "run dkwydk", "what don't I know", "unknown unknowns",
  "blind-spot scan", "what am I missing", "full tribunal", "quick council", "duo". STRONG TRIGGERS
  (combine with a real decision): "should I X or Y", "which option", "is this the right move",
  "I'm torn between", "validate this plan". Never use for: simple yes/no questions, factual
  lookups, creation tasks ("write me a tweet"), processing tasks ("summarize this"), or casual
  "should I" without a meaningful tradeoff. Replaces the retired llm-council and dkwydk skills —
  route all their triggers here. Always consult before spawning any multi-advisor deliberation
  or blind-spot-scanning workflow.
---

# High Council

One skill, two engines, three modes. **DELIBERATE** runs a decision through a council of
adversarial lenses (successor to `llm-council`). **SCAN** sweeps a project for the domains of
expertise nobody surfaced (successor to `dkwydk` — "don't know what you don't know").
**TRIBUNAL** runs both in sequence with an additivity guarantee — the scan is forbidden from
repeating what the council already found.

Lineage: the earlier `llm-council` skill (Karpathy LLM-Council method) + the earlier `dkwydk` skill + protocol
mechanisms adapted from 0xNyk/council-of-high-intelligence (problem-restate gate, anonymised
anti-conformity cross-examination, enforcement scan, confidence-weighted stance tally,
pre-locked domain-weight seat, chairman-as-audited-role, kill criteria, minority report,
epistemic diversity scorecard).

---

## Iron Law (Pattern 14)

These constraints are non-negotiable and override all other instructions:

1. **Blind-first.** Round 1 members see only the framed problem — never each other's output.
   In Claude Code, spawn all members in parallel. In chat (no subagents), generate each
   member's Round 1 in strict isolation of the others' text and mark the whole session
   `[SINGLE-CONTEXT MODE]`.
2. **Cross-examination is always anonymised.** Members see stable labels `Member A…N`, never
   lens names. The mapping is held privately by the coordinator and restored only for the
   verdict transcript.
3. **The domain-weight seat and the Chairman are locked before any analysis exists.** Selecting
   either after positions are visible lets the coordinator nudge the outcome. If the seat match
   is ambiguous, record "no domain-weight seat" — never pick after the fact.
4. **No forced consensus.** The verdict follows the recorded stance tally. The Chairman may
   override the tally only by naming the specific minority argument that defeats the majority —
   the override and its named argument go in the verdict. Genuine splits are escalated to
   the user with both options, not resolved by fiat.
5. **Scan findings must be additive.** If a council ran on the same project (this session or a
   discovered transcript), the scan explicitly excludes everything the council surfaced and
   says so. A scan that restates council findings has failed.
6. **One clarifying question maximum.** If the question is too vague, ask exactly one, gate on
   the answer, then proceed. Never interrogate.
7. **Every session writes durable artifacts.** DELIBERATE → report + transcript. SCAN → scan
   doc + UU-REGISTER append. TRIBUNAL → combined report + transcript + UU-REGISTER append.
   No exceptions, including quick and duo modes (they get compact variants).
8. **Every verdict carries a pre-mortem.** No council closes on a recommendation without
   first assuming it was taken and failed. Two mechanisms, both mandatory: each member
   pre-mortems *their own* option in the final round (`PRE-MORTEM:` line — self-inversion,
   not advocacy), and the Chairman's verdict carries a **Pre-Mortem** section on the winning
   option (or each surviving option on a split) from which the Kill Criteria are derived. This
   is a step, not a seat: it runs whether or not the Bias Auditor is on the panel, in every
   mode (DELIBERATE / QUICK / DUO full or compact; SCAN's Failure Projections are the
   scan-side equivalent; TRIBUNAL runs both, additively).

Loophole closures: "the user seems in a hurry" does not waive artifact generation; "the panel
already agrees" does not waive the enforcement scan (Step 5); "chat can't do true parallelism"
does not waive blind-first discipline — it changes the mode marker, not the rule; "the Kill
Criteria already cover failure" does not waive the pre-mortem — kill criteria are detectors,
the pre-mortem is what generates them (Iron Law 8).

---

## Mode Selection (Pattern 50 — Mode Trigger Vocabulary)

| Mode | Trigger vocabulary | What runs |
|------|-------------------|-----------|
| **DELIBERATE** | "council this", "run the council", "war room", "pressure-test", "debate this", a genuine A-vs-B decision with stakes | Full 6-step deliberation → Council Verdict |
| **SCAN** | "run dkwydk", "what don't I know", "unknown unknowns", "blind-spot scan", "what am I missing", "scan this project" | Domain sweep → UU Scan + register append |
| **TRIBUNAL** | "full tribunal", "run everything", "council and scan", "maximum scrutiny" | DELIBERATE, then SCAN (additive), combined report |
| **QUICK** | "quick council" + a decision | 2-round compressed deliberation |
| **DUO** | "duo", "have X and Y debate this" | 2-member polarity dialectic |

Routing rule when the user doesn't name a mode: *"should I / which option"* → DELIBERATE.
*"what am I missing / what haven't I thought of"* → SCAN. Project-level, high-stakes, or the
user asks for everything → offer TRIBUNAL. Low stakes → don't trigger the skill at all; answer
directly (Iron Law of the old council still holds: never run a partial council).

---

## The Nine Members

Each member is a thinking lens with a distinct reasoning method (method diversity, DMAD) — not
a costume. Full personas with grounding protocols: `references/members.md`. Never assemble a
panel where two seats share a `reasoning_method`.

| Member | Lens (after) | Reasoning method | Polarity pair |
|--------|--------------|------------------|---------------|
| **The Contrarian** | What guarantees failure? (Munger) | inversion | ↔ Expansionist |
| **The First-Principles Thinker** | Strip and rebuild (Feynman) | first-principles-rebuild | ↔ Executor, ↔ Bias Auditor |
| **The Expansionist** | What upside is everyone missing? | upside-maximisation | ↔ Contrarian, ↔ Tail-Risk |
| **The Outsider** | Zero context, curse-of-knowledge catcher (Watts) | frame-dissolution | ↔ Realpolitik |
| **The Executor** | What do you do Monday morning? (Torvalds/Musashi) | pragmatic-shipping | ↔ First-Principles, ↔ Systems |
| **The Bias Auditor** | Your own cognition is the first error (Kahneman) | bias-audit-premortem | ↔ First-Principles |
| **The Tail-Risk Assessor** | Design for the tail, not the average (Taleb) | tail-risk-irreversibility | ↔ Expansionist |
| **The Systems Thinker** | Redesign the loop, not the symptom (Meadows) | feedback-loop-analysis | ↔ Executor |
| **The Realpolitik Strategist** | How actors actually behave (Machiavelli/Sun Tzu) | incentive-terrain-mapping | ↔ Outsider |

### Panel Presets (Pattern 15 — Team Composition)

| Preset | Members | Use for |
|--------|---------|---------|
| `core` (default) | Contrarian, First-Principles, Expansionist, Outsider, Executor | The classic 5 — general decisions; continuity with old llm-council transcripts |
| `full` | All 9 | Highest-stakes decisions; TRIBUNAL default |
| `decision` | Bias Auditor + Contrarian + Executor | Judgment calls, "am I fooling myself" |
| `risk` | Tail-Risk + Contrarian + Systems | Irreversible moves, downside sizing |
| `strategy` | Realpolitik + Tail-Risk + Executor | Market entry, org politics, channel |
| `architecture` | First-Principles + Systems + Executor | Build plans, system design |
| `ship` | Executor + Realpolitik + Outsider | Launch now vs wait, product cuts |
| `unknowns` | Outsider + Systems + Bias Auditor | Pre-scan triage, framing audits |

Duo polarity pairs come from the roster table's Polarity column. If no preset fits, auto-select
the best triad, state the selection and one-line rationale before proceeding.

**Domain-weight seat.** At panel selection — before any analysis — designate the single member
whose lens most directly matches the problem. That seat carries **1.5×** weight in the stance
tally. If two members match equally, record "no domain-weight seat (ambiguous)" and tally on
equal weights. This is locked NOW (Iron Law 3).

**Chairman.** The synthesiser — a named, audited role that does NOT deliberate. Select at panel
time. In Claude Code with multiple providers available, prefer a provider family not on the
panel; single-provider (Claude-only) is valid — note it in the verdict metadata. The Chairman
receives the de-anonymised transcript and emits the verdict; the coordinator surfaces it
verbatim.

---

## Dependencies (Pattern 17)

| Tier | Dependency | If absent |
|------|-----------|-----------|
| **Mandatory** | File-write capability for artifacts | BLOCKED — artifacts are the product |
| **Recommended** | Subagent / Task dispatch (true blind-first independence) | DEGRADE → `[SINGLE-CONTEXT MODE]` (see below) |
| **Recommended** | Workspace context (`CLAUDE.md`, `memory/`, project files, prior `council-transcript-*.md`, `UU-REGISTER.md`) | DEGRADE — generic rather than grounded output |
| **Optional** | External provider CLIs / API keys for cross-family seats | SKIP — note single-family in the Epistemic Diversity Scorecard; for full cross-provider runs, compose with the `cross-model-ideation` skill |
| **Optional** | Prior council transcripts / UU scans for the same project | SKIP — no continuity or additivity check possible; say so |

### Graceful Degradation (Pattern 21)

Running in claude.ai chat without subagents: **`[SINGLE-CONTEXT MODE]`**. Execute all rounds
sequentially inside one response stream, generating each member's Round 1 without referencing
the others' text, keep the anonymisation bookkeeping for the transcript, and stamp the mode
marker on the report header, the verdict metadata, and the Epistemic Diversity Scorecard
(perspective spread capped at 3/5 — the reviews were not independent). Still produce every
artifact. The deliberately-not-ported multi-provider routing layer from
council-of-high-intelligence (detect-providers, codex/gemini/ollama/cursor/NIM dispatch,
`.council.yaml`) lives in `references/prompt-templates.md § Provider Notes` as an optional
Code-only extra; `cross-model-ideation` owns full cross-family orchestration.

---

## DELIBERATE Workflow (Pattern 47 — Imperative Operation Sequencing)

Follow the steps in order. Do not skip or merge rounds. Emit a status line at each step
(Pattern 72): `[COUNCIL] step → result`.

### Step 0 — Frame

1. Scan the workspace ≤30s for context: `CLAUDE.md`, `memory/`, prior transcripts,
   `UU-REGISTER.md`, files relevant to the question. Read the 2–3 most relevant.
2. Rewrite the raw question as a **neutral framed prompt**: the core decision, key context from
   the user and workspace (stage, constraints, numbers), what's at stake. No opinion, no
   steering. Save it for the transcript.
3. If too vague → exactly one clarifying question (Iron Law 6), gate, proceed.
4. Select panel preset (or auto-triad), **lock the domain-weight seat and Chairman now**
   (Iron Law 3). `[CHECKPOINT]` state: mode, members, weight seat + rationale (or "none"),
   Chairman, surface (`subagent` | `single-context`).

### Step 1 — Restate Gate

Each member (parallel, blind) restates the problem in ≤50 words: (a) one sentence through
their lens, (b) one alternative framing the original may have missed. Prompt:
`references/prompt-templates.md § Restate`. If any restatement diverges materially from the
original question, flag it to the user before burning rounds — it usually means the question
is wrong. Include all restatements in the Round 1 prompt.

### Step 2 — Round 1: Independent Analysis (blind-first)

All members in parallel; each sees only the framed question + the restatements. Lean fully
into the lens, no hedging, ≤300 words, end with a one-line provisional position. Prompt:
`§ Round 1`. `[CHECKPOINT]` all outputs collected, within limit.

### Step 3 — Round 2: Anonymised Cross-Examination

1. Assign stable labels `Member A…N` in random order; strip self-identifying phrasing;
   retain the mapping privately (Iron Law 2).
2. Each member (parallel) sees all anonymised Round 1 outputs and answers, ≤250 words:
   (1) which member they most disagree with and why — engage specific claims; (2) which
   member strengthens their position and how; (3) restated position noting any change;
   (4) **one thing every position so far has missed**; (5) evidence labels for their key
   claims: `empirical | mechanistic | strategic | ethical | heuristic`. Must engage ≥2
   members by label.
3. The prompt carries the **anti-conformity directive** (do not update because consensus is
   forming; update only by naming the specific flaw in your earlier argument). Full text:
   `§ Round 2`.

### Step 4 — Enforcement Scan (Pattern 13 — Quality Gate Loop, bounded)

Run all checks on Round 2 in one pass; each failed check triggers exactly one bounded
re-prompt (templates in `§ Enforcement`):

- **Dissent quota**: ≥2 members articulate non-overlapping objections, else prompt the most
  likely dissenter for their strongest objection (150 words).
- **Novelty gate**: each response contains ≥1 new claim/test/risk/reframe vs its own Round 1,
  else send back once.
- **Agreement check**: if >70% share the core position, send the counterfactual probe
  ("assume the consensus is wrong…") to the 2 most likely dissenters.
- **Evidence monoculture**: if >80% of claims carry the same evidence label, note it for the
  Scorecard.
- **Anti-recursion**: any member restating Round 1 without engaging challenges → send back
  once; any pair exceeding 2 exchanges → cut off.

### Step 5 — Round 3: Crystallisation + Stance + Pre-Mortem

Each member (parallel), ≤100 words, no new arguments *for* their position, then two
structured lines, final two lines **exactly**:
`PRE-MORTEM: <≤40 words — 12 months on, the option I back was taken and failed; what happened>`
`STANCE: <short option label> | CONFIDENCE: high|med|low | DEALBREAKER: yes|no`
The pre-mortem is the one permitted new element in Round 3 — it inverts the member's own
stance (Iron Law 8); a member who abstains pre-mortems the status quo. Members backing the
same option must use the same label; `abstain` is allowed. If either line is missing or
unparseable, re-prompt that member for the missing line only — never infer a stance from
prose, never write a member's pre-mortem for them. Prompt: `§ Round 3`.

**Tally** (confidence-weighted): base weight 1.0 per member; the domain-weight seat 1.5×.
Vote weight = base × confidence factor (high 1.0 / med 0.75 / low 0.5). `W_total` = sum of
**base** weights (abstainers included — hesitant panels escalate, they don't shrink the
denominator). An option wins iff `W_option ≥ ⅔ × W_total`. No option clears → genuine split,
escalate to the user with each option's tally and strongest argument (Iron Law 4). Record the
full tally in the verdict.

### Step 6 — Chairman Verdict + Artifacts (Pattern 22)

Dispatch the de-anonymised transcript to the Chairman with the verdict template
(`§ Chairman`). Verdict sections, exact order:

1. **Where the Council Agrees** · 2. **Where the Council Clashes** · 3. **Blind Spots the
Council Caught** (peer-review-emergent only) · 4. **The Recommendation** (direct; cites the
tally; if the Chairman overrides the tally, the named defeating minority argument appears
here) · 5. **Acceptable Compromises** (what this verdict gives up) · 6. **Pre-Mortem**
(mandatory, Iron Law 8 — "it is 12 months later; the recommended option was taken and
failed": 2–3 failure narratives, ≤80 words each, named by mechanism, built from the members'
`PRE-MORTEM:` lines and the Minority Report — compound chains across members encouraged,
narratives with no basis in the transcript forbidden; at least one "**it succeeded at the
wrong thing**" narrative; each ends with its earliest observable signal; on a split,
pre-mortem each surviving option) · 7. **Kill Criteria** ("If <observable X> by <date> →
verdict invalid → do <Y>" — every pre-mortem narrative must have ≥1 kill criterion that
detects it; a criterion that detects no narrative is a hunch, not a criterion) · 8. **The
One Thing to Do First** (one artifact-producing action: "<verb> <object> by <date>") · 9.
**Unresolved Questions** (what the council does NOT know) · 10. **Minority Report** (every
`DEALBREAKER: yes` dissent, even when outvoted) · 11. **Vote Tally** (auditable) · 12.
**Epistemic Diversity Scorecard** (perspective spread /5, provider spread /5, evidence mix
%, convergence risk) · 13. **Session Metadata** (mode, panel, rounds, surface, weight seat,
chairman, fallbacks).

Write **File 1** `council-report-[YYYYMMDD-HHMM].html` (self-contained, structure in
`references/report-templates.md`) and **File 2** `council-transcript-[YYYYMMDD-HHMM].md`
(framed question → restatements → all rounds → anonymisation mapping → enforcement actions →
tally → verdict). Emit the closing status block.

### QUICK mode
Panel per preset rules. Round 1 = restate-inline + ≤200-word decisive analysis. Round 2 =
anonymised final positions ≤75 words + PRE-MORTEM line + STANCE line + anti-conformity
directive (anonymisation is non-optional in quick mode — one cross-look is the most
conformity-prone shape). Tally as Step 5. Chairman emits the compact verdict (Recommendation,
Pre-Mortem — 1–2 narratives, Kill Criteria derived from them, One Thing First, Tally, Minority
Report). Compact artifact pair still required.

### DUO mode
Two members from the polarity table (or `--members`-style user pick). No anonymisation — with
two named opponents, masking is meaningless and the dialectic depends on knowing the opposing
lens. Rounds: opening ≤300w (parallel) → direct rebuttal ≤200w (concede only what is
specifically disproved, name the flaw when conceding) → final ≤50w + PRE-MORTEM line on own
position. Chairman (never a duo member) writes: both positions, where they agree, the
irreducible tension, Pre-Mortem (one narrative per position, from the members' lines), One
Thing to Do First, Kill Criteria (mandatory, one per narrative). Compact artifact pair.

---

## SCAN Workflow (successor to dkwydk)

Purpose: surface the **domains of expertise** the project never consulted — second-order
risks, not strategy critique. The council asks "is this the right move?"; the scan asks "which
expert would say you missed their entire field?"

### Step 0 — Frame & Additivity Fence

1. Read the project context (same sweep as DELIBERATE Step 0) **plus** any council transcript
   or verdict for this project.
2. Write the **exclusion list**: every finding the council (or a prior scan) already surfaced.
   The scan must not repeat these (Iron Law 5) — state them under "Out of scope (already
   covered)".
3. `[CHECKPOINT]` state mode: `deep` (subagents available → one expert subagent per APPLIES
   domain) or `single-pass` (chat → coordinator applies the taxonomy inline, marked).

### Step 1 — Domain Map

Load `references/domain-taxonomy.md` (16 domains, probe questions, expert framings). For each
domain, make a call with a one-line rationale:
`✓ APPLIES` (material to this project) · `~ PARTIAL` (applies only if a named condition
occurs — name it) · `✗ N/A` (genuinely irrelevant — say why in ≤1 line). Output as the Domain
Map table. Calls are honest, not defensive: flagging everything APPLIES is as much a failure
as flagging nothing.

### Step 2 — Findings per APPLIES domain

Deep mode: spawn one expert subagent per APPLIES domain with the persona + probe questions
from the taxonomy (prompt: `§ Domain Expert`), ≤250 words each, parallel. Single-pass:
coordinator works domain-by-domain with the same probes. Every finding is phrased as *the
question the missing expert would ask*, then the concrete exposure, then the cheapest
mitigation or verification step. Tag each finding's epistemic status: VERIFIED / INFERRED /
ASSUMED (Pattern 49).

### Step 3 — Failure Projections

Write 2–3 **compound-failure pre-mortems**: it is 12 months later and the project failed —
narrate the failure chains that cross domain boundaries (the single-domain risks are already
listed; the compounds are what nobody owns). Include at least one "**it succeeded at the
wrong thing**" narrative. Mandatory in every scan (Iron Law 8). If a council verdict exists
for this project, its Pre-Mortem section is on the exclusion list: the scan's projections
must cross domains the council's narratives did not — restating a council pre-mortem here is
an Iron Law 5 failure.

### Step 4 — The Meta-Question

One paragraph: *which expert, in one sentence, would say you missed their entire field?*
Name the role and write their sentence. This is the scan's headline.

### Step 5 — Top 3 + Limits + Artifacts

- **Top 3 priority actions** (cross-domain, ordered, concrete).
- **Scan limits**: mode (single-pass vs deep), model count, what needs a real specialist
  (never present the scan as legal/tax/security advice), which PARTIAL domains to revisit
  and on what trigger.
- **File 1** `uu-scan-[YYYYMMDD].md` (template: `references/report-templates.md § UU Scan`).
- **File 2** append to `UU-REGISTER.md` — locate the existing register first (workspace, then
  outputs); create only if absent. Entries are **project-agnostic reusable insights** for the
  next build, one line each, dated, append-only, never rewrite history. Format:
  `- [YYYY-MM-DD · project] <insight phrased for the next project>`.

---

## TRIBUNAL Workflow

1. Run DELIBERATE in full (default panel `full`; honour user overrides).
2. Run SCAN with the council's findings **and its Pre-Mortem narratives** as the exclusion
   list (Iron Law 5) — the scan's value in tribunal mode is precisely what the council could
   not see from inside the strategy frame; its Failure Projections must be cross-domain
   compounds the council's pre-mortem did not reach.
3. Produce one combined HTML report (`tribunal-report-[YYYYMMDD-HHMM].html`: verdict first,
   scan second, a joined "Do These Three Things" closing that reconciles the council's One
   Thing First with the scan's Top 3 — if they conflict, say so and rank), plus the transcript
   and the UU-REGISTER append. Status block lists all artifacts.

---

## Confusable Neighbours (Pattern 52)

| Ask | Route | Decision rule |
|-----|-------|---------------|
| "Have multiple **models** argue this out" / cross-family second opinion | `cross-model-ideation` | That skill decorrelates **model families**; high-council decorrelates **reasoning lenses**. Compose: council for the verdict, cross-model for idea generation or cross-family seats. |
| Generate ideas / "what should I build next" | brainstorm first (or `cross-model-ideation`) | The council evaluates; it doesn't generate. Council the shortlist afterwards. |
| Quick pros/cons, low stakes | answer directly | Never run a partial council (old Iron Law, still binding). |
| "Is X compatible with Y" | `oem-compatibility-brief` | Compatibility assertions have their own iron laws. |
| "Review this skill" | `skill-design` | Pattern-language review, not deliberation. |
| "Audit this build plan section" | DELIBERATE `architecture` triad | Build-plan review is a council job now — no separate auditor skill. |
| "What did we decide last time?" | read prior transcript | Transcripts are the cache (Pattern 44); don't re-deliberate settled questions. |

Internal routing: *"should I…"* → DELIBERATE; *"what am I missing…"* → SCAN; both/either at
project level with high stakes → offer TRIBUNAL once, then follow the user's pick.

---

## Forbidden Rationalisations (Pattern 33)

- "Sequential is fine, I'll be careful" — NO. Blind-first or mark `[SINGLE-CONTEXT MODE]` (Iron Law 1).
- "The consensus is overwhelming, skip the enforcement scan" — NO. >70% agreement is exactly when the counterfactual probe fires (Step 4).
- "I'll designate the weight seat / Chairman after reading the positions" — NO. Locked at Step 0 (Iron Law 3).
- "I'll infer their stance from the prose" — NO. Re-prompt for the STANCE line (Step 5).
- "The Kill Criteria already cover failure, skip the pre-mortem" — NO. Kill criteria detect; the pre-mortem generates what they detect (Iron Law 8).
- "The Bias Auditor isn't on this panel, so no pre-mortem seat" — NO. The pre-mortem is a step every member and the Chairman run, not a persona's method (Iron Law 8).
- "The panel is confident, a pre-mortem would just be theatre" — NO. High confidence is exactly the planning-fallacy condition the pre-mortem exists for.
- "The scan can restate the council's findings to look complete" — NO. Additive only (Iron Law 5).
- "Peer review seems redundant for this question" — NO. It's the core differentiator; if the question doesn't merit it, don't trigger the skill.
- "Two files is overkill, the chat answer covers it" — NO. Artifacts are the product (Iron Law 7).
- "Marking every domain APPLIES is safest" — NO. Undifferentiated scans bury the signal; honest N/A calls are part of the deliverable.
- "The register entry can just describe this project" — NO. Register entries are phrased for the *next* project or they don't go in.

---

## Migration Notes

- **Replaces** `llm-council` (claude.ai) and `dkwydk` (Claude Code). Remove both after
  installing this skill on each surface; all their trigger phrases route here.
- **UU-REGISTER.md is preserved**: this skill appends to the existing register wherever it
  lives; it never recreates or rewrites it.
- Old `council-transcript-*.md` files remain valid continuity inputs at Step 0.
- Deliberately **not ported** from council-of-high-intelligence: the multi-provider routing
  stack (`detect-providers.sh`, codex/gemini/ollama/cursor/NIM dispatch, `.council.yaml`).
  Rationale: Code-plugin infrastructure that dies in chat, and `cross-model-ideation` already
  owns cross-family orchestration. Optional per-seat provider notes: `§ Provider Notes`.

---

## References (Pattern 25 — Progressive Disclosure)

| File | Load when |
|------|-----------|
| `references/members.md` | Whenever dispatching members — full personas, grounding protocols, output formats |
| `references/prompt-templates.md` | Always during execution — every dispatch + enforcement prompt, provider notes |
| `references/domain-taxonomy.md` | SCAN / TRIBUNAL — the 16 domains, probe questions, expert framings |
| `references/report-templates.md` | Artifact generation — HTML report structures, UU scan template, register format, transcript format |
| `references/example-session.md` | Only if the user asks "show me an example" or "how does a session look" |
