---
label: Roadmap
icon: milestone
order: 810
---

# Roadmap: Media Upgrade & Security Enhancements

!!!warning In progress
This work lives on a separate branch. **Do not sync your fork with it yet** — it may break the logger until it's finished.
!!!

Firebase's free tier caps storage at 1GB, which isn't viable for media. The plan is to keep text messages in Firebase as-is, and offload images, videos, and voice messages to Hugging Face storage instead, fronted by a Cloudflare CDN.

## Phase 1 — Architecture & infrastructure

- Detect `imageMessage`, `videoMessage`, and `audioMessage` types in the Baileys listener
- Extract binary buffers with Baileys' `downloadMediaMessage`
- Push buffers to a Hugging Face dataset repo via the HF Hub API
- Serve media through a Cloudflare Pages + Workers CDN, so HF API tokens are never exposed to the frontend
- Store the resulting Cloudflare CDN URL, `mimeType`, and metadata in the existing Firestore `Messages` collection

## Phase 2 — Backend (`index.js`)

- Add dependencies for Hugging Face Hub uploads (`axios` or `fetch`)
- Expand the `messages.upsert` listener with conditional checks for media attachments
- Add an async upload utility that pushes buffers to Hugging Face and builds the Cloudflare CDN URL
- Extend the Firestore `set` operation with `mediaUrl`, `mediaType`, and `caption` (falling back to `text`)

## Phase 3 — Frontend (`index.html`)

- Update `renderMsgs` to check for `mediaUrl` and conditionally render `<img loading="lazy">`, `<video controls>`, or `<audio controls>`
- Keep media containers consistent with the existing Material Design 3 styling (12px border radius, surface container alignment)
- Rely on browser caching via Cloudflare CDN headers for media rather than storing raw files in IndexedDB or the service worker cache

## Phase 4 — Security

- Re-verify Firestore rules stay read-only/update-only safe with the new media metadata shape
- Ensure `escapeHTML` correctly sanitizes incoming media URLs to prevent XSS
- Add CSP headers on the frontend deployment to whitelist the specific Cloudflare subdomains used for media delivery

## Phase 5 — Testing & deployment

- Run the Docker container locally to confirm Baileys downloads/buffers large video files without crashing
- Verify the Cloudflare Worker proxies Hugging Face dataset URLs with correct CORS headers
- Push to GitHub and monitor Render build logs for the updated backend
