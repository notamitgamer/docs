---
label: 4. Setup Frontend
order: 850
---

# Step 4: Setup Frontend (The Viewer)

1. Download `index.html` from the repository.
2. Open it in a text editor.
3. Find the configuration line near the top of the `<script>` block. Before editing, it looks like this:

```javascript
const RENDER_BACKEND_URL = "";
```

4. Fill in your Render URL, e.g. `https://your-app.onrender.com` (**no trailing slash**).

That's the only setting needed. As of v4.2.1, the frontend has no Firebase configuration of its own — it authenticates against your Render backend (`/api/verify`) and gets a session token back, then uses that token for every chat/message request over Server-Sent Events. Firebase credentials only ever live on the backend, set in [Deploy the Backend](deploy-backend.md).

## Deploy the frontend

You can host this single file anywhere:

- **Firebase Hosting** (recommended): `firebase init` → Hosting → select `public` directory → put `index.html` there → `firebase deploy`
- **GitHub Pages**: enable Pages in your repo settings
- **Netlify / Vercel**: drag and drop the folder containing `index.html`

Continue to [Usage](usage.md).
