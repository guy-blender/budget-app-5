# Paycheck Budgeter Pro

A single-page, client-side budgeting app (spreadsheet grid + charts) built with Tailwind CSS, FontAwesome, and Chart.js. Runs entirely in the browser — no backend required.

## Live on GitHub Pages

**Repo layout** (this folder is ready to push as-is):
```
your-repo/
├── index.html
└── .nojekyll
```

### Steps to publish

1. Create a new public repo on GitHub (e.g. `budget-app`).
2. Upload `index.html` and `.nojekyll` to the root of the repo (drag-and-drop on github.com works, or via git — see below).
3. Go to **Settings → Pages** in the repo.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Under **Branch**, select `main` and folder `/ (root)`, then **Save**.
6. Wait ~1 minute, then your site will be live at:
   `https://<your-username>.github.io/<repo-name>/`

### Or via command line
```bash
git init
git add index.html .nojekyll
git commit -m "Initial commit: Paycheck Budgeter Pro"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```
Then enable Pages as described above.

## How data storage works here

- All budget data is saved to your browser's `localStorage` automatically — it works fully offline and persists between visits on the same browser/device.
- The page also *attempts* to sign in and sync to Firebase/Firestore for cross-device sync, but ships with a placeholder `demo-key` config. Since that config isn't a real project, the sign-in attempt will fail quietly and the app **falls back to local-only mode** — this is expected and the app still works perfectly.
- If you want real cross-device cloud sync:
  1. Create a free project at [Firebase Console](https://console.firebase.google.com/).
  2. Enable **Anonymous Authentication** (Build → Authentication → Sign-in method) and **Firestore Database** (Build → Firestore Database → Create database).
  3. In `index.html`, find the `firebaseConfig` object near the top and replace the placeholder values with your project's actual config (found in Project Settings → General → Your apps → SDK setup and configuration).
  4. Firebase web config keys are meant to be public/client-side — just make sure to set proper [Firestore Security Rules](https://firebase.google.com/docs/firestore/security/get-started) restricting access to each user's own `uid`, since this repo will be public.

## Notes on the PIN "lock" feature

The "Privacy PIN" is a display lock only (hides the screen behind an overlay) — the PIN is stored in plain text in `localStorage` and is **not** real encryption. It won't stop anyone with browser dev tools access. Treat it as a screen-privacy convenience, not real security, especially since this will be a public GitHub Pages site anyone with the link could visit.
