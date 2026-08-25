# Prerequisites

Before you start, make sure you have the following:

1. A **GitHub** account
2. A **Render** account (free tier works)
3. A **Firebase** account (free Spark plan works)
4. A **WhatsApp** account on your phone
5. An **UptimeRobot** account (free)

## How it fits together

- **Backend (Render + Docker)** — runs the Baileys WhatsApp listener, authenticates the frontend, and writes messages to Firestore
- **Database (Firebase Firestore)** — stores your chat logs
- **Frontend (`index.html`)** — a single static file you host anywhere (Firebase Hosting, GitHub Pages, Netlify, Vercel). It never talks to Firestore directly — it authenticates against and streams chat data from your Render backend only
- **UptimeRobot** — pings your Render backend every 5 minutes so the free tier doesn't spin down from inactivity

Continue to [Firebase Setup](firebase-setup.md).
