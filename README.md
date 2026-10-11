<p align="center">
  <a href="https://pi.dev">
    <img alt="pi logo" src="https://pi.dev/logo-auto.svg" width="128">
  </a>
</p>

# Pi (trimmed fork)

> Personal fork of [pi](https://github.com/earendil-works/pi), trimmed to the coding-agent core.
> Removed relative to upstream: the release/CI infrastructure (GitHub workflows, Nix, husky,
> install-lock, publish/release scripts) and the experimental runtime stack
> (`durable`, `env`, `client`, `protocol`, `server`, `src/experimental`).
> Working rules for this fork are in [AGENTS.md](AGENTS.md).

Pi is a minimal, extensible agent harness that you can make your own.

Adapt Pi to your workflows, not the other way around. Customize Pi with [extensions](packages/coding-agent/docs/extensions.md), [skills](packages/coding-agent/docs/skills.md), [prompt templates](packages/coding-agent/docs/prompt-templates.md), and [themes](packages/coding-agent/docs/themes.md). Bundle them as [Pi packages](packages/coding-agent/docs/packages.md) and share via npm or git.

Pi ships with powerful defaults but skips features like sub-agents and plan mode. Ask Pi to build what you want, or install a package that does it your way.

Use Pi [interactively](packages/coding-agent/docs/usage.md), automate it in [print or JSON mode](packages/coding-agent/docs/cli.md), control it over [RPC](packages/coding-agent/docs/rpc.md), or build apps with the [Pi TypeScript SDK](packages/coding-agent/docs/sdk.md).

## Getting started

Requires Node.js 22.19 or newer. From a fresh clone:

```bash
npm install --ignore-scripts   # dependencies only; no lifecycle scripts
npm run hydrate:model-data     # first checkout only: fetch model catalog data (needs network)
npm run build:offline          # build all packages using the hydrated model data
```

Run the built CLI:

```bash
node packages/coding-agent/dist/cli.js
```

Or run Pi directly from TypeScript sources without building (from the repo root):

```bash
./pi-test.ps1   # Windows
./pi-test.sh    # macOS / Linux
```

Start Pi in the directory where you want it to work, connect a provider with `/login`, then give it a task.

For local models via llama.cpp, see [llama-cpp.md](packages/coding-agent/docs/llama-cpp.md); for OpenAI-compatible endpoints and other providers see [providers.md](packages/coding-agent/docs/providers.md) and [custom-provider.md](packages/coding-agent/docs/custom-provider.md).

## Packages

This monorepo contains the Pi CLI and the packages it needs:

| Package | Description |
|---------|-------------|
| **[@earendil-works/chord](packages/chord)** | Application composition runtime for services, replicated state, RPC, and plugins |
| **[@earendil-works/pi-telemetry](packages/telemetry)** | Vendor-neutral telemetry contracts and typed schema utilities |
| **[@earendil-works/pi-ai](packages/ai)** | Unified multi-provider LLM API (OpenAI, Anthropic, Google, llama.cpp, etc.) |
| **[@earendil-works/pi-agent-core](packages/agent)** | Agent runtime with tool calling, state management, and transport abstraction |
| **[@earendil-works/pi-codemode](packages/codemode)** | Sandboxed JavaScript execution where the only capability is calling injected tools |
| **[@earendil-works/pi-mcp](packages/mcp)** | Standalone Model Context Protocol client |
| **[@earendil-works/pi-coding-agent](packages/coding-agent)** | Interactive coding agent CLI |
| **[@earendil-works/pi-tui](packages/tui)** | Terminal UI library with differential rendering |

## Permissions & Containerization

Pi does not include a built-in permission system for restricting filesystem, process, network, or credential access. By default, it runs with the permissions of the user and process that launched it.

If you need stronger boundaries, containerize or sandbox Pi. See [packages/coding-agent/docs/containerization.md](packages/coding-agent/docs/containerization.md) for three patterns:

- **Gondolin extension**: keep `pi` and provider auth on the host while routing built-in tools and `!` commands into a local Linux micro-VM.
- **Plain Docker**: run the whole `pi` process in a local container for simple isolation.
- **OpenShell**: run the whole `pi` process in a policy-controlled sandbox.

## Development

```bash
npm run build:offline   # rebuild all packages from existing model data
npm run build           # refresh model data (network), then build all packages
npm run check           # biome + TypeScript import/entry-graph checks + typecheck
npm test                # script tests + all package test suites
npm --prefix packages/coding-agent test   # coding-agent vitest suite only
./test.sh               # test suites in an isolated home (POSIX bash only)
```

- Full documentation: `packages/coding-agent/docs/` — [quickstart](packages/coding-agent/docs/quickstart.md), [configuration](packages/coding-agent/docs/configuration.md), [models](packages/coding-agent/docs/models.md), [windows](packages/coding-agent/docs/windows.md), [tmux](packages/coding-agent/docs/tmux.md), ...
- `packages/ai/src/providers/data/` is generated by `npm run hydrate:model-data` and is not committed; fresh checkouts need it once before `build:offline`.

## Supply-chain notes

- Direct external dependencies are pinned to exact versions in each `package.json`.
- `.npmrc` sets `save-exact=true` and `min-release-age=2` so same-day dependency releases are avoided during npm resolution.
- `package-lock.json` is the dependency ground truth; installs use `--ignore-scripts`.

## License

MIT. See [LICENSE](LICENSE). Based on [pi](https://github.com/earendil-works/pi) by Mario Zechner.
