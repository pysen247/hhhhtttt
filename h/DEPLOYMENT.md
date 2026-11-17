# SafeTour deployment readiness

## Current architecture
The project runs an Express HTTP server, a WebSocket Gemini Live endpoint, and a Vite React frontend in one long-lived Node process. Data persists in a local JSON file. This is not compatible with a standard Vercel static-site deployment: static hosting cannot serve `/api/*`, WebSocket sessions, or durable filesystem writes.

## Safe deployment path
1. Build locally with `npm install`, `npm run lint`, and `npm run build`.
2. Move persistent records and sessions to managed PostgreSQL; migrate passwords and records without exposing passport or emergency contact data.
3. Deploy the Node/Express/WebSocket backend to a persistent Node hosting service with WebSocket support and persistent database connectivity. Set `NODE_ENV=production`, `DIGITAL_ID_SECRET`, `GEMINI_API_KEY`, database connection secret, and correct CORS origin.
4. Deploy the Vite frontend to Vercel after configuring its API base URL and the WebSocket URL to point to the backend; configure the frontend's Maps browser key with appropriate referrer restrictions.
5. Validate end-to-end tourist login, authority access, itinerary generation, SOS simulations, and location permissions. Never describe simulated alerts as connected to emergency responders.

## Secrets and privacy
Never commit `.env`, `.env.local`, `data/safetour_db.json`, actual API keys, user profiles, or production records. Rotate any keys accidentally published. The bundled project uses sample emergency and safety data; it is not an emergency dispatch system.

## Current verification
Dependency installation was attempted but did not finish before timeout in this environment. Lint/build/runtime verification remains pending. No live production deployment has been confirmed.

## Vercel frontend configuration (prepared)
`vercel.json` configures a Vite frontend-only build and SPA navigation. It deliberately excludes `/api/*` from SPA rewrites. The existing Express/WebSocket backend must be hosted separately and frontend API calls updated before a functional deployment. This is not a complete SafeTour deployment.
