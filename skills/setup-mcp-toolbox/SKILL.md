---
name: setup-mcp-toolbox
description: A skill dedicated to downloading, setting up, and running the MCP Toolbox server. Focuses on binary delivery, OS-specific environment setup, and running the server instance.
---

## Setup Toolbox Instructions

You are an expert at installing and bootstrapping the MCP Toolbox. When this skill is active, you MUST follow these phases in order:

### Phase 1: Discovery & Clarification
Determine the user's OS and preferred method. Use the latest version from the [releases page](https://github.com/googleapis/genai-toolbox/releases) (defaulting to `v0.27.0`).
Confirm users preferred installation method. Provide recommendation based on users setup.
* **The "Ambiguity Check"**: If a user asks to "Setup toolbox," you must prompt: *"I can set this up in three ways. Would you prefer a Local Binary (fastest), a Docker Container (isolated), or a Go SDK scaffold (for development)?"*

### Phase 2: Environment Probing & Download
Once a method is chosen, verify that the necessary environment is available. If a prerequisite is missing, provide instructions to install it:
* **For Homebrew**: Run `brew --version`. If missing, install via `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`.
* **For Docker**: Run `docker --version`. If missing, install [Docker Desktop](https://www.docker.com/products/docker-desktop/).
* **For Go**: Run `go version`. If missing, install via [go.dev/doc/install](https://go.dev/doc/install).
* **For NPX**: Ensure Node.js is installed (`node -v`).
* **For Binary**: No additional prerequisites (other than `curl`).

If the user chose **Local Binary**, intelligently identify the OS/Architecture and execute the download. Use the latest version from the releases page (defaulting to `v0.28.0`):
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
* **NPX (Quickstart)**: For experimentation, run `npx @toolbox-sdk/server --tools-file tools.yaml`.
* **Homebrew (macOS/Linux)**: Execute `brew install mcp-toolbox`.
* **Docker**: Execute `docker pull us-central1-docker.pkg.dev/database-toolbox/toolbox/toolbox:$VERSION`.
* **Source (Go)**: Run `go install github.com/googleapis/genai-toolbox@v$VERSION`.

### Phase 3: Minimal Configuration
Suggest using prebuilt servers for supported databases (Postgres, MySQL, Neo4j, Looker, etc.) which allow running without a `tools.yaml`. 
* **Confirm with the user** before proceeding with this method. 
* If confirmed, connection details are provided via environment variables, and you will run: `./toolbox --prebuilt [database] --stdio`
* **Otherwise**, generate a basic `tools.yaml` skeleton to allow the server to start without crashing. 

If `tools.yaml` needs to be configured, populate fields after getting values from user.
1. **Database Selection**: Ask the user which database they plan to use (e.g., PostgreSQL, MySQL, Spanner, etc.).
2. **Environment Variables**: Advise using `${ENV_NAME}` or `${ENV_NAME:default}` for secrets like passwords and ports to avoid hardcoding.
3. **Guidance**: Provide instructions on defining `sources` (connection details), `tools` (SQL statements and parameters), and `toolsets` (groups of tools).
4. **Prompts**: Explain how to define `kind: prompts` to create templates with structured messages and instructions (arguments) for LLM interaction.
5. **AuthServices**: For tools requiring authentication, explain `kind: authServices` (e.g., `type: google`) for Authorized Invocations or Authenticated Parameters.
6. **Specialized Skills**: Advise the user to activate a specialized database skill (e.g., `config-mcp-toolbox-postgres`) for detailed database configuration, authentication, and connection troubleshooting.

### Phase 4: Execution
Start the MCP server via the appropriate command (e.g., `./toolbox run` or `./toolbox serve`), verifying standard output for a successful initialization signal.
* **Dynamic Reloading**: Enabled by default. To disable it for static environments, append the `--no-reload` flag.
* **Stopping**: Use `ctrl+c` to terminate processes.

### Phase 5: Gemini CLI Integration (Optional)
Ask the user: *"Would you like to integrate the Toolbox with your Gemini CLI settings?"*
Upon confirmation, provide the following JSON for them to append to `~/.gemini/settings.json`:

```json
{
  "mcpServers": {
    "toolbox": {
      "command": "mcp-toolbox",
      "args": ["run"]
    }
  }
}
If Gemini CLI is already running, guide them to use `/mcp refresh`.

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
