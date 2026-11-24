# AGENTS.md — nepolaris

## Project intent

nepolaris is a single-user, self-hosted personal financial observatory. It must use **real double-entry bookkeeping** as its accounting core and put management-oriented analysis on top.

Authoritative context:
- [README.md](README.md)
- [docs/background.md](docs/background.md)
- [docs/design-policy.md](docs/design-policy.md)
- [docs/roadmap.md](docs/roadmap.md)

## Non-negotiable rules

1. Never allow a posted journal entry whose debit and credit totals differ.
2. All balance changes must be explainable from journal postings. Valuation snapshots are source observations, never direct ledger overwrites.
3. Keep imported source files/rows and generated journal entries separately, with traceability.
4. CSV import, transfer matching, and valuation adjustment must be idempotent.
5. Do not silently convert unreconciled cash flows into income, expense, or investment gains.
6. Corrections and reversals must be auditable. Closed periods are not silently editable.
7. Investment period returns inferred from month-end balances are **not** necessarily realized gains, unrealized gains, or taxable income.
8. Do not use binary floating point for monetary accounting.
9. Do not add bank APIs, scraping, detailed trading-history requirements, or multi-user architecture without a deliberate scope decision.
10. No real account numbers, real statements, secrets, credentials, or financial datasets in commits, Issues, PRs, examples, or CI logs.

## Implementation approach

- Start from a small domain model, invariants, tests, and documented design tradeoffs.
- Prefer the simplest viable Docker-based web architecture.
- Use synthetic/anonymized test fixtures. Cover double-entry balance, opening balances, import duplicates, transfer matching, valuation correction, reconciliation, and period closing.
- Preserve data portability and include backup/restore design.
- For a change affecting accounting behavior, explain the journal entries, impact on B/S and period results, and how to verify them.
- Do not assume a framework choice is final unless it appears in an accepted design decision.

## Working conventions

- Read the relevant Issue and project documents before implementation.
- Keep changes focused; document important choices in `docs/adr/` if they materially affect accounting semantics.
- Add or update tests with code changes.
- Use Japanese for user-facing product documentation by default; use clear English identifiers in code.
- GPL-3.0-or-later is the repository license. Preserve the license and copyright notices when distributing code.

## Initial instruction to Codex

Do not begin broad implementation merely from reading this file. First review the design principles, point out unresolved accounting edge cases, propose minimal schema and vertical slices, and implement according to the corresponding Issue.
