# 💕 Love Puzzle — Deploy to Vercel + Firebase

## Step 1: Create Firebase Project (free, 2 minutes)

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Click **"Create a project"** → name it (e.g. `love-puzzle`) → Continue
3. Disable Google Analytics (not needed) → **Create Project**
4. In the project dashboard, click the **web icon `</>`** to add a web app
5. Name it anything → **Register app**
6. You'll see a config like this — copy `apiKey` and `projectId`:
   ```js
   const firebaseConfig = {
     apiKey: "AIzaSy...",        // ← copy this
     projectId: "love-puzzle-xxxxx",  // ← and this
     ...
   };
   ```

## Step 2: Enable Firestore Database

1. In Firebase Console sidebar → **Build** → **Firestore Database**
2. Click **"Create database"**
3. Choose **"Start in test mode"** (allows read/write for 30 days)
4. Pick any region → **Enable**

> ⚠️ Test mode expires after 30 days. To keep it working, go to Firestore → Rules and set:
> ```
> rules_version = '2';
> service cloud.firestore {
>   match /databases/{database}/documents {
>     match /scores/{document} {
>       allow read: if true;
>       allow write: if true;
>     }
>   }
> }
> ```

## Step 3: Deploy to Vercel (1 minute)

### Option A: Via GitHub (recommended)
```bash
# In the love-puzzle-vercel folder:
git init
git add .
git commit -m "Love Puzzle 💕"

# Create a repo on GitHub, then:
git remote add origin https://github.com/YOUR_USERNAME/love-puzzle.git
git push -u origin main
```
Then go to [vercel.com](https://vercel.com) → **New Project** → Import your GitHub repo → **Deploy**

### Option B: Via Vercel CLI
```bash
npm i -g vercel
cd love-puzzle-vercel
vercel
```
Follow the prompts → it deploys instantly.

## Step 4: Play!

1. Open your Vercel URL (e.g. `https://love-puzzle.vercel.app`)
2. On first visit, paste your Firebase `apiKey` and `projectId`
3. Click **"CONNECT & PLAY"**
4. Your config is saved in the browser — you won't need to enter it again
5. Or click **"SKIP"** to use local-only scores

## How It Works

- **No server needed** — it's a single HTML file
- **Firebase Firestore** stores scores in the cloud (shared leaderboard!)
- **Falls back to localStorage** if Firebase isn't configured
- **Vercel** just serves the static file globally via CDN

## Files
```
index.html    — the entire game (single file!)
vercel.json   — Vercel deployment config
README.md     — this file
```
