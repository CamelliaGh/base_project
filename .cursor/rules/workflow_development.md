---
description: "Core project context and patterns for efficient workflow"
globs: 
  - "**/*.{js,ts,tsx,py,php,css}"
alwaysApply: true
---

# Development Workflow

## 1. Planning and Execution

- **Always provide a complete PLAN with REASONING** based on the existing codebase and logs before making changes.
- **Break problems into smaller, manageable steps**. Present the overall plan first and wait for approval if working in standard chat mode.
- **Implement feature then test immediately**. After implementing a task, run relevant tests to ensure existing functionality is not broken.

## 2. Clean Build and Lint

Before considering work complete:

- Fix all linter and syntax/type errors
- Verify the project builds successfully
- **Frontend:** `cd frontend && npm run lint && npm run build`
- **Backend:** Run `cd backend && ruff check . --fix`; fix any remaining linter/syntax errors; ensure the app runs (e.g. `uvicorn main:app`)
- **PHP:** Run `composer run lint` or `./vendor/bin/phpcs` (if PHP_CodeSniffer is configured); fix syntax with `php -l`; ensure the app runs (e.g. `php -S localhost:8000`, `php artisan serve`, or `symfony serve`)

## 3. Run Tests

- Run tests and fix any failures before marking work done
- **Frontend:** `cd frontend && npm test` (when configured)
- **Backend:** `cd backend && pytest` (when configured)
- **PHP:** `./vendor/bin/phpunit` or `composer test` (when configured)
- Add tests for new behavior; do not remove or skip tests to make builds pass

## 4. Mark Tasks Done

After completing a task in `frontend/TASKS.md`, `backend/TASKS.md`, or `php/TASKS.md`:

- Change `- [ ]` to `- [x]` for the completed task
- Do this in the same commit/change that implements it

## 5. Error Handling and Edge Cases

- Do not swallow errors; log and handle or rethrow
- **Do not suppress errors by adding fallbacks** (e.g., default values, retries, alternative code paths) without asking the user first; propose the fallback and get approval.
- Consider empty inputs, null/undefined, network failures, and error states in UI
- Validate user input; fail safely on invalid data
- **Always include error handling and logging** in generated code to ensure robustness.

## 6. Security and Secrets

- No hardcoded secrets, API keys, or credentials in code
- Use environment variables or secure config for sensitive values

## 7. Code Quality and Standards

- **Don't overengineer; keep the code simple.** Prefer clear, minimal solutions over clever or speculative complexity.
- **Use standard naming and conventions for the language** (e.g. PEP 8 for Python, PSR-12 for PHP, common JS/TS conventions for frontend).
- **Only modify code directly relevant to the specific request.** Avoid changing unrelated functionality.
- **Never replace code with placeholders** like `// ... rest of the processing ...`. Always include complete, functional code.
- **Use descriptive variable and function names** that align with existing project conventions.
- Remove debug code (console.log, print, var_dump/error_log, commented-out blocks)
- No temporary workarounds left without a TODO or ticket
- Keep commits focused; avoid mixing unrelated changes

## 8. Communication and Context

- **Explain your OBSERVATIONS clearly** and provide REASONING to identify the exact issue before proposing a solution.
- **Reference real files** in the codebase (e.g., `@components/UserCard.tsx`) for structure and pattern examples.
- **Keep the context clean** by closing unnecessary editor tabs and using specific prompts.

## 9. Verification Steps

- **Self-review code before completion:** Before finalizing a task, perform a self-review to check for common pitfalls, syntax errors, and adherence to the above rules.
- **Verify functionality:** Explicitly state how the generated/modified code can be tested (e.g., "Run `npm test`" or "Check UI element X").

## 10. Ask When Uncertain

- If you are **not more than 90% certain** about a design, implementation, or product decision, **ask the user** instead of guessing.
- Clarify requirements, preferences, or trade-offs before proceeding when confidence is low.
- Do not assume ambiguous intent; one short question is better than rework.
