# SizeMyFile for agents

Run explicit file workflows on your own computer using the same Rust/WASM and browser processors as SizeMyFile. An isolated Chromium process loads runtime assets from SizeMyFile. Only static GET requests are allowed; file-content uploads and account requests are blocked. This package does not require an API key or consume cloud quota. The first run needs network access to download the runtime.

## Install

Node.js 22 or newer is required. Extract the package, then run:

```sh
npm ci
npx playwright install chromium
node bin/sizemyfile.mjs --root /absolute/path/to/allowed/files
```

The last command starts an MCP stdio server. Configure Claude Desktop, Claude Code, Cursor, VS Code, Gemini CLI or another stdio MCP client with command `node`, arguments `[/absolute/path/to/bin/sizemyfile.mjs, --root, /absolute/path/to/allowed/files]`. Clients control how permissions and confirmations are presented. A client configuration is not a marketplace endorsement or approved listing.

The configured root is the only readable folder. Symlink escapes are rejected. Outputs are written with private permissions into a new `sizemyfile-results-*` directory inside that folder. Originals are never overwritten. Do not grant a folder containing unrelated secrets. Never put API keys in prompts or configuration committed to a repository.

## Workflow example

Save this as `plan.json`:

```json
{"files":["photo.webp"],"steps":[{"tool":"convert-image","options":{"output":"png"}},{"tool":"resize","options":{"width":600}},{"tool":"compress","options":{"output":"png","max_bytes":200000}}]}
```

Run `node bin/sizemyfile.mjs --root /your/files --run plan.json`. Or have your agent call `search_tools`, inspect the returned parameter schema, then call `run_workflow`. Each step consumes the immediately preceding outputs. Reports include route, checksums and step measurements.

The catalog currently exposes 96 locally executable tools out of 100 website tools. Office-to-PDF, searchable PDF OCR and the primary audio/video conversion tools require the remote connection. Some other media utilities use browser FFmpeg. Individual codecs have additional limits. Model containers are inspected, never executed or unpickled. AI-origin checks are advisory. Background removal requires visual review.

Workflows accept 1–50 files and 1–12 steps, with 32 MiB combined inputs and intermediate outputs. Some processors impose lower limits. A failed step stops the workflow. Supported tools and option schemas are in `catalog.json` and https://sizemyfile.com/agent-tools.json.

## Remote MCP

Endpoint: `https://sizemyfile.com/mcp` (Streamable HTTP). Connect through OAuth or supply a scoped agent key from https://sizemyfile.com/agents/connect as an Authorization bearer header. Remote workflows support 62 tools and use your existing cloud allowance. Inputs expire after one hour; outputs after four hours. Never upload without user authorization.

Docs: https://sizemyfile.com/agents · Privacy: https://sizemyfile.com/privacy · Support: info@seehash.com
