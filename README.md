# evals

Command-line client for [2027.dev evals](https://2027.dev/evals): list your prompts, request eval runs and read their results from a terminal, a script or an AI agent.

This repository hosts the release binaries.

## Install

```sh
curl -fsSL https://2027.dev/evals/install.sh | sh
```

Supported platforms: macOS (Apple silicon and Intel) and Linux x86_64. The script downloads the binary for your platform, verifies it against `SHA256SUMS` and installs it to `~/.local/bin/evals`. Set `EVALS_VERSION` to install a specific version, or `EVALS_INSTALL_DIR` to install somewhere else.

To install by hand, download `evals-<os>-<arch>` and `SHA256SUMS` from [Releases](https://github.com/team2027/evals-cli/releases), then:

```sh
shasum -a 256 -c SHA256SUMS --ignore-missing
chmod +x evals-darwin-arm64
mv evals-darwin-arm64 ~/.local/bin/evals
```

Full guide: [2027.dev/evals/cli-install](https://2027.dev/evals/cli-install)

## Authenticate

```sh
evals auth login
```

This opens your browser to approve a device code, then stores an API key for your organization in a file only you can read: `~/Library/Application Support/evals/auth-keyring.json` on macOS, `~/.config/evals/auth-keyring.json` on Linux. There is no keychain prompt. For CI and scripts, export an API key from `https://2027.dev/evals/<org>/settings` instead:

```sh
export EVALS_TOKEN=<your API key>
```

An exported `EVALS_TOKEN` wins over a stored login. `evals auth logout --scheme deviceLogin` removes the login from that file; the API key it created stays valid until you revoke it under API keys in your organization's settings. Upgrading from a version that used the macOS keychain? Run `evals auth login` once more.

## Usage

```sh
evals whoami                                # the account and org you call the API as
evals prompts list
evals prompts get --prompt-id <id>
evals runs request --prompt-id <id>         # trigger an eval run
evals runs get --run-id <id>                # status of a run
```

Output is a table in a terminal and JSON when piped. Useful global options:

```sh
evals prompts list --format json                        # json, yaml, csv, jsonl, table, raw
evals prompts list --query '[].{id: id, title: title}'  # JMESPath over the response
evals runs request --prompt-id <id> --dry-run           # show the request without sending it
```

`evals --help` lists every command; `evals <command> --help` shows its flags.

For AI agents, `evals generate-skills` writes `SKILL.md` files (into `./skills` by default) describing the commands.

## License

Apache-2.0
