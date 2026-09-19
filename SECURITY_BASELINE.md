# GitHub Master Security Baseline

Last verified: 2026-09-19

## Account repository inventory

The connected account currently exposes 16 repositories, all public.

### Core / governance

- `Gpt-asistan` — core AI engineering repository; hardening PR #3 has a fully green verification matrix and is blocked only by the independent approving-review requirement.
- `.github` — central community/security governance repository.
- `repo-template` — hardened template PR #5 is CI-green and blocked only by the independent approving-review requirement.
- `mehmetcerdik457-ctrl` — profile repository.

### Hardened and merged

- `benim-uygulamam` — security baseline merged.
- `telefon-yedek` — privacy boundary and Privacy Guard merged; assistant memory/notes removed from current main.
- `codespaces-react` — SHA-pinned Node CI, Dependabot, SECURITY and ownership governance merged.

### Hardened PRs awaiting independent review

- `studio`
- `doktor`
- `bot-starter`
- `hata-ayiklayici`
- `termux-mods`
- `apk-starter`
- `serverless-starter`

Each listed PR passed its current CI before the merge attempt. GitHub rejected the merge because an approving review from a reviewer with write access is required.

### Upstream forks intentionally left clean

- `Magisk` — fork of `topjohnwu/Magisk`.
- `Shizuku` — fork of `RikkaApps/Shizuku`.

These are kept close to upstream instead of injecting account-specific governance files into their source trees.

## Verified secret scan

Public default-branch searches found no matches for:

- `ghp_`
- `github_pat_`
- AWS `AKIA...`
- Google `AIza...`
- private-key PEM headers

`OPENAI_API_KEY` appeared only as an empty placeholder in an example environment file.

## Remaining account-level gates

These require account/repository administration or explicit user security actions and are not bypassed:

1. independent write-access reviews for protected repositories;
2. GitHub Rulesets / classic branch-protection administration;
3. repository-level auto-merge configuration;
4. private-repository creation / visibility decisions;
5. passkeys, 2FA, recovery codes, sessions, SSH/PAT review;
6. narrowing ChatGPT connector permissions that are currently set to Allow all actions;
7. optional Copilot approving-review configuration.

## Baseline principles

- no secrets or production signing material in source control;
- immutable SHA pinning for GitHub Actions;
- least-privilege workflow permissions;
- `persist-credentials: false` on checkout;
- Dependabot for relevant package ecosystems and GitHub Actions;
- PR-based changes to protected branches;
- CODEOWNERS where repository-local ownership is required;
- public repositories must reject private phone/application state.
