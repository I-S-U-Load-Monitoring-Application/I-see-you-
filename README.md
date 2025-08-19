# ⚡ Real‑Time Appliance Monitoring App

A Flutter mobile application for **real‑time energy usage monitoring** of appliances, powered by Firebase Realtime Database and on‑device TensorFlow Lite inference. Designed for instant feedback, sliding‑window AI analysis, and scalable integration with industrial and consumer devices.

---

## 🌟 Features

### 📡 Real‑Time Data Streaming
- **Live Firebase Listeners**: Streams the latest readings from `/raw_data` without replaying the entire history.
- **Sliding‑Window Processing**: Maintains a fixed‑size buffer (599 readings) per device for model input.
- **Zero‑Padding**: Starts inference immediately by padding empty slots until the window is full.

### 🤖 AI‑Powered Inference
- **Per‑Device Models**: Each appliance uses its own `.tflite` model from app assets.
- **Model Readiness Check**: Optional handshake via `ai_input/models/{modelKey}/status` in Firebase before loading.
- **On‑Device TensorFlow Lite**: Runs inference locally for instant results without cloud latency.
- **Latest‑Only Cache**: Displays the most recent inference result, then clears it until the next update.

### 🖥️ Device Management
- **Add/Remove Appliances**: Persisted in `/users/{uid}/devices` in Firebase.
- **Live Analysis Toggle**: Starts/stops streaming and inference per device.
- **Automatic Model Loading/Unloading**: Loads on toggle ON, unloads on toggle OFF or removal.

### 📊 Aggregation & Reporting
- **Daily Totals**: Aggregates inference results into `usagePerDay` for each device.
- **Future‑Ready Reporting**: Architecture supports pushing each inference result to Firebase for historical analytics.

---

## 🚀 Quick Start

### Prerequisites
- Flutter SDK (3.x recommended)
- Dart SDK (3.x)
- Firebase project with:
  - Realtime Database enabled
  - Authentication enabled (Email/Password or other)
- Android Studio or Xcode for device/simulator testing

### Installation
Clone the repository:
```bash
git clone https://github.com/your-org/real-time-appliance-monitoring.git
cd real-time-appliance-monitoring
Install dependencies:

bash
flutter pub get
Configure Firebase:

Add your google-services.json (Android) and/or GoogleService-Info.plist (iOS) to the project.

Update firebase_options.dart if using FlutterFire CLI.

🔧 Configuration
Firebase Database Rules
Recommended secure rules:

json
{
  "rules": {
    "users": {
      "$uid": {
        ".read": "$uid === auth.uid",
        ".write": "$uid === auth.uid"
      }
    },
    "raw_data": {
      ".read": true,
      ".write": true
    },
    "ai_input": {
      "models": {
        "$modelKey": {
          ".read": true,
          ".write": true
        }
      }
    }
  }
}
Model Readiness Flags
If using readiness checks, create in RTDB:

json
"ai_input": {
  "models": {
    "Fridge_tflite": { "status": "ready" },
    "TV_tflite": { "status": "ready" },
    "Microwave_tflite": { "status": "ready" },
    "Kettle_tflite": { "status": "ready" }
  }
}
Keys must be Firebase‑safe (no ., $, #, [, ], /).


🔌 Data Flow
Add Device → Writes to /users/{uid}/devices → UI updates via .onValue listener.

Toggle Live Analysis ON:

Loads model from assets (if ready).

Attaches .limitToLast(599) listener to /raw_data.

Seeds zero‑padded window, slides in new readings.

Runs inference on each update, updates usageCache.

UI Displays Result → Clears cache → Waits for next update.

Toggle OFF / Remove Device → Cancels listener, unloads model.

🛠️ Development
Available Scripts
bash
flutter run        # Run on connected device/emulator
flutter build apk  # Build Android APK
flutter build ios  # Build iOS app
Code Style
Follows Dart/Flutter best practices.

Provider for state management.

Clear separation of UI, service, and model logic.

📋 Requirements
Dependencies:

firebase_core

firebase_auth

firebase_database

provider

tflite_flutter

Supported Platforms: ✅ Android ✅ iOS

🆘 Troubleshooting
Model not ready: Ensure status: "ready" exists in RTDB under ai_input/models/{modelKey}.

No data streaming: Check Firebase rules and that /raw_data is receiving updates.

Output is 0: This can happen if the sliding window is still mostly zero‑padded. Once 599 real readings arrive, the model will produce meaningful results.

OOM / slow startup: Verify .limitToLast(599) is in place and listeners are cancelled when not needed.

🤝 Contributing
Fork the repository.

Create a feature branch:

bash
git checkout -b feature/amazing-feature
Commit changes:

bash
git commit -m 'Add amazing feature'
Push to branch:

bash
git push origin feature/amazing-feature
Open a Pull Request.

🙏 Acknowledgments
Built with Flutter & Firebase

TensorFlow Lite for on‑device inference
