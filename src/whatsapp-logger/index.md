---
label: WhatsApp Logger
icon: comment-discussion
order: 900
---

# WhatsApp Logger (Self-Hosted)

A privacy-focused, self-hosted WhatsApp archiving tool. It captures messages — including deleted ones — via a linked device connection and stores them in your own Firebase Firestore database.

!!!warning Security update in v4.2.1
Versions before v4.2.1 shipped a public Firebase Web SDK config in the frontend, which let anyone who viewed the page source read your chat database directly, bypassing login. As of v4.2.1, the frontend talks only to your Render backend over an authenticated connection — Firestore is never reachable from the browser. If you're on an older version, update and follow the revised [Firebase Setup](firebase-setup.md) and [Frontend Setup](setup-frontend.md) steps.
!!!

!!!success Is this safe to use?
Yes. WhatsApp bans accounts for *sending* spam or unauthorized automated messages — this tool is a **100% passive, read-only listener**. It connects using the official Multi-Device WebSocket protocol, the same way linking a second browser to WhatsApp Web works. Since it doesn't interact with anyone, there's no risk of being reported.
!!!

## Features

- **Anti-Delete** — messages are logged instantly, so they're preserved even if the sender deletes them
- **Privacy first** — you host the backend and database; no third-party servers touch your data
- **Secure access** — the frontend is password-protected against your own backend
- **Search & filter** — search by content or filter by date
- **Export** — download chat logs as `.txt` files
- **Offline ready** — IndexedDB caching lets you read logs without an internet connection

## Recommended setup

- Install the web app as a **PWA** after publishing it, for better security and a native feel
- Enable **PIN or biometric authentication** inside the web app (Settings)

## Get started

- [Prerequisites & Architecture](prerequisites.md)
- [Step 1 — Firebase Setup](firebase-setup.md)
- [Step 2 — Deploy the Backend](deploy-backend.md)
- [Step 3 — Connect WhatsApp](connect-whatsapp.md)
- [Step 4 — Setup the Frontend](setup-frontend.md)
- [Step 5 — Usage](usage.md)
- [Step 6 — Keep it Alive](keep-alive.md)
- [Troubleshooting](troubleshooting.md)

## Disclaimer

This tool is for personal archiving purposes. Using it to log conversations without consent may violate privacy laws in your jurisdiction. The author is not responsible for misuse.
