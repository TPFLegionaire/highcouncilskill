# High Council — Scan Domain Taxonomy

Sixteen domains of expertise a project can silently omit. This file merges what `dkwydk`
referenced as `domain-taxonomy.md` and `expert-personas.md` (those files never shipped; this
one does).

Per domain: **Expert** (the persona whose entire field might be missing — in deep mode this
line seeds the subagent identity), **Probes** (the questions the expert would ask first),
**Call guidance** (when to mark ✓ APPLIES / ~ PARTIAL / ✗ N/A). Every call gets a one-line
rationale in the Domain Map; PARTIAL calls must name the condition that would flip them to
APPLIES.

Honesty rule: an undifferentiated scan (everything APPLIES) buries the signal and fails the
deliverable. N/A with a reason is a finding.

---

## 1 · Security & Threat Model
**Expert:** application / infrastructure security engineer.
**Probes:** Who would attack this and why (data theft, abuse of compute, defacement, supply
chain)? Where do credentials, API keys, and tokens live at rest and in transit? What happens
when — not if — a dependency or the operator's own machine is compromised? Is there any
authenticated surface without rate limiting or audit trail? What's the blast radius of one
leaked secret?
**Call:** APPLIES for anything network-exposed, credential-holding, or agentic (tools that
fetch/execute). PARTIAL for local-only tooling (flips on deployment). N/A for pure documents.

## 2 · Privacy & Data Protection
**Expert:** data-protection officer (UK GDPR / EU GDPR / PECR first; other regimes flagged,
not improvised).
**Probes:** Is any personal data processed, even incidentally (names in scraped pages, contact
enrichment, logs)? What's the lawful basis, and is an LIA/Article 14 notice needed for
indirectly-collected data? Where does the data physically live and who are the processors?
Retention, deletion, and subject-access — designed or absent? Does any jurisdiction in scope
sit outside the GDPR frame (Israel, UAE/DIFC/ADGM, US state laws) — each needs its own check?
**Call:** APPLIES the moment identifiable individuals enter the pipeline. PARTIAL if data is
currently aggregate/corporate-only (flips on contact enrichment). N/A only when provably no
personal data.

## 3 · Legal, Regulatory & Contractual
**Expert:** commercial solicitor with platform/ToS literacy.
**Probes:** Do the data sources' ToS actually permit this collection and reuse? What licences
govern the dependencies and models, and do they permit commercial use? Any regulated activity
in scope (financial promotion, immigration advice, export-controlled tech)? Sanctions/export
screening where the buyer or content crosses borders? What contract terms is the operator
silently accepting via click-through?
**Call:** APPLIES for scraping, reselling data, regulated verticals, cross-border sales.
PARTIAL for internal-only tooling (flips on external users). Rarely N/A.

## 4 · Corporate Governance & Internal Approvals
**Expert:** information-security / data-governance officer at the parent company.
**Probes:** Does this need infosec, legal/DPO, or procurement sign-off *before* the first
byte is collected — is approval the real gate, not the technique? Is work running on personal
infrastructure or personal AI subscriptions that policy forbids for company data? Does an
internal AI policy exist that this quietly violates? Who owns the output — and would the
employer claim it (IP assignment clauses)? What does this look like in an audit at a US-listed
parent?
**Call:** APPLIES whenever employer data, employer benefit, or employer brand is in scope —
including "side" projects that touch work accounts. PARTIAL for fully personal projects with
no employer nexus. This domain produced the headline finding of the first dkwydk run; check
it early.

## 5 · IP & Ownership
**Expert:** IP lawyer.
**Probes:** Who owns the code, data, and brand — operator, employer, or ambiguous? Do
employment-contract IP clauses reach inventions made off-hours in an adjacent field? Are
trademarks cleared in the target markets before the name ships? Does training/derived data
carry upstream rights? Is open-sourcing any part a one-way door?
**Call:** APPLIES for anything intended to be commercialised, especially by an employed
founder. PARTIAL for throwaway internal tools. The unresolved-ownership state is itself a
finding — flag it as blocking further investment.

## 6 · Finance, Tax & Commercial
**Expert:** fractional CFO / accountant.
**Probes:** Does the unit economics survive the real cost stack (API tokens, subscriptions,
infra) at the stated price? Is subscription creep tracked against the operator's hard monthly
ceiling? VAT/sales-tax treatment for cross-border SaaS? At what revenue does the hobby become
a tax event or require the limited company's books to change? What's the cash exposure if the
main cost input (model pricing) doubles?
**Call:** APPLIES for anything charging money or with recurring costs. PARTIAL for free
internal tools with bounded spend.

## 7 · Operations & Maintenance Burden
**Expert:** SRE who has inherited a founder's side project.
**Probes:** Who operates this when the operator is on holiday, ill, or busy at the day job —
what breaks silently in two weeks of neglect? What's the true weekly maintenance cost against
the operator's real hours budget? Which manual steps exist that everyone forgot are manual?
Is there a bus-factor-of-one component (cookie-based workaround, hand-run script, personal
laptop) in the critical path?
**Call:** APPLIES for anything with users or scheduled jobs. PARTIAL for on-demand personal
tools. For a solo operator this domain is almost never N/A.

## 8 · Dependencies & Supply Chain
**Expert:** platform-risk analyst.
**Probes:** Which single third party can kill this with a ToS change, price change, API
deprecation, or model retirement? Are pinned versions and lockfiles real, and is there an
upgrade path when the pin rots? What's the fallback when the primary model/API degrades? Any
dependency whose licence or ownership is drifting? Which "free tier" is the architecture
secretly load-bearing on?
**Call:** APPLIES for anything built on external APIs, models, marketplaces, or data feeds —
which is nearly everything the operator builds. Name the top single point of failure.

