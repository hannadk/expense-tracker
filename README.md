# Expense Tracker

Income / expense / investment tracker. Works on any phone, installs like an app, works offline, downloads Excel reports, optional free sync across devices.

## Files
- index.html   - the whole app (design, themes, logic). Edit this to customise.
- config.js    - paste your Firebase values here to turn on sync across devices.
- manifest.json, sw.js, icon-192.png, icon-512.png - make it installable and offline.
- xlsx.full.min.js - Excel library (keep it).

## Customise on GitHub (no tools needed)
1. Open your repository on github.com, click index.html, then the pencil icon (Edit).
2. Make the change, click "Commit changes".
3. Wait about a minute, then refresh the site. If you still see the old version, close and reopen the app once.
Tip: ask Claude "change X in my index.html" and paste the file; paste the new version back in the editor.

## Turn on sync (same code = same data on every device) - free
1. Go to console.firebase.google.com, sign in with a Google account, Add project (turn Google Analytics off).
2. Build > Firestore Database > Create database. Pick a nearby location (e.g. asia-south1 Mumbai), start in Production mode.
3. Firestore > Rules tab. Replace everything with the text below, then Publish:

rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /trackers/{id} {
      allow get, create, update: if true;
      allow list, delete: if false;
    }
  }
}

4. Project settings (gear icon) > General > "Your apps" > Web icon (</>) > register app (any name, no hosting).
   Copy projectId and apiKey from the config shown.
5. On GitHub open config.js, edit, and put them between the quotes:
   window.CFG={projectId:"your-project-id",apiKey:"your-api-key"};
   Commit.
6. Open the app. Enter a code (6+ characters) twice. On your other devices enter the SAME code twice: your data loads.

## Notes
- Your code is the key to your data. Anyone who knows it can open your data, so use a code that is not easy to guess (6+ characters, letters and digits are better than 123456).
- Entries merge across devices; deletes also sync.
- Without config.js values the app still works, but each device keeps its own data.
- Download the Excel report now and then as a backup.
