# GAMESHELF — Xbox Library Manager

```
  ██████╗  █████╗ ███╗   ███╗███████╗███████╗██╗  ██╗███████╗██╗     ███████╗
 ██╔════╝ ██╔══██╗████╗ ████║██╔════╝██╔════╝██║  ██║██╔════╝██║     ██╔════╝
 ██║  ███╗███████║██╔████╔██║█████╗  ███████╗███████║█████╗  ██║     █████╗
 ██║   ██║██╔══██║██║╚██╔╝██║██╔══╝  ╚════██║██╔══██║██╔══╝  ██║     ██╔══╝
 ╚██████╔╝██║  ██║██║ ╚═╝ ██║███████╗███████║██║  ██║███████╗███████╗██║
  ╚═════╝ ╚═╝  ╚═╝╚═╝     ╚═╝╚══════╝╚══════╝╚═╝  ╚═╝╚══════╝╚══════╝╚═╝
```

> **A terminal-aesthetic Xbox game library manager and achievement tracker. Built from the ground up as a native desktop application for Windows and Linux.**

---

## Credits

GAMESHELF was designed, developed, and built entirely by **[YOUR NAME]**. Every line of code — from the boot sequence animation to the achievement sync engine to the spine-view library rendering — was written by hand. This is a passion project born out of the frustration of not having a good local-first, privacy-respecting way to track an Xbox game collection.

No templates. No frameworks. No AI-generated boilerplate. Just raw HTML, CSS, JavaScript, and Rust.

---

## Table of Contents

