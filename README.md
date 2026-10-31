# Flying Swords

Ten thousand glowing swords controlled by the movement of your hand, right in the browser. Hand tracking uses your webcam, with no install and no server needed.

Inspired by a demo video of flying swords controlled with bare hands.

## Features

- 10,000 swords rendered in a single draw call (`InstancedMesh`) with Three.js
- Real-time hand tracking with MediaPipe Hands, running locally in the browser
- Recognized gestures:

| Gesture | Effect |
| --- | --- |
| Open hand | Swords form a rotating sphere. The distance between thumb and pinky sets its size |
| Fist | The sphere compresses and spins faster |
| Fist, then open hand | Explosion, then the swords gradually return |
| Index finger only | A stream of swords flows in the direction of your finger |

- Mouse mode when no webcam is available: hold click = fist, release = explosion, wheel = size
- Press `F` for fullscreen
- A single HTML file, no build step

## Getting started

The webcam is only available on pages served from `localhost` or over `https`, so don't open the file directly.

```bash
git clone https://github.com/ewen177/flying-swords.git
cd flying-swords
python3 -m http.server 8000
```

Then open `http://localhost:8000/flying-swords.html` in Chrome (or any Chromium-based browser) and allow webcam access.

An internet connection is required: Three.js and MediaPipe are loaded from CDNs.

### Deploy with GitHub Pages

Enable GitHub Pages in the repository settings (deploy from the `main` branch). The site is served over `https`, so the webcam works out of the box, and the page is available at `https://ewen177.github.io/flying-swords/flying-swords.html`. To get the shorter `https://ewen177.github.io/flying-swords/` address, rename the file to `index.html`.

## Settings

Everything lives in the script of `flying-swords.html`.

| Parameter | Purpose |
| --- | --- |
| `N` | Number of swords (lower it if the animation lags) |
| `stiff` | Spring stiffness: higher means the swords follow your hand more tightly |
| `damp` | Damping: higher means fewer oscillations |
| `burst - dt * 0.22` | Explosion duration (smaller = longer) |
| `9 + Math.random() * 13` | Explosion strength |
| `modelComplexity` | `0` for faster tracking, `1` for more accuracy |

## Tips

- Use a well-lit room: the webcam reaches a higher frame rate with more light.
- Keep your hand clearly visible, palm facing the camera.
- Tracking is limited to one hand.

## Built with

- [Three.js](https://threejs.org/) (r128)
- [MediaPipe Hands](https://developers.google.com/mediapipe/solutions/vision/hand_landmarker)

## License

MIT
