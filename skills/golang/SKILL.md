---
name: golang
description: Strict Go (golang) coding, testing, and file organization standards for the user's projects.
triggers:
  - "**/*.go"
---

## Language & Logic

- **Context:** NEVER use `context.Context` to pass logic-influencing Values (`WithValue`).
- **Timeouts:** NO hidden timeouts; all timeouts MUST be handled via `context.Context`.
- **Branching:** Use `switch` instead of chained `if` statements for >2 semantic branches.
- **Workspace:** Prefer editing `go.work` over `go.mod`.
- **Linter:** Adhere to all linter rules (e.g., `rangeint`). Satisfaction of the linter is mandatory.
- **Logging:** NO `fmt.Print*` for logs. Use `logger` package with appropriate levels. Use `Trace` for frequency >1/sec.
- **Errors:** Favor custom non-pointer error types over wrapping (`errors.Wrap`, `fmt.Errorf`) where feasible.

## Testing Protocols

- **Timeout:** `go test` timeout must NEVER exceed 4 minutes.
- **Location:**
  - Unit: `<filename>_test.go` next to source.
  - Integration: `<filename>_integration_test.go` at highest-level tested code.
  - System/E2E: `tests/e2e/` or `tests/system/`.
- **Naming:** `Test<FunctionOrFeature><WhatIsBeingTested>`.
- **Mocks:** Use mocks for external communications in unit and internal integration tests.
- **Build Tags:** Use `test_integration` for external integration and `test_e2e` for E2E tests.

## Files & Errors

- **Specificity:** File names must be specific. Group short files only if semantically very close.
- **Error Registry:** Always keep all error types in `errors.go`.
