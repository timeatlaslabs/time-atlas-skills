# Time Atlas skills

Skills for AI assistants to use the [Time Atlas](https://timeatlas.app)
MCP server: ask about your life as Time Atlas recorded it — places, trips,
activity, sleep, notes, photos, books, weather — and add notes to your
journal.

Time Atlas is an iPhone app:
[download it on the App Store](https://apps.apple.com/us/app/time-atlas-life-tracker/id6738783076).
Your data stays on your phone; the MCP server relays each question to the
app.

## What is here

```
skills/time-atlas/        The skill: SKILL.md and a reference of the tools
.mcp.json                 The MCP server, https://ai.timeatlas.app/mcp
.claude-plugin/           Claude Code plugin and marketplace manifests
```

## Install

### Claude Code

```
/plugin marketplace add timeatlaslabs/time-atlas-skills
/plugin install time-atlas@time-atlas
```

This adds the skill and the MCP server. Run `/mcp` and sign in to
Time Atlas.

### OpenClaw

Copy `skills/time-atlas` to `~/.openclaw/skills/` (or to your workspace's
`skills/`), add the server to `openclaw.json` and sign in:

```json5
{
  mcp: {
    servers: {
      "time-atlas": {
        url: "https://ai.timeatlas.app/mcp",
        transport: "streamable-http",
        auth: "oauth",
      },
    },
  },
}
```

```
openclaw mcp login time-atlas
```

### Claude (claude.ai, Desktop, mobile)

Add Time Atlas from Settings › Connectors. The skill is optional there;
to add it, upload `skills/time-atlas` as a zip in Settings › Capabilities.

### ChatGPT

ChatGPT connects to MCP servers as custom connectors, in Developer Mode
(a beta on the web, on some plans only):

1. In Settings › Apps & Connectors › Advanced, turn on Developer Mode.
2. In Apps & Connectors, choose Create and enter:
   - Name: Time Atlas
   - MCP Server URL: `https://ai.timeatlas.app/mcp`
   - Authentication: OAuth
3. Sign in with the code from the app (see below).
4. In a chat, choose Time Atlas from the tools (+) menu.

The menus have moved between ChatGPT versions; if they differ, see
OpenAI's help on connectors in Developer Mode. Where your ChatGPT cannot
load skills, you can give it the guidance in the skill by pasting the
"Using the tools" section of [SKILL.md](skills/time-atlas/SKILL.md) into a
project's instructions or your custom instructions.

### Other agents

Copy `skills/time-atlas` to wherever your agent loads
[Agent Skills](https://agentskills.io) from, and add
`https://ai.timeatlas.app/mcp` as a remote MCP server with OAuth.

## Signing in

Signing in opens a Time Atlas page that asks for a code. Get it in the
app: **Chat › menu (⋯) › Connect to Claude**. You can see and disconnect
the assistants you have connected on the same screen.

## Privacy

See the [Time Atlas privacy notice](https://www.timeatlaslabs.com/legal/privacynotice.html).

## License

MIT
