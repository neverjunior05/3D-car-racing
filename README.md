# Desk Racer

Desk Racer is a browser-based miniature kart time trial. Drive a tiny kart around a multi-level roller-coaster track winding through a detailed desktop diorama. The scene is rendered in 3D with Three.js, while a heads-up display shows the current lap, elapsed time, speed, and position on the course.

The circuit is designed at 1:87 scale: the modeled kart is about 18 mm long and the tabletop is about 1.1 m wide. The course climbs and spirals around desk objects, including a laptop stand, a cat figurine, and a desk lamp.

## Features

- Three-dimensional desktop scene, coaster track, and micro-kart.
- Three-lap time trials with a start countdown, lap timer, lap splits, and finish screen.
- Keyboard driving and on-screen touch controls for mobile-sized screens.
- Four quick-select camera views: chase, cockpit, full desk, and drone.
- Live track minimap and speedometer.
- Optional auto-pilot and sound, including sampled engine and tire effects.
- Rendering effects such as depth of field, bloom, shadows, and a warm lighting setup.

## Controls

| Input | Action |
| --- | --- |
| `W` or `↑` | Accelerate |
| `S` or `↓` | Brake |
| `A` or `←` | Steer left |
| `D` or `→` | Steer right |
| `1` | Chase view |
| `2` | Cockpit view |
| `3` | Full desk view |
| `4` | Drone view |
| `M` | Toggle sound |
| `Enter` | Start the time trial or race again |
| `Escape` | Toggle the settings popover |

Click the **Desk Racer** title to reopen the welcome and controls dialog. After completing a race, choose **Race Again** or **Auto-Pilot** on the finish screen. On touch devices, use the on-screen steering, accelerate, and brake buttons.

## Run locally

### Requirements

- Node.js and npm
- A modern browser with WebGL enabled
- An internet connection for the 3D models and web fonts

### Install and start

```bash
npm install
npm run dev
```

Open the local URL printed by Vite (by default, `http://localhost:3000`). No API key, `.env.local` file, or backend service is required to play.

### Build and check

```bash
npm run lint
npm run build
npm run preview
```

`npm run lint` runs the TypeScript compiler without emitting files. `npm run build` creates the production site in `dist/` and downloads the GLB model files from Google’s hosted Desk Racer assets, so a working internet connection is required whenever you build. `npm run preview` serves the built site locally.

## Project layout

| Path | Purpose |
| --- | --- |
| `index.html` | Application shell, HUD, welcome and finish dialogs, and touch controls. |
| `src/main.js` | Three.js setup, model and data loading, input handling, race flow, camera behavior, and rendering. |
| `src/physics/KartPhysicsController.js` | Rapier physics world, track-following kart controller, and auto-pilot behavior. |
| `src/scene/` | Procedural scene, track, kart, environment, lighting, and texture builders. |
| `src/audio/WebAudioSynth.js` | Web Audio engine and playback of the included audio samples. |
| `public/assets/data/desk_manifest.json` | Desk-object dimensions and miniature-scale reference data. |
| `public/assets/data/track_spline.json` | Track path and orientation samples used by the course and physics. |
| `public/assets/audio/` | Engine, tire, curb, and sputter audio samples. |
| `vite.config.ts` | Vite server configuration, model proxy routes, and production model download. |

The app loads the desk manifest and track spline from `public/assets/data`. The four GLB models (`desk_props`, `kart_1to87`, `room_environment`, and `track_coaster`) are hosted externally; the Vite development and preview servers proxy requests for them, and the production build copies them into the output directory.

## Troubleshooting

- **The scene is blank or does not render:** Check that WebGL is enabled and supported by your browser and graphics driver.
- **Models do not appear:** Check your internet connection and browser network errors; the GLB files are fetched from Google-hosted assets.
- **The build fails while fetching models:** Retry with network access to `www.gstatic.com` and check that the model URLs are reachable.
- **There is no sound:** Use the `M` key or sound button to enable audio. Browsers may wait for a user interaction before allowing playback.
