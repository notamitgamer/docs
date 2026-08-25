# Step 1: Firebase Setup (The Database)

1. Go to the [Firebase Console](https://console.firebase.google.com/) and create a new project.

## Create the database

1. Navigate to **Firestore Database** in the sidebar.
2. Click **Create Database**.
3. Select a location (e.g. `nam5` or `eur3`).
4. Start in **Production Mode**.

## Set security rules

Go to the **Rules** tab in Firestore and replace the rules with the following. As of v4.2.1, the frontend never talks to Firestore directly — it only talks to your Render backend, which uses the Admin SDK (which always bypasses these rules regardless of what they say). So there's no reason for any client-side reads or writes to be allowed:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      // Deny all direct client access. The Admin SDK (your Render backend)
      // bypasses these rules entirely, so this only blocks browsers/apps
      // that try to read or write Firestore directly with a client SDK.
      allow read, write: if false;
    }
  }
}
```

!!!danger If you're upgrading from an older version
Earlier versions of this project shipped a public `firebaseConfig` in the frontend with permissive `allow read: if true` rules — this let anyone who inspected the page source read your entire chat database directly, bypassing the login screen. If you're on v4.2.1 or later, switch to the rules above and make sure your `index.html` has no `firebaseConfig` or Firebase SDK `<script>` tags left in it (see [Setup the Frontend](setup-frontend.md)).
!!!

## Get backend credentials (service account)

1. Go to **Project Settings** (gear icon) → **Service accounts**.
2. Click **Generate new private key**.
3. This downloads a `.json` file.

!!!danger Keep this safe
This file grants admin access to your database. You'll paste its contents into a Render environment variable in the next step — never commit it to a public repo.
!!!

That's everything you need from Firebase — the frontend doesn't need any Firebase configuration at all. It only ever talks to your Render backend, which uses the service account credentials above.

Continue to [Deploy the Backend](deploy-backend.md).
