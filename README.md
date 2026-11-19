# SizeMyFile agent integrations

Connect agents to file conversion, compression and inspection workflows.

- Remote MCP: https://sizemyfile.com/mcp (Streamable HTTP with OAuth)
- Documentation and supported limits: https://sizemyfile.com/agents
- Account connections and private file uploads: https://sizemyfile.com/agents/connect
- Public tool contract: https://sizemyfile.com/agent-tools.json
- Local runner: `agent/` — see its README for installation and folder permissions.
- Portable OpenAI/Claude plugin package: `plugin/`.
- Official MCP Registry descriptor: `server.json`.

The catalog has 100 website tools, with 96 supported through the local runner and 62 remotely. These overlap; not every format or operation is supported in every runtime. Local file workflows use Rust/WASM and browser processors. Remote operations use Rust edge where possible and bounded server fallback when permitted. Each step consumes the previous step’s actual outputs.

## Quick connections

Claude Code: `claude mcp add --transport http sizemyfile https://sizemyfile.com/mcp`

Claude, ChatGPT and Muse: add a custom remote MCP connector with the endpoint above, then complete SizeMyFile OAuth when the client requests it. Marketplace availability depends on independent review; custom connection support does not imply a published directory listing.

For stdio clients, install the local package and configure command `node`, arguments `[/absolute/path/to/agent/bin/sizemyfile.mjs, --root, /absolute/path/to/allowed/files]`.

Only the integration adapter code in this repository is MIT licensed. Downloaded SizeMyFile runtime components and dependencies retain their respective licenses. The hosted service uses the terms and privacy policy linked below. This repository does not include the private application deployment configuration or secrets.

Support: info@seehash.com · https://sizemyfile.com/contact

Privacy: https://sizemyfile.com/privacy · Terms: https://sizemyfile.com/terms
