<!-- markdownlint-disable -->

# Hardening Report: cschleiden--replace-tokens/v1.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **cschleiden--replace-tokens/v1.2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses actions/checkout@v1, which is a mutable tag reference rather than a pinned 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) version without any change to the workflow file. Pin to a full SHA, e.g. actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v1.

Locations:

- `.github/workflows/test.yml:14`

### missing-permissions (severity: medium)

The workflow file has no top-level permissions: key and the single job (test) also has no job-level permissions: key. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions. Add a top-level permissions: block with the minimal scopes required (e.g. contents: read).

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned actions/checkout@v1 to actions/checkout@50fbc622fc4ef5163becd7fab6573eac35f8462e # v1 using the resolved commit SHA. 2. Added a top-level `permissions: contents: read` block to restrict the GITHUB_TOKEN to the minimum required scope for this workflow (checkout + npm build/test).

