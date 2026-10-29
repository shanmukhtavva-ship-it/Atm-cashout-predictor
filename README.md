# SaRi • Warm Sound • All Languages

**SaRi** is a polished, mobile-friendly music streaming web application designed for songs across all languages—featuring Telugu, Hindi, Tamil, English, Punjabi, Malayalam, Kannada, Spanish, Korean, Japanese, French, Arabic, and global indie styles.

The name **SaRi** evokes the foundational notes *"Sa Re Ga Ma"* of Indian classical music, blended with modern warm aesthetic minimalism, rich dynamic album art, and an intuitive music-first interface.

---

## 🌟 Key Features

### 1. Modern Music-First Home Experience
- **SaRi Spotlight:** Curated hero showcase featuring an animated spinning vinyl disk, track trivia story, and quick play.
- **Multilingual Language Filter Bar:** Instant horizontal scroll filters for **Telugu, Hindi, Tamil, English, Punjabi, Malayalam, Kannada, Spanish, Korean, Japanese, French, and Arabic**.
- **Trending Across Languages:** Dynamic feed filtered by language selection.
- **Fresh Drops & New Releases:** Dedicated badge-tagged new releases section.
- **Curated Editorial Playlists:** Themed mood playlists (*"Monsoon Chai & Raagas"*, *"Deccan Strings"*, *"Midnight Lo-Fi & Warm Vinyl"*, *"World Gypsy & Flamenco"*, *"Punjab Beats"*).
- **Genre & Mood Explorer:** Interactive hub chips for Classical Fusion, Acoustic Melody, Lo-Fi Chill, Sufi Soul, Indie Pop, and Folk Roots.

### 2. Real-Time Interactive Search
- Instant, debounced live search querying track title, artist name, album, language, genre, and full lyrical phrases.
- Clear search button and result count indicator.
- Interactive table row view with play-on-hover, direct like toggle, and playlist additions.

### 3. Persistent Music Player Dock
- **Full Playback Controls:**
  - Play / Pause (with keyboard shortcut `Spacebar`)
  - Next / Previous (`ArrowRight`, `ArrowLeft`)
  - Fast-forward / Rewind (`Shift+ArrowRight`, `Shift+ArrowLeft`)
  - Interactive Scrubbing Seek Bar with elapsed time and total duration tooltip
  - Shuffle mode toggle (`S`)
  - 3-State Repeat mode cycle (`R`): Off → Repeat All → Repeat One
  - Volume control slider & mute toggle (`M`, `ArrowUp`, `ArrowDown`)
  - **Live Canvas Audio Visualizer:** Real-time animated frequency EQ bars synced to playback.
  - **Playback Queue Drawer:** Inspect upcoming songs, jump to any track, and reorder.
  - **MediaSession OS Integration:** Control playback via OS lock screen, media keys, and Bluetooth headsets.

### 4. Liked Songs & Custom Playlists
- **Liked Songs Library:** Persistent favorites library synced to `localStorage`, with track count, total listening duration, and single-click "Play All Liked" / "Shuffle Liked".
- **Custom Playlist Creator:** Interactive "Create Playlist" modal, add any track from any view, remove tracks, and delete custom playlists.

### 5. Mobile-Friendly Responsive Design
- **Mobile Bottom Navigation Bar:** Quick access to Home, Search, Liked, Playlists, and Settings.
- **Mobile Expandable Player Sheet:** Tap the bottom mini-player to open a full-screen sheet with large artwork, big touch controls, and auto-scrolling lyrics reader.
- Responsive breakpoints for tablets and small mobile devices (<480px) with minimum 44px touch targets.

---

## 🎧 Audio Architecture & Procedural Synth Engine

Because SaRi respects copyright and streaming licenses, it does **not** scrape unauthorized audio or claim to offer commercial pirate streams. Instead, SaRi features a built-in **Web Audio API Procedural Synthesizer Engine** (`js/utils/synthAudio.js`):
- Generates warm harmonic acoustics, chord progressions, lead scales, ambient tanpura/pad drones, and lo-fi percussion pulses in real time.
- Adapts BPM, musical keys (C, D, G, A, Em), and modal scales to each track.
- Connects directly to the `AnalyserNode` for the live visualizer canvas.
- Seamlessly falls back to HTML5 `Audio` elements whenever external licensed audio streams are provided.

---

## 🔌 Catalog Provider Architecture (Ready for Commercial APIs)

SaRi isolates all catalog access behind the `MusicCatalogProvider` abstraction interface (`js/providers/catalogProvider.js`):

