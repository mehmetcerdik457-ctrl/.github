# GitHub Master Security Baseline

Last verified: 2026-09-19

## Account repository inventory

The connected account currently exposes 16 repositories, all public.

## Central governance and automation

The central `.github` repository is active on `main` and contains:

- account-wide SECURITY / contribution / support / conduct guidance;
- CODEOWNERS and pull-request governance;
- reusable SHA-pinned Python CI;
- reusable SHA-pinned Node CI;
- reusable public-repository Privacy Guard.

Central reusable automation merge:

`fea0cdba87dd09c88648eb29302e65c32ba7fd44`

### Live reusable-workflow verification

The central workflows were not merely stored; they were consumed by real repositories and passed:

- profile repository → reusable Python baseline → **SUCCESS**
- `codespaces-react` → reusable Node baseline with locked install, Vitest and Vite build → **SUCCESS**
- `telefon-yedek` → reusable Privacy Guard + stricter phone-state guard → **SUCCESS**

## Core / governance repositories

- `Gpt-asistan` — PR #3 exact head `4be5f4f399a278100dea9b12a1f5dbc8e04c0f88`; full workflow matrix green; merge blocked only by required independent write-access approval.
- `repo-template` — PR #5 CI-green; hardened template and governance-label automation; merge blocked only by required independent write-access approval.
- `.github` — central governance and reusable automation merged and verified.
- `mehmetcerdik457-ctrl` — profile repository now consumes the central reusable Python baseline.

## Hardened and merged repositories

- `benim-uygulamam` — security baseline merged; duplicated CI later replaced by central reusable Python CI.
- `telefon-yedek` — privacy boundary merged; assistant memory/notes removed from current `main`; central reusable Privacy Guard and stricter phone-state guard both verified.
- `codespaces-react` — security baseline merged; Node CI centralized into the reusable Node baseline and verified.
- profile repository — central reusable Python CI merged and verified.

## Hardened PRs awaiting independent review

The following PRs now use the central reusable Python baseline. Each current exact head passed CI, and each exact-head merge attempt was rejected only by the required independent write-access approval:

- `studio` — PR #5 — `03c835c0f08ecb5345c0c7de779695c74ada84f0`
- `doktor` — PR #4 — `899efbfae8551f12d3868c064f3cba9533c3ceaa`
- `bot-starter` — PR #4 — `c18e38f42d865f65b1b5da0704c0054c3191556a`
- `hata-ayiklayici` — PR #4 — `407498833819410c2bcb2240a042115a678d43cc`
- `termux-mods` — PR #4 — `b2cdb15982cfdfe58c6d76034814aa7050968c5c`
- `apk-starter` — PR #4 — `9db66c6606a24f1f297ad4c165138797ae3f1340`
- `serverless-starter` — PR #4 — `982a09360343a7599a2b8fbd136cb98e6a49b23d`

## Upstream forks intentionally left clean

- `Magisk` — fork of `topjohnwu/Magisk`.
- `Shizuku` — fork of `RikkaApps/Shizuku`.

Account-specific governance files were intentionally not injected into these upstream forks, preserving cleaner synchronization with their sources.

## Verified public secret scan

Public default-branch searches found no matches for:

- `ghp_`
- `github_pat_`
- AWS `AKIA...`
- Google `AIza...`
- private-key PEM headers

`OPENAI_API_KEY` appeared only as an empty placeholder in an example environment file.

## telefon-yedek privacy state

The public repository previously tracked test assistant memory/notes. Inspection found demo/test content rather than credentials or sensitive account data. Those files were removed from current `main`.

Current guardrails reject:

- assistant memory and note state;
- JSONL private state;
- environment files;
- databases / SQLite state;
- keystores and private-key containers;
- obvious credential markers.

Historical Git commits can still contain deleted historical files; current-main deletion does not rewrite Git history.

## Remaining account-level gates

These require account/repository administration or explicit user security actions and are not bypassed:

1. independent write-access reviews for protected repositories;
2. GitHub Rulesets / classic branch-protection administration;
3. repository-level auto-merge configuration;
4. private-repository creation / visibility decisions;
5. passkeys, 2FA, recovery codes, active sessions, SSH keys and PAT review;
6. narrowing ChatGPT connector permissions that are currently set to **Allow all actions** on several critical apps;
7. optional Copilot approving-review configuration;
8. deleting merged feature branches where repository settings do not auto-delete them.

## Baseline principles

- no secrets or production signing material in source control;
- immutable SHA pinning for GitHub Actions;
- least-privilege workflow permissions;
- `persist-credentials: false` on checkout;
- centralized reusable CI where coupling is appropriate;
- Dependabot for relevant package ecosystems and GitHub Actions;
- PR-based changes to protected branches;
- CODEOWNERS where repository-local ownership is required;
- public repositories must reject private phone/application state;
- upstream forks should remain close to upstream unless there is a deliberate maintained divergence.
