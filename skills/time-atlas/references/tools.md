# Time Atlas MCP tools

The server's own `tools/list` has the full descriptions and input schemas;
this is an overview for choosing between them. All tools except `add_note`
only read.

## Questions answered from the timeline

These take a question and answer it from the user's data, so ask one
complete question at a time.

- **`timeline_question`**: what happened in a date range: places,
  movements, activities, notes. "What did I do last Tuesday?", "Describe
  my week from Jan 1 to 7."
- **`structured_data_question`**: statistics and trends from tracked data:
  steps, distances, workouts, sleep, time spent at places, logged tallies.
  "How much did I walk last week?", "What's my average sleep this month?"
- **`search_question`**: searches journal notes and location history for
  specific events, places or memories; can be limited to a period.
  "When did I last go to the dentist?", "What did I write about the
  concert?"
- **`answer_media_question`**: books, movies and TV from the reading and
  viewing history and notes, with optional ratings and dates, and music
  listened to (from Last.fm): the most played artists, tracks and albums,
  or with `music_search` those of one artist, track or album. "What books
  did I read last year?", "Which five-star movies have I seen?", "When did
  I last listen to Radiohead?"
- **`ask_about_user`**: asks Pat, the app's own assistant, which knows the
  whole record including routines and people. Good for broad questions:
  "What kind of food do I like?", "Who did I spend time with in Paris?"

## Lists

These return records to work with; most take optional `start_date` and
`end_date`.

- **`get_trips`**: trips with dates, places and the user's description.
- **`get_restaurants`**, **`get_bars`**, **`get_hotels`**: places visited,
  with visit counts, meals, first and last visits, ratings and notes. Most
  visited first.
- **`get_places_by_category`**: the same for any other category, such as
  `museum`, `gym`, `cafe` or `park` (singular).
- **`get_calendar_events`**: calendar events, with an optional text query.
  What was planned, not necessarily what happened.
- **`personal-weather`**: weather observations where the user was: time,
  place, condition, temperature, wind and more. Long periods are thinned
  out evenly; ask for a shorter period for every observation.

## Where the user is

- **`get_user_home`**: home coordinates and address.
- **`get_user_location`**: the latest location of the phone, with the
  place there.
- **`suggest_places`**: recommendations for places or things to do,
  near the user unless told otherwise.

## Writing

- **`add_note`**: adds a note to today's journal, without asking the user.
  It shows in the app's diary with the day.