## 9 · Reliability & Failure Modes
**Expert:** incident-response lead.
**Probes:** What data can be permanently lost, and when was restore last *tested* (a backup
that's never been restored is a hypothesis)? What does partial failure look like — wrong
answers served confidently vs clean errors? Idempotency of jobs and webhooks? What's the
incident story when a paying user hits corruption at 2am? What degrades first under load?
**Call:** APPLIES once anything persists state or serves users. PARTIAL for regenerable-
from-source pipelines (flips on first paying user).

## 10 · Performance & Scale
**Expert:** performance engineer.
**Probes:** Where does it fall over first — DB, embedding search, LLM rate limits, single
worker? Is the cost curve linear with usage or super-linear? What's the p95 experience at 10×
current load? Any O(n²) hiding in a matching/crosswalk loop?
**Call:** APPLIES for user-facing latency-sensitive systems or per-unit-cost businesses.
PARTIAL for batch/internal (flips at a named usage threshold). Frequently a legitimate ~ for
pre-PMF projects — say so rather than inventing scale problems.

## 11 · Observability & Auditability
**Expert:** platform engineer who has debugged production blind.
**Probes:** When output is wrong, can you reconstruct *why* — inputs, prompt/model version,
retrieved context? Are decisions that face customers or auditors logged with provenance? Cost
observability: can you attribute spend to feature/tenant? Would you notice silent degradation
(model drift, source-site format change) before a user does?
**Call:** APPLIES for LLM-mediated answers presented as fact, multi-tenant SaaS, or anything
with compliance exposure. PARTIAL for interactive-only tools where the human is the monitor.

## 12 · Accessibility & Usability
**Expert:** accessibility auditor / UX researcher.
**Probes:** Keyboard navigation, contrast, screen-reader labels on the public surfaces? Does
the target buyer (non-technical sales/ops person) survive first contact without the founder
present? Error states written for the user or for the developer? Mobile reality for an
email-first product?
**Call:** APPLIES for public web products, especially selling to non-developers. PARTIAL for
internal/technical-audience tools (flips on public launch or enterprise procurement, where
accessibility becomes a contractual question).

## 13 · People, Stakeholders & Channel
**Expert:** channel/alliances manager.
**Probes:** Whose commission, territory, or status does this quietly threaten — and what will
they do about it? Is there a channel-conflict rule for going direct where partners exist? Who
is the internal sponsor, and what happens when they move on? Who *sells* the output after the
artifact is delivered — is conversion owned by anyone? Which relationships is the operator
spending (favours, credibility) and is the spend deliberate?
**Call:** APPLIES for anything with an employer, partner, or multi-actor go-to-market nexus.
PARTIAL for purely personal tools. Adjacent to Domain 4 but distinct: 4 is *approval*, 13 is
*behaviour after approval*.

## 14 · Reputation, Brand & Trust
**Expert:** communications / brand-risk advisor.
**Probes:** What's the screenshot that goes viral for the wrong reason (hallucinated claim
under a real brand, scraped data presented as endorsed)? Does the output carry a brand that
isn't the operator's to spend? What happens to trust on the first confidently-wrong answer to
a paying customer? Is there a correction/retraction path?
**Call:** APPLIES when output ships under an employer's or client's brand, or makes factual
claims to buyers. PARTIAL for anonymous/internal work.

## 15 · Market Timing & Competition
**Expert:** competitive-strategy analyst.
**Probes:** What does the incumbent (or the platform itself) do when this works — copy, bundle,
cut off the API? Is the window open because of insight or because nobody else thinks it's
worth doing? What's the substitute the buyer uses today at price zero? If a frontier-model
release makes the core feature a commodity next quarter, what survives?
**Call:** APPLIES for commercial products. PARTIAL for internal tooling. Keep it additive —
councils usually cover strategy; this domain earns APPLIES only for the *unexamined*
competitive mechanics (platform response, commoditisation), not a strategy re-run.

## 16 · Ethics & Societal
**Expert:** responsible-tech reviewer.
**Probes:** Who is harmed if this works exactly as designed (surveillance-adjacent uses,
exclusion, dual-use)? Does automation here shift risk onto people with no recourse (visa
applicants acting on wrong data, SMEs bidding on misqualified tenders)? Is there a disclosure
duty when AI generated the artifact? Would the operator defend the design choices in public?
**Call:** APPLIES when output influences high-stakes decisions for third parties. PARTIAL for
internal analytics. N/A is legitimate for most pure infrastructure — with the one-line reason.

---

## Deep-Mode Subagent Seeding

In deep mode, spawn one subagent per ✓ APPLIES domain. Identity = the **Expert** line; task =
answer the **Probes** against the project snapshot; ≤250 words; output format = the Finding
Block in `report-templates.md § UU Scan`; epistemic tags mandatory (VERIFIED / INFERRED /
ASSUMED). Subagents receive the exclusion list (council findings) and are instructed to skip
anything on it.

## Register Feed

Any finding that generalises beyond this project is a candidate UU-REGISTER entry — rephrase
it for the next project before appending (e.g. not "AcmeAlerts needs a ToS check" but
"[date · project] For any product built on scraped sources, the ToS check is a launch gate,
not a post-launch cleanup").
