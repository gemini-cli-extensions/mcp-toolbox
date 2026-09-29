# DEVELOPER.md

This document provides instructions for setting up your development environment
and contributing to the MCP Toolbox Gemini CLI Extension project.

## Prerequisites

Before you begin, ensure you have the following:

1.  **Gemini CLI:** Install the Gemini CLI version v0.6.0 or above. Installation
    instructions can be found on the official Gemini CLI documentation. You can
    verify your version by running `gemini --version`.
2.  **MCP Toolbox tools.yaml:** For testing, you will need a custom tools.yaml.
    The server reads it from its working directory and exits if it is missing.
3.  **Node.js:** Every manifest starts the server with `npx`, so Node.js must be
    on your path.
4.  **Claude Code and Codex (optional):** Needed only to test those harnesses.
    See [Testing in Other Harnesses](#testing-in-other-harnesses).

## Developing the Extension

### Plugin Manifests

Each harness reads its own manifest, so this repository ships several:

| File | Read by | Purpose |
| --- | --- | --- |
| `gemini-extension.json` | Gemini CLI | Extension manifest: version, MCP server, and `MCP-TOOLBOX.md` as the context file |
| `.claude-plugin/plugin.json` | Claude Code | Plugin manifest: version and MCP server |
| `.claude-plugin/marketplace.json` | Claude Code, Codex | Marketplace that lists this repository (`"source": "./"`), so users can install straight from it |
| `plugin.json` | Codex, other Agent Plugins hosts | Portable [Agent Plugins](https://agent-plugins.org) manifest: name, version, and metadata |
| `mcp.json` | Codex, other Agent Plugins hosts | Portable MCP server configuration |
| `.codex-plugin/plugin.json` | Codex | Install-surface metadata (`interface`): display name, category, and default prompt |
| `mcp_config.json` | Antigravity | MCP server configuration |

Keep these rules in mind when you edit them:

*   **Codex loads the MCP server only from `mcp.json`.** The root `plugin.json`
    makes this a portable package, so Codex ignores any `mcpServers` in
    `.codex-plugin/plugin.json`. Codex reads `interface` from
    `.codex-plugin/plugin.json`, not from the `codex` block under
    `extensions["com.google.cloud.data.agent-plugins"]` in `plugin.json`, so
    keep the two in sync. See
    [Build plugins](https://developers.openai.com/codex/plugins/build#manifest-fields).
*   **The MCP server is declared in four files.** `gemini-extension.json`,
    `.claude-plugin/plugin.json`, `mcp.json`, and `mcp_config.json` each declare
    `mcp_toolbox` because each harness reads a different file. Keep the four
    identical. Renovate bumps the pinned `@toolbox-sdk/server` version in all of
    them; add any new file that declares the server to `.github/renovate.json5`.
*   **The plugin version is in four files.** `gemini-extension.json`,
    `plugin.json`, `.claude-plugin/plugin.json`, and `.codex-plugin/plugin.json`
    each carry `version`, and Release Please bumps all four. Claude Code only
    updates an installed plugin when this string changes, so add any new
    manifest with a `version` to `extra-files` in `release-please-config.json`.
    See [Plugin loading](https://code.claude.com/docs/en/plugins/loading).

### Running from Local Source

The core logic for this extension is handled by the `@toolbox-sdk/server` npm
package, which each manifest runs with `npx`. The development process involves
installing the extension locally into the Gemini CLI to test changes. To test in
Claude Code or Codex, see
[Testing in Other Harnesses](#testing-in-other-harnesses).

1.  **Clone the Repository:**

    ```bash
    git clone https://github.com/gemini-cli-extensions/mcp-toolbox.git
    cd mcp-toolbox
    ```

2.  **No binary to download.** The manifests run the server with
    `npx -y @toolbox-sdk/server@<version> --stdio`, so `npx` fetches it on first
    use. You need Node.js on your path and nothing else. The pinned version is
    repeated in every manifest that declares the server, and Renovate bumps all
    of them in one PR.

3.  **Link the Extension Locally:** Use the Gemini CLI to install the
    extension from your local directory.

    ```bash
    gemini extensions link .
    ```
    The CLI will prompt you to confirm the linking. Accept it to proceed.

4.  **Testing Changes:** After linking, start the Gemini CLI (`gemini`).
    You can now interact with the `mcp-toolbox` tools to manually test your changes
    against your connected database.

### Testing in Other Harnesses

The steps above use the Gemini CLI. To test the same working tree in Claude
Code or Codex:

*   **Claude Code:** Load the plugin for a single session:

    ```bash
    claude --plugin-dir .
    ```

    Or install it through the repository's own marketplace, the same way users
    do:

    ```bash
    claude plugin marketplace add ./
    claude plugin install mcp-toolbox-devkit@mcp-toolbox-devkit-marketplace
    ```

    A marketplace added from a local directory loads the plugin in place, so
    your edits apply at the next session or after `/reload-plugins`. See
    [Plugin loading](https://code.claude.com/docs/en/plugins/loading). Run
    `/mcp` to check that `mcp_toolbox` is connected.

*   **Codex:** Codex also reads `.claude-plugin/marketplace.json`. Add the
    repository as a local marketplace and confirm that Codex resolves it:

    ```bash
    codex plugin marketplace add ./
    codex plugin marketplace list
    ```

    Then install `mcp-toolbox-devkit` from the Plugins Directory. The Codex
    docs route local installs through the ChatGPT desktop app. See
    [Build plugins](https://developers.openai.com/codex/plugins/build#add-a-marketplace-from-the-cli).

## Testing

### Automated Presubmit Checks

A GitHub Actions workflow (`.github/workflows/presubmit-tests.yml`) is triggered
for every pull request. This workflow primarily verifies that the extension can
be successfully installed by the Gemini CLI.

Currently, there are no automated unit or integration test suites
within this repository. All functional testing must be performed manually. All tools
are currently tested in the [MCP Toolbox GitHub](https://github.com/googleapis/mcp-toolbox).

### Other GitHub Checks

*   **License Header Check:** A workflow ensures all necessary files contain the
    proper license header.
*   **Conventional Commits:** This repository uses
    [Release Please](https://github.com/googleapis/release-please) to manage
    releases. Your commit messages must adhere to the
    [Conventional Commits](https://www.conventionalcommits.org/) specification.
*   **Dependency Updates:** [Renovate](https://github.com/apps/forking-renovate)
    is configured to automatically create pull requests for dependency updates.

## Building the Extension

There is no build step. The repository holds every file a harness needs: the
manifests, `MCP-TOOLBOX.md`, and `skills/`. The MCP server is not bundled. Each
manifest runs it with `npx -y @toolbox-sdk/server@<version> --stdio`.

Harnesses install this plugin straight from the repository. Claude Code and
Codex clone it, and Antigravity copies a local directory, so a binary shipped
only inside a release archive would never reach three of the four harnesses.
That is why the server runs from npm rather than from a packaged binary.

## Maintainer Information

### Team

The primary maintainers for this repository are defined in the
[`.github/CODEOWNERS`](.github/CODEOWNERS) file:

*   `@gemini-cli-extensions/senseai-eco`
*   `@gemini-cli-extensions/mcp-toolbox-maintainers`

### Releasing

The release process is automated using `release-please`. It consists of an automated changelog preparation step followed by the manual merging of a Release PR.

#### Automated Changelog Enrichment

Before a Release PR is even created, a special workflow automatically mirrors
relevant changelogs from the core `googleapis/mcp-toolbox` dependency. This
ensures that the release notes for this extension accurately reflect important
upstream changes.

The process is handled by the [`mirror-changelog.yml`](.github/workflows/mirror-changelog.yml) workflow:

1. **Trigger:** The workflow runs automatically on pull requests created by
   Renovate for `toolbox` version updates.
2. **Parsing:** It reads the detailed release notes that Renovate includes in
   the PR body.
3. **Changelog Injection:** The script formats the filtered entries as
   conventional commits and injects them into the PR body within a
   `BEGIN_COMMIT_OVERRIDE` block.
4. **Release Please:** When the main Release PR is created, `release-please`
   reads this override block instead of the standard `chore(deps): ...` commit
   message, effectively mirroring the filtered upstream changelog into this
   project's release notes.

> **Note for Maintainers:** The filtering script is an automation aid, but it
> may occasionally produce "false positives" (e.g., an internal logging change
> that happens to contain the keyword). Before merging a `toolbox` dependency
> PR, maintainers must **review the generated `BEGIN_COMMIT_OVERRIDE` block**
> and manually delete any lines that are not relevant to the end-users of this
> extension. The curated override block is the final source of truth for the
> release changelog.

#### Release Process

1.  **Release PR:** When commits with conventional commit headers (e.g., `feat:`,
    `fix:`) are merged into the `main` branch, `release-please` will
    automatically create or update a "Release PR".
2.  **Merge Release PR:** A maintainer approves and merges the Release PR. This
    action triggers `release-please` to create a new GitHub tag and a
    corresponding GitHub Release.
3.  **No asset step.** The release carries no attached archives. Every harness
    installs from the repository at the tag.
