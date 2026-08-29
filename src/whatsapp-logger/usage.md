---
label: 5. Usage
order: 840
---

# Step 5: Usage

1. Navigate to your hosted frontend URL.
2. You'll see a login screen.
3. Enter the same `AUTH_USER` / `AUTH_PASS` configured on Render.
4. Once unlocked, your chats load from Firebase:
   - **Sidebar** — chat list sorted by newest activity
   - **Search** — filter contacts by name or phone number
   - **Export** — download chat history as a `.txt` file

## Missing history on a new device or browser?

If you open a chat and it shows nothing even though the server has history for it — for example right after clearing your browser's site data, or the first time you load the app on a new device — go to `Settings` → refresh icon → `Hard Reset`, enter your credentials, and it will pull your entire message history back down chat-by-chat, with a progress bar showing real fetch progress.

## Theme

Pick between Catppuccin Latte (light), Catppuccin Mocha (dark), or a true-black AMOLED theme under `Settings` → `Appearance` → `Theme`.

Continue to [Keep it Alive](keep-alive.md).
