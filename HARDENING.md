<!-- markdownlint-disable -->

# Hardening Report: lewagon--wait-on-check-action/v1.9.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `374911c4be584df24e6da57af2d990570ef0f859`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **lewagon--wait-on-check-action/v1.9.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### prior-fix (severity: high)

Carried forward from this version's previous harden, which fixed it; fix it again unless the code no longer has the problem. The previous harden changed action.yml without recording a finding for it, and this analysis reported nothing there. Re-apply its security changes unless the code no longer needs them. The previous patch:
```diff
diff --git a/action.yml b/action.yml
index ee6d673..cdeba55 100644
--- a/action.yml
+++ b/action.yml
@@ -56,19 +56,34 @@ inputs:
     description: "Enable Bundler cache in ruby/setup-ruby"
     required: false
     default: "true"
-
 runs:
   using: "composite"
   steps:
     - name: Set the ruby version
       uses: ruby/setup-ruby@3ff19f5e2baf30647122352b96108b1fbe250c64
       with:
         ruby-version: 3.2
         bundler-cache: ${{ inputs.bundler-cache }}
         working-directory: ${{ github.action_path }}
       env:
         BUNDLE_PATH: "${{ github.action_path }}/vendor/bundle"
-
     - name: Install dependencies without caching
       if: inputs.bundler-cache == 'false'
       run: bundle install
@@ -76,7 +91,6 @@ runs:
       shell: bash
       env:
         BUNDLE_PATH: "${{ github.action_path }}/vendor/bundle"
-
     - run: bundle exec entrypoint.rb
       working-directory: ${{ github.action_path }}
       shell: bash
@@ -95,7 +109,6 @@ runs:
         CHECKS_DISCOVERY_TIMEOUT: ${{ inputs.checks-discovery-timeout }}
         WAIT_FOR_DUPLICATES: ${{ inputs.wait-for-duplicates }}
         BUNDLE_PATH: "${{ github.action_path }}/vendor/bundle"
-
 branding:
   icon: "check-circle"
   color: "green"

```

Locations:

- `action.yml`

## Iteration Notes

### Iteration 1

**Fixes applied:** prior-fix

**Notes:**

The previous harden's diff only deleted blank lines in action.yml. The file is already secure: ruby/setup-ruby is pinned to the full SHA 3ff19f5e2baf30647122352b96108b1fbe250c64, and all inputs are passed through env: rather than written into run: scripts. No edits were needed, so the file was left unchanged.

