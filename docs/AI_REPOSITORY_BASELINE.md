# AI Repository Security Baseline

This is the mandatory baseline for new AI, agent, Android, backend, model-routing, and automation repositories owned by this account.

## Repository boundary

- Sensitive AI core, owner-control logic, private prompts, private datasets, internal architecture, signing material, and production configuration are private by default.
- Public repositories contain only intentionally open-source code and documentation.
- Secrets, private keys, keystores, recovery codes, tokens, credentials, and production datasets are never committed.

## Protected main branch

The default branch must be protected with:

- pull requests required before merge;
- at least one independent approving review;
- stale approvals dismissed after material changes;
- required conversations resolved;
- required CI/security checks;
- force pushes blocked;
- branch deletion blocked;
- administrator bypass kept minimal;
- signed commits or equivalent provenance enabled when the repository workflow supports it.

Repository-level auto-merge may be enabled only when it preserves every required review and status check.

## Mandatory repository files

- `.github/CODEOWNERS`
- `.github/dependabot.yml`
- `.github/PULL_REQUEST_TEMPLATE.md`
- structured issue forms
- `SECURITY.md`
- `CONTRIBUTING.md`
- `SUPPORT.md`
- lockfiles for dependency-managed runtimes
- explicit runtime/toolchain versions

## CI and supply chain

- Third-party GitHub Actions are pinned to full immutable commit SHAs.
- Checkout credentials are not persisted unless an explicitly reviewed write job needs them.
- Workflow permissions default to read-only and are widened at the smallest job scope.
- `pull_request_target` is forbidden for untrusted code execution.
- Shared caches are disabled by default for security-sensitive or artifact-analysis workflows.
- Dependency changes are reviewed before merge.
- CodeQL or an equivalent static-analysis gate is enabled for supported languages.
- Secret/privacy scanning runs before merge.
- Release artifacts receive SHA-256 evidence, SBOM, and provenance/attestation where supported.

## Runtimes

Central baseline runtimes are exact versions, not floating selectors.

- Node.js baseline: 24.21.0 LTS.
- Python baseline: 3.14.7 stable.

Projects may pin a different supported exact version when compatibility requires it, but must not use floating selectors such as `3.x`, `latest`, or an unreviewed moving tag in security-sensitive CI.

## Secrets and cloud access

- Repository source contains secret names/placeholders only.
- Development, staging, and production are separated.
- Prefer GitHub Environments and deployment-provider secret stores.
- Prefer short-lived OIDC/federated credentials over long-lived cloud tokens.
- Production environments require an explicit approval policy where supported.
- API keys are narrowly scoped, rotated, and revocable.
- Raw secrets must not be pasted into issues, pull requests, logs, documentation, or chat transcripts.

## AI/model controls

- Model provider credentials are isolated by environment.
- Model-routing policy, cost limits, allowed models, and fallback behavior are explicit.
- External model/tool calls use least-privilege scopes.
- Private prompts, memory stores, retrieval corpora, and user data are separated from public code.
- Model outputs do not become trusted code, configuration, or release evidence without validation.

## Android and signing

- Production Android signing keys and keystores stay outside source control.
- APK/AAB provenance, package identity, version, signer, hash, and build inputs are captured before release.
- Forensic analysis operates on immutable/read-only copies and must not silently alter source APK/APKM bytes.

## Backup, recovery, and audit

- Source and release evidence are backed up outside the primary repository.
- Recovery procedures are documented and periodically tested.
- Credential compromise, dependency compromise, GitHub App compromise, and signing-key incidents have explicit response procedures.
- Claims of PASS require exact current evidence for the relevant commit/run/artifact.

## Human/admin gates

The following controls require GitHub account or repository administration and cannot be considered complete from source files alone:

- account passkeys / 2FA / recovery codes;
- active-session, PAT, SSH/signing-key, OAuth and GitHub App audit;
- repository visibility;
- branch protection / rulesets;
- secret scanning and push protection availability;
- repository-level auto-merge setting;
- collaborator/write-access reviewer policy;
- creation of new private repositories.

These gates remain open until verified from the exact account/repository UI or an authorized administration API.
