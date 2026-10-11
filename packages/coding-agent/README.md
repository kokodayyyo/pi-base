<p align="center">
  <a href="https://pi.dev">
    <img alt="Pi logo" src="https://pi.dev/logo-auto.svg" width="128">
  </a>
</p>

# Pi coding agent

> Part of a trimmed personal fork of [pi](https://github.com/earendil-works/pi); see the
> [repository README](../../README.md) and [AGENTS.md](../../AGENTS.md) for the fork's scope
> and working rules.

Pi is a minimal, extensible agent harness that you can make your own.

Adapt Pi to your workflows, not the other way around. Customize Pi with [extensions](docs/extensions.md), [skills](docs/skills.md), [prompt templates](docs/prompt-templates.md), and [themes](docs/themes.md). Bundle them as [Pi packages](docs/packages.md) and share via npm or git.

Pi ships with powerful defaults but skips features like sub-agents and plan mode. Ask Pi to build what you want, or install a package that does it your way.

Use Pi [interactively](docs/usage.md), automate it in [print or JSON mode](docs/cli.md), control it over [RPC](docs/rpc.md), or build apps with the [Pi TypeScript SDK](docs/sdk.md).

## Run

From the repository root:

```bash
node packages/coding-agent/dist/cli.js   # built CLI (run npm run build:offline first)
./pi-test.ps1                            # from sources, Windows
./pi-test.sh                             # from sources, macOS / Linux
```

Start Pi in the directory where you want it to work, connect a provider with `/login`, then give it a task.

See [docs/index.md](docs/index.md) for full setup and usage instructions.

## License

MIT. See [../../LICENSE](../../LICENSE). Based on [pi](https://github.com/earendil-works/pi) by Mario Zechner.
