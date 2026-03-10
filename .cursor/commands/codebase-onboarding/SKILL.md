---
name: codebase-onboarding
description: Produces a structured onboarding report for a codebase: tech stack, main flows, how to run, and security considerations. Use when the user wants to get familiar with a new codebase, onboard to a project, understand main flows, run instructions, tech stack, or vulnerabilities.
---

# Codebase Onboarding

When the user asks to get familiar with a new codebase (or similar: onboard me, explain this project, main flows, how to run, tech stack, vulnerabilities), produce a **Codebase Onboarding Report** by exploring the repo and then filling the template below.

## Workflow

1. **Discover structure**: List root; find config files (package.json, requirements.txt, pyproject.toml, Cargo.toml, go.mod, Dockerfile, docker-compose*, Makefile, README, .env.example).
2. **Tech stack**: Infer from lockfiles, configs, and entry points (e.g. main, index, app).
3. **How to run**: Extract from README, package scripts, Makefile, docker-compose, and any run/deploy docs.
4. **Main flows**: Identify entry points, key routes/APIs, and critical user or data flows (auth, core features).
5. **Vulnerabilities & hygiene**: Check for hardcoded secrets, outdated/vulnerable deps, unsafe patterns (eval, shell injection, SQL concatenation), missing env validation, and exposed config.

Use codebase search and file reads; do not guess. If something is unclear, say so in the report.

## Report Template

Output the report in markdown using this structure:

```markdown
# Codebase Onboarding Report

## 1. Tech stack
- **Languages**: …
- **Frameworks / runtimes**: …
- **Databases / services**: …
- **Tooling**: (build, lint, test, package manager)

## 2. How to run
- **Prerequisites**: (runtime versions, env vars, services)
- **Install**: (commands to install deps)
- **Run locally**: (dev/server commands)
- **Tests**: (how to run tests)
- **Optional**: (Docker, staging, prod hints if present)

## 3. Main flows
- **Entry points**: (e.g. main.py, src/index.tsx, cmd/server)
- **Critical paths**: (e.g. auth flow, core API, key UI flows)
- **Notable structure**: (monorepo layout, backend vs frontend, key modules)

## 4. Security & vulnerabilities
- **Secrets**: (hardcoded credentials? .env usage? .gitignore for secrets?)
- **Dependencies**: (known vulnerable packages? outdated major versions?)
- **Risks**: (injection, missing validation, unsafe defaults, exposed config)
- **Recommendations**: (short, actionable)

---
*Report generated from codebase exploration. Verify run commands and versions in the repo.*
```

## Tips

- Prefer reading README, CONTRIBUTING, and package/root configs first.
- For “main flows”, trace from entry point to a few key features; no need to list every file.
- For vulnerabilities, use dependency audit commands if available (e.g. `npm audit`, `pip-audit`, `cargo audit`) and note when not run; still flag obvious code/config risks.
- Keep the report scannable: bullets and short paragraphs; link to key files when helpful.
