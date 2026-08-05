---
label: 1. Firebase Setup
order: 880
---

# Step 1: Firebase Setup (The Database)

1. Go to the [Firebase Console](https://console.firebase.google.com/) and create a new project.

## Create the database

1. Navigate to **Firestore Database** in the sidebar.
2. Click **Create Database**.
3. Select a location (e.g. `nam5` or `eur3`).
4. Start in **Production Mode**.

## Set security rules

Go to the **Rules** tab in Firestore and replace the rules with the following. This allows anyone to read, but only your backend (via the Admin SDK) can write:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      // 1. Allow Read: Essential for your HTML page to fetch chats.
      allow read: if true;

      // 2. Allow Update: Enables the "Rename Chat" feature from the frontend.
      // This allows updating existing documents (like changing the name)
      // but prevents creating NEW documents or Deleting them.
      allow update: if true;

      // 3. Block Create/Delete: Only the Backend (Render) can create new messages
      // or delete them. This prevents random people from injecting fake chats.
      allow create, delete: if false;
    }
  }
}
```

## Get backend credentials (service account)

1. Go to **Project Settings** (gear icon) → **Service accounts**.
2. Click **Generate new private key**.
3. This downloads a `.json` file.

!!!danger Keep this safe
This file grants admin access to your database. You'll paste its contents into a Render environment variable in the next step — never commit it to a public repo.
!!!

## Get frontend configuration

1. Go to **Project Settings** → **General**.
2. Scroll to "Your apps" and click the **Web (`</>`)** icon.
3. Register the app (nickname: "Logger Frontend").
4. Copy the `firebaseConfig` object (API key, project ID, etc.) — you'll need it for `index.html` later.

Continue to [Deploy the Backend](deploy-backend.md).
