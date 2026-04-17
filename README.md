# 🍽️ Food Picker

A simple web app that randomly picks a restaurant from your list — so your spouse can keep saying no until you find one they actually want.

## Features

- Add restaurants with optional address or Google Maps link
- Uses your location + a radius slider to only pick places nearby
- "She said no" marks the pick rejected and auto-picks another
- "She said yes" locks in the choice
- Everything saved locally in your browser (no account, no server)

## Usage

### Run it

Just open `index.html` in a browser — no build step, no server needed.

Or serve it locally:

```bash
npx http-server . -p 8765
```

Then visit http://localhost:8765.

### Adding a restaurant

1. Type the **name** in the first field.
2. (Optional) Type an **address** or paste a **Google Maps link** in the second field.
3. Click **Add**.

**Google Maps links:** Works with full `google.com/maps/...` URLs and short `maps.app.goo.gl/...` links (uses a CORS proxy to expand them). If you pasted a link and left the name blank, it'll auto-fill the restaurant name from the link.

> `share.google/...` links don't work — they require JavaScript to resolve. Use **Share → Copy link** from the Google Maps app to get a `maps.app.goo.gl` link instead.

### Setting your location + radius

1. Click **📍 Use my location** (browser will ask for permission).
2. Drag the **radius slider** (1–50 km) to set how far you'll travel.
3. Only restaurants within range will be picked. Entries with no address are always eligible.

### Picking

1. Click **🎲 Pick a Restaurant**.
2. Two buttons appear:
   - **👎 She said no** — marks the pick rejected, auto-picks another.
   - **👍 She said yes!** — locks it in.
3. Keep rejecting until you get a yes, or run out of options.

### Fixing broken entries

If a restaurant is missing coordinates (failed geocoding when added):

- Click the **↻** icon next to it to retry just that one.
- Or click **Fix missing locations** in the list header to bulk-retry everything.

### Reset

- **Reset rejections** puts everything back in play without deleting anything.
- Click the **×** next to any restaurant to delete it.

## Where's the data stored?

In your browser's `localStorage`. That means:

- It persists across page reloads on the same browser.
- It does **not** sync between devices or browsers.
- Clearing site data will wipe everything.

Keys used: `foodPicker.restaurants`, `foodPicker.userLocation`, `foodPicker.radius`.

## Tech

Single-file vanilla HTML/CSS/JS. Uses:

- [OpenStreetMap Nominatim](https://nominatim.openstreetmap.org/) for geocoding addresses
- [allorigins.win](https://allorigins.win/) / [codetabs.com](https://codetabs.com/) as CORS proxies to expand Google Maps short links
- Browser Geolocation API for your location
