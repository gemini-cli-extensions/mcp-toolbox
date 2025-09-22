# Gemini CLI Extension - MCP Toolbox

> [!NOTE]
> This extension is currently in beta (pre-v1.0), and may see breaking changes until the first stable release (v1.0).

Develop and query your custom tools using the power of natural language, directly
from your command line through [MCP
Toolbox](https://github.com/googleapis/genai-toolbox). Go from an idea to a
running, invocable tool in minutes, without ever leaving your terminal.

Learn more about [Gemini CLI Extensions](https://github.com/google-gemini/gemini-cli/blob/main/docs/extension.md).

## Why Use the MCP Toolbox Extension?

* **Reliable Custom Servers:** Quickly create a **custom MCP server** with tools designed to reliably return accurate results. This saves significant development time and cost by ensuring your agent gets precise data without extensive guidance or fine-tuning.
* **Enterprise Data Awareness:** Instantly upgrade your developer environment by providing your agents with **enterprise-grade data awareness**. Connect your AI systems directly to your data sources for smarter, more relevant operations.
* **Accelerated Agent Development:** Fast-track your AI project by easily testing and validating tool usage with a **pre-built agent environment**.

## Prerequisites

Before you begin, ensure you have the following:

*   [Gemini CLI](https://github.com/google-gemini/gemini-cli) installed with version +v0.6.0.
*   Any required APIs and permissions for connecting to your database.

## Installation

```bash
gemini extensions install github.com/gemini-cli-extensions/mcp-toolbox
```

## Configuration

* Add your [`tools.yaml` configuration file](https://googleapis.github.io/genai-toolbox/getting-started/configure/) to the directory you
are running Gemini CLI.

Ensure [Application Default Credentials](https://cloud.google.com/docs/authentication/gcloud) are available in your environment if connecting to Google Cloud services.

## Usage

Interact with your custom tools using natural language.

## Additional Extensions

Find additional extensions to support your entire software development lifecycle at [github.com/gemini-cli-extensions](https://github.com/gemini-cli-extensions), including a generic [PostgreSQL extension](https://github.com/gemini-cli-extensions/postgres).

## Troubleshooting

* "cannot execute binary file": Ensure the correct binary for your OS/Architecture has been downloaded. See [Installing the server](https://googleapis.github.io/genai-toolbox/getting-started/introduction/#installing-the-server) for more information.
