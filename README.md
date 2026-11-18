# ⚡ VoltTrack — EV Charging Energy Tracker & Analytics

> A beautiful, fully client-side dashboard to track, analyse, and optimise your electric vehicle charging sessions. No backend, no login, no installation — just open and go.

![VoltTrack Dashboard](screenshots/dashboard.png)

---

## ✨ Features

### 📊 Executive Dashboard
- **6 KPI Summary Cards** — Total energy (kWh), total cost (₹), session count, average cost/kWh, average session duration, driving efficiency (km/kWh)
- **Global Date-Range Filter** — Presets: Last 30 days, Last 3 months, Last 6 months, All time, plus a custom start/end date picker; every chart responds instantly

### 📈 5 Interactive Recharts Visualizations
| Chart | Type | What it shows |
|---|---|---|
| Monthly Energy Consumption | Bar chart | kWh delivered by month |
| Monthly Charging Cost | Line chart | ₹ spent by month with dots |
| Energy by Charger Type | Donut chart | Home AC / Public AC / DC Fast share |
| Charging Activity by Hour | 24 h bar chart | Sessions per hour, peak bar highlighted |
| Efficiency Over Time | Line chart | km/kWh from consecutive odometer deltas + reference line |

### 📋 Session Manager
- **Sortable table** (click any column header) with 15-row pagination
- **Search** by location, ID, date, or charger type
- **Filters** by charger type badge + date range pickers
- **Edit / Delete** each session inline
- **CSV Export** — downloads all sessions as a dated `.csv` file
- **CSV Import** — merge sessions from any CSV, duplicate IDs are skipped

### ➕ Add / Edit Session Form
- Fully validated inputs with inline error messages (no alert dialogs)
- **Auto-calculates** energy from Start/End SoC % and total cost from rate × kWh
- Charger type selector auto-fills location, rate, and typical duration defaults
- Persists to `localStorage` instantly

### 💡 Automated Insights (plain language)
1. Most expensive charging location by unit rate
2. Cheapest vs. most expensive charger type (rate spread multiplier)
3. Peak charging hour window and % of sessions
4. Month-over-month energy change (kWh & %)
5. Potential savings if 100% of charging was done at home
6. Projected cost for next month (3-month rolling trend model)
7. Actionable efficiency recommendations

### 🎨 UI / UX
- Dark / Light mode toggle, persisted in `localStorage`
- Mobile-first responsive layout with a **bottom tab bar** on small screens
- Toast notifications (no native `alert()` dialogs)
- Error boundary — a section crash shows a friendly card, not a blank screen
- Full-page loading splash while React initialises
- Empty states with descriptive messages for every zero-data scenario
- SVG favicon + SEO meta tags

---

## 🗂 File Structure

```
Portfolio/
├── index.html                  # Complete SPA — React + Tailwind + Recharts (CDN)
├── sample_data.js              # 150 sessions exposed as window.SAMPLE_CHARGING_SESSIONS
├── sample_charging_sessions.json  # Raw 150-session JSON dataset
├── favicon.svg                 # Lightning bolt SVG favicon
├── server.js                   # Lightweight Node.js static file server (dev only)
├── package.json
├── vercel.json                 # Vercel deployment config
├── netlify.toml                # Netlify deployment config
├── .nojekyll                   # GitHub Pages — disable Jekyll
├── .gitignore
└── README.md
```

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| UI Framework | **React 18** (via unpkg CDN, no build step) |
| JSX Transpiler | **Babel Standalone** (in-browser) |
| Styling | **Tailwind CSS** (via CDN Play) |
| Charts | **Recharts 2.12** (UMD build via unpkg) |
| Persistence | Browser **localStorage** |
| Icons | Inline SVG components |
| Dev Server | Node.js built-in `http` module |
| Deployment | Static file hosting (Vercel / Netlify / GitHub Pages) |

> **No build step, no npm install, no bundler.** The entire app is a single `index.html` file that runs anywhere.

---

## 🚀 Run Locally

### Option A — Node.js dev server (recommended)
```bash
# Clone or download the repo
cd Portfolio

# Start the included server
node server.js
# → VoltTrack web server running at http://localhost:3000/
```
Then open **http://localhost:3000/** in your browser.

### Option B — `npx serve` (zero install)
```bash
npx serve .
# → Serving at http://localhost:3000
```

### Option C — Direct file open
Double-click `index.html` in your file manager. The sample data is embedded in `sample_data.js` so it works without a server.

