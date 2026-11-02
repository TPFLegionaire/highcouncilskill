# High Council — Example Session (skeleton)

Loaded only when the user asks how a session looks. Abbreviated TRIBUNAL run; word budgets
compressed for illustration.

---

**User:** "Full tribunal: should AcmeAlerts launch email-first at £99/mo, or wait until the
dashboard is self-serve?"

**[COUNCIL] framed** — Step 0 reads `CLAUDE.md`, the AcmeAlerts design notes, prior
transcripts, `UU-REGISTER.md`. Framed question captures: solo operator, ~14 h/week, £99 + 30
credits model locked, concierge onboarding decided, unresolved IP-ownership flag. Panel:
`full` (tribunal default). Domain-weight seat: **Executor** (launch-timing question, 1.5×).
Chairman: locked, non-deliberating. Surface: single-context (chat) → session marked.

**Step 1 — Restate gate.** Nine restatements. The Outsider's reframe — *"is the question
launch timing, or whether the operator can support ANY launch at 14 h/week?"* — diverges
materially → flagged to the user before Round 1 (question retained, reframe noted).

**Step 2 — Round 1 (blind).** E.g. Tail-Risk: names the IP-ownership ambiguity as the one
ruin-class exposure — revenue before ownership is resolved converts an open question into a
dispute. `Position: resolve IP before first invoice.` Executor: Monday-morning action is a
10-lead concierge pilot; first step ≤1 day (send 3 warm-intro emails).

**Step 3 — Round 2 (anonymised, A–I).** Bias Auditor (as "Member D") tags the launch case
with planning fallacy + names the flaw in Member G's base-rate claim; updates own position
citing Member B's channel point. "What Everyone Missed" items: nobody priced support load
into the 14 hours; nobody defined what cancels the pilot.

**Step 4 — Enforcement.** Agreement check trips (7/9 favour "pilot now") → counterfactual
probe to the two dissenters. One returns the flip evidence: "if the employer claims the IP,
pilot revenue is discovery-able" — feeds the Minority Report, and one pilot-now backer
downgrades to med after naming that flaw (valid update: flaw named).

**Step 5 — Stances + Pre-Mortems.** Each member's last two lines, e.g. Executor:
`PRE-MORTEM: pilot ran, 3 paying users, employer asked for the invoices; six months of
revenue became the IP dispute's evidence.` then
`STANCE: pilot-now | CONFIDENCE: high | DEALBREAKER: no` ×5 …
`STANCE: resolve-ip-first | CONFIDENCE: high | DEALBREAKER: yes` ×2 … 1 med, 1 abstain.
Tally: W_total 9.5 (Executor 1.5×). `pilot-now` 6.25 ≥ ⅔·9.5 (6.33)? No — 6.25 < 6.33 →
**no option clears**. Genuine split escalated.

**Step 6 — Verdict (excerpt).** Recommendation presents the split: pilot-now carries the
weight but not the threshold; the DEALBREAKER dissent (IP) is the blocker both camps accept
resolving first. Pre-Mortem (per surviving option, from the members' lines): pilot-now —
"**Revenue as evidence**" (Executor + Tail-Risk lines joined; first signal: an HR calendar
invite with no agenda) and "**Succeeded at the wrong thing**" (3 users who buy the alerting,
not the enrichment — the roadmap built the wrong half); resolve-ip-first — "**Permission
loop**" (approval sits with a VP for a quarter; first signal: no reply in 14 days). Kill
criteria, each tagged: "If IP position not confirmed in writing by {date+14d} → pilot
invalid → pause invoicing. [detects: Revenue as evidence]". One Thing First: "Send the IP-ownership question to
{contact} by Friday." Minority Report: the two resolve-ip-first dealbreakers, argument
verbatim. Scorecard: perspective 4/5, provider 1/5, evidence mix 30/25/30/5/10, convergence
risk Low. Artifacts: `council-report-….html`, `council-transcript-….md`.

**[SCAN] (additive).** Exclusion list = the council's findings (IP, support load, pilot kill
criteria, channel point…). Domain Map: 16 rows — e.g. Legal ✓ (source-ToS re-check at
commercial use), Governance ✓ (employer nexus of a work-adjacent SaaS), Privacy ~ (flips when
contact enrichment ships), Accessibility ~ (flips at self-serve dashboard), Performance ✗
(pre-PMF, single-tenant — reason given). Findings only for ✓ domains, epistemic-tagged.
Meta-question: *a commercial solicitor — "you priced the product before confirming you may
sell data derived from these sources commercially."* Top 3 actions ranked. Register append:
`- [2026-07-04 · AcmeAlerts] Any pricing decision made before source-ToS commercial-use
confirmation is provisional — ToS is the launch gate, not cleanup.`

**Tribunal close.** `tribunal-report-….html` with "Do These Three Things" reconciling the
council's One Thing First (IP email) with the scan's Top 3 — conflict shown (IP vs ToS
ordering), ranked with one line of reasoning. Status block lists all artifacts.
