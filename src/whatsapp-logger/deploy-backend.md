---
label: 2. Deploy Backend
order: 870
---

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

!!!tip Go to `https://your-app.onrender.com/logs` to see the logs from server. You have to login first to see the logs.!!!

Continue to [Connect WhatsApp](connect-whatsapp.md).
