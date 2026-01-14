# OpenWork

OpenWork is a native (Tauri) desktop UI for running **OpenCode** with a friendly, non-technical workflow.

It supports:
- **Host mode**: start `opencode serve` locally in a chosen project folder.
- **Client mode**: connect to an existing OpenCode server by URL.
- **Sessions**: create/select sessions, send prompts, stream live updates via SSE.
- **Execution plan**: render OpenCode todos as a timeline.
- **Permissions**: surface permission requests and reply (allow once / always / deny).
- **Templates**: save and re-run common workflows (stored locally).
- **Skills manager**: view installed skills and install/import skills via OpenPackage.

## Requirements

- Node.js + `pnpm`
- Rust toolchain (for Tauri): `cargo`, `rustc`
- OpenCode CLI installed and available on PATH: `opencode`

## Quick Start

Install dependencies:

```bash
pnpm install
```

Run as a desktop app (Tauri):

```bash
pnpm dev
```

Run the web UI only:

```bash
pnpm dev:web
```

## How It Works

- In **Host mode**, OpenWork spawns:
  - `opencode serve --hostname 127.0.0.1 --port <free-port>`
  - with the selected project folder as the process working directory.
- The UI uses `@opencode-ai/sdk/v2/client` to:
  - connect to the server
  - list/create sessions
  - send prompts
  - subscribe to `/event` SSE
  - read todos and permission requests

## Folder Picker

The folder picker uses the Tauri dialog plugin. The capability permission file is at:
- `src-tauri/capabilities/default.json`

## Skills (OpenPackage)

The **Skills** screen supports:
- Installing a package (e.g. `github:anthropics/claude-code`) into the current workspace.
- Importing a local skill folder into `.opencode/skill/<skill-name>`.

Notes:
- If `opkg` is not installed globally, OpenWork falls back to `pnpm dlx opkg ...`.

## Useful Scripts

Typecheck:

```bash
pnpm typecheck
```

Build web bundle:

```bash
pnpm build:web
```

API smoke tests (non-UI):

```bash
pnpm test:e2e
pnpm test:events
pnpm test:sessions
pnpm test:health
```

## Security Notes

- OpenWork intentionally hides model reasoning/tool metadata by default.
- Permissions are surfaced via OpenCode permission requests (when configured to ask).
- Host mode is local by default (`127.0.0.1`).

## License

TBD.
