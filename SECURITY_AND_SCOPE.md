# Security And Scope

## Included

This repository includes general-purpose Windows bioinformatics and computational biology workflow skills for:

- scientific evidence planning;
- manuscript writing and reviewer-risk audit;
- publication plot styling;
- multi-panel figure assembly;
- publication content packaging;
- Windows command execution;
- PDF handling.

## Excluded

This repository intentionally excludes:

- private project paths;
- unpublished algorithm-specific instructions;
- confidential datasets;
- manuscript-specific conclusions;
- project-specific figure layouts;
- access tokens, credentials, API keys, or private repository links.

## User Responsibilities

Users remain responsible for:

- confirming target-journal author guidelines and submission requirements;
- verifying statistical methods, assumptions, and tests;
- confirming data-sharing, privacy, consent, and ethics requirements;
- checking software licences and third-party data restrictions;
- reviewing any generated manuscript text, figures, or code before use.

## Recommended Pre-Publication Check

Before publishing a fork or derivative repository, run a keyword scan for accidental private content:

```powershell
rg -n "private|confidential|credential|project-specific-term|local-absolute-path" .
```

Add project-specific terms from your own environment to the search pattern.

## Scientific Claim Boundary

These skills are designed to reduce overclaiming and improve traceability. They do not prove scientific claims. Manuscript-ready conclusions still require appropriate data, controls, statistical support, and domain review.
