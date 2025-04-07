# narsil-mcp

> The blazing-fast, privacy-first MCP server for deep code intelligence

[![License](https://img.shields.io/badge/License-MIT%20OR%20Apache--2.0-blue.svg)](LICENSE-MIT)
[![Rust](https://img.shields.io/badge/rust-1.70%2B-orange.svg)](https://www.rust-lang.org)
[![Tests](https://img.shields.io/badge/tests-passing-brightgreen.svg)](https://github.com/postrv/narsil-mcp)
[![MCP](https://img.shields.io/badge/MCP-compatible-blue.svg)](https://modelcontextprotocol.io)

A Rust-powered MCP (Model Context Protocol) server providing AI assistants with deep code understanding through 90 specialized tools.

## Why narsil-mcp?

| Feature | narsil-mcp | XRAY | Serena | GitHub MCP |
|---------|------------|------|--------|------------|
| **Languages** | 32 | 4 | 30+ (LSP) | N/A |
| **Neural Search** | Yes | No | No | No |
| **Taint Analysis** | Yes | No | No | No |
| **SBOM/Licenses** | Yes | No | No | Partial |
| **Offline/Local** | Yes | Yes | Yes | No |
| **WASM/Browser** | Yes | No | No | No |
| **Call Graphs** | Yes | Partial | No | No |
| **Type Inference** | Yes | No | No | No |

## Key Features

- **Code Intelligence** - Symbol extraction, semantic search, call graph analysis
- **Neural Semantic Search** - Find similar code using embeddings (Voyage AI, OpenAI)
- **Security Analysis** - Taint analysis, vulnerability scanning, OWASP/CWE coverage
- **Supply Chain Security** - SBOM generation, dependency auditing, license compliance
- **Advanced Analysis** - Control flow graphs, data flow analysis, dead code detection

### Why Choose narsil-mcp?

- **Written in Rust** - Blazingly fast, memory-safe, single binary (~30MB)
- **Tree-sitter powered** - Accurate, incremental parsing for 32 languages
- **Zero config** - Point at repos and go
- **MCP compliant** - Works with Claude, Cursor, VS Code Copilot, Zed, and any MCP client
- **Privacy-first** - Fully local, no data leaves your machine
- **Parallel indexing** - Uses all cores via Rayon
- **Smart excerpts** - Expands to complete syntactic scopes
- **Security-first** - Built-in vulnerability detection and taint analysis
- **Neural embeddings** - Optional semantic search with Voyage AI or OpenAI
- **WASM support** - Run in browser with WebAssembly build
- **Real-time streaming** - Results as indexing progresses for large repos

## Supported Languages

| Language | Extensions | Symbols Extracted |
|----------|------------|-------------------|
| Rust | `.rs` | functions, structs, enums, traits, impls, mods |
| Python | `.py`, `.pyi` | functions, classes |
| JavaScript | `.js`, `.jsx`, `.mjs` | functions, classes, methods, variables |
| TypeScript | `.ts`, `.tsx` | functions, classes, interfaces, types, enums |
| Go | `.go` | functions, methods, types |
| C | `.c`, `.h` | functions, structs, enums, typedefs |
| C++ | `.cpp`, `.cc`, `.hpp` | functions, classes, structs, namespaces |
| Java | `.java` | methods, classes, interfaces, enums |
| C# | `.cs` | methods, classes, interfaces, structs, enums, delegates, namespaces |
| **Bash** | `.sh`, `.bash`, `.zsh` | functions, variables |
| **Ruby** | `.rb`, `.rake`, `.gemspec` | methods, classes, modules |
| **Kotlin** | `.kt`, `.kts` | functions, classes, objects, interfaces |
| **PHP** | `.php`, `.phtml` | functions, methods, classes, interfaces, traits |
| **Swift** | `.swift` | classes, structs, enums, protocols, functions |
| **Verilog/SystemVerilog** | `.v`, `.vh`, `.sv`, `.svh` | modules, tasks, functions, interfaces, classes |
| **Scala** | `.scala`, `.sc` | classes, objects, traits, functions, vals |
| **Lua** | `.lua` | functions, methods |
| **Haskell** | `.hs`, `.lhs` | functions, data types, type classes |
| **Elixir** | `.ex`, `.exs` | modules, functions |
| **Clojure** | `.clj`, `.cljs`, `.cljc`, `.edn` | lists (basic AST) |
| **Dart** | `.dart` | functions, classes, methods |
| **Julia** | `.jl` | functions, modules, structs |
| **R** | `.R`, `.r`, `.Rmd` | functions |
| **Perl** | `.pl`, `.pm`, `.t` | functions, packages |
| **Zig** | `.zig` | functions, variables |
| **Erlang** | `.erl`, `.hrl` | functions, modules, records |
| **Elm** | `.elm` | functions, types |
| **Fortran** | `.f90`, `.f95`, `.f03`, `.f08`, `.f`, `.for`, `.fpp` | programs, subroutines, functions, modules |
| **PowerShell** | `.ps1`, `.psm1`, `.psd1` | functions, classes, enums |
| **Nix** | `.nix` | bindings |
| **Groovy** | `.groovy`, `.gradle` | methods, classes, interfaces, enums, functions |

## Installation

### Via Package Managers (Recommended)

**macOS / Linux (Homebrew):**
```bash
brew tap postrv/narsil
brew install narsil-mcp
```

**Windows (Scoop):**
```powershell
scoop bucket add narsil https://github.com/postrv/scoop-narsil
scoop install narsil-mcp
```

**Rust/Cargo (all platforms):**
```bash
cargo install narsil-mcp
```

**Node.js/npm (all platforms):**
```bash
npm install -g narsil-mcp
# or
yarn global add narsil-mcp
# or
pnpm add -g narsil-mcp
```

**Nix:**
```bash
# Run directly without installing
nix run github:postrv/narsil-mcp -- --repos ./my-project

# Install to profile
nix profile install github:postrv/narsil-mcp

# With web visualization frontend
nix profile install github:postrv/narsil-mcp#with-frontend

# Development shell
nix develop github:postrv/narsil-mcp
```

### One-Click Install Script

**macOS / Linux:**
```bash
curl -fsSL https://raw.githubusercontent.com/postrv/narsil-mcp/main/install.sh | bash
```

**Windows (PowerShell):**
```powershell
irm https://raw.githubusercontent.com/postrv/narsil-mcp/main/install.ps1 | iex
```

**Windows (Git Bash / MSYS2):**
```bash
curl -fsSL https://raw.githubusercontent.com/postrv/narsil-mcp/main/install.sh | bash
```

> **Note for Windows users:** The PowerShell installer provides better error messages and native Windows integration. It will automatically configure your PATH and check for required build tools if building from source.

### From Source

**Prerequisites:**
- Current stable Rust (this release was verified with Rust 1.98 and 1.99)
- On Windows: [Visual Studio Build Tools](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2022) with "Desktop development with C++"

```bash
# Clone and build
git clone git@github.com:postrv/narsil-mcp.git
cd narsil-mcp
cargo build --release

# Binary will be at:
# - macOS/Linux: target/release/narsil-mcp
# - Windows: target/release/narsil-mcp.exe
```

### Feature Builds

narsil-mcp supports different feature sets for different use cases:

```bash
# Default build - native MCP server (~30MB)
cargo build --release

# With RDF knowledge graph and CCG tools (~35MB) - SPARQL queries, Code Context Graph
cargo build --release --features graph

# With neural vector search (~32MB) - adds TF-IDF similarity
cargo build --release --features neural

# With ONNX model support (~50MB) - adds local neural embeddings
cargo build --release --features neural-onnx

# With embedded visualization frontend (~31MB)
cargo build --release --features frontend

# Full-featured build with graph + frontend (~40MB)
cargo build --release --features graph,frontend

# Experimental browser/WASM source build (not release-qualified)
cargo build --release --target wasm32-unknown-unknown --no-default-features --features wasm
```

| Feature | Description | Size |
|---------|-------------|------|
| `native` (default) | Full MCP server with all tools | ~30MB |
| `graph` | + RDF knowledge graph, SPARQL, CCG tools | ~35MB |
| `frontend` | + Embedded visualization web UI | ~31MB |
| `neural` | + TF-IDF vector search, API embeddings | ~32MB |
| `neural-onnx` | + Local ONNX model inference | ~50MB |
| `wasm` | Experimental browser source build (no file system, git) | Not release-qualified |

> **Important:** The `--graph` CLI flag requires the binary to be built with `--features graph`. If you pass `--graph` to a binary built without this feature, you'll see a warning and SPARQL/CCG tools won't be available. See [Troubleshooting](#graph-feature-not-working) below.

> **For detailed installation instructions, troubleshooting, and platform-specific guides**, see [docs/INSTALL.md](docs/INSTALL.md).

## Usage

### Basic Usage

**macOS / Linux:**
```bash
# Index a single repository
narsil-mcp --repos /path/to/your/project

# Index multiple repositories
narsil-mcp --repos ~/projects/project1 --repos ~/projects/project2

# Enable verbose logging
narsil-mcp --repos /path/to/project --verbose

# Force re-index on startup
narsil-mcp --repos /path/to/project --reindex
```

**Windows (PowerShell / CMD):**
```powershell
# Index a single repository
narsil-mcp --repos C:\Users\YourName\Projects\my-project

# Index multiple repositories
narsil-mcp --repos C:\Projects\project1 --repos C:\Projects\project2

# Enable verbose logging
narsil-mcp --repos C:\Projects\my-project --verbose

# Force re-index on startup
narsil-mcp --repos C:\Projects\my-project --reindex
```

### Full Feature Set

```bash
narsil-mcp \
  --repos ~/projects/my-app \
  --git \           # Enable git blame, history, contributors
  --call-graph \    # Enable function call analysis
  --persist \       # Save index to disk for fast startup
  --watch \         # Auto-reindex on file changes
  --lsp \           # Enable LSP for hover, go-to-definition
  --streaming \     # Stream large result sets
  --remote \        # Enable GitHub remote repo support
  --neural \        # Enable neural semantic embeddings
  --neural-backend api \  # Backend: "api" (Voyage/OpenAI) or "onnx"
  --neural-model voyage-code-2 \  # Model to use
  --neural-dimension 3072 \  # Override embedding dimensions (auto-detected per model)
  --graph           # Enable SPARQL/RDF knowledge graph and CCG tools (requires --features graph build)
```

> **Note about `--graph`:** This flag enables SPARQL queries and Code Context Graph (CCG) tools, but **only if the binary was built with `--features graph`**. The default binary does not include this feature. If you need SPARQL/CCG capabilities, build from source with:
> ```bash
> cargo build --release --features graph
> ```
> If you pass `--graph` to a binary without the feature, you'll see a warning at startup and the server will continue without SPARQL/CCG tools.

**Note:** Neural embeddings require an API key (or custom endpoint). The easiest way to set this up is with the interactive wizard:

```bash
# Run the neural API key setup wizard
narsil-mcp config init --neural
```

The wizard will:
- Detect your editor (Claude Desktop, Claude Code, Zed, VS Code, JetBrains)
- Prompt for your API provider (Voyage AI, OpenAI, or custom)
- Validate your API key
- Automatically add it to your editor's MCP config

Alternatively, you can manually set one of these environment variables:
- `EMBEDDING_API_KEY` - Generic API key for any provider
- `VOYAGE_API_KEY` - Voyage AI specific API key
- `OPENAI_API_KEY` - OpenAI specific API key
- `EMBEDDING_SERVER_ENDPOINT` - Custom embedding API endpoint URL (optional, allows using self-hosted models)

### Configuration

**v1.1.0+ introduces optional configuration** for fine-grained control over tools and performance. **All existing usage continues to work** - configuration is completely optional!

#### Quick Start

```bash
# Generate default config interactively
narsil-mcp config init

# List available tools
narsil-mcp tools list

# Apply a preset via CLI
narsil-mcp --repos ~/project --preset minimal
```

#### Automatic Editor Detection

narsil-mcp detects your editor and applies an optimal preset automatically:

| Editor | Preset | Tools | Context Tokens | Why |
|--------|--------|-------|----------------|-----|
| **Zed** | Minimal | 26 | ~4,686 | Fast startup, minimal context |
| **VS Code** | Balanced | 51 | ~8,948 | Good feature balance |
| **Claude Desktop** | Full | 90 | ~12,001 | Maximum capabilities |

**Token Savings:**
- **Minimal preset:** 61% fewer tokens vs Full
- **Balanced preset:** 25% fewer tokens vs Full

#### Presets

Choose a preset based on your use case:

```bash
# Minimal - Fast, lightweight (Zed, Cursor)
narsil-mcp --repos ~/project --preset minimal

# Balanced - Good defaults (VS Code, IntelliJ)
narsil-mcp --repos ~/project --preset balanced --git --call-graph

# Full - All features (Claude Desktop, comprehensive analysis)
narsil-mcp --repos ~/project --preset full --git --call-graph

# Security-focused - Security and supply chain tools
narsil-mcp --repos ~/project --preset security-focused
```

#### Configuration Files

**User config** (`~/.config/narsil-mcp/config.yaml`):

```yaml
version: "1.0"
preset: "balanced"

tools:
  # Disable slow tools
  overrides:
    neural_search:
      enabled: false
      reason: "Too slow for interactive use"

performance:
  max_tool_count: 50  # Limit total tools
```

**Project config** (`.narsil.yaml` in repo root):

```yaml
version: "1.0"
preset: "security-focused"  # Override user preset

tools:
  categories:
    Security:
      enabled: true
    SupplyChain:
      enabled: true
```

**Named repository profiles** are useful for multi-repo workspaces:

```yaml
version: "1.0"
profiles:
  platform:
    repos:
      - ~/src/api
      - ~/src/web
    git: true
    call_graph: true
    persist: true
    preset: balanced
```

```bash
narsil-mcp --profile platform
narsil-mcp config profiles
```

**Priority:** CLI flags > Environment vars > Project config > User config > Defaults

#### Environment Variables

```bash
# Select repos/profile
export NARSIL_REPOS=~/src/api,~/src/web
export NARSIL_PROFILE=platform

# Apply preset
export NARSIL_PRESET=minimal

# Enable specific categories
export NARSIL_ENABLED_CATEGORIES=Repository,Symbols,Search

# Disable specific tools
export NARSIL_DISABLED_TOOLS=neural_search,generate_sbom
```

#### CLI Commands

```bash
# View effective config
narsil-mcp config show

# Validate config file
narsil-mcp config validate ~/.config/narsil-mcp/config.yaml

# List tools by category
narsil-mcp tools list --category Search

# Search for tools
narsil-mcp tools search "git"

# Export config
narsil-mcp config export > my-config.yaml

# List named repository profiles
narsil-mcp config profiles
```

**Learn More:**
- [Configuration Guide](docs/configuration.md) - Full configuration reference
- [Installation Guide](docs/INSTALL.md) - Platform-specific installation

### Visualization Frontend

Explore call graphs, imports, symbol references, and control flow interactively in your browser.

```bash
# Build with embedded frontend
cargo build --release --features frontend

# Run with HTTP server
narsil-mcp --repos ~/project --http --call-graph
# Open http://localhost:3000
```

**Five graph views:**

| View | Description |
|------|-------------|
| **Call Graph** | Function call relationships with depth control and direction filtering |
| **Import Graph** | File-level import dependencies across the codebase |
| **Symbol Graph** | All references to a symbol, with file clustering |
| **Hybrid** | Combined call + import graph with split budget |
| **Control Flow** | Real CFG with basic blocks, branches, and loop back-edges |

**Features:**
- Interactive Cytoscape.js graphs with drag, zoom, and double-click drill-down
- Complexity metrics overlay with color coding (green/yellow/orange/red)
- Security vulnerability overlay highlighting taint sources and sinks
- Six layout algorithms (dagre, force-directed, breadthfirst, concentric, circle, grid)
- File tree sidebar with syntax-highlighted code viewer
- URL-driven state (shareable links, browser back/forward)
- Dark mode support
- Node detail panel with code excerpts and navigation to source

> **Full documentation:** See [docs/frontend.md](docs/frontend.md) for setup, API endpoints, and development mode.

### Neural Semantic Search

Find similar code using neural embeddings - even when variable names and structure differ.

```bash
# Quick setup with wizard
narsil-mcp config init --neural

# Or manually with Voyage AI
export VOYAGE_API_KEY="your-key"
narsil-mcp --repos ~/project --neural --neural-model voyage-code-2
```

Supports Voyage AI, OpenAI, custom endpoints, and local ONNX models.

> **Full documentation:** See [docs/neural-search.md](docs/neural-search.md) for setup, backends, and use cases.

### Type Inference

Built-in type inference for Python, JavaScript, and TypeScript - no mypy or tsc required.

| Tool | Description |
|------|-------------|
| `infer_types` | Get inferred types for all variables in a function |
| `check_type_errors` | Find potential type mismatches |
| `get_typed_taint_flow` | Enhanced security analysis with type info |

```python
def process(data):
    result = data.split(",")  # result: list[str]
    count = len(result)       # count: int
    return count * 2          # returns: int
```

### Forgemax Integration (Experimental)

For large-scale agentic workflows, narsil-mcp can be used through [Forgemax](https://github.com/postrv/forgemax) — a Code Mode MCP gateway that collapses all 90 tools into just 2 (`search` + `execute`), reducing tool schema overhead from ~12,000 tokens to ~1,000.

```bash
# Install Forgemax
cargo install forgemax

# Run narsil-mcp through Forgemax (uses forge.toml in repo root)
forgemax
```

The included `forge.toml` configures narsil-mcp with sensible defaults:

```toml
[servers.narsil]
command = "narsil-mcp"
args = ["--repos", ".", "--git", "--call-graph", "--persist", "--watch"]
transport = "stdio"

[sandbox]
timeout_secs = 10
max_heap_mb = 64
max_concurrent = 8
```

The LLM writes JavaScript that calls through typed proxy objects inside a sandboxed V8 isolate — credentials, file paths, and internal state never leave the host. This approach is particularly useful when working with multiple MCP servers simultaneously, as it keeps the total tool context small and predictable.

### MCP Configuration

Add narsil-mcp to your AI assistant by creating a configuration file. Here are the recommended setups:

---

**Claude Code** (`.mcp.json` in project root - Recommended):

Create `.mcp.json` in your project directory for per-project configuration:
```json
{
  "mcpServers": {
    "narsil-mcp": {
      "command": "narsil-mcp",
      "args": ["--repos", ".", "--git", "--call-graph"]
    }
  }
}
```

Then start Claude Code in your project:
```bash
cd /path/to/project
claude
```

Using `.` for `--repos` automatically indexes the current directory. Claude now has access to 90 code intelligence tools.

> **Tip**: Add `--persist --index-path .claude/cache` for faster startup on subsequent runs.

For global configuration, edit `~/.claude/settings.json` instead. See [Claude Code Integration](docs/playbooks/integrations/claude-code.md) for advanced setups.

---

**Cursor** (`.cursor/mcp.json`):
```json
{
  "mcpServers": {
    "narsil-mcp": {
      "command": "narsil-mcp",
      "args": ["--repos", ".", "--git", "--call-graph"]
    }
  }
}
```

---

**VS Code + GitHub Copilot** (`.vscode/mcp.json`):
```json
{
  "servers": {
    "narsil-mcp": {
      "command": "narsil-mcp",
      "args": ["--repos", ".", "--git", "--call-graph"]
    }
  }
}
```

> **Note for Copilot Enterprise**: MCP support requires VS Code 1.102+ and must be enabled by your organization administrator.

---

**Claude Desktop** (`claude_desktop_config.json`):
```json
{
  "mcpServers": {
    "narsil-mcp": {
      "command": "narsil-mcp",
      "args": ["--repos", "/path/to/your/projects", "--git"]
    }
  }
}
```

---

**Zed** (`settings.json` → Context Servers):
```json
{
  "context_servers": {
    "narsil-mcp": {
      "command": "narsil-mcp",
      "args": ["--repos", ".", "--git"]
    }
  }
}
```

> **Note for Zed**: narsil-mcp starts immediately and indexes in the background, preventing initialization timeouts.

---

### Claude Code Plugin

For **Claude Code** users, we provide a plugin with slash commands and a skill for effective tool usage.

**Install via Marketplace (Recommended):**
```shell
# Add the narsil-mcp marketplace
/plugin marketplace add postrv/narsil-mcp

# Install the plugin
/plugin install narsil@narsil-mcp
```

**Or install d