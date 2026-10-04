# ThreeLineage

**[Open the interactive Missing Receipt demo](https://sigilith.github.io/threelineage-showcase/)** — a browser simulation of the scenarios below; no live core execution.

### The action happened. The receipt didn't. What happens next?

**Execution governance and failure-handling evidence, developed by Ky Nash.**

AI systems can describe a policy. The engineering question is what actually happens when a tool is about to act, recording fails, or a worker disappears midway through an operation.

ThreeLineage explores that boundary through execution controls, intent/outcome records and deliberate failure testing. This is a public showcase of observed behaviour and available engineering services. It does not distribute the core implementation.

[Discuss a paid pilot](mailto:threelineage@outlook.com) · [Developer profile](https://github.com/Sigilith)

---

## Featured demonstration: The Missing Receipt

A controlled local worker writes one delivery, then terminates before recording completion. A fresh process attempts another governed execution using the same ledger.

**Observed result: the next reservation is denied, and the delivery count stays at one.**

| Experiment | Observed result |
| --- | --- |
| Approved operation | One delivery and a completion record |
| Policy veto | No delivery |
| Reservation persistence failure | Callback does not start |
| Process dies after delivery, before completion recording | One delivery; execution remains unresolved |
| Fresh process attempts execution against that ledger | Denied; still one delivery |
| Deliberately naive retry of the non-idempotent operation | Two deliveries |

The comparison is intentionally naive. It is not a benchmark of other products.

## Evidence, with a defined scope

On **3 October 2026**, the demonstration passed four automated tests and a separate scenario run on **Python 3.10 and 3.12, Ubuntu**, in GitHub Actions. The earlier demonstration also passed locally and on Termux as reported by the developer.

Tested source revision: **870f181607987a885ea9eed458f86664b98121c3**.

The tests cover crash/restart behaviour, rejection of tampered records, preservation of existing output, and the limitation around recorded completion failures. These are developer-run checks, not independent certification or a formal proof. Source and detailed execution records are not distributed in this showcase. A supervised walkthrough and an agreed evaluation can be requested by email.

### What the demonstration establishes

For the tested execution gate, an unresolved started operation prevents subsequent reservations against the same intact ledger. In this specific crash window, restarting does not automatically repeat the effect.

### What it does not establish

- Exactly-once delivery, universal crash safety or protection against every storage failure.
- Containment of code that bypasses the gate or chooses another ledger.
- Independent authentication of the complete ledger history.
- A permanent freeze after every completion error: a successfully recorded terminal failure can allow later work.
- Atomic commitment of an external effect and its receipt. Reconciliation still needs a deliberate design.

The demonstrated unresolved operation also blocks other reservations on that ledger. That availability cost is part of the result, not hidden from it.

## Framework roles

| Component | Focus |
| --- | --- |
| ThreeLineage-Core | Governed execution boundaries and durable intent/outcome recording |
| TraceGuard | Runtime verification and audit integration, including signed telemetry in the supplied daemon implementation |

The Missing Receipt experiment uses a supplied ThreeLineage-Core snapshot. It does not demonstrate a TraceGuard daemon or an end-to-end integration of every framework component.

## Work with ThreeLineage

**Start with one operation whose behaviour can be measured.** A paid pilot can focus on a tool call, API request or file-writing workflow.

1. Map the execution boundary, bypass paths and failure assumptions.
2. Agree the policy and measurable acceptance criteria.
3. Implement a bounded adapter or proof of integration.
4. Exercise approved, denied, interrupted and recording-failure scenarios.
5. Deliver the agreed implementation, test evidence and limitations report.

Adaptation, recovery design, technical documentation and continuing support can be scoped separately. Price, deliverables, access, ownership and any software licence are agreed before work starts. No certification or regulatory compliance is implied.

**Contact: [threelineage@outlook.com](mailto:threelineage@outlook.com)**

Include the workflow you want to control, the consequence of a duplicate or unauthorised action, your deadline and budget range. Please do not send credentials or sensitive customer data in the initial enquiry.

## Visibility and ownership

This repository contains presentation material only. It grants no licence to the core software and offers no core source download. Public descriptions can be read and discussed; the underlying implementation is not included here. The public browser simulator is included; the private core implementation is not.

Framework authorship: **Ky Nash / ThreeLineage**. No endorsement by Google, AISI or another organisation is claimed.
