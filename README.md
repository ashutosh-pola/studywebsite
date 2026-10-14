# ⏱️ Study Tracker — Single-File Dark Mode Web App

A clean, responsive, single-file (`index.html`) Study Tracker inspired by **GitHub's dark theme**. Includes an accurate background-proof stopwatch, a full 52-week contribution heatmap, live metric cards, JSON backups, and plug-and-play cloud sync architecture.

---

## 🌟 Highlights

- **Single-File Zero Dependency Architecture**: HTML, CSS, and JavaScript are 100% self-contained in [index.html](file:///Users/ashutosh/Antigravity/mac%20app%20for%20timer/index.html). No build steps, bundlers, or npm packages required.
- **Accurate Background Stopwatch**: Calculates elapsed time using real `Date.now()` timestamp deltas so the timer never drifts or slows down when browser tabs are in the background or mobile screens sleep. Automatically restores active sessions across page refreshes.
- **52-Week GitHub Activity Heatmap**:
  - Full 365+ day grid with days **Mon–Sun** on the Y-axis and **Jan–Dec** on the X-axis.
  - 5-tier color scale based on daily minutes:
    - `0m`: Dark Grey (`#161b22`)
    - `1 – 30m`: Deep Green (`#0e4429`)
    - `31 – 60m`: Medium Green (`#006d32`)
    - `61 – 120m`: Bright Green (`#26a641`)
- **Subjects & Custom Colors**:
  - Categorize sessions by subject (e.g. Mathematics, Computer Science, Physics, Reading, etc.).
  - Choose a custom color for each subject with curated swatches or an RGB color picker.
  - **Subject Distribution Bar**: Multi-color visual progress bar displaying the percentage split of your study time.
  - **Dynamic Heatmap Filtering**: Filter the entire 52-week heatmap by any subject to see only time logged for that subject in its custom color hue!
  - **Subject Tooltip Breakdown**: Hovering any heatmap square displays an itemized list of subjects studied on that date with matching colored dots.
- **Summary Metrics**:
  - **Today's Focus**: Total minutes/hours logged today against your daily target.
  - **Current Streak**: Automatically tracks consecutive active study days.
  - **Total Hours**: Cumulative study time across all recorded sessions.
- **Offline & Backup Ready**:
  - Works out of the box via `localStorage`.
  - **Export Backup (JSON)**: Instant one-click download.
  - **Import Backup**: Restore or merge study logs from any previous JSON backup.
  - **Seed Demo Data**: One-click test button to populate 90 days of realistic sample study logs.

---

## 🚀 Free Hosting & Deployment

Because this app is a single static `index.html` file, you can host it for free in seconds:

### Option 1: GitHub Pages (Recommended)
1. Create a new repository on GitHub (e.g. `study-tracker`).
2. Push `index.html` to the repository.
3. In the repository settings, go to **Pages** -> under **Build and deployment**, select **Deploy from a branch** -> branch: `main` / folder: `/(root)`.
4. Click **Save**. Your site will be live at `https://<your-username>.github.io/study-tracker/`.

### Option 2: Vercel
1. Install Vercel CLI (or connect your GitHub repository to Vercel dashboard):
   ```bash
   npx vercel
   ```
2. Follow the prompt (defaults to static deployment). Your app will be live immediately with free global HTTPS.

### Option 3: Firebase Hosting
1. Install Firebase CLI:
   ```bash
   npm install -g firebase-tools
   firebase login
   firebase init hosting
   ```
2. Set your public directory to `.` (current directory).
3. Deploy:
   ```bash
   firebase deploy --only hosting
   ```

---

## ☁️ Cross-Device & ESP32 Sync (Firebase Firestore)

The application includes a clean **`StorageAdapter`** abstraction located inside the `<script>` tag of [index.html](file:///Users/ashutosh/Antigravity/mac%20app%20for%20timer/index.html).

### To enable live cloud sync across all your devices:
1. Create a free project at [Firebase Console](https://console.firebase.google.com/) and enable **Cloud Firestore**.
2. Add the Firebase compat SDK to `<head>` in `index.html`:
   ```html
   <script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-app-compat.js"></script>
   <script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore-compat.js"></script>
   ```
3. In `index.html`, set `USE_FIREBASE = true;` and paste your project config:
   ```javascript
   const USE_FIREBASE = true;
   const FIREBASE_CONFIG = {
     apiKey: "AIzaSy...",
     authDomain: "my-study-app.firebaseapp.com",
     projectId: "my-study-app",
     storageBucket: "my-study-app.appspot.com",
     messagingSenderId: "...",
     appId: "..."
   };
   firebase.initializeApp(FIREBASE_CONFIG);
   ```
4. Now, any study session logged from your phone, laptop, or an external device (like an ESP32 sending an HTTP POST webhook or Firestore REST API call) will sync in real time!
