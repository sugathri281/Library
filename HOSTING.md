# Put Study Library on your phone (free, works offline)

The app is a handful of static files. It needs a web address of its own so that Chrome on Android can install it and keep it available offline. Any free static host works. GitHub Pages is described below because it costs nothing and stays up.

## Steps (GitHub Pages)

1. Create a free account at github.com and sign in.
2. Create a new repository. Name it something plain, such as `study`. Choose Public. (A free account can only publish public repositories. The repository holds only the app, never your notes.)
3. Open the repository, choose Add file, then Upload files. Drag in **all files from this folder**: `index.html`, `manifest.webmanifest`, `sw.js` and the three `icon-*.png` files. Commit the upload.
4. Open the repository's Settings, then Pages. Under Build and deployment, set Source to Deploy from a branch, pick the `main` branch and the `/ (root)` folder, and save.
5. After a minute or two the page shows your address, usually `https://YOUR-NAME.github.io/study/`.
6. On your Android phone, open that address in Chrome. Wait for it to finish loading once, then use the menu and choose **Install app** (or Add to Home screen). Open it once from the new icon while you are online, so fonts and helpers are saved for offline use.

Other free hosts (Cloudflare Pages, Netlify) also work with the same files.

## Setting up your database

This version of the app needs a small free database so your notes sync between your phone and your computer, instead of staying stuck on one device. Follow **FIREBASE.md** (in this same folder) once, before or after hosting the files — it walks through creating a free Supabase project, running one script, and connecting the app. The app will ask you for two values from that setup the first time you open it.

## Moving notes you already had in the old, local-only version

1. In the old version, open More and choose Download backup.
2. In this new version, once you're signed in, open More, choose Restore from backup, pick that file, and choose Replace.


## What works offline

Once you have signed in at least once, reading, highlighting, editing, the glance map, revision schedule, the answer studio, export to Word and PDF, and read-aloud (using your phone's installed voices) all work with no signal. Anything you change while offline is held on the device and copied to your database automatically the next time you have a connection.

Signing in for the very first time, and importing Word or PDF files, both need a connection.

## Updating the app later

Replace `index.html` in the repository. Then change `VERSION` at the top of `sw.js` (for example `studylib-v2`) so phones pick up the new version. Close and reopen the app once or twice.
