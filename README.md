# 🎮 Orb Rush

A fast-paced keyboard reaction game built with React, TypeScript, and Firebase. Test your reflexes across 10 challenging levels with multiple game modes and global leaderboards!

![Orb Rush](https://img.shields.io/badge/React-18-blue) ![TypeScript](https://img.shields.io/badge/TypeScript-5-blue) ![Firebase](https://img.shields.io/badge/Firebase-Firestore-orange)

## ✨ Features

### 🎯 Core Gameplay
- **10 Unique Levels** — Progressive difficulty with distinct visual themes
- **4 Orb Types**:
  - 🔵 **Tap** — Click at the perfect moment for max points
  - 🟠 **Hold** — Press and hold until the ring fills
  - 🟣 **Delayed** — Wait for the countdown, then strike
  - ⚪ **Ghost** — Fades to invisible, hit while unseen for bonus points
- **Timing-Based Scoring** — Ring changes color (yellow→green→gold) as perfect zone approaches
- **Combo System** — Chain hits for up to 2.5× multiplier
- **Lives System** — 5 lives per game, lose on miss/wrong key/early press

### 🎮 Game Modes
- **CLASSIC** 🔵 — Balanced challenge
- **ZEN** 🟢 — Relaxed mode with infinite lives, slower pace
- **CHAOS** 🔴 — 2× speed, more orbs, intense screen effects

### 🌟 Advanced Features
- **Speed Warp** (Levels 7-10) — Game randomly speeds up (RUSH) or slows down (SLOW)
- **Screen Effects** — Shake, flash, chromatic aberration, distortion, glitch, invert
- **Level Selection** — Free access to all levels, no unlocking required
- **Retry System** — Improve your scores on any level
- **Per-Level Bests** — Track your best score for each level

### 🏆 Global Leaderboards
- **Firebase Integration** — Real-time cloud leaderboards
- **Username System** — Set your name, compete globally
- **Rank Display** — See your position (e.g., "#42 / 1,234")
- **Top 100** — View the best players per level/mode
- **Separate Rankings** — Classic/Zen/Chaos have independent leaderboards

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ and npm

### Installation

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/orb-rush-game.git
cd orb-rush-game

# Install dependencies
npm install

# Run development server
npm run dev
```

Open [http://localhost:5173](http://localhost:5173) in your browser.

### Build for Production

```bash
npm run build
npm run preview  # Preview production build locally
```

## 🔥 Firebase Setup (Required for Leaderboards)

The game works without Firebase, but you won't have global leaderboards. To enable them:

1. **Create Firebase Project**
   - Go to [Firebase Console](https://console.firebase.google.com/)
   - Click "Add project" → name it (e.g., "orb-rush")
   - Register a web app

2. **Get Your Config**
   - Copy the `firebaseConfig` object from Firebase Console
   - Paste into `src/firebase.ts` (replace placeholder values)

3. **Enable Firestore**
   - Firebase Console → Build → Firestore Database → Create
   - Choose "Start in production mode"

4. **Set Security Rules**
   - See `FIREBASE_SETUP.md` for complete rules
   - Allows public reads, validated writes

5. **Create Indexes**
   - See `FIREBASE_SETUP.md` for index configurations
   - Required for fast leaderboard queries

**Full step-by-step guide:** See `FIREBASE_SETUP.md`

## 🎨 Tech Stack

- **React 18** — UI framework
- **TypeScript** — Type safety
- **Vite** — Build tool & dev server
- **TailwindCSS** — Styling
- **Firebase Firestore** — Cloud database for leaderboards
- **CSS Animations** — Screen effects & orb animations

## 📁 Project Structure

```
orb-rush-game/
├── src/
│   ├── components/
│   │   ├── Game.tsx           # Main game loop & logic
│   │   ├── OrbView.tsx        # Individual orb rendering
│   │   ├── HUD.tsx            # Score/lives/combo display
│   │   ├── MainMenu.tsx       # Animated menu screen
│   │   ├── LevelSelect.tsx    # Level picker with mode selection
│   │   ├── LevelComplete.tsx  # Results screen
│   │   ├── GameOver.tsx       # Final score screen
│   │   ├── Leaderboard.tsx    # Global rankings
│   │   └── NameInput.tsx      # Username entry
│   ├── firebase.ts            # Firebase config & helpers
│   ├── levels.ts              # 10 level configurations
│   ├── types.ts               # TypeScript interfaces
│   ├── App.tsx                # Screen routing & state
│   ├── main.tsx               # React entry point
│   └── index.css              # Global styles & animations
├── FIREBASE_SETUP.md          # Firebase setup guide
└── package.json
```

## 🎮 How to Play

1. **Enter your name** on first visit
2. **Choose a game mode** (Classic/Zen/Chaos)
3. **Select a level** (1-10)
4. **Watch the countdown** (3, 2, 1, GO!)
5. **Press the correct keys** when orbs appear:
   - **Tap orbs** — Press once at the right moment
   - **Hold orbs** — Press and hold until filled
   - **Delayed orbs** — Wait for countdown, then press
   - **Ghost orbs** — Hit while invisible for max points
6. **Avoid mistakes** — Wrong keys and misses cost lives
7. **Build combos** — Chain hits for bonus multipliers
8. **Check leaderboards** — See how you rank globally!

## 🏅 Scoring System

- **Base Points**: Varies by orb type (10-20 per orb)
- **Timing Multiplier**: 1.0× to 4.5× based on accuracy
- **Combo Multiplier**: Up to 2.5× for 16+ combo
- **Final Score**: Normalized 0-10,000 per level

### Timing Zones (Tap Orbs)
- **OK** (1.0×) — Any hit
- **GOOD** (1.8×) — Yellow ring (≥45%)
- **GREAT** (2.5×) — Green ring (≥70%)
- **⭐ PERFECT** (4.0×) — Gold pulsing ring (≥88%)

## 🐛 Known Issues

- IDE may show stale TypeScript errors (ignore if `npx tsc --noEmit` passes)
- Firebase requires manual setup (not included in repo)

## 📝 License

MIT License - feel free to use this project however you'd like!

## 🙏 Credits

Created with ❤️ using React, TypeScript, and Firebase.

---

**Enjoy the game!** 🎮✨
