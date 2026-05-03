---
trigger: always_on
---

# Skill: Standard Git Protocol

## 1. Branch Creation & Naming
- **Source:** Always branch OFF `main`.
- **Sync First:** Before creating a new branch, you MUST run `git pull origin main`.
- **Naming Pattern (Mandatory):** Branches must use the format `[type]/[kebab-case-description]`.
  - **Types:** - `feat/` (New functionality/features)
    - `fix/` (Bug fixes)
    - `refactor/` (Code cleanup/structural changes)
    - `docs/` (Changes to README or non-ignored documentation)
  - **Forbidden:** Vague names like `phase-3`, `pr-2`, or `temp-work`.
  - **Example:** `feat/auth-manager-sqlite`, `fix/connection-retry-logic`.
- **Atomic Commits:** Each commit must contain exactly one logical change. Use descriptive messages (e.g., `feat: add encryption to VPS keys`).

## 2. Pre-Flight Check (Crucial)
- **Relevant Testing:** Before pushing, run the relevant test suite:
  - Use `pytest` for backend/logic changes.
  - Use `playwright` for frontend/UI changes.
  - Run both if the mission spans the full stack.
- If tests fail, the @Builder MUST attempt 3 self-corrections using terminal logs before reporting a stall.
- **Dependency Isolation:** Only use `pip` within the project's virtual environment. If a new library is required, it must be added to `requirements.txt` as the first step of the branch.
- **Persistence:** If 3 self-corrections fail, the agent must output a `FAIL_LOG.md` artifact detailing the exact error, the attempts made, and a request for human intervention.

## 3. Handoff
- Push branch to remote. Do NOT merge to main or develop.
- Notify User and @QA-Engineer for final verification.

## 4. Handoff & PR Protocol
- **Authorized Agents:** Both the **@builder** and **@qa-engineer** are authorized to create Pull Requests.
- **The Target:** All PRs must target the `main` branch. 
- **Description Requirement:** Any agent creating a PR must generate the automated technical description and verification logs.

## 5. Repository Hygiene (Hard Restrictions)
- **Docs Isolation:** You are strictly forbidden from committing or pushing any files located in the `docs/` folder. This directory is for local reference only.
- **Gitignore Integrity:** Ensure `docs/` is added to the `.gitignore` file during project scaffolding. If you see a `docs/` file in `git status`, do NOT add it to the staging area.