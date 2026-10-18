# fin-ai-classifier

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Domain Profile](https://img.shields.io/badge/domain-fin%20%7C%20domain%2F1.0-blue.svg)](domain.manifest.json)
[![Status: RESERVED](https://img.shields.io/badge/status-RESERVED%20%7C%20open%20claim-orange.svg)](domain.manifest.json)
[![Gate: five-level](https://img.shields.io/badge/gate-silent%2Fwarn%2Fconfirm%2Fblock%2Frequire--owner-8a2be2.svg)](gate-map.json)
[![Privacy: default-off](https://img.shields.io/badge/privacy-default--off-brightgreen.svg)](privacy.json)

> **Status: RESERVED (placeholder · open for claim)** — this repository ships the four-piece industry-access skeleton already built to the platform protocol, and waits for an operator with the proper domain qualification to claim it and fill in the real rules.

It turns "which risk class is this financial AI application, and which obligations apply" into verifiable attributes: the AI only surfaces the class and mapped obligations — it does **not** issue a compliance conclusion.

## What this domain covers

Risk classification and obligation mapping for AI applications in financial scenarios (credit, insurance underwriting, investment advice, AML monitoring). The AI lays out the risk class and the corresponding obligations; compliance determination stays with the institution and the regulator.

## Quick start

This repo is a **domain-profile skeleton** (four JSON files), not a runnable application. Validate with standard JSON tooling:

```bash
git clone https://github.com/SynomosAI/fin-ai-classifier.git
cd fin-ai-classifier
python -m json.tool domain.manifest.json > /dev/null
python -m json.tool gate-map.json        > /dev/null
python -m json.tool privacy.json         > /dev/null
python -m json.tool checker.io.json      > /dev/null
```

The checker (MCP tool) IO contract is in `checker.io.json`. A minimal call:

```json
{
  "subject_ref": "mpp:cn:3c6a7b8d",
  "attribute_keys": ["fin.risk_class", "fin.human_oversight"],
  "evidence": ["tsa:2026-09-12#sha256:5e6f..."],
  "request_id": "req-20260912-0004"
}
```

> The checker has exactly one action — *show and verify*. It has **no "judge" option**: client-facing investment advice, product recommendations, buy/sell calls, "already compliant" and "ready to launch" conclusions are all on the `_forbidden_outputs` blacklist.

## Domain identity

| Item | Value |
|---|---|
| Domain ID | `fin` (globally unique; never reused) |
| Domain name | Finance · AI-application risk classification |
| Profile version | `domain/1.0` |
| Status | `RESERVED` |
| Placeholder since | 2026-09-12 |

## Attributes

| Key | Type | Meaning |
|---|---|---|
| `fin.risk_class` | enum | Risk class · minimal/limited/high/unacceptable/undetermined |
| `fin.use_case_type` | enum | Use case setting the risk baseline and stacked obligations · credit_decision/insurance_underwriting/investment_advice/aml_monitoring/customer_service/internal_ops/other |
| `fin.human_oversight` | enum | Human-oversight strength · none/post_hoc/in_the_loop/human_decides |
| `fin.disclosure_obligation` | boolean | Whether AI involvement must be disclosed to the client |

## Red lines (machine-readable)

1. No client-facing investment advice, product recommendation, or buy/sell call.
2. No "already compliant / regulator-approved" concluding wording.
3. High-risk applications require human review; the AI must not alone give a "ready to launch" conclusion.

Each red line has a corresponding blocking rule in `gate-map.json`.

## The four-piece access set

| File | Role |
|---|---|
| `domain.manifest.json` | Domain declaration: attribute list, issuer requirements, validity, red lines |
| `gate-map.json` | Friction per action: silent / warn / confirm / block / require-owner |
| `privacy.json` | Privacy declaration: default-off, minimal, withdrawable, deletable |
| `checker.io.json` | Checker (MCP tool) IO contract — show & verify, never judge |

## References

Interim Measures for the Management of Generative AI Services; PBoC evaluation norms for AI-algorithm financial applications (reference); regulator guidance on AI applications in financial institutions (reference). References only explain the source of attributes; they do not constitute legal advice.

## How to claim

1. Fork this repo and fill in `operator` and `checker_endpoint`.
2. Calibrate attribute values and red-line wording per currently effective rules.
3. Run the platform-side validator self-check (all five criteria must pass).
4. Open a PR with qualification evidence and the rule basis.

## License / 署名

Code and configurations are used under the MIT licence. Document copyright belongs to SynomosAI.

© 2026 SynomosAI. All rights reserved.
