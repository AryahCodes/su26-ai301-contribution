## Contribution 2: Tabnine Provider for Nous

**Issue:** [Adapter: Tabnine — orthogonalhq/nous-core #300](https://github.com/orthogonalhq/nous-core/issues/300)

**Fork:** https://github.com/AryahCodes/nous-core

**Working Branch:** https://github.com/AryahCodes/nous-core/tree/feat/tabnine-provider

### Status

✅ Phase I: Issue Selection — Complete  
✅ Phase II: Reproduce and Plan — Complete  
✅ Phase III: Build — Complete  
🚧 Phase IV: Submit and Iterate — Not Started

---

## Phase III: Build

### Implementation Notes

Implemented a complete Tabnine CLI provider leaf under:

`self/subcortex/providers/src/providers/tabnine/`

The implementation follows Nous's contributor-friendly provider architecture and uses the existing Qwen Code provider as the primary structural reference.

Added:

- `definition.ts`
- `adapter.ts`
- `implementation.ts`
- `provider.ts`
- `index.ts`

The provider uses the shared `agent-cli` protocol and declares:

`executionCapabilityProfile: 'one_shot_command'`

This matches Tabnine's headless CLI behavior, where each request launches a new Tabnine process using a command such as:

`tabnine -p "<prompt>"`

The provider does not enable Tabnine's `-y` auto-accept mode by default because that option automatically approves tool actions. The default integration therefore uses the safer headless prompt mode.

The implementation also includes:

- Input validation using the existing Nous text-model schema
- Shared agent-CLI request execution
- Injectable runners for unit testing
- CLI executable discovery and override support
- Timeout and abort handling
- Non-zero exit and spawn error handling
- Environment-variable allowlisting
- `TABNINE_TOKEN` authentication support
- `TABNINE_HOST` support/documentation
- Plain-text response parsing with fallback behavior
- Generated provider catalog registration
- Public package exports

Tabnine does not receive a manually defined `wellKnownProviderId`. Its provider ID is generated automatically from its `vendorKey` according to the existing Nous provider identity system.

### Challenges Faced

One issue discovered during implementation was Tabnine's `-y` flag.

Initially, `-y` was configured as a required headless argument. After reviewing Tabnine's CLI behavior more carefully, I determined that `-p` is sufficient for headless prompt execution while `-y` enables automatic approval of tool actions.

The provider was updated so the default invocation is:

`tabnine -p "<prompt>"`

instead of:

`tabnine -y -p "<prompt>"`

Another difference from the Qwen Code provider was model selection. Tabnine does not use a documented `--model` CLI argument for this workflow, so the provider intentionally does not generate one.

I also added explicit coverage for the `one_shot_command` execution profile to verify that Tabnine remains available for compatible command-bound execution while being incompatible with persistent Cortex chat/system requirements.

### Testing Strategy

Added two Tabnine-specific test files:

- `src/__tests__/providers/tabnine.test.ts`
- `src/__tests__/provider-definitions/tabnine-definition.test.ts`

These contain **34 Tabnine-specific tests** covering:

- Provider definition metadata
- Provider schema validation
- Execution capability profile
- Adapter request formatting
- Response parsing and malformed-output fallback
- CLI argument construction
- Input validation
- Successful invocation
- Non-zero process exits
- Spawn failures
- Timeouts
- Abort behavior
- stdout/stderr handling
- Environment allowlisting
- Executable overrides
- Fake/injected runner behavior
- Streaming
- Provider factory creation

Additional integration coverage was added for provider registration, provider type derivation, the generated provider catalogs, pipeline integration, role compatibility, and CLI session-manager behavior.

Validation commands included:

```bash
pnpm --filter @nous/subcortex-providers run generate:providers

pnpm --filter @nous/subcortex-providers run check:generated

pnpm --filter @nous/subcortex-providers run typecheck
