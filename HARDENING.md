<!-- markdownlint-disable -->

# Hardening Report: cschleiden--replace-tokens/v1.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **cschleiden--replace-tokens/v1.3** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### missing-permissions (severity: medium)

The workflow file .github/workflows/test.yml has no top-level `permissions:` key and the single job (`test`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (write access to contents, etc.). A minimal permissions block should be added.

Locations:

- `.github/workflows/test.yml:1`

### unpinned-uses (severity: high)

Two `uses:` references in .github/workflows/test.yml are pinned to mutable version tags rather than immutable 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the upstream action tag is moved or compromised.

Failing references:
- `uses: actions/checkout@v4` (line 13)
- `uses: actions/setup-node@v4` (line 14)

These should be replaced with their full SHA digests, e.g.:
- `uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`
- `uses: actions/setup-node@39370e3970a6d050c480ffad4ff0ed4d3fdee5af # v4`

Locations:

- `.github/workflows/test.yml:13`
- `.github/workflows/test.yml:14`

## Iteration Notes

### Iteration 1

**Fixes applied:** missing-permissions, unpinned-uses

**Notes:**

Added `permissions: {}` at the workflow top level to prevent overly broad default token permissions. Pinned `actions/checkout@v4` to SHA `11d5960a326750d5838078e36cf38b85af677262` and `actions/setup-node@v4` to SHA `49933ea5288caeca8642d1e84afbd3f7d6820020`, both with `# v4` comments for readability.

