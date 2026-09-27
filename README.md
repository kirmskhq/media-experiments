# Media Experiments

Small fun browser experiments for kids with webcams, hand tracking and live video filters.

**Live site:** https://kirmskhq.github.io/media-experiments/

## Experiments

### [Roblox Hand Portal](https://kirmskhq.github.io/media-experiments/hand_portal_roblox.html)

Frame a window with both hands in front of the webcam and see the video inside it through a Roblox-style filter. Pinch all five fingertips together (or press ←/→) to switch filters.

Filters: Roblox Avatar (turns faces into the classic yellow-headed Roblox character), Studs, Noob, Toon, Voxel, Neon Obby, Lava, Oof, BrickColor and Baseplate.

Hand and face tracking run fully in the browser with [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/hand_landmarker); no video leaves your device.

## How it works

Each experiment is a single static HTML file with no build step and no server code.

- **Hand tracking:** [MediaPipe Tasks Vision](https://www.npmjs.com/package/@mediapipe/tasks-vision) `HandLandmarker` (WebAssembly + GPU delegate, loaded from jsDelivr) finds 21 landmarks per hand in every webcam frame. The index-finger and thumb tips of both "L" gestures form the portal's four corners, and all five fingertips bunched together switches the filter.
- **Face tracking:** MediaPipe `FaceLandmarker` with blendshapes gives head position, tilt, turn, blinks and jaw opening, which drive the Roblox head drawn over each face.
- **Filters:** a WebGL 1 fragment shader renders the mirrored video through the chosen effect (bricks and studs, palette mapping, Sobel edge outlines, posterizing, animated lava and neon).
- **Compositing:** a 2D canvas draws the plain video, clips to the portal shape, then draws the filtered frame and the avatar on top.
- **Camera:** `getUserMedia`, so the page needs HTTPS (GitHub Pages) or `localhost`.

## Running locally

Browsers only allow camera access over HTTPS or on `localhost`:

```sh
python3 -m http.server
# then open http://localhost:8000/
```
