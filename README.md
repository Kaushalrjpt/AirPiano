# 🎹 Air Piano

Play a full 88-key piano in mid-air using only your webcam and your hands.

Air Piano is a single HTML file. It uses real-time hand tracking to follow your fingertips and the Web Audio API to synthesize piano-like sound. Everything runs in the browser, with no backend, no build step and no installation.

> **Demo video:** [_add your LinkedIn / YouTube link here_](https://lnkd.in/p/gFtwbP_X)
---

## ✨ Features

- **Full 88-key keyboard** (A0 to C8): 52 white keys and 36 black keys.
- **Up to 10 fingers at once.** Every fingertip is tracked independently and plays the key under it.
- **Glissando.** Slide one finger across the keyboard and every key it passes plays, even keys skipped between two camera frames.
- **Accurate key detection.** Fingertip smoothing and hysteresis stop jitter from triggering the neighbouring key, and black keys are only triggered when your finger is clearly in the black-key zone.
- **Low-latency audio** using the Web Audio `interactive` latency hint and a lightweight camera feed.
- **Two play styles:** touch the keys, or tap with a quick downward finger motion.
- **Mouse and touch input** work too, with no camera needed.
- **Settings:** volume, tap sensitivity, hand overlay and note names.

---

## 🚀 Getting started

### Option 1: Run locally
1. Clone the repo:
   ```bash
   git clone https://github.com/<your-username>/air-piano.git
   cd air-piano
   ```
2. Serve the folder (the browser needs a secure context for camera access):
   ```bash
   python3 -m http.server 8000
   ```
3. Open `http://localhost:8000/AirPiano.html` in **Chrome** or **Edge**.
4. Click **Start camera** and allow camera access.

### Option 2: GitHub Pages
Enable GitHub Pages for the repo and open the published `AirPiano.html` URL. It is served over HTTPS, so the camera works right away.

> An internet connection is required on first load, because the MediaPipe library and model files come from a CDN.

---

## 🖐️ How to play

| Gesture | What happens |
|---|---|
| Move a fingertip onto a key | The note plays (touch mode) |
| Quick downward finger tap | The note plays (tap mode), with velocity-based loudness |
| Slide one finger across keys | Glissando: every key you pass plays |
| Several fingers on several keys | Chord: all notes play together |
| Lift or move your finger away | The note fades out |

**Tips**
- Use good, even lighting, and keep your hands fully inside the camera frame.
- Keep your palm facing the camera with fingers slightly spread when playing chords.
- If notes trigger too easily or not easily enough, adjust **Tap sensitivity** in Settings.

---

## 🛠️ How it works

1. **Capture:** the webcam stream is read at 960×540.
2. **Hand tracking:** [MediaPipe Hands](https://developers.google.com/mediapipe) returns 21 landmarks per hand, and the 5 fingertips are used for playing.
3. **Smoothing:** each fingertip is smoothed adaptively, steady when still and instant when moving fast.
4. **Key resolution:** the fingertip position maps to a key, with hysteresis so the note doesn't flip to a neighbour near an edge. Black keys use a depth rule.
5. **Trigger logic:** a note fires on touch or on a downward tap, each finger runs its own state machine, and a short grace period covers dropped tracking frames.
6. **Sound:** each note is a small additive synth (triangle plus sine harmonics) with a piano-like envelope, routed through a compressor so chords don't clip.

**Tech:** HTML, CSS, vanilla JavaScript, MediaPipe Hands, Web Audio API, Canvas 2D.

---

## 📁 Project structure

```
air-piano/
├── AirPiano.html   # the whole app: UI, tracking logic and synth
├── README.md
└── docs/           # screenshots / demo assets
```

---

## ⚠️ Known limitations

- Accuracy depends on lighting, camera quality and hand visibility.
- Tracking latency depends on your device, since it is a combination of camera and model speed.
- On a 88-key layout the keys are narrow, and a wider browser window gives better precision.
- Tested mainly in desktop Chrome. Other browsers may vary.

---

## 🗺️ Roadmap

This project is a stepping stone toward something bigger. Ideas for upcoming iterations:

- [ ] Better tracking speed and a fast/precise mode switch
- [ ] Selectable instruments and sound banks
- [ ] Recording and playback
- [ ] Adjustable keyboard range and zoom
- [ ] Visual feedback and falling-note modes

_Edit this list to match your actual plans._

---

## 🙏 Acknowledgements

- [MediaPipe Hands](https://developers.google.com/mediapipe) by Google for hand landmark detection.


## 👤 Author

**Kaushal Pratap Rajput**
[LinkedIn](https://www.linkedin.com/in/kaushal-pratap-rajput-4216b1329/) · [Github](https://github.com/Kaushalrjpt)
