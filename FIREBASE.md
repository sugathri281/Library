# Set up your free database (Firebase)

This gives the app somewhere to keep your notes so they sync between your phone and your computer. It costs nothing for a personal library of notes, and it's a separate Google product from any Supabase projects you already have, so it won't use up those.

## 1. Create the project

1. Go to console.firebase.google.com and sign in with a Google account.
2. Click **Add project** (or **Create a project**). Give it any name, e.g. `study-library`. You can decline Google Analytics for this project — it isn't needed.
3. Wait for it to finish setting up, then continue into the project.

## 2. Turn on email sign-in

1. In the left menu, open **Build** → **Authentication**.
2. Click **Get started** if this is the first time, then open the **Sign-in method** tab.
3. Choose **Email/Password**, turn it **on**, and save.

## 3. Create the Realtime Database

1. In the left menu, open **Build** → **Realtime Database**.
2. Click **Create Database**. Pick the location closest to you.
3. When asked about security rules, choose **Start in locked mode** (we'll paste proper rules next).
4. Once it's created, open the **Rules** tab and replace everything with:

```json
{
  "rules": {
    "users": {
      "$uid": {
        ".read": "auth != null && auth.uid === $uid",
        ".write": "auth != null && auth.uid === $uid",
        "topics": {".indexOn": "updated"},
        "examples": {".indexOn": "updated"},
        "questions": {".indexOn": "updated"},
        "plans": {".indexOn": "updated"},
        "links": {".indexOn": "updated"}
      }
    }
  }
}
```

5. Click **Publish**. This means each signed-in person can only ever read or write their own notes — nobody else's, including other people who might one day use the same project.

## 4. Get your two connection values

1. Still on the **Realtime Database** page, copy the **URL** shown near the top — it looks like `https://your-project-default-rtdb.firebaseio.com` or ends in `.firebasedatabase.app`.
2. Go to the gear icon → **Project settings** → **General** tab. Under "Your apps", if there's no web app yet, click the `</>` icon to register one (any nickname, no other options needed). Copy the **Web API Key** shown there — a string starting `AIza...`.

## 5. Connect the app

1. Open the app (the address from the hosting guide, or right here if you haven't hosted it yet).
2. On first open it asks for these two values. Paste them in and continue.
3. Create an account with any email address and a password of your choosing — this is just to keep your notes private to you, nothing gets emailed and there's no confirmation step.
4. That's it. Open the same address on your other device and sign in with the same email and password to see the same notes.

## Notes on how this works

- Your notes are still kept on each device (so the app stays fast and works offline). They also get copied to your Firebase project whenever you have a signal, so every signed-in device catches up.
- If you edit the same topic on two devices while both are offline, the version saved most recently wins when they reconnect. For anything important, it's still worth keeping the occasional backup file from More → Download backup.
- The security rules above are what actually keep your notes private — not just the app's own logic — so it's worth pasting them in exactly as shown.
- If you ever want to stop syncing, use More → "Use a different database" to disconnect. Your notes stay on that device either way.
- Firebase's free Spark plan comfortably covers a personal notes library (the built-in limits are generous for text), and it's billed per project, so your other two Supabase projects are unaffected.