> **Note:** Chrome blocks `file://` fetches of sibling scripts. If charts don't load, use Option A or B.

---

## ☁️ Deploy to Production

### ▲ Vercel (Recommended — free, instant, CDN)

1. Push the project to a GitHub (or GitLab) repository:
   ```bash
   git init
   git add .
   git commit -m "Initial VoltTrack release"
   git remote add origin https://github.com/YOUR_USERNAME/volttrack.git
   git push -u origin main
   ```
2. Go to **[vercel.com](https://vercel.com)** → **New Project**
3. Import your GitHub repository
4. Settings (all auto-detected, nothing to change):
   - **Framework Preset:** Other / Static
   - **Build Command:** *(leave blank)*
   - **Output Directory:** `.` (root)
5. Click **Deploy**
6. ✅ Live in ~30 seconds at `https://volttrack.vercel.app`

> `vercel.json` is already committed — it sets security headers and correct MIME types automatically.

---

### 🌐 Netlify (Drag-and-drop or Git)

**Option A — Drag & Drop (fastest)**
1. Go to **[app.netlify.com](https://app.netlify.com)** → **Sites**
2. Drag the entire `Portfolio/` folder onto the **"Drag and drop your site folder here"** area
3. ✅ Live in ~10 seconds at a generated URL like `https://amazing-tesla-abc123.netlify.app`

**Option B — Git integration**
1. Push the project to GitHub (same steps as Vercel step 1 above)
2. Netlify → **Add new site → Import an existing project**
3. Connect GitHub → select your repo
4. Settings:
   - **Branch:** `main`
   - **Build command:** *(leave blank)*
   - **Publish directory:** `.`
5. Click **Deploy site**

> `netlify.toml` is already committed — Netlify picks it up automatically.

---

### 📄 GitHub Pages

1. Push to GitHub (same steps as Vercel step 1)
2. Go to your repo → **Settings → Pages**
3. **Source:** `Deploy from a branch`
4. **Branch:** `main` / **Folder:** `/ (root)`
5. Click **Save**
6. ✅ Live in ~1 minute at `https://YOUR_USERNAME.github.io/volttrack/`

> `.nojekyll` is already committed so GitHub won't strip your JS files.

**Important:** If deployed to a subfolder path (e.g. `/volttrack/`), `sample_data.js` reference in `index.html` uses a relative `./` path and will work correctly.

---

## 📸 Screenshots to Add

Create a `screenshots/` folder and add these images for the README:

| File | What to capture |
|---|---|
| `screenshots/dashboard.png` | Full dashboard in dark mode — all 6 KPI cards + date filter visible |
| `screenshots/charts.png` | Dashboard scrolled down to show all 5 Recharts charts |
| `screenshots/sessions.png` | Sessions page with the full table, search bar, and type filter badges |
| `screenshots/add-session.png` | Add Session modal open with form filled in |
| `screenshots/insights.png` | Insights page showing all 6 analytics cards |
| `screenshots/mobile.png` | Mobile viewport (375 px) showing bottom tab bar + dashboard cards |
| `screenshots/light-mode.png` | Dashboard in light mode |

**To capture:** Open the app in your browser, press `F12 → Network tab → Disable cache`, then use the browser's screenshot tool or a tool like [Screely](https://screely.com) to add a device frame before uploading.

---

## 📦 Data Model

Each charging session follows this schema:

```json
{
  "id":               "EV-CHG-0001",
  "date":             "2026-05-18",
  "startTime":        "22:15",
  "durationMinutes":  320,
  "energyAddedKwh":   37.8,
  "startSoC":         35,
  "endSoC":           80,
  "chargerType":      "Home AC",
  "locationName":     "Home - Garage Wallbox (7.4 kW)",
  "costPerKwh":       12.0,
  "totalCost":        453.60,
  "odometerKm":       24560
}
```

Sessions are persisted in `localStorage` under the key `ev_charging_sessions`.

---

## 🔄 Reset / Sample Data

Click **"Reload 150 Sample Sessions"** in the sidebar at any time to restore the full realistic 150-session dataset spanning May – November 2026.

The dataset includes:
- ~76% Home AC overnight charging (22:00–01:00)
- ~16% DC Fast charging on weekends (road trips)
- ~8% Public AC opportunistic charging (daytime errands)
- Gradual odometer increase from 24,560 km → 42,295 km
- Seasonal variation in energy consumption

---

## 📝 License

MIT — free to use, modify and deploy.
