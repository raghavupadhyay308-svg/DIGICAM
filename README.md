# RetroCam

A digital-camera-style web app with 40 live retro filters (CRT, VHS, NTSC, Code Rain, Webcam '95, Glitch, Super 8, Thermal, ASCII and more). Take photos, record videos, and download them directly. Single HTML file, no dependencies, no build step.

Inspired by [Retro Rad](https://retro-rad.higgsfield.app/). Filters are re-implemented in real time with the Canvas 2D API instead of AI image generation.

## Features
- Live camera preview with filters applied in real time (front/back camera)
- Photo (JPG) and video (MP4/WebM) capture via `canvas.captureStream` + `MediaRecorder`
- Upload an existing photo or video and apply filters
- Optional burned-in orange date stamp
- Memory-card gallery with one-click downloads

## Run
The camera needs a secure context, so use `localhost` or HTTPS:

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

## Deploy
Push `index.html` to a GitHub repo and enable GitHub Pages (Settings → Pages → main / root).

## Tech
Vanilla JS, Canvas 2D, MediaDevices API, MediaRecorder API.

## Adding a filter
Add an entry to the `F` array in `index.html`: `['Name', t => { /* draw on ctx `g` */ }]`.

## Cameras and FX menu
- 28 camera presets in two shelves: **Photo** (photo only) and **Photo & Video**. Each camera loads its own default look and the leather body updates its model name and trim colour.
- **FX Menu** lists all 40 filters in tabs (TV & Tape, Glitch, Film, Art, Special). Pick any filter on top of the selected camera.

## Camera controls
Tap a cell on the amber LCD (or the EV dial), then turn the control wheel (drag it, tap its sides, or use the Up/Down arrow keys).

| Control | Effect |
|---|---|
| EV | Exposure compensation, -2 to +2 in 1/3 steps |
| ISO | 100-3200: brighter image and more sensor noise |
| SHUT | Slow shutter speeds (1/30 to 1/4) leave motion trails |
| F | Aperture: wide f-numbers blur everything away from the focus point and add a vignette |
| WB | White balance presets |
| FLASH | Auto / On / Off (fires at capture, Auto only in low light) |
| TIMER | 3 s or 10 s self-timer |
| ZOOM | Digital zoom up to 4x |
| GRID / HIST | Rule-of-thirds grid and live histogram |

Tap the screen to move the focus point. Controls are simulated on the canvas pipeline, not real sensor settings.

## Video
Switch the Photo/Video toggle to **Video** and press the shutter to start and stop recording. Works on every camera preset. All filters and manual controls (EV, ISO, WB, aperture, zoom, grid) are baked into the recording.
- **MIC** ON records microphone audio. **FPS** sets 30 / 24 / 15 frames per second.
- Saves MP4 where the browser supports it (Safari, recent Chrome), otherwise WebM.
- Imported videos can also be filtered and re-recorded (without audio).
- Tap-to-focus works while recording. The flash only fires for photos.
