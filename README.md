# AURA Rajyotsava Cup 2026 – Live Score

Live badminton scoring for GitHub Pages, with scorer login (Firebase).

- **Scorer page:** `https://<your-github-name>.github.io/<repo>/` → sign in → score
- **Spectator live view (no login):** `https://<your-github-name>.github.io/<repo>/#watch`

Files: `index.html` (the app), `config.js` (your Firebase settings), `firestore.rules` (who can score).

---

## One-time setup (about 15 minutes)

### 1. Create the Firebase project (free "Spark" plan)
1. Go to https://console.firebase.google.com → **Add project** → name it e.g. `rajyotsava-live` → you can turn Google Analytics off → **Create**.
2. On the project home page click the **Web** icon `</>` → app nickname `live-score` → **Register app** (no need for Firebase Hosting).
3. Firebase shows a `firebaseConfig = { ... }` block. Copy those six values into **config.js**, replacing the `PASTE_...` text.

### 2. Turn on scorer login
1. Left menu **Build → Authentication → Get started**.
2. **Sign-in method** tab → **Email/Password** → enable the first switch → **Save**.
3. **Users** tab → **Add user** → enter each scorer's email and a password. (Scorers can later use "Forgot password?" on the sign-in screen to set their own.)
4. **Settings** tab → **Authorized domains** → **Add domain** → `<your-github-name>.github.io`

### 3. Create the score database
1. Left menu **Build → Firestore Database → Create database** → choose location **asia-south1 (Mumbai)** → start in **production mode**.
2. Open the **Rules** tab, delete what is there, paste the whole of **firestore.rules**, put your scorers' emails in the list (lowercase), and click **Publish**.

### 4. Publish on GitHub Pages
1. Create a repository (e.g. `rajyotsava-live`) and upload **index.html** and **config.js** (README and firestore.rules are optional).
2. Repository **Settings → Pages → Build and deployment → Deploy from a branch → main / (root) → Save**.
3. After a minute the site is live at `https://<your-github-name>.github.io/rajyotsava-live/`.

---

## Adding or removing a scorer
- Add their login in **Authentication → Users**, and add their email to the list in **Firestore → Rules** → **Publish**.
- To remove someone, delete their email from the Rules list (and the user, if you like).

## Matchday tips
- Use one phone per tie. If it dies, another scorer signs in and taps **Resume** on that tie.
- Delete practice ties from the scorer screen (Delete tie → tap again) before the tournament.
- Free plan limits (50,000 reads and 20,000 writes per day) comfortably cover a club tournament.
  Every point is one write; every spectator update is one read per open screen.
