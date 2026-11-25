# Focus Guard AI — On-Device Phone Distraction Detector

![TensorFlow.js](https://img.shields.io/badge/TensorFlow.js-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)
![Teachable Machine](https://img.shields.io/badge/Teachable%20Machine-4285F4?style=for-the-badge&logo=google&logoColor=white)
![Vercel](https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)
![GDG on Campus VTU](https://img.shields.io/badge/GDG%20on%20Campus-VTU%20Belagavi-34A853?style=for-the-badge)

**Focus Guard AI** is a beginner-friendly, browser-based computer vision web app built for the **GDG on Campus — VTU Belagavi** Teachable Machine Build Hour. It uses a custom image classification model (`me` vs. `me_phone`) powered by **Transfer Learning** and **TensorFlow.js** to detect phone distractions in real time—with **100% on-device privacy** (zero video frames ever leave your browser).

---

## Features

- **Real-Time Browser AI:** Runs MobileNet transfer learning directly on your device via `@tensorflow/tfjs` and `@teachablemachine/image`.
- **Personalized Session:** Prompts for your name at launch, tailors live focus alerts, and stamps your name onto the bottom status bar.
- **Live Focus Telemetry:** Tracks active **Focus Time**, **Phone Pickups**, and real-time **Focus Score (%)**.
- **Anti-Flicker Debounce & Audio Alerts:** Triggers visual alert mode and a gentle Web Audio API beep only when a phone is detected continuously for 1+ second.
- **Zero-Build Architecture:** Pure HTML, CSS, and vanilla JavaScript—no bundlers, no `npm install`, and instant free hosting on Vercel.

---

## Project Structure

```text
focus-guard/
├── index.html          # Complete frontend UI + TensorFlow.js inference logic
├── my_model/           # Exported Teachable Machine TensorFlow.js model
│   ├── metadata.json   # Class labels (me, me_phone) and model metadata
│   ├── model.json      # Neural network architecture graph
│   └── weights.bin     # Trained model weights
├── README.md           # Project documentation and setup guide
└── CONTRIBUTING.md     # Guidelines for contributors and remixers
```

> **Note:** Make sure any downloaded `.zip` archive (such as `tm-my-image-model.zip`) is deleted before pushing to GitHub or deploying to Vercel.

---

## Step-by-Step Setup Guide

### Prerequisites

- **Google Chrome** (recommended for WebGL acceleration and camera selection)
- **Webcam** OR a **Smartphone + DroidCam** (for lab PCs without built-in cameras)
- **Local Web Server:** Python 3 (`python3 -m http.server`) or VS Code **Live Server** extension

---

### Step 1: Lab PC Webcam Setup with DroidCam (Skip if Using a Laptop)

If your desktop does not have a built-in webcam, use your smartphone as a virtual camera:

1. Install **DroidCam** on your phone (Play Store / App Store) and the **DroidCam Client** on your PC ([droidcam.app](https://droidcam.app/)).
2. **Connect via USB (recommended on campus networks):**
   - **Android:** Enable *Developer Options* → turn ON *USB Debugging* → plug in via USB cable → open DroidCam on phone → click **Add → DroidCam → Refresh Device List** in the PC client.
   - **Wi-Fi Alternative:** Connect both devices to the exact same Wi-Fi network and select your phone from the refreshed device list.
3. **Select DroidCam in Chrome:**
   - Restart Chrome after connecting DroidCam.
   - Open `chrome://settings/content/camera` and choose **DroidCam Video** as the default camera.

---

### Step 2: Train & Export Your Own Model in Teachable Machine

1. Open [teachablemachine.withgoogle.com](https://teachablemachine.withgoogle.com/) → **Get Started** → **Image Project** → **Standard image model**.
2. Create **two classes** (exact names):
   - `me` — Sit naturally looking at the screen/desk with no phone visible (capture 60–80 samples with slight head/angle movement).
   - `me_phone` — Hold up or look down at your phone in natural positions (capture 60–80 samples).
3. *(Optional)* Check **Advanced** training settings:
   - **Epochs:** `50` (default; balanced speed & accuracy)
   - **Batch Size:** `16`
   - **Learning Rate:** `0.001`
4. Click **Train Model** (keep the browser tab open and active while training).
5. Test both poses in the **Preview** panel and click **Under the hood** to inspect accuracy, loss, and the confusion matrix.
6. Click **Export Model** → **TensorFlow.js** → **Download** → **Download my model**.
7. Unzip the downloaded files (`model.json`, `metadata.json`, `weights.bin`) into the `my_model/` folder inside `focus-guard/`.

*(Alternative: Choose **Upload my model** in Teachable Machine and replace `const MODEL_URL = "./my_model/";` in `index.html` with your hosted URL.)*

---

### Step 3: Run Locally

Do **not** open `index.html` by double-clicking it (`file://` URLs are blocked by browser CORS policies when loading `model.json`). Serve the folder over `localhost`:

#### Option A: Python (Works on Linux, macOS & Windows)
```bash
cd focus-guard
python3 -m http.server 8000
```
*(Use `python -m http.server 8000` on Windows if `python3` is not recognized.)*

#### Option B: VS Code Live Server
1. Open the `focus-guard` folder in VS Code.
2. Right-click `index.html` and click **Open with Live Server**.

Open **[http://localhost:8000](http://localhost:8000)** in Chrome (use `localhost`, not `0.0.0.0`, so Chrome permits webcam access).

---

### Step 4: Deploy Live to Vercel

Deploying gives you a free `https://` link that works directly on mobile phones using their built-in cameras.

#### Option A: Vercel Drop (No Git or CLI Needed)
1. Go to [vercel.com/drop](https://vercel.com/drop) and sign in.
2. Drag and drop your entire `focus-guard/` folder onto the page.
3. Click **Deploy** to get your live `*.vercel.app` URL.

#### Option B: GitHub + Vercel
1. Push this repository to GitHub.
2. Log in to [vercel.com](https://vercel.com) → **Add New → Project** → import your repo.
3. Leave **Framework Preset** as *Other* (empty Build Command and Output Directory) and click **Deploy**.

---

## Customization Tips

- **Use an Official Chapter Logo Image:** Place `gdg-logo.png` in `focus-guard/` and replace the `<svg>` inside `.gdg-logo-wrap` in `index.html` with:
  ```html
  <img src="./gdg-logo.png" alt="GDG on Campus VTU" style="height: 28px; width: auto;" />
  ```
- **Adjust Sensitivity:** Change `top.probability >= 0.75` or the `1000` ms debounce timer in `index.html` to tune how quickly alerts fire.

---

## Troubleshooting

| Issue | Likely Cause | Fix |
| :--- | :--- | :--- |
| Camera blocked in Chrome | Opened `http://0.0.0.0:8000` or `file://` | Always open `http://localhost:8000` locally, or use an `https://` Vercel URL. |
| `Failed to fetch model.json` | Missing `my_model/` folder or wrong filenames | Verify `my_model/model.json`, `metadata.json`, and `weights.bin` exist right next to `index.html`. |
| DroidCam not detected over Wi-Fi | College Wi-Fi blocks peer discovery | Switch to **USB connection** with Android USB Debugging enabled. |
| Solid green screen on DroidCam | Virtual driver out of sync | Quit DroidCam Client (**File → Exit**), relaunch it, and refresh Chrome. |
| Predictions feel inaccurate for another person | Dataset bias (lighting/background differences) | Retrain with samples from multiple angles, lighting setups, and people. |

---

## Author & Community

**Piyush Annigeri**
- GitHub: [@pixelcrisscross](https://github.com/pixelcrisscross)
- Role: Organizer, **GDG on Campus — Visvesvaraya Technological University (VTU), Belagavi**
- Community Org: [github.com/community-gdgvtu](https://github.com/community-gdgvtu)

Built for student builders exploring practical, privacy-first Machine Learning in the browser.

---

## Contributing

Contributions, UI improvements, and creative model remixes are welcome! Please read [CONTRIBUTING.md](./CONTRIBUTING.md) to get started.

---

## License

This project is open-source and available under the [MIT License](https://opensource.org/licenses/MIT).