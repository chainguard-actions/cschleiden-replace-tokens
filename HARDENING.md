<!-- markdownlint-disable -->

# Hardening Report: cschleiden--replace-tokens/v1.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **cschleiden--replace-tokens/v1.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow references actions/checkout@v1, which uses a mutable tag ('v1') instead of a pinned 40-character commit SHA. This means the action could be silently updated or compromised without the workflow noticing, enabling supply-chain attacks. It should be pinned to a full SHA, e.g. actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v1

Locations:

- `.github/workflows/test.yml:13`

### missing-permissions (severity: medium)

The workflow file .github/workflows/test.yml has no top-level 'permissions:' key, and the only job ('test') also has no job-level 'permissions:' key. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions. A minimal permissions block (e.g. 'contents: read') should be added at the top level or on the job.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed hardened/action/.github/workflows/test.yml: (1) Pinned actions/checkout@v1 to its full commit SHA (50fbc622fc4ef5163becd7fab6573eac35f8462e) with a # v1 comment for readability. (2) Added a top-level 'permissions: contents: read' block to restrict the GITHUB_TOKEN to the minimum permissions needed for checkout and npm build/test.

