---
name: setup-mcp-toolbox
description: A skill dedicated to downloading, setting up, and running the MCP Toolbox server. Focuses on binary delivery, OS-specific environment setup, and running the server instance using prebuilt configurations.
---

## Setup Toolbox Instructions

You are an expert at installing and bootstrapping the MCP Toolbox. When this skill is active, you MUST follow these phases in order:

### Phase 1: Discovery & Clarification
Determine the user's OS and preferred method. Use the latest version from the [releases page](https://github.com/googleapis/genai-toolbox/releases) (defaulting to `v0.28.0`).
Confirm the user's preferred installation method. Provide recommendations based on the user's setup.
* **The "Ambiguity Check"**: If a user asks to "Setup toolbox," you must prompt: *"I can set this up in three ways. Would you prefer a Local Binary (fastest), a Docker Container (isolated), or a Go SDK scaffold (for development)?"*

### Phase 2: Environment Probing & Download
Once a method is chosen, verify that the necessary environment is available. If a prerequisite is missing, provide instructions to install it:
* **For Homebrew**: Run `brew --version`. If missing, install via `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`.
* **For Docker**: Run `docker --version`. If missing, install [Docker Desktop](https://www.docker.com/products/docker-desktop/).
* **For Go**: Run `go version`. If missing, install via [go.dev/doc/install](https://go.dev/doc/install).
* **For NPX**: Ensure Node.js is installed (`node -v`).
* **For Binary**: No additional prerequisites (other than `curl`).

If the user chose **Local Binary**, intelligently identify the OS/Architecture and execute the download. Use the latest version from the releases page:

#### A. Binary Installation
* **Linux (AMD64)**: 
    `curl -L -o toolbox https://storage.googleapis.com/genai-toolbox/v$VERSION/linux/amd64/toolbox && chmod +x toolbox`
* **macOS (Apple Silicon)**: 
    `curl -L -o toolbox https://storage.googleapis.com/genai-toolbox/v$VERSION/darwin/arm64/toolbox && chmod +x toolbox`
* **macOS (Intel)**: 
    `curl -L -o toolbox https://storage.googleapis.com/genai-toolbox/v$VERSION/darwin/amd64/toolbox && chmod +x toolbox`
* **Windows (PowerShell)**: 
    `curl.exe -o toolbox.exe "https://storage.googleapis.com/genai-toolbox/v$VERSION/windows/amd64/toolbox.exe"`

#### B. Alternative Methods
* **NPX (Quickstart)**: For experimentation, run `npx @toolbox-sdk/server --prebuilt [database]`.
* **Homebrew (macOS/Linux)**: Execute `brew install mcp-toolbox`.
* **Docker**: Execute `docker pull us-central1-docker.pkg.dev/database-toolbox/toolbox/toolbox:$VERSION`.
* **Source (Go)**: Run `go install github.com/googleapis/genai-toolbox@v$VERSION`.

### Phase 3: No Configuration (Prebuilt Servers Only)
This core setup skill STRICTLY utilizes prebuilt servers to establish a baseline running state. **Do NOT generate a `tools.yaml` file.**

1. **Database Selection**: Ask the user which supported database they plan to connect to (e.g., Postgres, MySQL, Neo4j, Looker, etc.).
2. **Environment Variables**: Provide detailed instructions to the user to provide connection details via environment variables before running the server (e.g., `POSTGRES_USER`, `POSTGRES_PASSWORD`).
3. **Specialized Skills for Customization**: Explicitly advise the user: *"This setup uses a prebuilt server for immediate connectivity. If you need to write custom SQL tools, configure authentication (AuthServices), or define custom prompts, please let me know so I can activate the specialized database skill (e.g., `config-mcp-toolbox-postgres`) to help you generate a custom `tools.yaml`."*

### Phase 4: Execution
Start the MCP server using the prebuilt flag and verify standard output for a successful initialization signal.
* **Command**: `./toolbox --prebuilt [database] --stdio`
* **Dynamic Reloading**: Enabled by default. To disable it for static environments, append the `--no-reload` flag.
* **Stopping**: Instruct the user to use `ctrl+c` (SIGINT) to terminate the process.

### Phase 5: Gemini CLI Integration (Optional)
Ask the user: *"Would you like to integrate the Toolbox with your Gemini CLI settings?"*
Upon confirmation, provide the following JSON for them to append to `~/.gemini/settings.json`:

```json
{
  "mcpServers": {
    "toolbox": {
      "command": "mcp-toolbox",
      "args": ["--prebuilt", "[database]", "--stdio"]
    }
  }
}
```

### Phase 6. Launching Toolbox UI
To test tools and toolsets interactively (including authorized parameters):
* Execute: `./toolbox --ui`
* Direct the user to the local web interface (typically `http://127.0.0.1:5000/`) to interact with the UI.

### Phase 7. Verification, Testing & Telemetry
* **Logging**: Customize output with `--log-level [debug|info|warn|error]` and `--logging-format [standard|json]`.
* **Telemetry**: Toolbox supports OpenTelemetry. Enable exporting to Google Cloud (`--telemetry-gcp`) or OTLP (`--telemetry-otlp="endpoint"`).
* **MCP Inspector**: Use `npx @modelcontextprotocol/inspector` to test connectivity (SSE, Streamable HTTP, or STDIO) and tools interactively.   
* **Help**: Run `./toolbox help` for a full list of available flags and commands.
* **Verification**: Check that the server responds at `http://127.0.0.1:5000/`.
