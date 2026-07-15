# Contribution 2: Tabnine Provider for Nous

## Current Status

- ✅ Phase I: Issue Selection — Complete
- 🚧 Phase II: Reproduce and Plan — In Progress

---

## Phase I: Issue Selection

### Issue

[Adapter: Tabnine — orthogonalhq/nous-core #300](https://github.com/orthogonalhq/nous-core/issues/300)

### Project Fork

https://github.com/AryahCodes/nous-core

### Problem Summary

The Nous project currently does not include a Tabnine integration using its
new CLI-backed provider architecture. This issue asks for Tabnine to be
implemented as a provider leaf using the current `ProviderDefinitionLeaf`
contract.

The provider must define the appropriate CLI execution capability, follow the
repository's current provider-adapter structure, and include the required
tests.

### Why I Chose This Issue

I chose this issue because it combines artificial intelligence with software
engineering. Tabnine is an AI coding assistant, while the contribution itself
involves TypeScript, command-line integration, process execution,
configuration, output handling, error handling, and automated testing.

This issue will also give me experience working inside a large TypeScript
monorepo and learning how AI providers are integrated into a real application.

### Issue Selection Checklist

- [x] I understand the requested feature
- [x] The issue is labeled `good first issue`
- [x] The issue is currently open
- [x] The issue is unassigned
- [x] There is no linked pull request
- [x] Updated provider documentation is available
- [x] I commented on the GitHub issue
- [x] I claimed the issue in the CodePath candidate sheet
- [x] I forked the repository

---

## Phase II: Reproduce and Plan

### Working Branch

https://github.com/AryahCodes/nous-core/tree/feat/tabnine-provider

I created the branch from the repository's current provider integration branch:

```text
upstream/feat/contributor-friendly-inference-provider-surface
```

### Environment Setup

I cloned my fork, connected the upstream repository, created my working branch,
and pushed the branch to my fork.

```bash
git clone https://github.com/AryahCodes/nous-core.git
cd nous-core

git remote add upstream https://github.com/orthogonalhq/nous-core.git
git fetch upstream

git checkout -b feat/tabnine-provider \
  upstream/feat/contributor-friendly-inference-provider-surface

git push -u origin feat/tabnine-provider
```

The repository requires Node.js 22 or newer and pnpm 10.

During setup, I initially used Node.js 25. This caused the native
`better-sqlite3` binding to be unavailable on macOS ARM64.

The tests failed with the following error:

```text
Could not locate the bindings file for better-sqlite3
```

I resolved the environment issue by:

1. Installing `nvm`
2. Switching to Node.js 22
3. Reinstalling the project dependencies
4. Rebuilding `better-sqlite3`

I verified that the SQLite dependency worked by rerunning the previously
failing witness-router test:

```text
Test Files  1 passed
Tests       4 passed
```

### Baseline Test Results

The default full test command initially caused a native segmentation fault
while Vitest was using its thread-based worker pool.

I reran the suite with process-based workers and reduced concurrency:

```bash
pnpm exec vitest run \
  --pool=forks \
  --maxWorkers=2 \
  --reporter=dot
```

The baseline results were:

```text
Test Files  622 passed | 2 failed | 2 skipped
Tests       6326 passed | 2 failed | 4 skipped
```

The two remaining failures occurred in the existing Mistral provider pipeline
before I made any Tabnine implementation changes. I recorded these as baseline
failures rather than modifying unrelated provider code.

### Reproduction Process

This issue is a missing-feature request rather than a traditional bug.

The current limitation can be reproduced by checking whether a certified
Tabnine provider exists in the provider system.

```bash
find self/subcortex/providers/src/providers \
  -maxdepth 2 \
  -iname '*tabnine*'

rg -n "tabnine" self/subcortex/providers/src
```

### Current Behavior

There is currently no certified Tabnine provider leaf under:

```text
self/subcortex/providers/src/providers/tabnine/
```

As a result, Tabnine cannot be registered or selected through the current Nous
provider system.

### Expected Behavior

Nous should include a certified Tabnine CLI provider leaf that:

- Uses the current `ProviderDefinitionLeaf` contract
- Uses the shared agent-CLI protocol
- Declares the correct `executionCapabilityProfile`
- Invokes the Tabnine CLI correctly
- Validates input
- Parses command output
- Handles command failures and malformed output
- Appears in the generated provider catalog
- Passes the provider-specific test suite

### Relevant Documentation

I identified the following repository documentation as the primary source of
truth for this contribution:

```text
docs/content/docs/development/provider-adapters/quickstart.mdx
docs/content/docs/development/provider-adapters/cli-provider-guide.mdx
docs/content/docs/development/provider-adapters/provider-leaf-anatomy.mdx
docs/content/docs/development/provider-adapters/schemas-abi-reference.mdx
docs/content/docs/development/provider-adapters/testing-checklist.mdx
```

### Architectural Findings

CLI-backed providers use the same `ProviderDefinitionLeaf` structure as API
providers, but they must also define an `executionCapabilityProfile`.

The supported profiles are:

- `one_shot_command`
- `session_bound_command`
- `persistent_process`

The selected profile must match Tabnine's actual CLI behavior. I will verify
whether Tabnine runs as an independent command, maintains session state, or
uses a persistent process before selecting the profile.

A CLI provider leaf is expected to contain:

```text
self/subcortex/providers/src/providers/tabnine/
├── definition.ts
├── adapter.ts
├── provider.ts
└── index.ts
```

The provider should define a semantic `vendorKey`. It should not manually
define `wellKnownProviderId`, because the generated provider catalog derives
the built-in provider ID from the `vendorKey`.

### Implementation Plan

1. Review the CLI provider guide and provider-leaf architecture.
2. Identify the existing CLI provider that most closely matches Tabnine.
3. Determine how the Tabnine CLI is installed and detected.
4. Determine how the CLI is invoked and authenticated.
5. Determine whether the CLI supports one-shot, session-bound, or persistent
   execution.
6. Create the new Tabnine provider folder.
7. Add `definition.ts` with the provider metadata and execution profile.
8. Add `adapter.ts` for request formatting and output parsing.
9. Add `provider.ts` for provider construction and CLI execution.
10. Add `index.ts` for public exports.
11. Regenerate the provider catalogs.
12. Add tests for provider definition validation and generated exports.
13. Add tests for request formatting, successful responses, malformed output,
    missing CLI installation, command failures, and timeouts.
14. Add compatibility tests for the selected execution profile.
15. Run the provider-specific validation commands.
16. Run relevant regression tests and compare the results with the recorded
    baseline.

### Planned Validation Commands

```bash
pnpm --filter @nous/subcortex-providers run generate:providers

pnpm --filter @nous/subcortex-providers run check:generated

pnpm --filter @nous/subcortex-providers run typecheck

pnpm --filter @nous/subcortex-providers exec vitest run \
  src/__tests__/provider-codegen.test.ts \
  src/__tests__/public-exports.test.ts \
  src/__tests__/provider-definitions \
  src/__tests__/adapter-resolver.test.ts \
  src/__tests__/provider-pipeline-integration.test.ts \
  --config vitest.config.ts
```

### Phase II Completion Checklist

- [x] Forked and cloned the repository
- [x] Connected the upstream repository
- [x] Created and pushed a dedicated working branch
- [x] Installed the project dependencies
- [x] Resolved the local native dependency issue
- [x] Ran targeted baseline tests
- [x] Ran the full baseline test suite
- [x] Recorded existing test failures
- [ ] Confirmed the absence of an existing Tabnine provider using repository searches
- [ ] Identified the closest existing CLI provider implementation
- [ ] Confirmed Tabnine's actual CLI execution model
- [x] Created an initial implementation and testing plan
