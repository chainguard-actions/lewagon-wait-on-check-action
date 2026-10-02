<!-- markdownlint-disable -->

# Hardening Report: lewagon--wait-on-check-action/v1.9.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **lewagon--wait-on-check-action/v1.9.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite action at .github/actions/install/action.yaml references two actions by mutable version tags instead of full 40-character commit SHAs. This exposes the action to supply-chain attacks where a tag could be silently moved to point to malicious code.

Failing references:
- `uses: actions/checkout@v4` (line 8) — should be pinned to a full SHA
- `uses: ruby/setup-ruby@v1` (line 11) — should be pinned to a full SHA

Example fix: `uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`

Locations:

- `.github/actions/install/action.yaml:8`
- `.github/actions/install/action.yaml:11`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned both mutable tag references in hardened/action/.github/actions/install/action.yaml to full commit SHAs:
- actions/checkout@v4 → actions/checkout@11d5960a326750d5838078e36cf38b85af677262 # v4
- ruby/setup-ruby@v1 → ruby/setup-ruby@14594264cd68ce8a2345dd349bc3d138a4ef85c8 # v1
The human-readable version tags are preserved as inline comments for readability.

