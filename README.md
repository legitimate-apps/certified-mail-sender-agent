# Certified Mail Sender for agents

Prepare and track US domestic USPS Certified Mail from text or a PDF. The person reviews the print preview and pays on a private page. Agents can check USPS tracking and retrieve the signed electronic Return Receipt PDF when USPS supplies one.

## Connect

- Claude Code. Run `claude --plugin-dir /path/to/agent-package` to load this folder for a session. For a persistent install, run `claude plugin marketplace add legitimate-apps/certified-mail-sender-agent` and then `claude plugin install certified-mail-sender@legitimate-apps`.
- ChatGPT and Codex. The root `plugin.json`, `mcp.json`, and `skills/` follow the Agent Plugins format. Run `codex plugin marketplace add legitimate-apps/certified-mail-sender-agent` to add the catalog. In the ChatGPT desktop app, open Plugins, select Legitimate LLC, and install Certified Mail Sender. You can also connect directly using the [client setup guide](https://certifiedmailsender.com/assistants).
- Cursor. Copy this folder into `~/.cursor/plugins/local/` as `certified-mail-sender` and restart Cursor, or add the [MCP URL](https://certifiedmailsender.com/mcp) to your Cursor configuration.

The MCP endpoint is `https://certifiedmailsender.com/mcp`. For clients without MCP, use the [HTTP API](https://certifiedmailsender.com/openapi.json).

No account or prepaid balance is required for a first letter. The default connection quotes and prepares drafts without an API key. Use the whole private link from the draft to read or cancel it. Listing an API key’s letters requires that key. Contact support@certifiedmailsender.com for help.

## License

MIT. The certifiedmailsender.com service itself is governed by its [terms](https://certifiedmailsender.com/terms).
