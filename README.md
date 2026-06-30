# monō foundry LSP Plugin

A first-party [monō foundry](https://github.com/monoai-labs/mono-foundry) plugin that adds headless Language Server Protocol support. It overrides monofoundry's built-in code-intelligence tools with real LSP-backed implementations, so the agent gets accurate type information, go-to-definition, diagnostics, and refactoring from the actual language server running in your workspace.

## What it does

Without this plugin, monofoundry's code-intelligence tools (symbols, hover, navigation, diagnostics, rename, code actions) rely on text-based heuristics. With the LSP plugin installed, these tools are backed by a real language server:

| Tool               | Description                                                                                    |
| ------------------ | ---------------------------------------------------------------------------------------------- |
| `get_symbols`      | Document and workspace symbol search via `textDocument/documentSymbol` and `workspace/symbol`. |
| `hover_info`       | Type signatures and documentation at a position via `textDocument/hover`.                      |
| `code_navigation`  | Go-to-definition, references, implementations, and type definitions.                           |
| `peek_definition`  | Definition source context with surrounding lines and hover info.                               |
| `get_code_actions` | List and apply quick fixes and refactorings via `textDocument/codeAction`.                     |
| `rename_symbol`    | Workspace-aware symbol rename via `textDocument/rename`.                                       |
| `get_diagnostics`  | Real compiler diagnostics (errors, warnings, hints) via `textDocument/publishDiagnostics`.     |

## Supported languages

- **TypeScript / JavaScript** — via [`typescript-language-server`](https://github.com/typescript-language-server/typescript-language-server). The server binary is automatically downloaded and managed on first use. TypeScript is resolved from the workspace when available, falling back to a bundled version.

More languages will be added in future releases.

## Prerequisites

- [monō foundry](https://github.com/monoai-labs/mono-foundry) >= 0.17.0
- Node.js >= 22

## Install

```bash
monofoundry plugin install github:monoai-labs/mono-foundry-lsp-plugin
```

To install a specific version:

```bash
monofoundry plugin install github:monoai-labs/mono-foundry-lsp-plugin@v0.1.0
```

The plugin activates automatically when a `tsconfig.json` or `package.json` is detected in the workspace. No manual configuration is required for default usage.

## Configuration

The plugin supports per-workspace configuration via monofoundry's plugin settings:

```json
{
  "languages": {
    "typescript": {
      "enabled": true,
      "rootMode": "auto"
    }
  }
}
```

| Property                        | Default  | Description                                                                                         |
| ------------------------------- | -------- | --------------------------------------------------------------------------------------------------- |
| `languages.typescript.enabled`  | `false`  | Explicitly enable TypeScript language support.                                                      |
| `languages.typescript.rootMode` | `"auto"` | How the language server root is determined. `"auto"` detects from `tsconfig.json` / `package.json`. |

## Commands

```bash
monofoundry lsp status    # show runtime status (server, TypeScript resolution, client state)
monofoundry lsp doctor    # alias for status
```

## How it works

On activation, the plugin spawns a `typescript-language-server` process communicating over stdio. The language server binary is installed on first use into the plugin's storage directory and cached for subsequent sessions.

## Releases

Releases are published as GitHub Releases on this repository with a prebuilt tarball attached. See the [Releases page](https://github.com/monoai-labs/mono-foundry-lsp-plugin/releases) for available versions.

---

© monō ai Australia Pty Ltd. All rights reserved. Use is subject to monō ai's [legal policies](https://www.monoai.co/legal) and [terms of service](https://app.monoai.co/terms).
