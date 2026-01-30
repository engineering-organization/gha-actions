# gha-actions

This repository contains **reusable GitHub Actions workflows** built using a **GitHub App** to demonstrate secure, auditable automation.

The workflows use **short-lived GitHub App installation tokens** (generated per run using `APP_ID` and `APP_PRIVATE_KEY`) instead of long-lived PATs. For validation, a **SHA-256 fingerprint (first 12 characters only)** of the token is printed to confirm token rotation without exposing credentials.

## Available Reusable Workflows

### 1. Create GitHub Release
**Path:** `.github/workflows/create-release.yml`  
Creates a GitHub release for a provided tag using the GitHub App identity.

**Input**
- `tag` (string, required)

---

### 2. Create File, PR, and Merge
**Path:** `.github/workflows/create-file-pr-merge.yml`  
Creates a file on a new branch, opens a pull request, merges it to the base branch, and deletes the temporary branch using the GitHub App identity.

**Inputs**
- `filename` (string, required)
- `file_content` (string, required)
- `base_branch` (string, optional, default: `main`)

---

## Security & Audit Notes
- All actions are attributed to the **GitHub App**, not a user account.
- A **new installation token is generated for every run** (tokens are not reused).
- Only a **hashed token fingerprint** is logged for debugging purposes.
- Required secrets (`APP_ID`, `APP_PRIVATE_KEY`) must be provided by the calling repository.

These workflows are intended to illustrate **least-privilege access, clear system identity, and improved auditability** compared to PAT-based automation.
