# evals-cli

Command-line client for [2027.dev evals](https://2027.dev/evals) — automated agent experience (AX) evaluations for developer tools. List your prompts, trigger eval runs, and read reports and traces from the terminal or from an AI agent.

This repository hosts the release binaries only. The CLI is generated from the public evals REST API.

## Install

```sh
curl -fsSL https://2027.dev/evals/install.sh | sh
```

The script picks the binary for your platform, verifies it against `SHA256SUMS`, and installs it to `~/.local/bin/evals-cli`.

| Variable | Effect |
|----------|--------|
| `EVALS_CLI_VERSION` | Install a specific version, e.g. `0.1.4` (default: latest) |
| `EVALS_CLI_INSTALL_DIR` | Install somewhere else (default: `$HOME/.local/bin`) |

Supported platforms: macOS (Apple silicon and Intel) and Linux x86_64.

### Manual download

Download `evals-cli-<os>-<arch>` from [Releases](https://github.com/team2027/evals-cli/releases), check it against `SHA256SUMS`, make it executable and put it on your `PATH`:

```sh
shasum -a 256 -c SHA256SUMS --ignore-missing
chmod +x evals-cli-darwin-arm64
mv evals-cli-darwin-arm64 ~/.local/bin/evals-cli
```

## Authenticate

Create an API key in your organization's settings at `https://2027.dev/evals/<org>/settings`, then either store it:

```sh
evals-cli auth login
```

or pass it through the environment:

```sh
export EVALS_CLI_TOKEN=<your API key>
```

An exported `EVALS_CLI_TOKEN` wins over a stored login.

Log out: `evals-cli auth logout --scheme deviceLogin` removes the local login; the API key it created stays valid until you revoke it in Settings → API Keys (named `evals-cli login <date>`).

## Examples

```sh
evals-cli v1 listprompts
evals-cli v1 getprompt --prompt-id <id>
evals-cli v1 listruns --limit 10
evals-cli v1 --help
```

Output is a table in a terminal and JSON when piped (`--format json|yaml|csv|table`).

## Links

- [2027.dev/evals](https://2027.dev/evals)
- [Issues](https://github.com/team2027/evals-cli/issues)
