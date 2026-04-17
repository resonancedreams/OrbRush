# Firebase Setup Instructions

## 1. Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click **"Add project"**
3. Enter project name (e.g., "orb-rush")
4. Disable Google Analytics (optional)
5. Click **"Create project"**

## 2. Register Your Web App

1. In your Firebase project, click the **Web icon** (`</>`) to add a web app
2. Enter app nickname (e.g., "Orb Rush Web")
3. **Do NOT** check "Firebase Hosting" (unless you want to deploy there)
4. Click **"Register app"**
5. Copy the `firebaseConfig` object shown

## 3. Update Your Code

1. Open `src/firebase.ts`
2. Replace the placeholder config with your actual Firebase config:

```typescript
const firebaseConfig = {
  apiKey: "YOUR_ACTUAL_API_KEY",
  authDomain: "your-project-id.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project-id.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef123456"
};
```

## 4. Enable Firestore Database

1. In Firebase Console, go to **Build** → **Firestore Database**
2. Click **"Create database"**
3. Choose **"Start in production mode"** (we'll set rules next)
4. Select a location (choose closest to your users)
5. Click **"Enable"**

## 5. Set Firestore Security Rules

1. Go to **Firestore Database** → **Rules** tab
2. Replace the rules with:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow anyone to read leaderboard
    match /leaderboard/{entry} {
      allow read: if true;
      // Allow writes only if data is valid
      allow create: if request.resource.data.keys().hasAll(['username', 'score', 'level', 'mode', 'timestamp', 'userId'])
                    && request.resource.data.username is string
                    && request.resource.data.username.size() >= 2
                    && request.resource.data.username.size() <= 20
                    && request.resource.data.score is int
                    && request.resource.data.score >= 0
                    && request.resource.data.score <= 10000
                    && request.resource.data.level is int
                    && request.resource.data.level >= 1
                    && request.resource.data.level <= 10
                    && request.resource.data.mode in ['classic', 'zen', 'chaos']
                    && request.resource.data.timestamp is int
                    && request.resource.data.userId is string;
    }
  }
}
```

3. Click **"Publish"**

## 6. Create Firestore Indexes (for better performance)

1. Go to **Firestore Database** → **Indexes** tab
2. Click **"Create index"**
3. Create these composite indexes:

**Index 1:**
- Collection ID: `leaderboard`
- Fields:
  - `level` (Ascending)
  - `mode` (Ascending)
  - `score` (Descending)
- Query scope: Collection

**Index 2:**
- Collection ID: `leaderboard`
- Fields:
  - `level` (Ascending)
  - `mode` (Ascending)
  - `score` (Ascending)
- Query scope: Collection

4. Wait for indexes to build (usually takes a few minutes)

## 7. Test Your Setup

1. Run your app: `npm run dev`
2. Enter a username when prompted
3. Complete a level
4. Check Firebase Console → Firestore Database → `leaderboard` collection
5. You should see your score entry!

## Optional: Deploy to Firebase Hosting

```bash
npm install -g firebase-tools
firebase login
firebase init hosting
# Choose your project
# Set public directory to: dist
# Configure as single-page app: Yes
# Set up automatic builds: No
npm run build
firebase deploy
```

## Troubleshooting

**Error: "Missing or insufficient permissions"**
- Check your Firestore security rules are published
- Make sure you're using the correct Firebase config

**Error: "The query requires an index"**
- Go to the error link provided in console
- Click "Create index" and wait for it to build

**Scores not appearing**
- Check browser console for errors
- Verify Firebase config is correct
- Check Firestore rules allow writes
- Ensure indexes are built

## Features Implemented

✅ Username input on first visit
✅ Change username from main menu
✅ Auto-submit scores to Firebase after each level
✅ Global leaderboard (top 100 per level/mode)
✅ Your rank display (e.g., "#42 / 1,234")
✅ Separate leaderboards for Classic/Zen/Chaos modes
✅ Unique user ID per browser (prevents duplicate submissions)
