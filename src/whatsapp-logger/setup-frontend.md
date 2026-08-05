---
label: 4. Setup Frontend
order: 850
---

# Step 4: Setup Frontend (The Viewer)

1. Download `index.html` from the repository.
2. Open it in a text editor.
3. Find the configuration section (around line 675). Before editing, it looks like this:

```javascript
const RENDER_BACKEND_URL = "";

// Firebase Config
const firebaseConfig = {
    apiKey: "",
    authDomain: "",
    projectId: "",
    storageBucket: "",
    messagingSenderId: "",
    appId: ""
};
```

4. Fill in the details:
   - `RENDER_BACKEND_URL` — your Render URL, e.g. `https://your-app.onrender.com` (**no trailing slash**)
   - `firebaseConfig` — the keys you copied during [Firebase Setup](firebase-setup.md)

## Deploy the frontend

You can host this single file anywhere:

- **Firebase Hosting** (recommended): `firebase init` → Hosting → select `public` directory → put `index.html` there → `firebase deploy`
- **GitHub Pages**: enable Pages in your repo settings
- **Netlify / Vercel**: drag and drop the folder containing `index.html`

Continue to [Usage](usage.md).
