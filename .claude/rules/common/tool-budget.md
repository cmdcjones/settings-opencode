# Tool Budget (exploratory shell rate-limiting)

## Bash Classification

### VERIFICATION (uncapped, never counted, never nudged)

Never counted against budget; no L1/L2 steering applies. Runs:
- Build/typecheck/test/lint/format: `tsc`, `npm run *`, `pnpm run *`, `bun run *`, `yarn run *`, `cargo`, `go build`, `mypy`, `pyright`, `mvn`, `gradlew`, `dotnet build`, `dotnet test`, `dotnet format`, `eslint`, `ruff`, `clippy`
- Git state: `git status`, `git diff`, `git log`, `git stash`, `git show`
- Process & port checks: `lsof`, `netstat`, `ps`, `grep` on process lists
- Sequential command chains: any command whose output feeds the next command's input (genuine dependency)

### EXPLORATORY (counted against budget)

Counted toward the 3-call limit unless the brief raises it:
- Directory listing: `ls`, `rtk ls`, `find`, `rtk find`, `tree`
- Content search: `grep`, `rtk grep`, `rg`, `ag`
- File inspection: `cat`, `head`, `tail`, `wc`, `file`, `stat`
- Targeting: source code or repo structure

## Allowlist-First Principle

Unknown commands default to NOT counted. Under-enforce rather than block real work.

## Exploratory Budget Rules

- **Default**: 3 calls per dispatched task unless the brief raises it.
- **Pre-requisite**: When the CodeMemory index is up, one retrieve is enough to orient. Otherwise search. Do not require a memory call before grep. When CodeMemory is off, do not call it. See the `codebase-exploration` skill.
- **Target ratio**: exploratory bash : edits ≤ 2 (proven achievable at 1.35).

## Trip Levels (L1 and L2 ONLY)

L3 deny is deliberately deferred; conduct L1 steer + L2 justify only.

### L1 Steer (at 3rd exploratory call with 0 edits)

When CodeMemory is on, conductor nudges toward code-memory or Read: "Before the 4th exploratory bash, show progress: either code-memory topology tool or a Read to a targeted line range." When it is off, nudge toward a targeted Read or grep and do not call CodeMemory.

### L2 Justify (when ratio > 3 at ≥5 edits)

Require a one-line justification in the next message: `bash-budget: <why exploratory shell is still necessary>`.

## Anti-Displacement Rule

**Important**: Do NOT reroute a blocked exploratory call into a full-file Read. A 900-line Read costs more tokens than the `grep` it replaced.

- Use `Read` with line ranges (e.g., `offset`, `limit`).
- When CodeMemory is on, use code-memory topology tools (`definitions`, `callers`, `callees`, `importers`, `dependencies`).
- Fall back to targeted `grep` when CodeMemory is off or has no index.

## Code-Memory Graph Availability

If CodeMemory is off, or its topology tools return empty for a project, state so explicitly — exploratory shell is then legitimate to bootstrap the initial manifest.
