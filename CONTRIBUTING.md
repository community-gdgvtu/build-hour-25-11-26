# Contributing to Focus Guard AI

Thank you for your interest in contributing to **Focus Guard AI**! This project was created for beginners and student developers at **GDG on Campus — VTU Belagavi** to learn transfer learning, TensorFlow.js, and static web deployment. Whether it is your very first Pull Request or your hundredth, you are welcome here.

---

## Ways to Contribute

You do not need to be an ML expert to make a meaningful contribution:

- **UI/UX Enhancements:** Improve responsiveness, animations, accessibility, or add light/dark theme toggles.
- **Focus Features:** Add Pomodoro intervals, session summary exports, custom alert sounds, or focus streak milestones.
- **New Starter Templates / Remixes:** Add optional modes (e.g., *Posture Guardian*, *Rock-Paper-Scissors*, or *Sign Language Translator*).
- **Documentation & Guides:** Improve troubleshooting tips for Windows/Linux lab PCs, DroidCam setup notes, or beginner explanations.
- **Bug Fixes:** Report or fix browser compatibility, mobile camera orientation, or audio autoplay issues.

---

## Getting Started

1. **Fork** the repository on GitHub.
2. **Clone** your fork locally:
   ```bash
   git clone [https://github.com/](https://github.com/)<your-username>/focus-guard.git
   cd focus-guard
   ```
3. **Create a new branch** with a descriptive name:
   ```bash
   git checkout -b feat/pomodoro-timer
   ```
4. **Run locally** using a local HTTP server:
   ```bash
   python3 -m http.server 8000
   ```
   Open `http://localhost:8000` in Chrome to test your changes.
5. **Commit your changes** with clear, concise commit messages:
   ```bash
   git add .
   git commit -m "feat: add 25-minute Pomodoro focus mode"
   ```
6. **Push your branch** and open a **Pull Request** against `main`:
   ```bash
   git push origin feat/pomodoro-timer
   ```

---

## Project Guidelines

To keep this repository clean and beginner-friendly for Build Hour workshops:

1. **Keep It Zero-Build:** Prefer vanilla HTML, CSS, and JavaScript so students can run the project immediately without installing Node modules or configuring bundlers.
2. **Preserve 100% On-Device Privacy:** Never send webcam frames, images, or user data to any external backend server or third-party analytics tool.
3. **Keep the Repository Lightweight:**
   - Do **not** commit `.zip` archives (such as `tm-my-image-model.zip`) or raw training image folders.
   - Only replace `my_model/` if your PR intentionally improves the baseline model and clearly documents the new class labels.
4. **Test on Mobile & Desktop:** Verify that the layout and camera canvas work smoothly on both desktop screens and narrow mobile viewports.

---

## Pull Request Checklist

Before submitting your PR, please check that:

- [ ] Your code runs cleanly on `http://localhost:8000` with zero console errors.
- [ ] No unnecessary files (`.zip`, `.DS_Store`, temporary assets) are included.
- [ ] Screenshots or a short screen recording are attached for UI changes.
- [ ] `README.md` is updated if you changed setup steps or model class names.

---

## Beginner-Friendly Feature Ideas

Looking for a first issue to pick up? Try building one of these:

- **Pomodoro Mode:** Auto-switch between 25-minute focus sprints and 5-minute breaks.
- **Session Report Card:** Show a shareable end-of-session card with Focus Score %, Focus Time, and user name.
- **Confidence Threshold Slider:** Let users adjust detection strictness (`60%`–`95%`) right in the UI.
- **Camera Switcher:** Allow toggling between front and rear cameras when running on smartphones.

---

## Code of Conduct

Be welcoming, constructive, and respectful in all issues, discussions, and pull requests. This project follows the spirit of the **Google Developer Groups Community Guidelines**—every contributor should feel encouraged to learn and build together.