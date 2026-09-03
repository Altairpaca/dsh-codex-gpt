# dsh-codex-gpt

> **Maintenance status: legacy / superseded.** This repository preserves the original DSH agent-preset + token-sync approach. Active development has moved to [`Altairpaca/dsh-codex-bridge`](https://github.com/Altairpaca/dsh-codex-bridge), which adds an explicit runtime CLI, login-status diagnostics, proxy handling, launch checks, and a clearer credential boundary.

This project originally connected [DeepSeek Harness (DSH)](https://github.com/deepseek-ai/deepseek-harness) to the `openai-codex` provider using an agent preset and a PowerShell helper that copied a Codex/ChatGPT OAuth access token into DSH credential storage.

## Why this repository remains public

The implementation is kept as a small historical compatibility snapshot because it records the first working configuration and may still be useful when debugging an older local setup. It should not be treated as the current recommended installation path.

For new setups, use:

- [`dsh-codex-bridge`](https://github.com/Altairpaca/dsh-codex-bridge) for the maintained runtime/diagnostic path;
- official Codex login tooling for authentication;
- product-owned credential sources where possible instead of duplicating tokens between configuration stores.

## Legacy contents

- `agent-presets/code-gpt/` — DSH agent preset using the `openai-codex` provider and Codex subagent tooling.
- `scripts/sync-codex-token.ps1` — legacy helper that copies the current Codex access token into DSH credential storage.
- `docs/` — configuration notes for the original setup.

## Historical flow

The original setup was:

1. authenticate with the official Codex CLI;
2. read the resulting access token from the local Codex auth store;
3. copy it into the DSH credential store;
4. configure the DSH `openai-codex` provider and use the `code-gpt` preset.

This worked as a compatibility bridge, but token duplication creates an avoidable lifecycle problem: expiry/refresh and ownership of credential state become harder to reason about. The successor repository keeps this legacy fallback documented while moving the main interface toward status checks and product-owned authentication sources.

## Migration

If you already use this repository, there is no requirement to delete the preset immediately. Move operational scripts and future fixes to `dsh-codex-bridge`, then remove the legacy sync path once your DSH setup can rely on the maintained credential flow.

## License

MIT. See [`LICENSE`](LICENSE).
