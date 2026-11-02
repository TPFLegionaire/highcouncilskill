# High Council — a Claude skill

A [Claude skill](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview) for structured, adversarial decision-making and blind-spot scanning.

- **DELIBERATE** — runs a decision through a panel of distinct reasoning lenses (Contrarian, First-Principles, Expansionist, Outsider, Executor, Bias Auditor, Tail-Risk, Systems, Realpolitik): blind first round, anonymised cross-examination, anti-conformity enforcement, confidence-weighted stance tally, chairman verdict with pre-mortem and kill criteria.
- **SCAN** — sweeps a project across 16 expertise domains to surface the "unknown unknowns" nobody consulted.
- **TRIBUNAL** — both, with the scan forbidden from repeating the council's findings.
- Plus **QUICK** (2-round) and **DUO** (polarity debate) modes.

Every run writes durable artifacts: an HTML report and a markdown transcript (and a reusable `UU-REGISTER.md` for scans).

## Install

**Claude Code**
```bash
git clone https://github.com/TPFLegionaire/highcouncilskill.git
cp -r highcouncilskill/high-council ~/.claude/skills/
```

**claude.ai** — zip the `high-council/` folder and upload it under Settings → Capabilities → Skills.

## Use

```
council this: should I launch now at £99/mo or wait for self-serve?
quick council: Postgres or DynamoDB for this workload?
what am I missing on this project?
full tribunal: <decision>
```

Works best in Claude Code (members run as parallel subagents for true independence). In plain chat it runs in a marked `[SINGLE-CONTEXT MODE]`.

## Credits

Builds on Andrej Karpathy's LLM Council idea and adapts protocol mechanisms from [0xNyk/council-of-high-intelligence](https://github.com/0xNyk/council-of-high-intelligence).

## License

MIT — see [LICENSE](LICENSE).
