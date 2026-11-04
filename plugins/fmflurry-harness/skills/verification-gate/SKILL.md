---
name: verification-gate
description: "Use before claiming work is done, or when a stop hook blocks the turn. Run the project's verification command and paste the output."
---

Before you say done, run the project's verification command yourself and paste the output. If a `verify-this` skill exists, that command is the one. Otherwise run the project's build, lint, and the tests that cover the change. A subagent saying the build passed does not count. `ship-stop-gate` blocks a stop when that did not happen.

why-not-tooled: the stop hook is the gate. This skill does not pick a compiler from a manifest.
