# Features

One line per feature, with its version, status and the versioned ids of the functions that implement it. Ids come from `CODE_INDEX.md`. Update this file whenever a feature is added or changed, and add a line to the changelog.

Status is one of: planned, in progress, done.

## Claims

- **View a claim** (v1\_0): Show one claim's details. Status: done. Code: `claims.get_claim_v1_0`, `client.fetchClaim_v1_0`
- **Pay a claim** (v1\_1): Pay a claim for a given amount. Status: done. Code: `claims.pay_claim_v1_1`, `claim_service.ClaimService.apply_payment_v1_0`
- **Export claim to PDF** (v0\_1): Download a claim as a PDF. Status: planned. Code: none yet

## Changelog

Newest first. One line per change: date, feature, version, what changed.

- 2026-11-17, Pay a claim, v1\_1: Added an amount check before payment.
