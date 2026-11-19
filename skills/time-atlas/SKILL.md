---
name: time-atlas
description: Answer questions about the user's own life from their Time Atlas app — where they have been, trips, places visited, restaurants, activity and health stats, sleep, journal notes, photos, books and movies, calendar, and the weather where they were — and add notes to their Time Atlas journal. Use when the user asks about their past, their habits, places they have been, or wants something noted down, and when connecting the Time Atlas MCP server.
homepage: https://timeatlas.app
metadata: {"openclaw": {"emoji": "🗺️", "homepage": "https://timeatlas.app"}}
---

# Time Atlas

[Time Atlas](https://timeatlas.app) is an iPhone app that records the
user's life automatically: places, trips, movement and workouts, sleep and
health data, photos, and their own journal notes. Its MCP server lets you
ask about that record.

Everything lives on the user's iPhone. The MCP server only relays: each
tool call reaches the app, which answers from its own database. The user
needs the app installed and set up, version 1.6.2 or newer:
[Time Atlas on the App Store](https://apps.apple.com/us/app/time-atlas-life-tracker/id6738783076).

## Connecting

Server: `https://ai.timeatlas.app/mcp` (streamable HTTP), signed in with
OAuth.

Signing in opens a Time Atlas page that asks for a 6-letter code. The user
gets the code in the app: **Chat › menu (⋯) › Connect to Claude**. The code
is good for 15 minutes and once only; the app shows a new one as needed.
It is the only thing to enter: there is no account or password.

- **Claude (claude.ai, Desktop, mobile):** add Time Atlas from
  Settings › Connectors, or add a custom connector with the URL above, and
  choose Connect.
- **Claude Code:** `claude mcp add --transport http time-atlas https://ai.timeatlas.app/mcp`,
  then run `/mcp` and sign in. Installing this repository as a plugin adds
  the server for you.
- **OpenClaw:** add the server to `mcp.servers` in `openclaw.json`, then
  sign in with `openclaw mcp login time-atlas`:

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

- **ChatGPT:** turn on Developer Mode in Settings › Apps & Connectors ›
  Advanced, then create a connector with the URL above and OAuth
  authentication, and sign in. In a chat, choose Time Atlas from the
  tools (+) menu. Developer Mode is a beta on the web, on some plans
  only; see OpenAI's help for the current menus.
- **Other MCP clients:** any client that supports remote servers with OAuth
  (dynamic client registration, PKCE) works with the same URL.

## Using the tools

Pick the most specific tool; see [references/tools.md](references/tools.md)
for all of them.

| The user asks about | Tool |
| --- | --- |
| What happened on a day or in a period | `timeline_question` |
| Statistics, totals, trends (steps, sleep, workouts, time spent) | `structured_data_question` |
| A memory, event or place they may have written about | `search_question` |
| Trips | `get_trips` |
| Restaurants, bars, hotels | `get_restaurants`, `get_bars`, `get_hotels` |
| Other kinds of places (museums, gyms, cafés…) | `get_places_by_category` |
| Books, movies, TV, music | `answer_media_question` |
| Meetings and appointments | `get_calendar_events` |
| The weather where they were | `personal-weather` |
| Home or current location | `get_user_home`, `get_user_location` |
| Recommendations nearby | `suggest_places` |
| A broad question, or one the others do not fit | `ask_about_user` |
| Noting something down | `add_note` |

- **Dates:** tools take dates as `YYYY-MM-DD`, inclusive, in the user's
  local time. Turn "last week" or "in March" into dates yourself.
- **Narrow first:** list with a date range rather than everything, and use
  `get_trips` to find a trip's dates before asking about what happened on
  it.
- **Questions in the user's words:** tools that take a `query` or
  `question` answer one self-contained question each; include the dates
  and names it needs.
- **Notes:** `add_note` writes to the user's journal at once. Add a note
  when the user asks for one, write it as they would in their own diary,
  and tell them it was added.
- **Privacy:** this is the user's personal data. Use it to answer them; do
  not pass it to other tools or services unless they ask you to.

## When a call fails

- **"The Time Atlas app could not be reached"**: the app is woken up for
  each call, which can take a few seconds and sometimes fails (for
  example when the phone is off or in Low Power Mode). Wait a moment and
  retry once; if it fails again, ask the user to open the app.
- **401 / sign-in required**: the sign-in has expired or was removed in
  the app. Sign in again with a new code.
- **"Unknown connection ID"**: the app has not registered its connection.
  Ask the user to open Time Atlas, then **Chat › Connect to Claude** once.
- The first call after a while can be slow while the app wakes up; that is
  normal.
