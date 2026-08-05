# Case Study: Compliance & Credential Management for Behavioral Health Clinics

**Role:** Sole architect & builder
**Domain:** Healthcare compliance (HIPAA + 42 CFR Part 2)
**Status:** Private beta — source not public (active product)

## The Problem

MAT/MOUD (Medication-Assisted Treatment) clinics manage clinician
credentials, license expirations, and patient records under two
overlapping — and sometimes conflicting — federal regulations:
HIPAA and 42 CFR Part 2, which governs substance use disorder
records specifically. Most small clinics track this in spreadsheets,
creating real compliance and patient-safety risk: an expired license
or lapsed certification can go unnoticed for weeks.

Having worked inside behavioral health as a credentialed clinician
(CRS, CFRS, ASAM) using EPIC systems daily, I saw this gap firsthand —
not as a hypothetical, but as a lived operational problem.

## What I Built

A multi-tenant compliance and credential management platform that
automates the full lifecycle: credential intake → document storage →
expiration tracking → automated alerts → auditable compliance status.

## Why It's Architected the Way It Is (Security & Compliance Decisions)

| Requirement | Design Decision | Why It Matters |
|---|---|---|
| **HIPAA — Access Control** | Role-based access control enforced at every API layer, with tiered PHI visibility (support staff see masked data; clinical/admin roles see full records within their tenant only) | Prevents the most common breach cause: over-broad internal access |
| **HIPAA — Audit Controls** | Every access and change to protected data is written to an immutable, insert-only audit log with 6-year retention | Produces a defensible audit trail if a regulator or auditor asks "who accessed this record and when" |
| **HIPAA — Authentication** | Multi-factor authentication required for all accounts; SMS-based MFA is explicitly disallowed | SMS MFA is a known weak point (SIM-swap risk); this reflects current NIST guidance, not just a checkbox |
| **HIPAA — Encryption** | Data encrypted at rest and in transit using current industry-standard protocols | Baseline breach-impact reduction if storage or network layer is ever compromised |
| **Multi-Tenancy / Data Isolation** | Each clinic's data is logically isolated at the database layer, not just the application layer | Prevents a bug in application code from ever exposing one clinic's data to another — isolation is enforced even if the app has a mistake |
| **42 CFR Part 2 Alignment** | Design reviewed specifically against Part 2's stricter consent and re-disclosure rules for substance use disorder records, which HIPAA alone does not fully cover | Most generic healthcare software only builds to HIPAA; behavioral health/SUD clinics need this extra layer, and most vendors miss it |

## What This Demonstrates

- Translating regulatory language (HIPAA, 42 CFR Part 2) into concrete
  technical controls — the core skill of GRC/compliance engineering
- Identifying where two overlapping regulations create conflicting
  requirements and documenting the tradeoff explicitly, rather than
  quietly picking one
- Domain expertise most engineers don't have: I know what this
  workflow looks like from the clinician's side, not just the
  compliance checklist

## Want a Walkthrough?

Source code is private while this moves toward a commercial release.
Happy to give a live demo or a private repo walkthrough — reach out
via [LinkedIn link] or [email].