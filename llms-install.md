# Installing the LinkedCamp MCP server

This file is for an AI assistant setting the server up on a user's behalf.

## What this is

A **hosted, remote** MCP server. There is no package to install, no process to
run and no local configuration beyond pointing the client at a URL.

```text
https://mcp.linkedcamp.com/mcp
```

Transport is Streamable HTTP.

## Prerequisites

The user needs a LinkedCamp account on the **Pro** or **Agency** plan. There is
a 14-day free trial. The Turbo plan does not include MCP access.

## Preferred: OAuth

If the client supports remote MCP servers with OAuth (Claude, ChatGPT, Cursor,
VS Code), add the URL as a custom connector and let the client run the flow. It
supports OAuth 2.1 with PKCE and dynamic client registration, so nothing has to
be registered in advance.

During sign-in the user pastes their LinkedCamp API key and chooses what the
connection may do — Read only, Read and write, or Full access. Do not choose for
them; if they have not said, Full access is the default and matches how every
other client behaves.

## Fallback: API key header

For a client that cannot run OAuth but can set headers:

```json
{
  "mcpServers": {
    "linkedcamp": {
      "url": "https://mcp.linkedcamp.com/mcp",
      "headers": {
        "X-Api-Key": "<LINKEDCAMP_API_KEY>"
      }
    }
  }
}
```

The key is at **Settings → Integrations** in LinkedCamp. **Ask the user to paste
it themselves and never write it into a file you commit.** It carries the same
access as their account.

## Verify the connection

Call `whoami`. It returns the account, the plan, and `_derived.connection`,
which reports what this particular connection is allowed to do. If it answers,
the server is reachable and authenticated.

Then call `reference` before writing any campaign sequence — the enum vocabulary
is not guessable, and several fields are spelled unexpectedly.

## If a tool seems to be missing

Check `whoami._derived.connection` before concluding the feature does not exist.
A tool can be absent for three different reasons:

1. The connection was authorized at a narrower access tier.
2. The URL carries a `?toolsets=` parameter limiting which groups are loaded.
3. The user's plan or team permissions do not grant that section.

Say which one it is rather than looking for a substitute tool — the refusal is
real, and reconnecting with a wider choice is the fix for the first two.

## Things that are not available, by design

Do not look for a workaround for these; they are withheld deliberately:

- rotating the API key
- connecting a LinkedIn account — that flow needs a password and a verification PIN, and happens in the web app
- CRM credentials and billing

## Safety

28 tools are annotated destructive and clients will prompt before running them.
Treat that prompt as the floor, not the safeguard: launching a campaign and
sending a message reach real people and cannot be recalled. Show the user the
copy and the audience, and get an explicit yes, before either.

## Docs

- Overview — https://docs.linkedcamp.com/mcp/overview
- Quick start — https://docs.linkedcamp.com/mcp/quickstart
- Troubleshooting — https://docs.linkedcamp.com/mcp/troubleshooting
- Support — support@linkedcamp.com
