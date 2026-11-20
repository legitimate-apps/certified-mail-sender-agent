# Installing Certified Mail Sender (for AI agents doing the setup)

Certified Mail Sender is a hosted, remote MCP server. There is nothing to download, build or run locally, and no API key is needed to start.

- MCP endpoint: `https://certifiedmailsender.com/mcp`
- Transport: Streamable HTTP
- Authentication: none for quoting and preparing drafts. An optional API key (`Authorization: Bearer <key>`) adds `list_letters` and auto-send for people who sign in at https://certifiedmailsender.com/account.

## Cline

Add this to `cline_mcp_settings.json`:

```json
{
  "mcpServers": {
    "certified-mail-sender": {
      "type": "streamableHttp",
      "url": "https://certifiedmailsender.com/mcp"
    }
  }
}
```

## Other clients

- Claude Code: `claude mcp add --transport http certified-mail-sender https://certifiedmailsender.com/mcp`
- Codex: `codex mcp add certified-mail-sender --url https://certifiedmailsender.com/mcp`
- Cursor, VS Code, Windsurf: add an HTTP server with the URL above.

## Check that it works

Call `quote_letter` with `{"service": "certified_err", "pages": 1}` (Certified Mail with an electronic Return Receipt). You get the total in US dollars, and quoting never creates, pays for or mails a letter. The tools are `quote_letter`, `create_letter`, `get_letter`, `list_letters`, `send_letter_now` and `cancel_letter`.

## How it behaves

`create_letter` returns a private review link. The person who is sending the letter opens it, checks the print preview and pays. Nothing is mailed until they do, unless they set up auto-send with their own API key and balance. Never pay on the person's behalf.
