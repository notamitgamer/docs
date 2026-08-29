# Step 2: Deploy Backend (The Listener)

1. **Fork the repository** to your own GitHub account: [WhatsApp-Logger-Self-Hosted-](https://github.com/notamitgamer/WhatsApp-Logger-Self-Hosted-)
2. Log in to [Render](https://render.com/).
3. Click **New +** → **Web Service**.
4. Connect your forked repository.
5. **Runtime**: select **Docker**.
6. Add the following **environment variables** under "Advanced":

| Variable | Value |
|---|---|
| `FIREBASE_SERVICE_ACCOUNT` | The entire content of the service-account JSON file downloaded in the Firebase step |
| `AUTH_USER` | A username of your choice (e.g. `admin`) |
| `AUTH_PASS` | A strong password — this locks your logger |

7. Click **Create Web Service**.
8. Wait for deployment to finish. Render gives you a URL like `https://your-app.onrender.com`.

!!!tip Logs
Go to `https://your-app.onrender.com/logs` to see the logs from server. You have to login first to see the logs.
!!!

## Excluding specific chats from logging

If there are chats you don't want logged at all — a bot, a broadcast/status JID, a business account — edit `EXCLUDED_JIDS` in `src/config.js` on your fork before deploying:

```javascript
// --- CONFIGURATION ---
const PORT = process.env.PORT || 3000;
const AUTH_USER = process.env.AUTH_USER;
const AUTH_PASS = process.env.AUTH_PASS;
const MAX_LOGS = 500;
const MAX_CONNECTIONS_PER_TOKEN = 15;
const VERSION = '4.2.3';
const EXCLUDED_JIDS = new Set(['']);

module.exports = {
    PORT,
    AUTH_USER,
    AUTH_PASS,
    MAX_LOGS,
    MAX_CONNECTIONS_PER_TOKEN,
    VERSION,
    EXCLUDED_JIDS
};
```

`EXCLUDED_JIDS` is a set of full JIDs (the `...@s.whatsapp.net` / `...@g.us` / `...@lid` identifiers, not just a phone number) that are skipped entirely — they won't be cached, streamed, or included in exports. It ships empty by default. You can find a chat's exact JID from the live server logs (see the tip above) the first time it logs a message, then add it here, e.g. `new Set(['917278779512@s.whatsapp.net', '201554426618024@lid'])`, and redeploy.

Continue to [Connect WhatsApp](connect-whatsapp.md).
