# Certified Mail Sender for agents

Prepare and track US domestic USPS Certified Mail from text or a PDF. The person reviews the print preview and pays on a private page. Agents can check USPS tracking and retrieve the signed electronic Return Receipt PDF when USPS supplies one.

## Tools

The MCP server at `https://certifiedmailsender.com/mcp` (streamable HTTP, no install) has six tools:

- `quote_letter`: itemized price for 1-10 pages or a PDF, with or without the electronic Return Receipt. Free.
- `create_letter`: a draft from text, a base64 PDF or a PDF URL, with sender and recipient addresses. Free. Returns the private link where the person reviews the print preview and pays.
- `get_letter`: state, timeline, USPS tracking, proof of mailing, the cancel deadline and the Return Receipt PDF once USPS supplies it.
- `list_letters`: the letters created with an API key, newest first.
- `send_letter_now`: skips a paid letter's 30-minute cancellation hold when the person asks.
- `cancel_letter`: cancels before the letter goes to the printer and refunds the payment in full.

A typical session: the person says "send this notice to my landlord by certified mail with a return receipt"; the agent calls `quote_letter`, then `create_letter`, and gives the person the private link. After they pay, `get_letter` follows it through printing, USPS acceptance and delivery.

## Connect

- VS Code with GitHub Copilot. Add `{"servers": {"certified-mail-sender": {"type": "http", "url": "https://certifiedmailsender.com/mcp"}}}` to `.vscode/mcp.json`, or run **MCP: Add Server** and paste the URL.
- Claude Code. Run `claude --plugin-dir /path/to/agent-package` to load this folder for a session. For a persistent install, run `claude plugin marketplace add legitimate-apps/certified-mail-sender-agent` and then `claude plugin install certified-mail-sender@legitimate-apps`.
- ChatGPT and Codex. The root `plugin.json`, `mcp.json`, and `skills/` follow the Agent Plugins format. Run `codex plugin marketplace add legitimate-apps/certified-mail-sender-agent` to add the catalog. In the ChatGPT desktop app, open Plugins, select Legitimate LLC, and install Certified Mail Sender. You can also connect directly using the [client setup guide](https://certifiedmailsender.com/assistants).
- Cline. Add `{"type": "streamableHttp", "url": "https://certifiedmailsender.com/mcp"}` under `mcpServers` in `cline_mcp_settings.json`. [llms-install.md](llms-install.md) has the details for an agent doing the setup.
- Cursor. Copy this folder into `~/.cursor/plugins/local/` as `certified-mail-sender` and restart Cursor, or add the [MCP URL](https://certifiedmailsender.com/mcp) to your Cursor configuration.

The MCP endpoint is `https://certifiedmailsender.com/mcp`. For clients without MCP, use the [HTTP API](https://certifiedmailsender.com/openapi.json).

No account or prepaid balance is required for a first letter. The default connection quotes and prepares drafts without an API key. Use the whole private link from the draft to read or cancel it. Listing an API key’s letters requires that key. Contact support@certifiedmailsender.com for help.

## License

MIT. The certifiedmailsender.com service itself is governed by its [terms](https://certifiedmailsender.com/terms).
