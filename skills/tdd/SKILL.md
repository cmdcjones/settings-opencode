---
name: tdd
description: "Use when behavior changes. Add a test that fails before the fix. /tdd refactor pins current behavior first."
---

# Test-driven development

When behavior changes, add a test that fails before the fix. Then write the smallest code that makes it pass.

## Refactor mode

`/tdd refactor` does not start RED. Write characterization tests that pin the current observable behavior. Run them on the unchanged code. They pass immediately. A failure means the test is wrong: fix the test, not the code. Freeze those tests. The restructure does not edit them. New behavior still starts with a failing test.

Load `test-behavior-not-implementation`. Do not chase a coverage percentage.
