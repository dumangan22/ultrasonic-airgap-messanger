# 🔊 Sonic Chat - Ultrasonic Air-Gap Messenger

[![Deployment Status](https://img.shields.io/badge/Deployment-Live-success)](https://sonic.rohits.online)
[![Tech Stack](https://img.shields.io/badge/Built%20With-Next.js%2016%20%7C%20Web%20Audio%20API-blue)](https://nextjs.org)
[![PWA](https://img.shields.io/badge/PWA-Offline%20Ready-purple)](https://web.dev/progressive-web-apps/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

**Sonic Chat** is an experimental, offline-first messaging application that transmits data between devices using **high-frequency sound waves (19kHz - 19.5kHz)**.

It creates an "Air-Gapped" communication channel, allowing devices to chat without Internet, Wi-Fi, Bluetooth, or Servers. Just pure physics.

🚀 **Live Demo:** [https://sonic.rohits.online](https://sonic.rohits.online)

---

## ⚡ Key Features

- **📶 Totally Offline:** Works in Airplane mode. No internet required after initial load (PWA).
- **🔒 Air-Gapped Security:** Data travels via sound waves directly from Speaker to Microphone. No server storage.
- **📱 PWA Support:** Installable on Android, iOS, and Desktop as a native-like app.
- **🚫 Interference Protection:** Implements **CSMA** (Carrier Sense Multiple Access) to detect if the channel is busy before sending, preventing signal collisions.
- **🔊 High Frequency:** Uses near-ultrasonic frequencies (19kHz) which are barely audible to most humans but clear to microphones.

---

## 🛠️ How It Works (The Science)

This project uses the browser's **Web Audio API** for Digital Signal Processing (DSP).

### 1. The Protocol (Physical Layer)
We use a custom implementation of **FSK (Frequency Shift Keying)**:
* **19,000 Hz:** Represents Binary `0`
* **19,500 Hz:** Represents Binary `1` & Start Bit
* **Bit Rate:** ~3.3 bits per second (300ms duration per bit for reliability).

### 2. The Transmitter (Sender)
1.  Text is converted to **Binary (ASCII)**.
2.  An `OscillatorNode` generates a Sine wave.
3.  The frequency shifts between 19kHz and 19.5kHz based on the binary data.
4.  A **Start Bit** is sent first to wake up the receiver.

### 3. The Receiver (Listener)
1.  The Microphone input is fed into an `AnalyserNode`.
2.  We perform an **FFT (Fast Fourier Transform)** to visualize sound frequencies in real-time.
3.  **Signal Detection:** The app listens for a specific "Start Bit" threshold (energy at 19.5kHz).
4.  **Sampling:** Once triggered, it samples the audio spectrum every 300ms to reconstruct the binary stream ➔ Text.

---

## 💻 Tech Stack

- **Framework:** [Next.js 16](https://nextjs.org/) (App Router)
- **Audio Engine:** Native Web Audio API (`AudioContext`, `AnalyserNode`, `Oscillator`)
- **Styling:** Tailwind CSS
- **Icons:** Lucide React
- **PWA:** `@ducanh2912/next-pwa`
- **Deployment:** Vercel

---

## 📸 Screenshots

| Desktop View | Mobile View |
|:---:|:---:|
| *Floating WhatsApp-style interface* | *Full-screen immersive PWA experience* |
| ![Desktop](public/icon.png) | ![Mobile](public/icon.png) |

*(Note: Add actual screenshots to your public folder for better visual appeal)*

---

## 🚀 Getting Started Locally

Clone the project and run it on your local machine.

# 1. Clone the repository
git clone [https://github.com/rohitkumar91131/ultrasonic-airgap-messanger.git](https://github.com/rohitkumar91131/ultrasonic-airgap-messanger.git)

# 2. Navigate to directory
cd ultrasonic-airgap-messanger

# 3. Install dependencies
npm install

# 4. Run the development server
npm run dev


Open http://localhost:3000 with your browser.

Note: For microphone access to work on mobile devices during development, you must access the local server via HTTPS or localhost. Accessing via IP address (e.g., 192.168.x.x) often blocks the microphone due to browser security policies.

⚠️ Usage & Troubleshooting
Since this relies on physical sound waves, real-world factors matter:

Volume: Set your device volume to 70-80%. (Too loud causes distortion/echo).

Distance: Keep devices 10cm - 50cm apart for best results.

Permissions: You must allow Microphone access when prompted.

iOS/iPhone: Ensure the physical Silent Mode switch is OFF. iOS browsers often mute Web Audio when the phone is in silent mode.

Environment: Works best in quiet rooms. Loud background noise can interfere with the signal.

🔒 Privacy Policy
This app requires Microphone access solely to detect ultrasonic data signals in real-time.

No audio is recorded, stored, or transmitted to any server.

All processing happens Client-Side in the browser's RAM.

🤝 Contributing
Contributions are welcome! If you want to improve the encoding algorithm (maybe add Error Correction like Hamming Code?), feel free to fork and submit a PR.

Fork the Project

Create your Feature Branch (git checkout -b feature/AmazingFeature)

Commit your Changes (git commit -m 'Add some AmazingFeature')

Push to the Branch (git push origin feature/AmazingFeature)

Open a Pull Request

📄 License
Distributed under the MIT License. See LICENSE for more information.

Built with ❤️ and 🔊 by Rohit Kumar
