# Changelog

All notable changes to the monofoundry LSP plugin are documented here.

## v0.3.0 — 2026-07-01

- Added Python language support alongside TypeScript and JavaScript, with full code intelligence across all features.
- Workspace symbol search now merges results across all active language servers.
- Added a diagnostic command to check the status of each active language server.
- The plugin now activates automatically in Python workspaces.
- Increased minimum required platform version to 0.18.0.

## v0.2.2 — 2026-06-30

- Language server dependencies are now installed at enable time, eliminating the delay on first use.

## v0.2.1 — 2026-06-30

- Bug fixes and internal improvements.

## v0.2.0 — 2026-06-30

- Initial release: language server-backed code intelligence for TypeScript and JavaScript — symbol discovery, navigation, hover information, code actions, semantic rename, and diagnostics.