- [What is GAMESHELF?](#what-is-gameshelf)
- [Screenshots and Aesthetic](#screenshots-and-aesthetic)
- [Features](#features)
  - [Dashboard / Home](#dashboard--home)
  - [Library](#library)
  - [Game Detail View](#game-detail-view)
  - [Achievement Tracking](#achievement-tracking)
  - [Wishlist](#wishlist)
  - [Smart Backlog Queue](#smart-backlog-queue)
  - [Franchise Series](#franchise-series)
  - [Progress Journal](#progress-journal)
  - [Random Game Picker](#random-game-picker)
  - [Settings and Profile](#settings-and-profile)
- [Xbox Live Integration (OpenXBL)](#xbox-live-integration-openxbl)
  - [Getting an API Key](#getting-an-api-key)
  - [The CORS Proxy](#the-cors-proxy)
  - [Library Sync](#library-sync)
  - [Achievement Sync](#achievement-sync)
  - [Selective Sync](#selective-sync)
- [Installation](#installation)
  - [Linux (from .deb)](#linux-from-deb)
  - [Linux (from source)](#linux-from-source)
  - [Windows (from .msi)](#windows-from-msi)
  - [Windows (from source)](#windows-from-source)
- [Building from Source](#building-from-source)
  - [Prerequisites — Linux](#prerequisites--linux)
  - [Prerequisites — Windows](#prerequisites--windows)
  - [Build Steps](#build-steps)
  - [Generating Icons](#generating-icons)
- [Launching the App](#launching-the-app)
  - [Using the Launcher Scripts](#using-the-launcher-scripts)
  - [Manual Launch](#manual-launch)
  - [Stopping the Proxy](#stopping-the-proxy)
- [Data and Privacy](#data-and-privacy)
  - [Where Your Data Lives](#where-your-data-lives)
  - [Exporting Your Data](#exporting-your-data)
  - [Importing Your Data](#importing-your-data)
  - [Clearing Your Data](#clearing-your-data)
- [Migrating from the Browser Version](#migrating-from-the-browser-version)
- [Tech Stack](#tech-stack)
- [Troubleshooting](#troubleshooting)
- [License](#license)

---

## What is GAMESHELF?

GAMESHELF is a **local-first**, **offline-capable**, **native desktop application** for tracking your Xbox game library. It gives you a beautifully designed personal database for every game you own, every achievement you've unlocked, every game you're planning to buy, and every game you've abandoned halfway through.

The core philosophy behind GAMESHELF is that your data belongs to you. There is no cloud account, no subscription, no server storing your information, and no ads. Everything you enter into GAMESHELF lives on your machine in your browser's localStorage, under your control. If you want to sync with Xbox Live to pull your real achievement data, that's opt-in — and even then, the data that comes back is stored locally.

GAMESHELF was designed for Xbox gamers who care about their collections the way a vinyl collector cares about their records. It gives you tools that the Xbox app and Microsoft's own website simply don't offer: custom notes per game, a priority backlog queue powered by a scoring algorithm, franchise series groupings, per-game screenshot archives, tracked achievements that surface on your home screen, a timeline view of your gaming history, and a "surprise me" randomizer for when you can't decide what to play next.

The visual design is intentional. GAMESHELF looks like a retro terminal OS — black backgrounds, phosphor green text, monospace fonts, scan-line textures, and a boot sequence that loads like firmware. It's a love letter to the aesthetic of early PC gaming and hacker culture, wrapped around a genuinely useful piece of software.

---

## Screenshots and Aesthetic

GAMESHELF uses a custom design system built entirely in vanilla CSS. The color palette is built around deep blacks and phosphor greens, with gold accents for 100% completions and subtle glows and shadows throughout. The typefaces are **Orbitron** (display headings), **Rajdhani** (UI text), and **Share Tech Mono** (data and labels) — all from Google Fonts.

When you first launch the app, you're greeted by a full-screen boot sequence that simulates a BIOS/firmware startup: log lines printing one by one, a loading bar filling up, and then a glitch-transition animation as the UI slices in. It's completely skippable (it auto-completes) and purely cosmetic, but it sets the tone.

The library has two views:

- **Spine View** — Games are arranged on a virtual bookshelf, organized alphabetically with spine labels. Each spine can be customized with a color, height, label, and even a custom image, just like labeling spines on a real shelf.
- **Grid View** — A traditional cover art grid with completion percentage overlaid on each card and a gold star marking 100% completions.

---

## Features

### Dashboard / Home

The home screen is your command center. It opens with your **profile card**, which shows your gamertag, gamertag code, and four key stats at a glance: total games owned, story completions, 100% completions, and wishlist size. Below that is a live average completion percentage with a progress bar across your entire library.

Beneath the stats is the **Next to Play** panel — a recommendation engine that scores every game in your library and surfaces the six best candidates for what you should play next. The scoring algorithm weighs multiple factors:

- **Tracked achievements** — Games with more unfinished tracked achievements score higher
- **Story progress** — Games where you finished the story but haven't 100%'d yet get a bump
- **Recency** — Games you started recently score higher than ones you abandoned years ago
- **Completion proximity** — Games close to 100% are prioritized so you can push them over the finish line

Below that are two horizontal scroll carousels showing your **Library** and your **Wishlist** — quick visual access to recently added or notable entries in each.

### Library

The library page is where all your games live. You can filter by genre using the chip row at the top (Action, RPG, Shooter, Sports, Racing, Strategy, Adventure, Puzzle, Indie, Horror, or any custom tag), and sort by:

- Alphabetical (A–Z or Z–A)
- Completion percentage (highest first)
- Star rating (highest first)
- Date started (most recent first)

Games display in whichever view mode you prefer — spine or grid. You can switch between them using the view toggle buttons in the top-right of the library header.

Adding a game is done via the **Add Game** button. The add form accepts:

- Title, platform, year, developer, publisher
- Genre tags (multi-select)
- Completion percentage (0–100)
- Star rating (1–5)
- Start date and story completion date
- Cover art (uploaded from your machine, cropped with a built-in image cropper)
- Spine customization (color, height, custom label, custom spine image)
- Freeform notes
- Franchise series assignment

### Game Detail View

Clicking any game opens its detail page. This is the deepest view in the app and contains everything about a single game:

- **Cover art** displayed large, with a color-matched gradient background
- **Metadata** — title, platform, year, developer, publisher, completion percentage
- **Genre tags** displayed as styled chips
- **Star rating** — click the stars to rate or re-rate
- **Dates** — start date, story completion date, 100% completion date (auto-set when you mark a game complete)
- **Tracked achievements** — up to three achievements pinned as priority targets. These show on the home screen's recommended list and can be ticked off directly from this page
- **Screenshots** — a grid of attached screenshots. You can add, view, and manage them here
- **Edit button** — opens a full edit modal for all game metadata

When you 100% a game, the app triggers a confetti celebration animation and automatically records the date. A gold star badge appears on the game's card and spine in the library.

### Achievement Tracking

Every game has a dedicated **Achievements** page, accessible from the game detail view. This page shows:

- A circular ring chart showing your completion percentage for that game
- Total gamerscore earned vs. total available
- A full list of every achievement, showing:
  - Achievement name (hidden as "???" if locked, in the style of real Xbox achievements)
  - Description (hidden until unlocked)
  - Gamerscore value
  - Lock/unlock status
  - Date unlocked (if applicable)

You can toggle achievements unlocked manually by clicking them. Completion percentage updates in real time as you do.

Achievements can be added manually (name, description, gamerscore, icon type) or synced from Xbox Live via the OpenXBL integration. There are five icon types: Trophy, Shield, Star, Fire, and Skull — each with a custom SVG icon.

The **Track** system lets you pin up to three achievements per game as your current priorities. Tracked achievements appear on the game's detail page for quick reference and factor into the Next to Play scoring.

There is also a **Sync This Game** button at the top of the achievements page that triggers a single-game achievement sync from Xbox Live, rather than syncing your entire library at once.

### Wishlist

The wishlist is a separate collection for games you intend to buy or play but don't own yet. Each wishlist entry supports:

- Title, platform, year, developer, genre
- Price (so you can track sales)
- Cover art
- Notes

Wishlist games appear in their own carousel on the home screen and on a dedicated wishlist page. When you acquire a game, you can promote it from the wishlist to your main library.

There is also an **Import Specific Games** feature in the Settings page that lets you selectively pull individual games from your Xbox Live history into your library, rather than importing everything at once.

### Smart Backlog Queue

The backlog page is a prioritized list of every game in your library that isn't 100% completed. Games are automatically ranked using a weighted scoring engine that accounts for:

- Number of unfinished tracked achievements (×3 weight)
- Story progress (×2 weight)
- How recently you started the game (×1.5 weight)
- Manual priority flag (×2 weight)

This means you don't have to maintain a manual ranking — GAMESHELF does it for you based on what you've already told it. If you've been tracking three specific achievements in a game you started two weeks ago, that game will float to the top of your backlog queue automatically.

### Franchise Series

The series page groups your games by franchise, automatically detected from matching titles and series tags. For example, if you have Halo 3, Halo 4, and Halo Infinite in your library, they'll appear together as a "Halo" series entry showing your aggregate completion across the franchise.

You assign a game to a series when adding or editing it, using the Series field in the game form. Once two or more games share a series name, the series page will group them and show a combined progress bar.

### Progress Journal

The journal is an auto-generated log of your gaming activity, built from your library data. It surfaces milestones, completion events, start dates, and achievement unlocks in a chronological format. It's read-only and requires no manual input — it builds itself from the data you've already entered elsewhere in the app.

### Random Game Picker

Available as a modal from the library page, the random picker randomly selects a game from your incomplete library and presents it as your recommendation. If you don't like the pick, you can reroll. If you accept it, it opens the game's detail page. It's a simple tool for when you're staring at your library and can't decide.

### Settings and Profile

The settings page contains:

- **Profile** — Set your gamertag display name and tag code. Upload a gamerpic (profile photo) that appears in the sidebar.
- **OpenXBL API Integration** — Enter your API key and gamertag, test the connection, sync your library, sync all achievements, or run selective syncs.
- **Data** — Export your entire database to a JSON file, import from a previously exported JSON file, or clear all data.

---

## Xbox Live Integration (OpenXBL)

GAMESHELF can optionally connect to your real Xbox Live account through the [OpenXBL / xbl.io](https://xbl.io) API to automatically pull your game library and achievement data. This is entirely optional — the app works perfectly without it.

### Getting an API Key

1. Go to [xbl.io](https://xbl.io) and create a free account
2. Navigate to your account dashboard and generate an API key
3. Copy the key and paste it into GAMESHELF under **Settings → OpenXBL API Key**
4. Enter your Xbox Gamertag in the field below it
5. Click **Test Connection** to verify everything is working

The free tier of xbl.io is sufficient for personal use. There are rate limits, but for a personal game tracker they're unlikely to be a problem.

### The CORS Proxy

Web browsers and desktop WebViews enforce a security rule called CORS (Cross-Origin Resource Sharing) that prevents apps from making API requests to external servers unless those servers explicitly allow it. The xbl.io API does not include the headers needed for a Tauri WebView to reach it directly.

GAMESHELF solves this by running a tiny local proxy server — `proxy.js` — on port 8765. When the app needs to talk to xbl.io, it sends the request to `http://localhost:8765` instead, and the proxy forwards it to `https://xbl.io/api/v2` on your behalf. From xbl.io's perspective, the request is coming from a normal server-side client, so it responds without issue.

The proxy runs as a Node.js process and must be started before launching GAMESHELF. The easiest way to handle this is by using the included launcher scripts, which start the proxy automatically.

The proxy never stores any data. It is purely a passthrough — request goes in, request goes out. Your API key travels through it encrypted (HTTPS to xbl.io) and is never logged.

### Library Sync

Once your API key is set up, click **Sync Library** in Settings. GAMESHELF will:

1. Fetch your Xbox Live title history (all games associated with your account)
2. Compare the list against your existing library
3. Add any games not already present, with platform, title ID, and basic metadata filled in
4. Skip games that already exist to avoid duplicates
5. Report how many were added and how many were skipped

After a library sync, your Xbox games will have an `xblTitleId` attached to them, which is what enables achievement syncing.

### Achievement Sync

Click **Sync All Achievements** to update achievement data for every Xbox game in your library that has a title ID. For each game, GAMESHELF:

1. Fetches your achievement list from xbl.io
2. Adds any achievements not already in your local records
3. Updates unlock status and unlock dates for existing achievements
4. Recalculates each game's completion percentage
5. Reports total achievements synced and any games that failed

This can take a while if you have a large library. The sync processes games one at a time to respect rate limits.

### Selective Sync

If you only want to sync one specific game:

- **Import Specific Games** — Opens a picker showing your Xbox Live game history. Select individual titles to import rather than importing everything.
- **Sync Specific Achievements** — Opens a picker to sync achievements for individual games.
- **Sync This Game** — On the Achievements page for any Xbox game, this button syncs only that game's achievements without touching the rest of your library.

---

## Installation

### Linux (from .deb)

If you've been given a pre-built `.deb` package:

```bash
sudo dpkg -i gameshelf_1.0.0_amd64.deb
```

If you get dependency errors:

```bash
sudo apt --fix-broken install
```

Then launch using the included launcher script (see [Launching the App](#launching-the-app)).

### Linux (from source)

See [Building from Source](#building-from-source) below.

### Windows (from .msi)

If you've been given a pre-built `.msi` installer:

1. Double-click the `.msi` file
2. Follow the installation wizard
3. Copy `proxy.js` and `launch.bat` from this package to the same folder as `gameshelf.exe`
4. Use `launch.bat` to start the app (see [Launching the App](#launching-the-app))

### Windows (from source)

See [Building from Source](#building-from-source) below.

---

## Building from Source

### Prerequisites — Linux

Install Rust:
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source "$HOME/.cargo/env"
```

Install system dependencies (Ubuntu/Debian):
```bash
sudo apt update
sudo apt install -y \
  libwebkit2gtk-4.1-dev \
  libgtk-3-dev \
  libayatana-appindicator3-dev \
  librsvg2-dev \
  patchelf \
  build-essential \
  curl \
  wget \
  file \
  libssl-dev \
  libxdo-dev
```

Install Node.js (v18 or later):
```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```

### Prerequisites — Windows

1. Install [Node.js](https://nodejs.org/) — download the LTS installer and run it
2. Install [Rust](https://rustup.rs/) — download and run `rustup-init.exe`
   - When prompted, choose the default installation
   - Rust's installer will also prompt you to install the **Microsoft C++ Build Tools** — accept this, it's required
3. Restart your terminal/PowerShell after installation so the new paths take effect
4. Verify everything installed: `rustc --version` and `node --version` should both return version numbers

### Build Steps

Clone or extract this package, then open a terminal in the project folder:

```bash
# Install Node dependencies (just the Tauri CLI)
npm install

# Generate icons from your custom PNG (512x512 or larger recommended)
npm run tauri icon path/to/your/icon.png

# Development build (hot reload, opens immediately)
npm run tauri dev

# Production build (creates installer)
npm run tauri build
```

Build output on **Linux**: `src-tauri/target/release/bundle/`
- `deb/gameshelf_1.0.0_amd64.deb` — Debian/Ubuntu package
- `appimage/gameshelf_1.0.0_amd64.AppImage` — Portable single-file executable

Build output on **Windows**: `src-tauri\target\release\bundle\`
- `msi\gameshelf_1.0.0_x64_en-US.msi` — Windows installer
- `nsis\gameshelf_1.0.0_x64-setup.exe` — NSIS installer

First build will take several minutes — Rust is compiling the entire Tauri framework from scratch. Subsequent builds are much faster.

### Generating Icons

GAMESHELF needs icons in several sizes for different platforms. Tauri can generate them all from one source image:

```bash
npm run tauri icon /path/to/your-icon.png
```

Use a PNG that is at least **512×512 pixels**. The command generates:
- `icons/32x32.png`
- `icons/128x128.png`
- `icons/128x128@2x.png`
- `icons/icon.icns` (macOS)
- `icons/icon.ico` (Windows)
- `icons/icon.png`

All of these are referenced in `src-tauri/tauri.conf.json` under the `bundle.icon` array. Do not remove entries from that array or the build will fail.

---

## Launching the App

GAMESHELF requires the local API proxy to be running before you open the app. If you try to use the Xbox Live features without it, you'll see a "Network error: Load failed" message.

### Using the Launcher Scripts

The easiest approach. These scripts start the proxy and then launch the app in one step.

**Linux:**
```bash
chmod +x launch.sh   # only needed once
./launch.sh
```

Or if GAMESHELF is installed system-wide:
```bash
bash /path/to/gameshelf-dist/launch.sh
```

**Windows:**

Double-click `launch.bat`, or run it from PowerShell:
```powershell
.\launch.bat
```

### Manual Launch

If you prefer to manage processes yourself:

**Linux:**
```bash
# Terminal 1 — start proxy
node /path/to/gameshelf-dist/proxy.js

# Terminal 2 — start app
gameshelf
```

**Windows:**
```powershell
# PowerShell window 1 — start proxy
node C:\path\to\gameshelf-dist\proxy.js

# PowerShell window 2 — start app
.\gameshelf.exe
```

### Stopping the Proxy

**Linux:**
```bash
kill $(lsof -t -i:8765)
```

**Windows (PowerShell):**
```powershell
Stop-Process -Id (Get-NetTCPConnection -LocalPort 8765).OwningProcess
```

Or just close the terminal window where the proxy is running.

---

## Data and Privacy

### Where Your Data Lives

GAMESHELF stores all data in the Tauri WebView's localStorage. On disk, this is persisted at:

- **Linux:** `~/.local/share/com.gameshelf.app/` or `~/.local/share/gameshelf/`
- **Windows:** `C:\Users\<YourName>\AppData\Roaming\com.gameshelf.app\`

This is a standard browser storage location managed by WebKit (Linux) or WebView2 (Windows). The data is stored as JSON strings under named keys. Nothing is stored remotely. Nothing is transmitted to any server unless you explicitly trigger an Xbox Live sync.

The proxy script (`proxy.js`) does not log, store, or cache any data. It forwards requests and responses in memory only.

### Exporting Your Data

Go to **Settings → Export Data (JSON)**. This saves a complete snapshot of your library, wishlist, achievements, settings, and profile to a `.json` file anywhere you choose.

Keep this file backed up. It is your only copy of your data outside the app. If you reinstall or move to a new machine, this is how you restore everything.

The export file is human-readable and structured. It can be opened in any text editor.

### Importing Your Data

Go to **Settings → Import Data (JSON)** and select a previously exported file. This replaces your current library with the contents of the file. There is a confirmation prompt before anything is overwritten.

### Clearing Your Data

Go to **Settings → Clear All Data**. This wipes your entire library, wishlist, achievements, settings, and profile. There is a confirmation step. This action cannot be undone — export first if you want a backup.

---

## Migrating from the Browser Version

If you previously used GAMESHELF as a standalone HTML file in your browser:

1. Open the browser version
2. Go to **Settings → Export Data (JSON)** and save the file
3. Open the GAMESHELF desktop app
4. Go to **Settings → Import Data (JSON)** and load the file you saved

Your entire collection — games, achievements, notes, cover art, screenshots, and settings — will be restored exactly as it was.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML5, CSS3, JavaScript (ES2020) |
| Desktop shell | Tauri v2 (Rust) |
| WebView (Linux) | WebKit2GTK 4.1 |
| WebView (Windows) | Microsoft WebView2 |
| Xbox data | xbl.io / OpenXBL API v2 |
| API proxy | Node.js (built-in `http` / `https` modules, no dependencies) |
| Fonts | Orbitron, Rajdhani, Share Tech Mono (Google Fonts) |
| Build tools | Cargo (Rust), npm |
| Installer formats | .deb, .AppImage (Linux), .msi, .exe (Windows) |

No frontend framework. No CSS preprocessor. No JavaScript build step. The entire frontend is a single HTML file — `src/index.html` — that the Tauri shell loads directly. This makes the app exceptionally portable and easy to inspect or modify.

---

## Troubleshooting

**The app opens but Xbox sync fails with "Network error: Load failed"**

The proxy is not running. Start it before opening the app:
```bash
node /path/to/proxy.js
```
Then restart GAMESHELF.

**Port 8765 is already in use**

A previous proxy process is still running. Kill it:
```bash
# Linux
kill $(lsof -t -i:8765)

# Windows
Stop-Process -Id (Get-NetTCPConnection -LocalPort 8765).OwningProcess
```

**The app won't build on Linux — missing WebKit**

Ubuntu 24.04 ships WebKit 4.1. Make sure you're installing the right package:
```bash
sudo apt install libwebkit2gtk-4.1-dev
```
Do not install `libwebkit2gtk-4.0-dev` — that's the older version and will cause build failures with Tauri v2.

**The app won't build on Windows — MSVC not found**

You need the Microsoft C++ Build Tools. The easiest way to get them is through Rust's installer (`rustup-init.exe`) — it will prompt you to install them. Alternatively, install [Visual Studio Build Tools](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2022) and include the "Desktop development with C++" workload.

**Icons didn't change after running `npm run tauri icon`**

Clear the build cache and rebuild:
```bash
rm -rf src-tauri/target
npm run tauri build
```
On Linux, you may also need to refresh your desktop icon cache:
```bash
update-desktop-database ~/.local/share/applications
```

**The app builds but crashes immediately on Linux**

Make sure all WebKit dependencies are installed:
```bash
sudo apt install -y libwebkit2gtk-4.1-dev libgtk-3-dev libayatana-appindicator3-dev librsvg2-dev
```

**My data disappeared after reinstalling**

Data is stored in the WebView's localStorage. Uninstalling the `.deb` package on some systems wipes the app's data directory. Always export your data before uninstalling. Use **Settings → Export Data (JSON)** to save a backup.

**The boot animation takes too long**

It completes in about 2.5 seconds and cannot be skipped manually — it's timed to the animation. It only runs once per cold launch.

---

## License

GAMESHELF is personal-use software created by **[YOUR NAME]**. You're welcome to use it, modify it, and share it with friends. Attribution is appreciated. Selling it is not permitted.

The OpenXBL / xbl.io API is a third-party service with its own terms of use. GAMESHELF is not affiliated with or endorsed by Microsoft or Xbox.
# Gameshelf
