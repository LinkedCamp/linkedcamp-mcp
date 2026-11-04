<p align="center">
  <img src="assets/logo-white-400.png" alt="LinkedCamp" width="300">
</p>

<h1 align="center">LinkedCamp MCP server</h1>

<p align="center">
  Run LinkedIn and email outreach from ChatGPT, Claude, Cursor or any MCP client.
  <br>
  <a href="https://glama.ai/mcp/connectors/com.linkedcamp.mcp/linked-camp"><img src="https://glama.ai/mcp/connectors/com.linkedcamp.mcp/linked-camp/badges/score.svg" alt="LinkedCamp MCP connector"></a>
  <a href="https://mcptry.com/servers/com.linkedcamp/mcp"><img src="https://mcptry.com/badge/com.linkedcamp/mcp" alt="mcptry"></a>
  <a href="https://mcprush.com/to/linkedcamp-mcp?ref=badge"><img src="https://mcprush.com/badge/linkedcamp-mcp/card.svg" alt="Linkedcamp MCP server"></a>
</p>

<p align="center">
  <a href="https://docs.linkedcamp.com/mcp/overview">Documentation</a> ·
  <a href="https://www.linkedcamp.com/mcp?utm_source=github-linkedcamp-mcp&utm_medium=referral&utm_campaign=mcp-directory">Product page</a> ·
  <a href="mailto:support@linkedcamp.com">Support</a>
</p>

---

[LinkedCamp](https://www.linkedcamp.com/mcp?utm_source=github-linkedcamp-mcp&utm_medium=referral&utm_campaign=mcp-directory) is LinkedIn and email outreach for lead-gen
agencies. This is its official **hosted** MCP server: build and launch campaigns, write multi-step
sequences, triage the unified inbox, manage prospects and pull client reports —
all from an AI assistant.

Nothing to install and nothing to run. The server is hosted by LinkedCamp; you
point your client at one URL.

```text
https://mcp.linkedcamp.com/mcp
```

| | |
| --- | --- |
| **Transport** | Streamable HTTP (remote) |
| **Auth** | OAuth 2.1 with PKCE and dynamic client registration, or an `X-Api-Key` header |
| **Tools** | 133 across 14 groups — 64 read-only, 69 write, 28 flagged destructive |
| **Requires** | A [LinkedCamp](https://www.linkedcamp.com/mcp?utm_source=github-linkedcamp-mcp&utm_medium=referral&utm_campaign=mcp-directory) Pro or Agency plan. 14-day free trial. |
| **Registry** | `com.linkedcamp/mcp` |

## Connect

### Claude

Settings → Connectors → **Add custom connector**, then paste the URL above and
sign in. Claude handles OAuth for you.

### ChatGPT

Install the LinkedCamp app from the ChatGPT directory, or add the URL above as a
custom connector. Sign-in is the same OAuth flow.

### Cursor, VS Code, Windsurf and other config-file clients

```json
{
  "mcpServers": {
    "linkedcamp": {
      "url": "https://mcp.linkedcamp.com/mcp"
    }
  }
}
```

### Claude Code

```bash
claude mcp add --transport http linkedcamp https://mcp.linkedcamp.com/mcp
```

### Without OAuth

Any client that can set a header may send your API key directly instead of
running the OAuth flow:

```text
X-Api-Key: <your LinkedCamp API key>
```

Your key is under **Settings → Integrations** in LinkedCamp. Treat it as a
password: it carries the same access your account has.

## What you can do with it

| Group | Tools | What it covers |
| --- | --- | --- |
| `core` | 3 | Orientation — the plan, permissions and the enum vocabulary |
| `campaigns` | 19 | Create, configure, source prospects, launch, and manage once live |
| `flows` | 9 | Author the sequence a campaign runs, and see how each step performs |
| `leads` | 14 | Prospects, their history, and the scheduled actions behind it |
| `accounts` | 13 | The LinkedIn accounts and mailboxes campaigns send from, and their limits |
| `inbox` | 9 | LinkedIn and email conversations — where replies land and are answered |
| `analytics` | 5 | Performance by campaign, sending account and whole account |
| `library` | 20 | Tags, exclusion rules, saved copy, merge fields, blocked dates |
| `personas` | 5 | Ideal-customer definitions a `QUALIFIER` step scores leads against |
| `agents` | 13 | Agents that reply to prospects and book meetings, and their knowledge base |
| `content` | 6 | LinkedIn posts: drafting, scheduling and the publishing calendar |
| `crm` | 7 | Connected CRMs and manual follow-up around a conversation |
| `automation` | 4 | Account-wide, event-driven workflows |
| `settings` | 6 | Notifications, profile preferences and the team roster |

Full reference: **[docs.linkedcamp.com/mcp/overview](https://docs.linkedcamp.com/mcp/overview)**

## Safety

Outreach reaches real people, so the server is built to make that visible rather
than convenient.

- **28 tools are annotated destructive.** Clients surface that in their approval
  prompt, so a human confirms before anything is deleted or sent. The set is
  wider than "it deletes something" — launching a campaign, sending a test
  email, and changing who gets messaged are all flagged, because each reaches
  outside the account or is hard to undo.
- **You choose what a connection may do when you sign in.** Read only, Read and
  write, or Full access. Read only reaches the 64 tools that change nothing;
  Read and write adds ordinary writes but withholds the destructive ones; Full
  access reaches everything and still asks before each destructive call.
- **Your plan and team permissions still apply.** A section you cannot open in
  the web app is hidden from the tool list and refused on the call.
- **Some things are deliberately not exposed at all**: rotating your API key,
  connecting a LinkedIn account (that flow takes a password and a verification
  PIN), CRM credentials, and billing.

## A smaller tool list

Some clients are slower to start against 133 tool definitions, because they read
every one before answering anything. Name the groups you want:

```text
https://mcp.linkedcamp.com/mcp?toolsets=campaigns,flows,analytics
```

Leaving it off gives you everything. `core` is always included, and an
unrecognised name is ignored rather than leaving you with an empty connection.

## Support

- Documentation — [docs.linkedcamp.com/mcp/overview](https://docs.linkedcamp.com/mcp/overview)
- Troubleshooting — [docs.linkedcamp.com/mcp/troubleshooting](https://docs.linkedcamp.com/mcp/troubleshooting)
- Email — [support@linkedcamp.com](mailto:support@linkedcamp.com)

This repository holds the install documentation and client manifests only. The
server itself is hosted by [LinkedCamp](https://www.linkedcamp.com/mcp?utm_source=github-linkedcamp-mcp&utm_medium=referral&utm_campaign=mcp-directory) and is not open source.
