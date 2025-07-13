# 🚀 OpenRouter CLI

> **A powerful terminal-based AI assistant for software development**

OpenRouter CLI is a terminal-based AI assistant designed specifically for software developers. It combines the power of multiple AI models with ultra-fast native filesystem tools, providing an interactive chat interface that understands your codebase and helps you build, debug, and analyze code directly from the terminal.

## ✨ Key Features

### 🤖 **Multi-Model AI Integration**
- **Multiple AI Providers**: OpenRouter, OpenAI, Anthropic, Gemini, etc.
- **Model Switching**: Switch between GPT-4, Claude, Gemini, and more mid-conversation
- **Reasoning Modes**: Support for low/medium/high reasoning effort on compatible models
- **Context-Aware**: Automatically loads project context from `.buddyrules`, `.cursorrules`, `CLAUDE.md`, etc.

### ⚡ **Ultra-Fast Native Filesystem Tools**
- **14 Native Tools**: 5-10x faster than traditional MCP implementations
- **File Operations**: Read, write, modify, delete, copy, move files with advanced safety checks
- **Directory Management**: List, create, tree view, recursive operations
- **Search & Analysis**: Content search, file pattern matching, code analysis
- **Permission System**: Comprehensive security with path allowlists and audit logging

### 🎨 **Professional Terminal UI**
- **Beautiful Interface**: Modern TUI with syntax highlighting and themes
- **Keyboard Shortcuts**: Vim-like navigation and productivity shortcuts
- **Session Management**: Multiple conversations with history persistence
- **File Browser**: Integrated file picker and attachment system
- **Real-time Updates**: Live status indicators and progress feedback

### 🔧 **Advanced Development Features**
- **LSP Integration**: Language Server Protocol support for intelligent code assistance
- **Code Generation**: AI-powered code creation and modification
- **Diff Visualization**: Beautiful side-by-side code comparisons
- **RAG System**: Retrieval-Augmented Generation for codebase understanding
- **Smart Editing**: Context-aware code modifications and refactoring

## 🚀 Quick Start

### Installation

