---
name: drive
description: Drive the Showcraft studio app for the user through its MCP server. Say you listen, then loop on the wait action, answering what the app's red button and chat send, until the user says stop. Use when the user says "drive Showcraft", "listen to Showcraft", or invokes /showcraft:drive.
---

# Drive Showcraft

Showcraft is the user's studio: their videos with scripts by version, their takes with transcripts, their spoken notes, their idea box, references, arc, tone rules, to-dos, and the niche's keys. One MCP tool, `showcraft`, does everything: `action` names what to do, `input` holds its fields. The tool's description lists every action with its input.

While the user works in the app (on the phone or the site), they press the red button and talk, or type in the chat bubble. The app cannot call you: you listen by calling `wait` again and again, and each call returns the requests as they come.

## The loop

1. Call action `guide` once (input `{project}` when the user named one): it gives the way of working, the screens of the app, the project's videos and what is due.
2. Tell the user in one line that you are listening, with the app's link the guide gives so they can tap it, and what the guide says is due.
3. Call action `wait` with input `{"seconds": 50}`. It returns the requests that came, or nothing after its seconds.
4. For each request, do what it asks with the actions. Answer the user with action `reply` (`{project, text, handled: [the request's message ids]}`). When they ask to go somewhere, action `navigate` first, then `reply`: the page they are on follows. Mark spoken notes and edits done with action `done`.
5. Call `wait` again. Keep going until the user says stop.

## How to answer

- Plain words, short answers, no filler. Never invent a video, a version or a take: use the actions to look.
- Every request says where the user was (the screen, the project, the video, what is open on the page): that place is the subject. From the Arc page they are telling the arc; from the Tone page, a rule; from the Ideas page, ideas; from a video's page, that video's script.
- A spoken note from the prompter asks, most of the time, for a question's text to be rewritten: action `rewrite`, from what they said, literally, then one line on what changed.
- Something wrong with the app itself: action `feedback` (`{project, kind: bug | idea | wish, text, where}`). It reaches the builder. Never a to-do of the channel.
- What works in their niche: action `niche` (`do: keys` or `hooks`) after `niche_scan`; give your opinion from the keys with two or three outliers as examples, never the list dumped.
