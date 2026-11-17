# SafeTour security and deployment notes

## Changes in this iteration
- New signup passwords are salted with Node.js `scrypt` before storage.
- Removed predictable, pre-authorized demo bearer tokens.
- Demo accounts are denied login in production. In development their passwords are hashed in memory.
- Login rejects malformed credential types.
- Signup requires passwords of at least 10 characters.

## Remaining blockers before public release
- Replace JSON file persistence with managed PostgreSQL and a migration for existing accounts.
- Replace in-memory sessions with expiring, revocable, server-side persisted sessions.
- Implement rate limiting for authentication and SOS requests.
- Adapt Express and WebSocket routes for the chosen hosting architecture.
- Remove or replace all demonstration personal data; confirm all endpoints enforce ownership and roles.
- Audit client-side handling of Google Maps keys and backend Gemini keys.
- Build, lint and integration-test in an environment with npm registry access.
- Verify SOS workflows with simulations only; do not claim emergency-service integration without evidence.

## Local checks
`npm install && npm run lint && npm run build && npm run dev`

Never commit `.env.local`, real credentials or `data/safetour_db.json`.