#### Download Binaries
Visit our [releases page](https://github.com/knoxai/openrouter-cli/releases) and download the appropriate binary for your platform.

### 1. Choose Your Binary

Select the appropriate binary for your platform:

```bash
# For macOS (Intel)
./dist/or-darwin-amd64

# For macOS (Apple Silicon)
./dist/or-darwin-arm64

# For Linux (Intel/AMD)
./dist/or-linux-amd64

# For Linux (ARM)
./dist/or-linux-arm64

# For Windows
./dist/or-windows-amd64.exe
```

### 2. Easy Installation Methods

#### Option A: Copy to System PATH (Recommended)

```bash
# For macOS/Linux - copy to a directory in your PATH
sudo cp dist/or-darwin-arm64 /usr/local/bin/or

# Make executable
sudo chmod +x /usr/local/bin/or

# Now you can use it from anywhere
or
```

#### Option B: Add to PATH

```bash
# Add the dist directory to your PATH
export PATH="$PWD/dist:$PATH"

# Add to your shell profile for permanent access
echo 'export PATH="$PWD/dist:$PATH"' >> ~/.bashrc  # for bash
echo 'export PATH="$PWD/dist:$PATH"' >> ~/.zshrc   # for zsh
``

### 3. First-Time Setup

#### Set Your API Key

```bash
# Set OpenRouter API key
export OPENROUTER_API_KEY="your-api-key-here"

# Add to your shell profile for permanent access
echo 'export OPENROUTER_API_KEY="your-key-here"' >> ~/.bashrc  # for bash
echo 'export OPENROUTER_API_KEY="your-key-here"' >> ~/.zshrc   # for zsh
```

### Configuration

1. **Set your API key**:
```bash
export OPENROUTER_API_KEY="your-api-key-here"
```

2. **First run**:
```bash
or
```

The application will create a `.openrouter.json` configuration file in your project directory with sensible defaults.

## 🎯 Usage Examples

### Interactive Mode
```bash
# Start OpenRouter CLI
or

# Start in a specific directory
or -c /path/to/project
```

### Non-Interactive Mode
```bash
# Single prompt execution
or -p "Explain this Go code structure"

# JSON output format
or -p "List all Go files in this project" -f json

# Quiet mode (minimal output)
or -p "Check for security issues" -q
```

### Sample Conversations

**Codebase Analysis:**
```
You: Can you analyze this Go project structure and explain the main components?

AI: I'll analyze your codebase using my filesystem tools. Let me explore the structure...

[Uses list_directory and read_file tools]

This is a well-structured Go CLI application with the following architecture:
- cmd/ - CLI command definitions using Cobra
- internal/ - Core application logic with clean separation
- internal/tui/ - Terminal UI using Bubble Tea framework
- internal/llm/ - AI integration with multiple providers
- internal/tools/ - Native filesystem tools (14 ultra-fast tools)
...
```

**Code Generation:**
```
You: Create a REST API handler for user authentication with JWT tokens

AI: I'll create a comprehensive authentication handler for you...

[Uses write_file and create_directory tools to generate code]

Created the following files:
- handlers/auth.go - JWT authentication handler
- middleware/auth.go - Authentication middleware
- models/user.go - User model with validation
- utils/jwt.go - JWT token utilities
...
```

## 🛠️ Filesystem Tools

OpenRouter CLI includes 14 ultra-fast native filesystem tools organized into categories:

### 📁 File Operations
- **`read_file`** - Read complete file contents with encoding detection
- **`write_file`** - Create or overwrite files with backup support
- **`modify_file`** - Find and replace text with regex support
- **`delete_file`** - Safe file deletion with confirmation prompts
- **`copy_file`** - Copy files and directories with progress tracking
- **`move_file`** - Move or rename files with conflict resolution
- **`get_file_info`** - Detailed file metadata and statistics
- **`read_multiple_files`** - Batch read multiple files efficiently

### 📂 Directory Operations
- **`list_directory`** - List contents with detailed information
- **`create_directory`** - Create directories recursively
- **`tree`** - Display directory tree structure with filtering
- **`list_allowed_directories`** - Show accessible directories

### 🔍 Search Operations
- **`search_files`** - Find files by name, extension, or pattern
- **`search_within_files`** - Content search with regex support

## ⌨️ Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+C` | Exit application |
| `Ctrl+O` | Open model selection |
| `Ctrl+S` | Switch sessions |
| `Ctrl+F` | Open file picker |
| `Ctrl+T` | Toggle filesystem tools |
| `Ctrl+D` | Toggle debug mode |
| `Ctrl+?` | Show help |
| `Ctrl+R` | Refresh interface |
| `Tab` | Auto-complete |
| `↑/↓` | Navigate history |

## 🔧 Configuration

### Main Configuration (`.openrouter.json`)
```json
{
  "providers": {
    "openrouter": {
      "apiKey": "your-api-key",
      "disabled": false
    }
  },
  "agents": {
    "coder": {
      "model": "openrouter.claude-sonnet-4",
      "maxTokens": 16438,
      "reasoningEffort": "medium"
    },
    "task": {
      "model": "openrouter.gpt-4o",
      "maxTokens": 4096
    }
  },
  "data": {
    "directory": ".openrouter"
  },
  "tui": {
    "theme": "openrouter"
  },
  "lsp": {
    "go": {
      "command": "gopls",
      "args": ["serve"],
      "disabled": false
    }
  }
}
```

### LSP Configuration
Configure Language Server Protocol integration for intelligent code assistance:

```json
{
  "lsp": {
    "go": {
      "command": "gopls",
      "args": ["serve"]
    },
    "typescript": {
      "command": "typescript-language-server",
      "args": ["--stdio"]
    },
    "python": {
      "command": "pylsp"
    }
  }
}
```

## 🚀 Performance

### Benchmarks
- **Native Tools**: 5-10x faster than traditional MCP implementations
- **Memory Usage**: Optimized for low memory footprint (~50MB typical)
- **Startup Time**: Cold start under 500ms
- **File Operations**: Parallel processing with intelligent caching

### Optimization Features
- **Concurrent Processing**: Parallel file operations and AI requests
- **Smart Caching**: Intelligent caching of file contents and AI responses
- **Memory Management**: Efficient memory usage with garbage collection optimization
- **Connection Pooling**: Reused connections for AI providers

## 🔒 Security

### Permission System
- **Path Allowlists**: Restrict file access to approved directories
- **Operation Auditing**: Comprehensive logging of all file operations
- **Safe Defaults**: Conservative permissions with explicit opt-in for dangerous operations
- **Backup System**: Automatic backups before destructive operations

### Best Practices
- **API Key Management**: Environment variable support with secure storage
- **Input Validation**: Comprehensive validation of all user inputs and AI responses
- **Error Handling**: Graceful error handling with detailed logging
- **Audit Trail**: Complete audit trail of all operations

### Performance Monitoring
- **Built-in Profiling**: Memory and CPU profiling support
- **Tool Usage Statistics**: Track filesystem tool usage and performance
- **Session Analytics**: Conversation length, model usage, and response times
