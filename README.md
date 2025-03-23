# 🚀 GitVersion Branching & Versioning Demo

This repository demonstrates a **custom GitVersion setup** to support a structured branching strategy and automated semantic versioning. It's designed for teams looking to streamline release pipelines, ensure consistent versioning, and manage branching flows effectively.

---

## 🔀 Branching Strategy


### ➡️ Branch Types and Their Version Labels

| Branch Type     | Example Name           | Version Format         | Description                                      |
|-----------------|------------------------|-------------------------|--------------------------------------------------|
| `main`          | `main`                 | `1.0.0`                 | Production-ready releases, tagged with full semantic versions. |
| `develop`       | `develop`              | `1.1.0-INT`             | Integration branch, minor version bumps, pre-release `INT`. |
| `feature`       | `feature/xyz`          | `1.1.0-TEST-xyz`        | Feature branches, inherit from develop or main, custom TEST label. |
| `release`       | `release/1.1.0`        | `1.1.0-QA`              | Candidate for production, tagged with QA label. |
| `hotfix`        | `hotfix/urgent-fix`    | `1.0.1-QA`              | Patch releases off of `main`. |
| `support`       | `support/legacy`       | `1.0.1`                 | Maintenance on older versions. |
| `pull-request`  | `pr/123`               | `1.1.0-PullRequest.123` | Preview versions for PR builds. |

---

## 🔁 Merge Flow

1. **Production Release**: `release/* ➜ main`  
2. **Post-Release Development**: `main ➜ develop`  
   - Bumps **minor** version for the next dev cycle.
3. **Feature Integration**: `feature/* ➜ develop`  
4. **Release Creation**: `develop ➜ release/*`

---

## ⚙️ GitVersion Highlights

- **Semantic Versioning** with `Major.Minor.Patch`
- **Branch-specific labels** for better traceability
- **Regex-based tagging and branching patterns**
- **Commit message-based version bumps**:
  - `+semver: breaking` → major
  - `+semver: feature` → minor
  - `+semver: fix` → patch
  - `+semver: none` → skip bump

---

## 🛠️ Configuration Summary

GitVersion is configured with the following key options:

- **`main`**:
  - Tagged with semantic versions (e.g., `1.0.0`)
  - Accepts merges from `release` and `hotfix`
- **`develop`**:
  - Bumps **minor** version on `main ➜ develop` merge
  - Uses `-INT` suffix
- **`feature/*`**:
  - Label format: `TEST-{BranchName}`
  - No automatic increment; uses parent's version
- **`release/*`**:
  - Static version from `develop`
  - Label: `-QA`
- **Other branches (`hotfix`, `support`)**:
  - Custom handling per type, inherit version or apply patch increment

---

## 📦 Example Versions

| Action                                  | Version Outcome        |
|----------------------------------------|------------------------|
| Tag on `main`                          | `1.0.0`                |
| Merge `main ➜ develop`                 | `1.1.0-INT`            |
| Create `feature/awesome-ui` from dev   | `1.1.0-TEST-awesome-ui`|
| Merge `develop ➜ release/1.1.0`        | `1.1.0-QA`             |
| Merge `release/1.1.0 ➜ main`           | `1.1.0`                |

---

## 📂 Repository Contents

- `.gitversion.yml`: Full configuration file for GitVersion.
- Sample branches demonstrating version output.
- Git tags representing semantic releases.

---

## ✅ Getting Started

1. Fork this repository
2. Play around with branches and PRs
3. Have a look at the tags and action summaries
