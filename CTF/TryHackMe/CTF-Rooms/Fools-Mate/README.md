Fools-Mate — README.md
# Fools-Mate

## Checkmate the Engine: Bypassing Client-Side and Server-Side Chess Validation

## Overview

Fools-Mate is a TryHackMe web exploitation challenge focused on bypassing client-side validation and interacting directly with the application's API.

The challenge presents a chess position where White has a mate-in-one move:

```text
6k1/5ppp/8/8/8/8/5PPP/R5K1

The correct move is:

Ra8#

However, the web interface refuses to allow the move and displays a Windows-style error dialog.

The objective is to understand why the browser rejects the move and bypass the client-side restriction by communicating directly with the backend API.

1. Reconnaissance

The first step was to inspect the application's network traffic.

The browser's window.fetch function was wrapped in the DevTools console so that every request and response could be observed:

const origFetch = window.fetch;
window.fetch = function(...args) {
  console.log('FETCH:', args);
  return origFetch(...args).then(r => r.clone().json().then(j => {
    console.log('RESP:', j);
    return r;
  }));
};

After making a normal move on the chess board, the API communication became visible.

The application sends moves to:

/api/move

using a POST request with a JSON body.

Example:

{
  "from": "f2",
  "to": "f3"
}

The server responds with information including:

The resulting FEN
Game status
The bot's reply move

No authentication token or request signature was required.

2. Understanding the Client-Side Validation

The application's frontend uses the chess.js library to validate chess moves.

When attempting to play the winning move:

Ra8#

the browser-side JavaScript determines that the move is blocked.

Instead of sending the request to the server, the client displays an error dialog.

This means the request never reaches the backend.

The important distinction is:

User
 ↓
Browser
 ↓
Client-side validation
 ↓
API

The client-side validation prevents the request from reaching the API.

Therefore, bypassing the browser interface allows the backend to be tested directly.

3. Bypassing the UI

Instead of interacting with the chess board, the API can be called directly from the browser's DevTools console.

The move was sent manually:

fetch('/api/move', {
  method: 'POST',
  headers: {'Content-Type': 'application/json'},
  body: JSON.stringify({from: 'a1', to: 'a8'})
}).then(r=>r.json()).then(console.log);

This bypasses the client-side chess validation entirely.

The request is sent directly to:

/api/move

with:

{
  "from": "a1",
  "to": "a8"
}
4. Server Response

The server accepted the move and returned:

{
  "ok": true,
  "move": "a1a8",
  "status": "checkmate",
  "winner": "white",
  "flag": "THM{REDACTED}"
}

The important result was:

status: checkmate
winner: white

The flag was also returned directly in the API response.

5. Attack Chain
Chess Application
        ↓
Inspect Network Traffic
        ↓
Hook window.fetch()
        ↓
Discover /api/move
        ↓
Identify JSON Request Format
        ↓
Identify Client-Side Validation
        ↓
Bypass Chess UI
        ↓
Call /api/move Directly
        ↓
a1 → a8
        ↓
Checkmate
        ↓
Flag
6. Key Lesson

Client-side validation should never be treated as a security boundary.

The browser is controlled by the user, meaning JavaScript validation can be inspected, modified, or completely bypassed.

In this challenge:

Client:
Rejects the move

Server:
Accepts the move

The backend therefore trusted a request that the frontend was designed to prevent.

7. Security Recommendation

Move legality should be enforced server-side against the actual game state.

The client can perform validation for:

User experience
Immediate feedback
Reduced unnecessary requests

However, the server must independently validate:

Whether the move is legal
Whether the piece can make the move
Whether the move is valid for the current game state
Whether the resulting game state is legitimate

The security model should therefore be:

Client Validation
       ↓
Convenience / UX

Server Validation
       ↓
Security / Correctness
Tools Used
Browser DevTools
JavaScript Console
Network / Fetch inspection
fetch()
chess.js
Key Takeaways
Client-side controls can be bypassed.
Browser JavaScript should never be considered a trusted security boundary.
DevTools can reveal hidden API endpoints and request formats.
Direct API interaction can bypass restrictions enforced only by the frontend.
Server-side validation is essential for security-sensitive application logic.