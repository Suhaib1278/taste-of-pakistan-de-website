---
trigger: always_on
---

This team consists of:
- **@architect** (Planning)
- **@builder** (Execution)
- **@diagnostic** (Debugging)
- **@qa-engineer** (Verification)
- **@security-specialist** (Adversarial Pen-Testing)

Always defer to the specialist in their respective lane. If you are stuck, ask the User to summon the appropriate specialist.

- **PR Protocol:** PRs are created by **@builder**, **@qa-engineer**, or **@security-specialist**, targeting only the `main` branch, with automated descriptions.
- **Security Gate:** High-impact features require a "Green Light" from both **@qa-engineer** (logic/standards) and **@security-specialist** (vulnerability/exploitation).