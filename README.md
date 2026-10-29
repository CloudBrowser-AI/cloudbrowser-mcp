# CloudBrowser MCP Server

Give ChatGPT, Claude and your AI agents a real browser. CloudBrowser runs Chrome in the cloud. Your assistant opens a browser, navigates, reads pages, clicks, types and takes screenshots, and you can watch live or take over at any time.

- **Endpoint:** `https://mcp.cloudbrowser.ai` (Streamable HTTP)
- **Auth:** OAuth, sign in with your CloudBrowser account
- **Website:** https://cloudbrowser.ai/mcp
- **Official MCP Registry:** `ai.cloudbrowser/mcp`

## What you can do

- Open cloud Chrome browsers in your CloudBrowser account and connect to them.
- Navigate, read page content, find elements, click, type, run scripts and take screenshots.
- Save browser sessions and resume them later.
- Start a remote desktop to watch the browser live or take over.
- Detect CAPTCHAs. Login and verification walls stay with you.

## Connect

The server uses OAuth. Your client opens a browser window, you sign in with your CloudBrowser account and approve access. You do not copy an API key.

### Claude (claude.ai and Claude Desktop)

Open **Settings → Connectors → Add custom connector**, enter `https://mcp.cloudbrowser.ai` and select **Connect**.

### Claude Code

```bash
claude mcp add --transport http cloudbrowser https://mcp.cloudbrowser.ai
```

Then run `/mcp` in Claude Code and authenticate `cloudbrowser`.

### Codex CLI

```bash
codex mcp add cloudbrowser --url https://mcp.cloudbrowser.ai
codex mcp login cloudbrowser
```

### Cursor

Add this to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "cloudbrowser": { "url": "https://mcp.cloudbrowser.ai" }
  }
}
```

### VS Code

```bash
code --add-mcp '{"name":"cloudbrowser","type":"http","url":"https://mcp.cloudbrowser.ai"}'
```

### Gemini CLI

```bash
gemini mcp add --transport http cloudbrowser https://mcp.cloudbrowser.ai
```

### ChatGPT and other clients

Add a custom connector (in ChatGPT, developer mode) with the URL `https://mcp.cloudbrowser.ai`. Any client that supports Streamable HTTP and MCP OAuth works.

## Tools

The server advertises 20 tools. Your client gets the current schemas from `tools/list`.

- **Workspace:** `browser_workspace`, `resume_saved_session`
- **Browser lifecycle:** `open_browser`, `close_browser`, `get_browsers`, `start_remote_desktop`, `stop_remote_desktop`
- **Saved sessions:** `get_saved_sessions`, `remove_saved_session`
- **Connections:** `connect_to_browser`, `disconnect_browser`, `get_connected_browsers`
- **Page work:** `navigate_to_url`, `get_page_content`, `click_element`, `type_text`, `get_elements`, `take_screenshot`, `evaluate_script`, `detect_captcha`

## Authentication and account

OAuth 2.1 with PKCE and dynamic client registration. Sign in with your CloudBrowser account. Scope: `browser:control` (`openid email` optional). Developers can send their own account token instead: `Authorization: Bearer <your CloudBrowser API token>`. Keep the token in your client's secret settings, never in a prompt.

You need a CloudBrowser account. Browser usage follows your CloudBrowser plan.

## Links

- Website: https://cloudbrowser.ai
- MCP setup page: https://cloudbrowser.ai/mcp
- Native client packages (Claude Code, Gemini CLI and more): https://github.com/CloudBrowser-AI/skills
- Privacy policy: https://cloudbrowser.ai/privacy

## About this repository

This repository is the public home of the hosted CloudBrowser MCP server. It holds this setup guide and the registry metadata (`server.json` for the official MCP Registry, `glama.json` for Glama). The server runs as a hosted service at `https://mcp.cloudbrowser.ai`. Its source code is not in this repository.

Found a problem or have a question? Open an issue.

## License

The contents of this repository are available under the [MIT License](LICENSE).
