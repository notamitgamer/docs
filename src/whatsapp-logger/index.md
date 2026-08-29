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

## Upgrade notes (v4.2.x)

If you're updating from an older version, here's everything that changed across the v4.2.x line in one place:

- **v4.2.1 — Security fix.** Removed the public Firebase Web SDK config from the frontend (see the warning above). The frontend now only talks to your Render backend, never Firestore directly. Update your Firestore rules to deny all direct client access, as shown in [Firebase Setup](firebase-setup.md).
- **v4.2.2 — Real-time sync now covers every chat, not just the one you have open.** Previously, new messages only arrived for a chat you already had open — anything happening in other chats sat on the server until you clicked into them. Now a single sync connection streams updates for *all* chats at once, so incoming messages show up across every contact the moment they arrive, the way WhatsApp itself behaves when your phone comes back online.
- **v4.2.2 — Full resync with real progress.** `Settings` → refresh icon → `Hard Reset` now pulls your entire message history chat-by-chat instead of one giant download, so the progress bar reflects actual messages fetched instead of a rough guess. Use this if you ever open a chat that shows nothing locally even though the server has history for it — for example after clearing site data, or on a new device or browser.
- **UI refresh.** Reworked to three selectable themes — Catppuccin Latte (light), Catppuccin Mocha (dark), and a true-black AMOLED theme — replacing the old dark-mode toggle and the multiple chat-background picker. Find it under `Settings` → `Appearance` → `Theme`.

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
- [Frequently Asked Questions](faqs.md)

## Disclaimer

This tool is for personal archiving purposes. Using it to log conversations without consent may violate privacy laws in your jurisdiction. The author is not responsible for misuse.
