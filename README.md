# cloud-itonami-lei-549300o7prtlvbf2ze53

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by Cushman & Wakefield, Inc..**

This repository archives the publicly published Terms of Use / Terms and Conditions of
**Cushman & Wakefield, Inc.**, with source-url and retrieval-date provenance, per
[ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.md)
(`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`). It is a read-only
reference/archive repository — it does not act, propose, or execute anything on the
company's behalf, and is not a governed Advisor/Governor actor.

## Company identity

- **Legal name**: Cushman & Wakefield, Inc.
- **LEI (ISO 17442)**: [549300O7PRTLVBF2ZE53](https://search.gleif.org/#/record/549300O7PRTLVBF2ZE53) (GLEIF-verified)
- **Jurisdiction**: US-NY — the live GLEIF record (last updated 2025-10-20) places the
  entity in New York, registered with the NY Department of State's Corporation and
  Business Entity Database (`RA000628`, registration `270620`, ISO 20275 legal form
  `PJ10` Business Corporation, created 1969-01-03, previous legal name
  `RCA Products, Inc.`). This README and `blueprint.edn` previously said US-DE;
  `facts.edn` below carries the registry's answer with provenance, and the checker
  flags US-DE as drift today.
- **Website**: https://www.cushmanwakefield.com
- **Ticker**: CWK (NYSE) — a listing of the group, not a security of this legal
  entity: GLEIF maps **0 ISINs** to this LEI (a measured zero, see `facts.edn`).
  The NYSE issuer is the group's UK parent, Cushman & Wakefield plc; a GLEIF
  fulltext search for that name on 2026-08-23 surfaced no record, so its LEI is
  not asserted here.

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of archived Terms of Use documents,
  each entry carrying `:tos/full-text`, `:tos/source-url`, `:tos/retrieved-at`,
  `:tos/sha256`, `:tos/doc-type`, and a `:tos/supersedes` chain for future revisions.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record.
- `facts.edn` — 9 verified registry facts with per-fact provenance (the entity, its
  registration, issuer and issuer accreditation, registration authority, legal form,
  securities count, children count and both parent-reporting exceptions).
  **Generated** — see below.
- `scripts/verify-facts.cljs` — re-fetches every source `facts.edn` cites and fails if
  the live record disagrees. Vendored from `com-junkawasaki/root`
  (`scripts/lei-verify-facts.cljs`); fix issues in the canonical and re-vendor.

## Verifying the record

The LEI claims above used to be assertions with nothing in the repository behind
them — and one of them (US-DE) was wrong. `facts.edn` now carries them as data, and
every value in it was read out of a public registry response whose URL and
retrieval time sit next to the value:

```
nbb scripts/verify-facts.cljs           # check the recorded facts against the live sources
nbb scripts/verify-facts.cljs --write   # re-fetch and rewrite facts.edn
```

Eleven GLEIF/ISO requests back the file (`CHECKED 11` when it was written,
2026-08-23T07:29Z, golden copy 2026-08-22T16:00Z) — the LEI record (legal name
`CUSHMAN & WAKEFIELD, INC.`, jurisdiction `US-NY`, entity **ACTIVE**, registration
**ISSUED** with the next renewal due 2026-10-27, last updated 2025-10-20,
`FULLY_CORROBORATED`, conformity flag `CONFORMING`, no BIC, S&P Global id
`877111`, OpenCorporates `us_ny/270620`; entity status and registration status
are different fields and are recorded separately), its **0 ISINs**, read from
`meta.pagination.total` of the cited page (the page was fetched and reported an
empty collection, so there is no `:security` entity to mirror and the count is
not an unasked question), its managing LOU and LEI-issuer accreditation
(Bloomberg Finance L.P., LEI `5493001KJTIIGC8Y1R12`, accredited 2017-04-13),
registration authority `RA000628` (Corporation and Business Entity Database,
Division of Corporations, State Records and UCC, NY Department of State), ISO
20275 legal form `PJ10` (Business Corporation, `US-NY`), reporting exceptions at
both consolidation levels (`NON_CONSOLIDATING` — GLEIF's relationship data records
no accounting-consolidation parent for this entity and gives that reason; this
file records the registry's answer, not a group chart), and **0 direct children**,
read from `meta.pagination.total` of the cited page — a measured zero. The
`direct-parent` and `ultimate-parent` endpoints answered `404` because GLEIF
publishes the exception side of that pair for this entity, which the checker
treats as a fact rather than a failure.

The checker's exit codes are three, not two: `0` every recorded fact matches the
live sources, `1` a citation broke or a fact drifted, `3` the check could not be
performed at all — an absent `facts.edn`, or every request failing at the
transport level. A check that could not run must not be indistinguishable from a
check that ran and found nothing, so it refuses to report a pass rather than
exiting 0. All outcomes were exercised before this landed: unmodified `0`
(`OK all 9 recorded fact(s) still match`); `:securities/isin-count` edited
`0` → `1` → `1` naming `DRIFT gleif-isins :securities/isin-count`;
`:company/jurisdiction` rewritten back to `US-DE` → `1` naming
`DRIFT gleif-lei-record :company/jurisdiction`; the
`gleif-direct-parent-reporting-exception` entity deleted → `1` naming
`ADDED gleif-direct-parent-reporting-exception`; the measured
`:relationship/direct-child-count` rewritten `0` → `1` → `1` naming
`DRIFT gleif-direct-children-count`; the ultimate-level
`:relationship/exception-reason` rewritten → `1` naming
`DRIFT gleif-ultimate-parent-reporting-exception :relationship/exception-reason`;
`:company/registered-as` rewritten `270620` → `270621` → `1` naming the drift in
both `gleif-lei-record` and `gleif-registration-authority`; the GLEIF host in
the checker rewritten to an unresolvable name → `3` (`INCONCLUSIVE … refusing to
report a pass`); and with no `facts.edn` at all → `3`.

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`) for why this repo exists,
why it is keyed by LEI rather than GTIN or ticker, and why full-text archival (with
provenance) was chosen over excerpt-only storage.
