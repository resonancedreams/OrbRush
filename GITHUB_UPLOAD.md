# 📤 How to Upload to GitHub

## Option 1: Using GitHub Desktop (Easiest)

1. **Download GitHub Desktop**: https://desktop.github.com/
2. **Open GitHub Desktop**
3. **Click** "File" → "Add Local Repository"
4. **Browse** to `C:\Users\Alexander Chong\Desktop\orb-rush-game`
5. **Click** "Create a repository" (if prompted)
6. **Click** "Publish repository"
7. **Uncheck** "Keep this code private" (if you want it public)
8. **Click** "Publish repository"

Done! Your game is now on GitHub.

## Option 2: Using Command Line

Open PowerShell in the `orb-rush-game` folder and run:

```powershell
# Initialize Git repository
git init

# Add all files
git add .

# Create first commit
git commit -m "Initial commit: Orb Rush game with Firebase leaderboards"

# Create repository on GitHub (you'll need to do this manually first)
# Go to github.com → Click "+" → "New repository"
# Name it "orb-rush-game"
# Don't initialize with README (we already have one)

# Link to your GitHub repository (replace YOUR_USERNAME)
git remote add origin https://github.com/YOUR_USERNAME/orb-rush-game.git

# Push to GitHub
git branch -M main
git push -u origin main
```

## Option 3: Upload via GitHub Web Interface

1. **Go to** https://github.com/new
2. **Name** your repository: `orb-rush-game`
3. **Don't** check "Initialize with README"
4. **Click** "Create repository"
5. **Click** "uploading an existing file"
6. **Drag and drop** all files from `orb-rush-game` folder
7. **Click** "Commit changes"

## 🎯 What's Included

Your folder contains:
- ✅ All source code (`src/` folder)
- ✅ Configuration files (package.json, vite.config.ts, etc.)
- ✅ README.md with full documentation
- ✅ FIREBASE_SETUP.md with setup instructions
- ✅ .gitignore (excludes node_modules, build files)
- ❌ node_modules (excluded, users run `npm install`)
- ❌ dist (excluded, users run `npm run build`)

## 📝 After Uploading

1. **Update README.md** with your actual GitHub username
2. **Add a screenshot** to make it look professional
3. **Set up GitHub Pages** (optional) to host the game:
   - Settings → Pages → Source: GitHub Actions
   - Use Vite deployment workflow

## 🔒 Important: Firebase Security

**DO NOT** commit your actual Firebase config with real API keys!

If you've already added your Firebase config to `src/firebase.ts`:
1. Keep the placeholder values in the GitHub version
2. Add `src/firebase.ts` to `.gitignore`
3. Create `src/firebase.example.ts` with placeholders
4. Document in README that users need to add their own config

Or use environment variables:
```typescript
const firebaseConfig = {
  apiKey: import.meta.env.VITE_FIREBASE_API_KEY,
  // ...
};
```

Then users create a `.env.local` file (which is gitignored).

## 🚀 Next Steps

After uploading:
- Add topics/tags to your repo (react, typescript, game, firebase)
- Add a license (MIT is common for open source)
- Consider adding screenshots to README
- Share your game! 🎮
