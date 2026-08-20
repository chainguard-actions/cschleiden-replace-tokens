<!-- markdownlint-disable -->

# Hardening Report: cschleiden--replace-tokens/v1.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **cschleiden--replace-tokens/v1.4** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow references actions using mutable version tags instead of full 40-character commit SHA digests. `actions/checkout@v6` and `actions/setup-node@v6` are both pinned to floating version tags. If these tags are moved (e.g., by a supply-chain compromise), the workflow will silently execute different code. Each should be pinned to a full SHA, e.g. `actions/checkout@<40-char-sha> # v6`.

Locations:

- `.github/workflows/test.yml:13`
- `.github/workflows/test.yml:14`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the `test` job also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (e.g., `write` access to contents). A minimal `permissions:` block (e.g., `contents: read`) should be added at the top level or on the job.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed hardened/action/.github/workflows/test.yml: (1) Pinned actions/checkout@v6 to full SHA d23441a48e516b6c34aea4fa41551a30e30af803 and actions/setup-node@v6 to full SHA 249970729cb0ef3589644e2896645e5dc5ba9c38, preserving the original tag in comments. (2) Added a top-level `permissions: contents: read` block to restrict the GITHUB_TOKEN to the minimum required permissions.

