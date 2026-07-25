# The Sweet Ledger

A mobile point-of-sale app for logging sales and tracking stock, shared live across every device on your team. Runs entirely in the browser — no app store needed.

## What you're setting up

- **Firebase Realtime Database** — a free, hosted database that stores your products and sales, and pushes updates to every phone instantly.
- **GitHub Pages** — free hosting for the app itself, at a public URL you can open on any phone.

Total time: about 20–30 minutes, once.

---

## Step 1 — Create a Firebase project (~5 min)

1. Go to [console.firebase.google.com](https://console.firebase.google.com) and sign in with a Google account.
2. Click **Add project**, give it a name (e.g. `sweet-ledger`), and finish the setup wizard. You can turn off Google Analytics — you don't need it.
3. Once the project is created, click the **`</>`** (web) icon on the project overview page to register a new web app. Give it any nickname. You don't need Firebase Hosting here — that checkbox can stay unchecked.
4. Firebase will show you a `firebaseConfig` object that looks like this:

   ```js
   const firebaseConfig = {
     apiKey: "AIzaSy...",
     authDomain: "sweet-ledger.firebaseapp.com",
     databaseURL: "https://sweet-ledger-default-rtdb.firebaseio.com",
     projectId: "sweet-ledger",
     storageBucket: "sweet-ledger.appspot.com",
     messagingSenderId: "123456789",
     appId: "1:123456789:web:abcdef"
   };
   ```

   Keep this tab open — you'll need these values in Step 3.

## Step 2 — Turn on the Realtime Database (~5 min)

1. In the left sidebar of the Firebase Console, go to **Build > Realtime Database**.
2. Click **Create Database**. Pick any location close to you.
3. When asked about security rules, choose **Start in test mode** for now (we'll lock it down properly next).
4. Once created, go to the **Rules** tab and replace the contents with what's in `firebase-rules.json` in this folder, then click **Publish**.

   This restricts the database so only the `products` and `sales` paths this app uses can be read or written — nothing else on your Firebase project is exposed.

   > **Note on security:** these rules allow anyone who has your app's URL and Firebase config to read and write sales data — there's no login. That's normal for a small internal team tool, but if you ever want to lock it down further (e.g. require a login), Firebase Authentication can be added later — just ask.

## Step 3 — Add your config to the app (~2 min)

1. Open `index.html` in a text editor.
2. Find this block near the top of the `<script>` section:

   ```js
   const firebaseConfig = {
     apiKey: "YOUR_API_KEY",
     authDomain: "YOUR_PROJECT.firebaseapp.com",
     databaseURL: "https://YOUR_PROJECT-default-rtdb.firebaseio.com",
     projectId: "YOUR_PROJECT",
     storageBucket: "YOUR_PROJECT.appspot.com",
     messagingSenderId: "YOUR_SENDER_ID",
     appId: "YOUR_APP_ID"
   };
   ```

3. Replace it with the real values from Step 1.
4. Save the file.

## Step 4 — Push to GitHub (~5 min)

If you don't already have a repo for this:

```bash
cd sweet-ledger
git init
git add .
git commit -m "Sweet Ledger POS app"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/sweet-ledger.git
git push -u origin main
```

(Create the empty repo on GitHub first at github.com/new, without a README, then run the commands above.)

## Step 5 — Turn on GitHub Pages (~2 min)

1. On GitHub, open your repo's **Settings > Pages**.
2. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
3. Set **Branch** to `main` and folder to `/ (root)`, then **Save**.
4. GitHub will give you a live URL after a minute or two, typically:

   ```
   https://YOUR_USERNAME.github.io/sweet-ledger/
   ```

## Step 6 — Install it on phones (~1 min per phone)

Open that URL on each phone, then:

- **iPhone:** tap the Share icon → **Add to Home Screen**
- **Android:** tap the Chrome menu (⋮) → **Add to Home screen**

It'll launch full-screen with its own icon from then on, and every device will see the same live sales and stock data.

---

## Updating the app later

Any time you want to change something (add a feature, tweak styling), edit `index.html`, then:

```bash
git add .
git commit -m "describe your change"
git push
```

GitHub Pages redeploys automatically within a minute or two.
