# NutriLog – free setup (Firebase)

Google sign-in + cloud sync + hosting, all on Firebase's free **Spark** plan (no credit card).
Each person who signs in with their Google account gets their own private data, synced across phone and PC.

## 1. Create the Firebase project (5 min)
1. Open https://console.firebase.google.com and click **Add project** (name it e.g. `nutrilog-yourname`). You can turn Google Analytics off.
2. **Build → Authentication → Get started → Sign-in method → Google → Enable**, choose a support email, Save.
3. **Build → Firestore Database → Create database**, pick a location close to you (e.g. `asia-south1` Mumbai), start in **production mode**.
4. **Project settings (gear icon) → General → Your apps → Web app (`</>`)**. Register the app (tick *Also set up Firebase Hosting* if shown). Copy the `firebaseConfig` values.

## 2. Paste your config
Open `public/index.html`, search for `const CFG=` and replace the four placeholders:

```js
const CFG={apiKey:'...',authDomain:'YOUR-PROJECT-ID.web.app',projectId:'YOUR-PROJECT-ID',appId:'...'};
```
Tip: set `authDomain` to `YOUR-PROJECT-ID.web.app` (not `.firebaseapp.com`). Sign-in works more reliably on phones.
The apiKey in this config is not a secret. Your data is protected by `firestore.rules`.

## 3. Deploy (free hosting + security rules)
Install Node.js, then in this folder:
```
npm install -g firebase-tools
firebase login
firebase use --add        # pick your project
firebase deploy
```
You get a live link like `https://YOUR-PROJECT-ID.web.app`.

## 4. Use it on your phone
Open the link, tap **Continue with Google**, then add it to your home screen
(Android Chrome: ⋮ → Install app. iPhone Safari: Share → Add to Home Screen).
If the page was opened before on that device, the app offers to upload the data saved in that browser to your account.

## Family and friends
Just share the link. Everyone signs in with their own Google account and sees only their own data.

## Good to know
- **Free limits (Spark):** Firestore allows roughly 50,000 reads and 20,000 writes per day and 1 GiB storage. A handful of people logging meals stays far below that.
- **AI food estimates:** optional. Each person can paste their own Anthropic API key under Today → Goals & limits. The key stays on that device only, so nobody else pays for it.
- **Offline:** works offline; changes sync when you are back online.
- **Alerts:** calorie alerts show inside the app (and as browser notifications while it is open). Background push needs a paid server, so it is not included.
- **Backups:** Today → Goals & limits → Backup & restore still works.
- **Not set up yet?** If you leave the placeholders, the app runs in "this browser only" mode (no login), like before.
