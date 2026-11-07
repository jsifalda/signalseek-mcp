<p align="center"><img src="icon.svg" width="72" alt="SignalSeek"></p>

[![M8ven Score](https://m8ven.ai/badge/mcp/jsifalda-signalseek-mcp-14ersf?v=ae70c2dc1b2e59414ee0db2cb8799155)](https://m8ven.ai/mcp/jsifalda-signalseek-mcp-14ersf?s=readme)

# SignalSeek MCP server

Reddit lead monitoring for AI agents. SignalSeek watches Reddit for people who describe the problem your product solves, scores each thread, and drafts a reply. You read the matches and drafts from Claude, then you write the reply yourself on Reddit.

**SignalSeek never posts.** The server has no posting tool of any kind.

- Endpoint: `https://signalseek.cc/api/mcp`
- Transport: streamable HTTP
- Auth: OAuth. You sign in to your own SignalSeek account. Claude reaches that one account and no other.
- Registry name: `io.github.jsifalda/signalseek` in the [official MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=signalseek)
- Website: [signalseek.cc](https://signalseek.cc) · Connector page: [signalseek.cc/mcp](https://signalseek.cc/mcp)

## Connect in Claude

1. Open Claude on the web or in the Desktop app.
2. Pro and Max: open **Customize**, then **Connectors**, then **+ Add**, then **Add custom connector**.
3. Enter a name and the URL `https://signalseek.cc/api/mcp`. Paste `/api/mcp`, not `/mcp`. Click **Continue**.
4. Under OAuth client, keep **Use Claude's published identity (Recommended)**. Click **Add**, then **Connect**.
5. Sign in to SignalSeek and approve.
6. Ask Claude: "List my SignalSeek campaigns."

Team and Enterprise: an Owner adds the connector under **Organization settings → Connectors → Add → Custom → Web**. Members then click **Connect** under **Customize → Connectors**.

The connector syncs to your account, so it also works in the Claude iOS app.

## Other MCP clients

Point the client at `https://signalseek.cc/api/mcp` over streamable HTTP. The server does not support OAuth dynamic client registration. Use a client that supports OAuth client ID metadata documents.

## Tools

| Tool | What it does | Access |
|---|---|---|
| `list_campaigns` | Lists your campaigns with status, interval and match counts | Read |
| `get_campaign` | Reads one campaign in full, plus its strategy summary | Read |
| `get_campaign_strategy` | Reads a campaign's persona, subreddits and search terms | Read |
| `get_campaign_stats` | Reads a campaign's draft counts and last monitoring run | Read |
| `list_drafts` | Lists the Reddit opportunities SignalSeek found, with a summary of each draft | Read |
| `get_draft` | Reads one draft in full | Read |
| `create_campaign` | Creates a campaign and, by default, generates its strategy | Write |
| `generate_campaign_strategy` | Generates search terms, subreddits and a reply persona for a draft campaign | Write |
| `update_campaign` | Changes a campaign's settings or status (pause, resume, archive) | Write |
| `update_persona` | Changes a campaign's reply persona | Write |
| `add_subreddits` | Adds subreddits to a campaign, each checked against Reddit first | Write |
| `update_subreddit` | Excludes, restores or removes one subreddit. Remove works only on subreddits you added | Write |
| `add_search_terms` | Adds search terms to a campaign | Write |
| `update_search_term` | Excludes, restores or removes one search term | Write |
| `generate_draft_reply` | Writes the reply for a draft and stores it on that draft | Write |
| `approve_draft` | Marks a draft approved inside SignalSeek. It does not post | Write |
| `reject_draft` | Turns a draft down, with an optional tag and reason that tune later matches | Write |

"Write" tools change data inside your SignalSeek account only. No tool writes to Reddit.

## Things you can ask

- "What came in overnight?"
- "Show me the draft for the best match."
- "Create a SignalSeek campaign for my invoicing app. It is for freelance designers who hate chasing late payments."
- "Pause the campaign for the product I shut down."

## Privacy

- SignalSeek reads public Reddit content. It never posts, comments or sends messages.
- Each OAuth token is tied to one SignalSeek account.
- Pricing and terms: [signalseek.cc](https://signalseek.cc)

## About this repo

This repo holds the public docs and the MCP Registry manifest (`server.json`). The server itself is a hosted service, and its source is private.

## License

MIT. See [LICENSE](LICENSE).
