# Power Office MCP Server
MCP Server for Power Office with read and write capabilities.

This repository contains all the information needed to connect to your [Power Office](https://peliqan.io/ai/Power%20Office/) account using MCP.

# What is the Peliqan MCP Server?

The [Peliqan MCP (Model Context Protocol) Server](https://peliqan.io/mcp) lets AI assistants like Claude Code, Claude Desktop and ChatGPT connect to your Power Office account. Once connected, the AI can explore your data, answer business questions and take actions inside of Power Office.

# Prerequisites
* A [Peliqan](https://peliqan.io) account, visit https://peliqan.io to sign up for a free trial.
* An Power Office connection added in Peliqan.
* A Peliqan API token: generate an API token in Peliqan under Admin > API keys, or create a personal API key under User Settings.
* An MCP Client: ChatGPT, Claude Code, Claude Desktop etc.

# Setup the MCP Server

## Setup in Claude Code (terminal)

Add the following to your ~/.claude.json file. If the file doesn't exist yet, create it.

```
{
  "mcpServers": {
    "peliqan": {
      "type": "http",
      "url": "https://mcp.eu.peliqan.io/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_PELIQAN_API_TOKEN"
      }
    }
  }
}
```

Replace YOUR_PELIQAN_API_TOKEN with your Peliqan API token.

After saving, restart Claude Code. You should see Peliqan listed when you type /mcp in the chat.

## Setup in Claude Desktop

Open Claude Desktop settings → Developer → Edit Config and add the below block under mcpServers:

For Mac:

```
"mcpServers": {
    "peliqan": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://mcp.eu.peliqan.io/mcp",
        "--header",
        "Authorization: Bearer YOUR_PELIQAN_API_TOKEN"
      ]
    }
  }
```

For Windows:

```
"mcpServers": {
    "peliqan": {
      "command": "C:\\\"Program Files\"\\nodejs\\npx”
      "args": [
        "mcp-remote",
        "https://mcp.eu.peliqan.io/mcp",
        "--header",
        "Authorization: Bearer YOUR_PELIQAN_API_TOKEN"
      ]
    }
  }
```
Replace YOUR_PELIQAN_API_TOKEN with your Peliqan API token.

Make sure npx and mcp-remote are installed on your computer.

For Mac:

```
brew install node
npx mcp-remote
```

For Windows (PowerShell):

```
winget install OpenJS.NodeJS
npx mcp-remote
```

## Other MCP Clients

Any MCP-compatible AI client that supports HTTPS transport can connect using the same URL and API token. Check your client's documentation on how to add an MCP Server.

For clients that support custom headers, use the URL https://mcp.eu.peliqan.io/mcp and header `Authorization: Bearer YOUR_PELIQAN_API_TOKEN`.

For clients that only accept a URL (without custom header support), append your API token as a query parameter:

```
https://mcp.eu.peliqan.io/mcp?api_key=YOUR_PELIQAN_API_TOKEN
```
Replace YOUR_PELIQAN_API_TOKEN with your API token.

## Verifying the connection

Once connected, try these prompts to confirm everything is working:

"List my Peliqan connections"
"Show me all data tables in my Peliqan account”

If you see results from your Peliqan account, you're all set.

# Getting your API token in Peliqan

## Account-wide API token

* Log in to Peliqan at https://app.eu.peliqan.io
* Go to Admin > API Token & Webhooks
* Copy your API token

## Personal API token

* Log in to Peliqan at https://app.eu.peliqan.io
* Click on the user icon in the bottom left corner of Peliqan
* Select User Settings > API token
* Copy your API token

# Need help?

Reach out to Peliqan support: support@peliqan.io. You can also ask your AI (e.g. Claude) directly. Once the Peliqan MCP Server is connected, the AI has full context on how Peliqan works.
