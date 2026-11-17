# Fork history

Tracks how this fork (`rahulsaipandit/delta`) stays in sync with upstream (`chuunibian/delta`, remote `upstream`).

Add a new entry at the top of **Sync log** every time upstream is merged. Record the upstream commit range, what changed, and any local handling.

## Sync log

### 2026-11-17 — merged upstream `main` @ `70d75ac`

- Range: `c05984a..70d75ac` (1 PR), merged into `perf-fixes` as `3ee3e35`. Clean merge, no conflicts; fast-forwarded to `main`.
- **PR #65 `fix/linux-webkit-smooth-scroll`** (MrScripty, merged 2026-10-25)
  - `src-tauri/src/lib.rs`: Linux-only (`cfg(target_os = "linux")`) block that disables WebKitGTK smooth scrolling on the main webview, fixing laggy touchpad scrolling in the directory tree.
  - `src-tauri/Cargo.toml`: Linux-only dependency `webkit2gtk = "2"`.
  - `Cargo.lock`: one line adding `webkit2gtk` to `delta`'s dependencies. The package (2.0.1) was already locked as a Tauri transitive dependency.
- Security check: the only logic is one WebView setting, with no IPC, file or network access. No new package enters the lockfile, and Windows builds are unaffected. Not compiled on Linux here, so confirm in CI.
- Local handling: none. The uncommitted `package-lock.json` 0.1.0 → 0.1.8 bump is still uncommitted.

### 2026-10-19 — merged upstream `main` @ `c05984a`

- Range: `45306ae..c05984a` (1 PR), merged into `perf-fixes` as `cd7d41a`. Clean merge, no conflicts.
- **PR #63 `startup-themeing-tweak`** (Austin Bian, 2026-09-12)
  - `index.html`: inline style and script set the `dark`/`light` class on `<html>` before the JS bundle loads, which removes the white flash on launch. Reads `vite-ui-theme` from localStorage, defaulting to dark. Must stay in sync with `src/components/theme-provider.tsx` and `src/App.tsx`.
  - `src-tauri/tauri.conf.json`: window `backgroundColor` set to `#0c0a09`.
  - `src/components/progress.tsx`: whitespace cleanup, plus an empty `getTotalCount` stub (no behaviour yet).
  - `Cargo.lock`: `delta` 0.1.0 → 0.1.8 (lockfile sync only).
- Local handling: our uncommitted `Cargo.lock` edit was the same one-line bump as upstream, so it was discarded in favour of upstream's. The `package-lock.json` 0.1.0 → 0.1.8 bump is still uncommitted, because upstream did not touch that file.

### Baseline — upstream `main` @ `45306ae` (PR #59)

Last upstream state in the fork before the entry above. Recent upstream PRs up to that point:

| Date | PR | Summary |
| --- | --- | --- |
| 2026-06-14 | #59 `add-nix-devshell` (VictorVow) | Nix devShell for building from source |
| 2026-05-31 | #58 `bump-version` | Version bump |
| 2026-05-31 | #57 `show-snapshot-folder` | Show snapshot folder |
| 2026-05-28 | #56 `show-snapshot-folder` | Show snapshot folder |
| 2026-05-14 | #55 `path-hashing-bugfixes` | Path hashing bug fixes |
| 2026-05-03 | #54 `add-sort` | Sorting |

## Fork-only commits (not in upstream)

- `68c7f5d` Harden snapshot storage and add portable, comparable snapshots
- `b6dda7d` Add a portable section in Readme
