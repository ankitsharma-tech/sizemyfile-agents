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

## Try the file tools

- [Free Parquet viewer](https://sizemyfile.com/tools/parquet-viewer): inspect schema and rows, then export supported data formats.
- [Free JSON, YAML and TOML converter](https://sizemyfile.com/tools/json-yaml-toml-converter): convert compatible configuration values; unsupported representations are reported.
- [Increase file size](https://sizemyfile.com/increase-file-size): set a minimum byte size or enlarge supported images. More bytes do not add image detail.
- [Image conversion](https://sizemyfile.com/tools/image-converter): convert an image and pass its actual output to the next operation.

These pages describe supported formats and limits. Choose on-device only to prevent cloud file uploads. Optional remote tools use the account allowance and documented retention rules.

[SizeMyFile on Glama](https://glama.ai/mcp/servers/ankitsharma-tech/sizemyfile-agents) lists this integration for MCP discovery.

## Quick connections

Claude Code: `claude mcp add --transport http sizemyfile https://sizemyfile.com/mcp`

Claude, ChatGPT and Muse: add a custom remote MCP connector with the endpoint above, then complete SizeMyFile OAuth when the client requests it. Marketplace availability depends on independent review; custom connection support does not imply a published directory listing.

For stdio clients, install the local package and configure command `node`, arguments `[/absolute/path/to/agent/bin/sizemyfile.mjs, --root, /absolute/path/to/allowed/files]`.

Only the integration adapter code in this repository is MIT licensed. Downloaded SizeMyFile runtime components and dependencies retain their respective licenses. The hosted service uses the terms and privacy policy linked below. This repository does not include the private application deployment configuration or secrets.

Support: info@seehash.com · https://sizemyfile.com/contact

Privacy: https://sizemyfile.com/privacy · Terms: https://sizemyfile.com/terms
