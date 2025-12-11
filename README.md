# 🌃 Pattaya Nightlife Map (Consolidated)

An interactive real-time nightlife map of Pattaya, Thailand, combining the best features from multiple projects.

## ✨ Features

### Core Map Functionality
- 🗺️ **Interactive Leaflet Map**: Emoji-based venue markers with color intensity
- 🚶 **Corridor Visualization**: Real-time traffic flows from Lantana Plaza to nightlife zones
- ☀️ **Early Hotspot Detection**: Identifies venues with high 12:00-17:00 activity
- 🌧️ **Weather Integration**: Multiple providers (demo, OpenWeather, Open-Meteo)
- 🌃 **Night Lights Layer**: Toggle dark-themed map tiles

### Analytics & Insights
- 📊 **After-Shift Analysis**: Top 3 venues by social mentions (22:00-06:00)
- 🌍 **Multi-language Segments**: Separate rankings for Expat vs. Asian audiences
- 📈 **Dynamic Scoring**: Weather-adjusted venue scores
- 🔥 **Now/Tonight Strip**: Real-time corridor traffic and venue activity

### Filtering & UI
- 🍲 **Mokata/BBQ Filter**
- 🎤 **Karaoke Filter**
- 🎩 **Gentlemen's Clubs Filter**
- 🌙 **Open Late Filter**
- 🌅 **Open Early Filter**
- 📱 **Mobile-First Design**

## 🚀 Quick Start

### Prerequisites
- Python 3.8+
- Node.js 18+ (for Playwright tests)
- SQLite3 (usually pre-installed)

### Installation

```bash
cd ~/Projects/pattaya_map_wip

# Run setup script
chmod +x install.sh run.sh
./install.sh
```

### Start the Server

```bash
./run.sh
```

Open: **http://localhost:8000**

## 🧪 Testing with Playwright

```bash
# Install test dependencies
cd tests
npm install
npx playwright install

# Run all tests
npm test

# Run with browser visible
npm run test:headed

# Run with Playwright UI
npm run test:ui
```

## 📊 API Endpoints

| Endpoint | Description |
|----------|-------------|
| `GET /api/pattaya/all_nightlife_venues` | All venues with coordinates, scores, tags |
| `GET /api/pattaya/corridor_flows` | Traffic data from Lantana (last 90 min) |
| `GET /api/pattaya/xzyte_summary` | Xzyte area venue counts |
| `GET /api/pattaya/aftershift_top3` | Top venues tonight (All/Expat/Asian) |
| `GET /api/pattaya/weather_context` | Current weather + rain status |
| `GET /api/venues` | All venues (extended) |
| `GET /api/venues/{slug}` | Single venue by slug |
| `GET /health` | Health check |

## 🔧 Configuration

Edit `config/secrets.txt` to configure API keys:

```bash
# Weather Provider (demo, openweather, open-meteo)
WEATHER_PROVIDER=openweather
OPENWEATHER_API_KEY=your_key_here

# Map Tiles (optional)
MAPTILER_API_KEY=your_key_here

# WiFi Density Data (optional)
WIGLE_API_NAME=your_name
WIGLE_API_TOKEN=your_token
```

## 🏗️ Project Structure

```
pattaya_map_wip/
├── backend/
│   ├── app/
│   │   ├── main.py          # FastAPI application
│   │   └── __init__.py
│   └── requirements.txt
├── frontend/
│   ├── index.html           # Main HTML page
│   ├── map.js               # Leaflet map + UI logic
│   └── style.css            # Mobile-first styling
├── database/
│   ├── schema.sql           # Database schema
│   ├── seed_data.sql        # Demo venues
│   └── nightlife.db         # SQLite database (created on install)
├── tests/
│   ├── playwright/
│   │   ├── map.spec.ts      # Map E2E tests
│   │   └── api.spec.ts      # API integration tests
│   ├── playwright.config.ts
│   └── package.json
├── config/
│   └── secrets.txt          # API keys (gitignored)
├── install.sh               # Setup script
├── run.sh                   # Run script
├── README.md
└── AGENTS.md
```

## 📱 Mobile Support

The map is fully responsive and optimized for mobile devices:
- Touch-friendly controls
- Swipe to pan, pinch to zoom
- Collapsible panels to maximize map space
- Dark theme for nighttime use

## 🔒 Security

- API keys stored in `config/secrets.txt` (gitignored)
- Optional encryption via `tools/encrypt_secrets.py`
- CORS enabled for development
- SQLite with foreign key enforcement

## 🛠️ Development

### Running in Development Mode

```bash
cd backend
source ../.venv/bin/activate
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

### Adding New Venues

```sql
INSERT INTO venues (city_id, zone_id, slug, name, lat, lng)
VALUES (
  (SELECT id FROM cities WHERE name='pattaya'),
  (SELECT id FROM zones WHERE name='walking_street'),
  'venue_slug',
  'Venue Name',
  12.9271,
  100.8785
);

INSERT INTO venue_tags (venue_id, tag)
VALUES (
  (SELECT id FROM venues WHERE slug='venue_slug'),
  'mokata'  -- or karaoke, gclub, open_late, open_early
);
```

## 📝 Source Projects

This project consolidates features from:
- **Master-pattaya-map**: Corridors, weather integration
- **pattaya-nightlife-map**: Early/after-shift analysis, secrets encryption
- **pattaya-hotspots-complete**: Extended venue categories

---

Built with ❤️ for Pattaya nightlife exploration.
