# SafeTour — Vercel demo deployment

## Direct ZIP/folder deployment

1. Extract this ZIP. In Vercel, open the existing `safetour-ai` project, then drag the **extracted folder** into the deployment upload area. If the UI rejects folders, import the extracted source through GitHub.
2. Framework: Vite. Build: `npm run build:frontend`. Output: `dist`.
3. Set environment variables under Project Settings > Environment Variables:
   - `DIGITAL_ID_SECRET`: long random secret (required for API function to initialize).
   - `GEMINI_API_KEY`: your Gemini API key, server-side only, if you use AI features.
   - `GOOGLE_MAPS_PLATFORM_KEY`: Google Maps browser key (restricted to your Vercel domains and appropriate Google APIs).
4. Redeploy after saving environment variables.
5. Verify `/api/health`, tourist login, map, and AI features.

## Important limitations — SIH DEMO ONLY

The API is deployed as a serverless Express function. The app still uses a JSON database stored in `/tmp`, which is **ephemeral and not shared between function instances**. Registration, incidents, SOS records, and digital IDs are **not reliable or durable** and must NOT be used for real emergency response or personal records. Migrate to a hosted database before any real-world use.

The Gemini Live WebSocket (`/live`) cannot run on Vercel Functions. Live voice streaming requires a separate long-running WebSocket service or a supported realtime architecture. This is NOT a full production deployment.

Keep this project as an SIH prototype, and use simulated alerts and anonymized demo data. The bundled sensitive database has been excluded.
