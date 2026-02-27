---
name: setup-mcp-toolbox
description: A skill dedicated to downloading, setting up, and running the MCP Toolbox server. Focuses on binary delivery, OS-specific environment setup, and running the server instance.
---

## Setup Toolbox Instructions

You are an expert at installing and executing the GenAI Toolbox. When this skill is active, you MUST follow these steps:

### 1. Installation Phase
Determine the user's OS and preferred method. Use the latest version from the [releases page](https://github.com/googleapis/genai-toolbox/releases) (defaulting to `v0.27.0`).
Confirm users preferred installation method. Provide recommendation based on users setup.

#### Environment Validation
Once a method is chosen, verify that the necessary environment is available. If a prerequisite is missing, provide instructions to install it:
* **For Homebrew**: Run `brew --version`. If missing, install via `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`.
* **For Docker**: Run `docker --version`. If missing, install [Docker Desktop](https://www.docker.com/products/docker-desktop/).
* **For Go**: Run `go version`. If missing, install via [go.dev/doc/install](https://go.dev/doc/install).
* **For NPX**: Ensure Node.js is installed (`node -v`).
* **For Binary**: No additional prerequisites (other than `curl`).

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

### 2. Configuration (tools.yaml)
Before running the server, the user must configure the `tools.yaml` file.
1. **Database Selection**: Ask the user which database they plan to use (e.g., PostgreSQL, MySQL, Spanner, etc.).
2. **Environment Variables**: Advise using `${ENV_NAME}` or `${ENV_NAME:default}` for secrets like passwords and ports to avoid hardcoding.
3. **Guidance**: Provide instructions on defining `sources` (connection details), `tools` (SQL statements and parameters), and `toolsets` (groups of tools).
4. **Prompts**: Explain how to define `kind: prompts` to create templates with structured messages and instructions (arguments) for LLM interaction.
5. **AuthServices**: For tools requiring authentication, explain `kind: authServices` (e.g., `type: google`) for Authorized Invocations or Authenticated Parameters.
6. **Specialized Skills**: For more complex configurations, recommend the user activate a specialized database skill if available (e.g., `setup-mcp-postgresql`) to get expert help with the `tools.yaml` structure.

### 3. Running and Invoking
Once the binary is available and the `tools.yaml` is configured, guide the user through execution:

* **Standard Server**: `./toolbox --tools-file "tools.yaml"`
    *(Note: If installed via Homebrew, simply use `toolbox` without the `./`)*
* **Prebuilt Servers (Recommended)**: Suggest using prebuilt servers for supported databases (Postgres, MySQL, Neo4j, Looker, etc.) which allow running without a `tools.yaml`. **Confirm with the user** before proceeding with this method. If confirmed, connection details are provided via environment variables:
    `./toolbox --prebuilt [database] --stdio`
* **CLI Invocation**: For ephemeral runs or debugging, use `./toolbox [source] invoke [tool-name] '[json-params]'`.
* **Dynamic Reloading**: Enabled by default. To disable it, add the `--disable-reload` flag.
* **Stopping**: Use `ctrl+c` to terminate processes.

### 4. Gemini CLI Integration (Optional)
**Important**: Ask the user if they want to integrate the Toolbox MCP server with their Gemini CLI. If they confirm:
1. Update `~/.gemini/settings.json` with the following:
   ```json
   {
     "mcpServers": {
       "MCPToolbox": { "httpUrl": "http://localhost:5000/mcp" }
     },
     "mcp": { "allowed": ["MCPToolbox"] }
   }
   ```
2. If Gemini CLI is already running, guide them to use `/mcp refresh`.

### 5. Launching Toolbox UI
To test tools and toolsets interactively (including authorized parameters):
* Execute: `./toolbox --ui`
* Direct the user to the local web interface (typically `http://127.0.0.1:5000/`) to interact with the UI.

### 6. Verification, Testing & Telemetry
* **Logging**: Customize output with `--log-level [debug|info|warn|error]` and `--logging-format [standard|json]`.
* **Telemetry**: Toolbox supports OpenTelemetry. Enable exporting to Google Cloud (`--telemetry-gcp`) or OTLP (`--telemetry-otlp="endpoint"`).
* **MCP Inspector**: Use `npx @modelcontextprotocol/inspector` to test connectivity (SSE, Streamable HTTP, or STDIO) and tools interactively.   
* **Help**: Run `./toolbox help` for a full list of available flags and commands.
* **Verification**: Check that the server responds at `http://127.0.0.1:5000/`.

### 7. Deployment Options
When the user is ready for production, guide them through deployment:
* **Cloud Run**: Best for serverless. Requires uploading `tools.yaml` to Secret Manager and deploying with `--set-secrets`.
* **GKE (Kubernetes)**: Best for complex orchestrations. Requires GSA/KSA binding and mounting `tools.yaml` as a secret.
* **Docker Compose**: Best for local multi-container setups. Define a `toolbox` service and link it to your database container.
