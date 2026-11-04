# Verification gate

Before you say done, run the project's verification command yourself and paste the output. If a `verify-this` skill exists, that command is the one. Otherwise run the project's build, lint, and the tests that cover the change. A subagent saying the build passed does not count.

Skip when the turn only changed docs, or when the user told you to skip. Say that you skipped.

why-not-tooled: the stop hook is the gate. This file does not pick a compiler from a manifest.
