# GitHub Actions Version Research

Research into the current and latest major versions of all GitHub Actions used in the `warscape_community_editor` CI and release workflows.

## Summary

| Action | Current in Workflows | Latest Available | Recommended Tag | Primary Source |
|---|---|---|---|---|
| `actions/checkout` | `@v4` | `v7` (`v7.0.1`) | `@v7` | [actions/checkout Releases](https://github.com/actions/checkout/releases) |
| `actions/cache` | `@v4` | `v6` | `@v6` | [actions/cache Releases](https://github.com/actions/cache/releases) |
| `dtolnay/rust-toolchain` | `@stable` | `@stable` | `@stable` | [dtolnay/rust-toolchain](https://github.com/dtolnay/rust-toolchain) |
| `Swatinem/rust-cache` | `@v2` | `v2.9.3` | `@v2` | [Swatinem/rust-cache Releases](https://github.com/Swatinem/rust-cache/releases) |
| `softprops/action-gh-release` | `@v2` | `v3` (`v3.0.0`) | `@v3` | [softprops/action-gh-release Releases](https://github.com/softprops/action-gh-release/releases) |

---

## Detailed Findings

### 1. `actions/checkout`
* **Primary Source:** [https://github.com/actions/checkout/releases](https://github.com/actions/checkout/releases) and [CHANGELOG.md](https://github.com/actions/checkout/blob/main/CHANGELOG.md)
* **Current in repo:** `@v4`
* **Latest:** `@v7` (`v7.0.1`)
* **Evolution & Breaking Changes:**
  * **v5:** Switched action runtime from Node.js 20 to Node.js 24 (minimum runner version `2.327.1`).
  * **v6:** Switched to ECMAScript modules (ESM); credentials stored in temporary files under `$RUNNER_TEMP` rather than `.git/config`.
  * **v7:** Default security protection against "pwn request" attacks: refuses to check out fork pull requests under privileged triggers (`pull_request_target`, `workflow_run`) unless explicitly enabled with `allow-unsafe-pr-checkout: true`. Safe for standard `push`, `pull_request`, `schedule`, and `workflow_dispatch`.

### 2. `actions/cache`
* **Primary Source:** [https://github.com/actions/cache/releases](https://github.com/actions/cache/releases)
* **Current in repo:** `@v4`
* **Latest:** `@v6`
* **Evolution & Breaking Changes:**
  * **v5:** Upgraded runtime to Node.js 24 (minimum runner `2.327.1`).
  * **v6:** Migrated internal packages to ESM and updated core dependencies.

### 3. `dtolnay/rust-toolchain`
* **Primary Source:** [https://github.com/dtolnay/rust-toolchain](https://github.com/dtolnay/rust-toolchain)
* **Current in repo:** `@stable`
* **Latest:** `@stable`
* **Notes:**
  * Unlike standard GitHub Actions, `dtolnay/rust-toolchain` does not use semantic version tags (`@v1`, `@v2`). The `@<ref>` segment is parsed directly by the action to determine which Rust toolchain channel or version to install (`@stable`, `@nightly`, `@beta`, or `@1.x.y`).
  * `@stable` continues to be the recommended, up-to-date reference for stable Rust toolchains.

### 4. `Swatinem/rust-cache`
* **Primary Source:** [https://github.com/Swatinem/rust-cache/releases](https://github.com/Swatinem/rust-cache/releases)
* **Current in repo:** `@v2`
* **Latest:** `@v2` (specifically patch release `v2.9.3`)
* **Notes:**
  * Major version 2 remains the active track. Pointing to `@v2` automatically resolves to the latest patch (`v2.9.3`) and requires no major migration.

### 5. `softprops/action-gh-release`
* **Primary Source:** [https://github.com/softprops/action-gh-release/releases](https://github.com/softprops/action-gh-release/releases)
* **Current in repo:** `@v2`
* **Latest:** `@v3` (`v3.0.0`)
* **Evolution & Breaking Changes:**
  * **v3:** Upgraded runtime from Node.js 20 to Node.js 24.
  * Inputs and output parameter schemas remain backward-compatible with `v2`.
  * `v2` (final release `v2.6.2`) is no longer maintained.
