# Troubleshooting

**"No chats found"**
: Send a message to the linked WhatsApp account to trigger the first log.

**"Incorrect Credentials"**
: Make sure your Render backend is running, and that you're using the exact `AUTH_USER` / `AUTH_PASS` defined in Render's environment variables.

**Chat shows a long ID (e.g. `1155...@lid`) instead of a phone number**
: Wait a few minutes — the backend automatically syncs contacts and updates the record with the real phone number.
