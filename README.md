# Gemini CLI Extension - MCP Toolbox

Develop and query your custom tools using the power of natural language, directly
from your command line through [MCP
Toolbox](https://github.com/googleapis/genai-toolbox). Go from an idea to a
running, invocable tool in minutes, without ever leaving your terminal.

Learn more about [Gemini CLI Extensions](https://github.com/google-gemini/gemini-cli/blob/main/docs/extension.md).

## Why Use MCP Toolbox Extensions?

* **Simplified development**: Integrate tools to your agent in less than 10 lines of code, reuse tools between multiple agents or frameworks, and deploy new versions of tools more easily.
* **Better performance**: Best practices such as connection pooling, authentication, and more.
* **Enhanced security**: Integrated auth for more secure access to your data
* **End-to-end observability**: Out of the box metrics and tracing with built-in
  support for OpenTelemetry.

## Prerequisites

Before you begin, ensure you have the following:

*   [Gemini CLI](https://github.com/google-gemini/gemini-cli) installed.

## Installation

```bash
gemini extensions install github.com/gemini-cli-extensions/mcp-toolbox.git
```

## Usage

Add your `tools.yaml` configuration file for MCP Toolbox to the directory you
are running Gemini CLI.