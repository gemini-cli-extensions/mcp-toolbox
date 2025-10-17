# DEVELOPER.md

This document provides instructions for setting up your development environment
and contributing to the MCP Toolbox Gemini CLI Extension project.

## Prerequisites

Before you begin, ensure you have the following:

1.  **Gemini CLI:** Install the Gemini CLI version v0.6.0 or above. Installation
    instructions can be found on the official Gemini CLI documentation. You can
    verify your version by running `gemini --version`.
2.  **MCP Toolbox tools.yaml:** For testing, you will need a custom tools.yaml.

## Developing the Extension

### Running from Local Source

The core logic for this extension is handled by a pre-built `toolbox` binary. The development process involves installing the extension locally into the Gemini CLI to test changes.

1.  **Clone the Repository:**

    ```bash
    git clone https://github.com/gemini-cli-extensions/mcp-toolbox.git
    cd mcp-toolbox
    ```

2.  **Download the Toolbox Binary:** The required version of the `toolbox` binary
    is specified in `toolbox_version.txt`. Download it for your platform.

    ```bash
    # Read the required version
    VERSION=$(cat toolbox_version.txt)

    # Example for macOS/amd64
    curl -L -o toolbox https://storage.googleapis.com/genai-toolbox/v$VERSION/darwin/amd64/toolbox
    chmod +x toolbox
    ```
    Adjust the URL for your operating system (`linux/amd64`, `darwin/arm64`, `windows/amd64`).

3.  **Install the Extension Locally:** Use the Gemini CLI to install the
    extension from your local directory.

    ```bash
    gemini extensions install .
    gemini extensions link .
    ```
    The CLI will prompt you to confirm the installation. Accept it to proceed.

4.  **Testing Changes:** After installation, start the Gemini CLI (`gemini`).
    You can now interact with the `mcp-toolbox` tools to manually test your changes
    against your connected database.

## Testing

### Automated Presubmit Checks

A GitHub Actions workflow (`.github/workflows/presubmit-tests.yml`) is triggered
for every pull request. This workflow primarily verifies that the extension can
be successfully installed by the Gemini CLI.

Currently, there are no automated unit or integration test suites
within this repository. All functional testing must be performed manually. All tools
are currently tested in the [MCP Toolbox GitHub](https://github.com/googleapis/genai-toolbox).

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

The "build" process for this extension involves packaging the extension's
metadata files (`gemini-extension.json`, `mcp-toolbox.md`, `LICENSE`) along with the
pre-built `toolbox` binary into platform-specific archives (`.tar.gz` or `.zip`).

This process is handled automatically by the
[`package-and-upload-assets.yml`](.github/workflows/package-and-upload-assets.yml)
GitHub Actions workflow when a new release is created. Manual building is not
required.

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
relevant changelogs from the core `googleapis/genai-toolbox` dependency. This
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
3.  **Package and Upload:** The new release triggers the
    `package-and-upload-assets.yml` workflow. This workflow builds the
    platform-specific extension archives and uploads them as assets to the
    GitHub Release.