```
                       ┌───────────────────────────────┐
                       │     SaRi Application UI       │
                       └───────────────┬───────────────┘
                                       │
                       ┌───────────────▼───────────────┐
                       │     ProviderManager           │
                       └───────────────┬───────────────┘
                                       │
             ┌─────────────────────────┴────────────────────────┐
             ▼                                                  ▼
┌───────────────────────────────┐              ┌─────────────────────────────────┐
│     DemoCatalogProvider       │              │ Commercial Provider Adapters    │
│  - Royalty-free metadata      │              │  - Spotify Web API (OAuth PKCE) │
│  - Web Audio synth playback   │              │  - Subsonic / Navidrome Server  │
│  - 128kbps demo preview label │              │  - Audius Open Audio Network    │
└───────────────────────────────┘              │  - Apple MusicKit JS            │
                                               └─────────────────────────────────┘
```

### What Works Now (Demo Mode)
- Full interactive UI, search, language filtering, queue management, liked songs, custom playlists, seek, volume, shuffle, repeat, visualizer, and procedural Web Audio playback across 12 languages.
- Clear demo notices and transparent licensing labels (`isDemo: true`).

### What Needs a Licensed Provider
- Commercial pop chart releases, official studio master audio files, and high-fidelity 320kbps / lossless FLAC streaming require configuring API credentials in the **Provider & Audio Settings** hub.

---

## ⌨️ Keyboard Shortcuts

| Key | Action |
| :--- | :--- |
| `Space` | Play / Pause |
| `ArrowRight` | Seek +5 seconds |
| `Shift + ArrowRight` | Next Track |
| `ArrowLeft` | Seek -5 seconds |
| `Shift + ArrowLeft` | Previous Track |
| `ArrowUp` | Volume Up (+5%) |
| `ArrowDown` | Volume Down (-5%) |
| `M` | Mute / Unmute |
| `L` | Like / Unlike Current Track |
| `S` | Toggle Shuffle |
| `R` | Cycle Repeat (Off → All → One) |

---

## 🧪 Build Check & Automated Testing

### 1. PowerShell Build Check
Run the build check script from the project folder:
```powershell
powershell -ExecutionPolicy Bypass -File .\build_check.ps1
```
This validates:
1. File structure & hierarchy
2. HTML5 semantic tokens & view containers
3. CSS balanced syntax & design system variables
4. Multilingual catalog coverage (12 languages & `isDemo: true` enforcement)
5. Catalog provider interface compliance
6. Test suite file readiness

### 2. Unit Test Suite
Open `tests/index.html` in your browser or run `window.runSaRiTests()` in the browser developer console.

---

## 📁 Directory Structure

```
sari/
├── index.html                  # Single-Page Music Streaming App UI
├── README.md                   # Project overview & provider documentation
├── build_check.ps1             # Automated build verification script
├── styles/
│   ├── main.css                # Warm espresso design tokens, sidebar, header
│   ├── components.css          # Cards, hero vinyl, player dock, modals
│   └── responsive.css          # Mobile bottom nav & player sheet
├── js/
│   ├── app.js                  # Master application orchestrator & events
│   ├── state.js                # LocalStorage state management
│   ├── player.js               # Audio controller & MediaSession integration
│   ├── data/
│   │   ├── catalog.js          # Multilingual track metadata (12 languages)
│   │   ├── playlists.js        # Curated editorial playlists
│   │   └── genres.js           # Genres & moods taxonomy
│   ├── providers/
│   │   ├── catalogProvider.js  # Abstract interface contract
│   │   ├── demoProvider.js     # Demo catalog implementation
│   │   └── providerManager.js  # Provider registration & configuration
│   └── utils/
│       ├── formatters.js       # Time, count, and HTML sanitizer
│       ├── synthAudio.js       # Web Audio API procedural music engine
│       └── visualizer.js       # HTML5 canvas frequency EQ visualizer
└── tests/
    ├── index.html              # Test suite browser runner
    └── app_spec.js             # Automated unit & integration tests
```

---

## 🚀 Running SaRi

SaRi offers multiple zero-friction ways to run on Windows, Mac, or Linux:

### Method 1: Instant Direct Launch (No Server Needed)
Simply double-click:
- **`open_in_browser.bat`** (or open [`sari-standalone.html`](file:///C:/Users/shanm/.gemini/antigravity/scratch/sari/sari-standalone.html) or [`index.html`](file:///C:/Users/shanm/.gemini/antigravity/scratch/sari/index.html) directly in Chrome, Edge, Firefox, or Safari).
- Works completely offline and directly via the `file://` protocol.
- Includes the full standalone IIFE bundle with procedural audio synthesizer and EQ visualizer.

### Method 2: One-Click Local Web Server
Double-click:
- **`run_app.bat`**
- Uses Windows' built-in .NET HttpListener (zero dependencies, no Node/npm/Python needed).
- Automatically serves at `http://localhost:5173` and opens your browser.

### Method 3: PowerShell Build Verification
```powershell
powershell -ExecutionPolicy Bypass -File "build_check.ps1"
```
#   a t m _ c a s h o u t _ p r e d i c t o r  
 