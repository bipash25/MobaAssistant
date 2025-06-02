# MobaAssistant

**MobaAssistant** is a cross-platform (Android & iOS) AI-driven assistant app for Mobile Legends: Bang Bang players. It delivers real-time in-game guidance, comprehensive hero analytics, and post-match insights—all while remaining lightweight to avoid any performance impact during gameplay.

---

## Table of Contents

1. [Project Overview](#project-overview)  
2. [Key Features](#key-features)  
3. [Architecture & Technology Stack](#architecture--technology-stack)  
4. [Getting Started](#getting-started)  
   - [Prerequisites](#prerequisites)  
   - [Installation](#installation)  
   - [Running Locally](#running-locally)  
5. [Usage](#usage)  
6. [Performance & Optimization](#performance--optimization)  
7. [Roadmap](#roadmap)  
8. [Contributing](#contributing)  
9. [License](#license)  
10. [Contact](#contact)  

---

## Project Overview

MobaAssistant is designed to act as a **personal assistant** for MLBB players: no social feeds, no chats—just pure, data-driven guidance. Its primary objectives are:

- **Real-time In-Game Support:** Overlay-based AI recommendations for drafts, item builds, cooldown tracking, and situational alerts without lagging the game.
- **Comprehensive Hero Database:** Dynamic hero stats, skill combinations, pro builds, and counter-pick suggestions—updated automatically after every patch.
- **Post-Match Analytics & Coaching:** Detailed performance breakdowns, mistake highlights, and personalized drills to accelerate player improvement.
- **Lightweight & Efficient:** Engineered to use minimal memory/CPU/GPU so players can run MobaAssistant alongside MLBB on a single device without performance degradation.

---

## Key Features

### 1. Hero Guides
- **Detailed Hero Profiles:** Stats, abilities, recommended build paths (items, emblems, spells).  
- **Tier Lists & Meta Trends:** AI-generated rankings that adjust after each patch.  
- **Pro Builds & Strategies:** Aggregated from top tournament data; updated automatically.  
- **Counter-Pick & Synergy Analysis:** Suggests which heroes to pick/ban and which teammates to pair with.

### 2. Real-Time Assistant
- **Draft Helper:** AI-driven counter-pick suggestions and role allocation during hero selection.  
- **In-Game Overlay:**  
  - Track enemy cooldowns (ulimates, core skills).  
  - “Fight or Flee” recommendations based on health, mana, and nearby allies/enemies.  
  - Gold difference & XP gain tracking with efficiency tips.  
  - Mini-map heatmap indicating likely enemy rotations.  

### 3. Match Analysis
- **Post-Game Breakdown:** Damage dealt, damage taken, kill participation, gold/xp graphs.  
- **Role Efficiency Metrics:** Farming efficiency, rotation efficiency, objective participation.  
- **Accuracy & Mistake Detection:** Automatic identification of overextension, poor vision, and positioning errors.  
- **Personalized Improvement Suggestions:** AI-driven coaching drills (last-hitting, map awareness, etc.).

### 4. Interactive Calculators & Simulators
- **Skill Calculator (AI):** Simulate emblem/skill build effects on hero stats.  
- **Damage Calculator (AI):** Run realistic “hero vs. hero” matchups with chosen items.  
- **Draft Simulator (AI):** Practice drafting scenarios against AI-modeled opponents and test synergy lines.

### 5. AI Coach & Training Modules
- **Adaptive Hero Suggestions:** Based on play style, recent performance, and meta shifts.  
- **Last-Hitting Trainer:** Interactive farm simulations to optimize CS accuracy.  
- **CC Chain Calculator:** Identify ideal crowd-control sequences for team comps.  
- **Power Spike Notifications:** Alerts when a hero reaches critical power thresholds.

### 6. Buff/Objective Tracker & Timers
- **Jungle Buff Timers:** Blue, Red, and Neutral objective timers with dynamic reminders.  
- **Lord/Turtle Notifications:** Optimal contest/rotation recommendations based on team strength.

### 7. Patch Notes & Changelog Integration
- **Automatic Patch Fetcher:** Web scraping + NLP that pulls official MLBB patch notes.  
- **Dynamic Meta Impact Analysis:** Highlights hero/item buffs, nerfs, and balance changes.  
- **One-Tap Update:** Fetch → Parse → Retrain AI Models → Update in-App Data.

### 8. Real-Time Adjustments & Alerts
- **Role Synergy Analysis:** Suggests complementary heroes and lane assignments on the fly.  
- **Lane Matchup Suggestions:** Real-time lane assignments based on enemy picks.  
- **Gold & XP Efficiency Tracking:** Alerts when behind/on pace; suggests farming routes or rotations.  
- **Team Fight Analyzer:** Real-time breakdown of ongoing skirmishes and win-probability shifts.  
- **Pattern Recognition for Enemy Behavior:** Predicts enemy ganks based on historical data.

### 9. Replay Analysis Tools
- **Deep Replay Parsing:** Highlighting ward placements, gank patterns, and rotation inefficiencies.  
- **Team Fight Recap:** Visual timeline of ability usage, positioning, and outcome analysis.

### 10. Meta Builds & Emblem Recommendations (AI)
- **Auto-Generated Builds:** Based on win rates, pick rates, and synergy trends.  
- **Emblem Set Suggestions:** Tailored by hero role, patch data, and play style.

### 11. Future Enhancements
- **AR Integration (Optional):**  
  - Augmented overlays showing skill range, attack radius, and enemy threat zones in real-time.  
- **Voice Assistant (Optional):**  
  - Voice prompts for real-time decision-making (e.g., “Enemy ultimate ready, retreat!”).  
- **Custom Hero Tutorial Uploads:**  
  - Allow users to upload their own videos/text tutorials; AI will index and surface relevant segments.

---

## Architecture & Technology Stack

### 1. Frontend (Mobile App)
- **Framework:**  
  - **Flutter (Dart)** OR **React Native (TypeScript)**  
    - Single codebase for Android & iOS.  
    - Native module integration for performance-sensitive features (overlays, screen capture).
- **UI/UX:**  
  - Modern, minimalistic design with vector icons/data overlays for minimal GPU load.  
  - **Dark Mode & Light Mode** support.  
  - Customizable dashboard—users pick which modules to prioritize.

### 2. AI/ML
- **On-Device Inference:**  
  - **TensorFlow Lite** / **ONNX Runtime Mobile** (quantized models) for fast, low-memory inference.  
  - Pre-trained models for:  
    - Patch note NLP (summarization/extraction).  
    - Real-time object detection (health bars, cooldown icons).  
    - Predictive analytics (win rate, power spike identification).
- **Cloud-Based Processing (Optional):**  
  - **Google Cloud Functions / AWS Lambda / Azure Functions** for heavy tasks like:  
    - Bulk replay analysis.  
    - Full AI retraining after major patch release.  
  - **FastAPI (Python)** or **Express/Node.js** as AI-backend microservices.

### 3. Data & Storage
- **Local Storage:**  
  - **SQLite** or **Realm** for user preferences, cached patch data, and lightweight hero stats.  
  - **Secure Encrypted Storage** for sensitive tokens/credentials (if any).
- **Remote Storage (Optional):**  
  - **Firebase Realtime Database / Firestore** or **MongoDB Atlas** for:  
    - Centralized patch note archive.  
    - Aggregated pro build data.  
    - User-submitted replays/tutorials (if extending to that feature in future).
- **Caching Strategy:**  
  - In-memory caching of critical data (e.g., current match state).  
  - Disk caching with LRU eviction for older patch data, hero images, and overlays.

### 4. Screen Capture & Overlay
- **Android:**  
  - **MediaProjection API** + **SurfaceView** for capturing game frames selectively.  
  - **Overlay Windows** (SYSTEM_ALERT_WINDOW permission) for drawing transparent UI on top of MLBB.
- **iOS:**  
  - **ReplayKit** or **Screen Recording APIs** for live capture.  
  - **MetalKit** or **SceneKit** for minimal-overhead overlay rendering.

### 5. CI/CD & DevOps
- **Version Control:** GitHub (branching strategy: `main`, `develop`, `feature/*`).  
- **Continuous Integration:**  
  - **GitHub Actions** or **Bitrise** for automated build/test on Android & iOS simulators.  
  - Automated linting (Dart analyzer or ESLint) and unit/UI tests.
- **Continuous Deployment (Beta):**  
  - **Firebase App Distribution** or **TestFlight** for over-the-air beta releases.  
  - **Google Play Internal Testing Track** for Android.
- **Release Pipeline:**  
  1. Merge `feature/*` → `develop`.  
  2. Run automated tests, linting, and static analysis.  
  3. Manual QA on nightly builds (internal testers).  
  4. Merge `develop` → `main` for production-ready builds.  
  5. Publish to App Store & Play Store.

---

## Getting Started

### Prerequisites
1. **Flutter SDK** (v2.0+) OR **React Native CLI** (v0.65+).  
2. **Android Studio** (with Android SDKs & emulators) & **Xcode** (for iOS).  
3. **Node.js** (v14+) & **npm/yarn** (if using React Native).  
4. **Python 3.8+** (for AI backend microservices with FastAPI).  
5. **TF Lite Converter** (for quantizing AI models).  
6. **Git** for version control.  

---

### Installation

#### 1. Clone Repository
```bash
git clone https://github.com/your-username/MobaAssistant.git
cd MobaAssistant
````

#### 2. Frontend Setup

* **Flutter**

  ```bash
  cd mobile_app
  flutter pub get
  ```
* **React Native**

  ```bash
  cd mobile_app
  yarn install        # or npm install
  cd ios && pod install && cd ..
  ```

#### 3. AI Backend Setup (Optional)

Inside the `ai_backend` folder:

```bash
cd ai_backend
python3 -m venv venv
source venv/bin/activate   # macOS/Linux
venv\Scripts\activate      # Windows

pip install -r requirements.txt
```

* **Environment Variables** (create a `.env` file):

  ```
  OPENAI_API_KEY=your_openai_api_key
  FIREBASE_API_KEY=your_firebase_key
  MONGODB_URI=your_mongodb_connection_string
  ```

#### 4. Model Preparation

1. Place your pre-trained models (e.g., `.tflite` or `.onnx`) inside `ai_backend/models/`.
2. If you need to quantize:

   ```bash
   python quantize_model.py --input_model path/to/float_model.tflite --output_model path/to/quantized_model.tflite
   ```

---

### Running Locally

#### 1. Start AI Backend (if applicable)

```bash
cd ai_backend
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

#### 2. Launch Mobile App

* **Flutter**

  ```bash
  cd mobile_app
  flutter run   # specify device/emulator if needed
  ```
* **React Native**

  ```bash
  cd mobile_app
  # Android
  npx react-native run-android

  # iOS
  npx react-native run-ios
  ```

---

## Usage

1. **Initial Setup:**

   * On first launch, grant screen-capture and overlay permissions.
   * Log in (optional) or use app in guest mode for core features.
   * Choose preferred heroes/roles to seed personalized recommendations.

2. **In-Game Mode:**

   * Tap **“Activate Real-Time Assistant”** to start screen capture & overlay.
   * During hero draft, view AI suggestions for counter-picks and lane assignments.
   * While playing, real-time alerts will show cooldowns, gold difference, and “Fight or Flee” signals.

3. **Post-Match Mode:**

   * Analyze your last match: detailed performance metrics, mistakes, and drill recommendations.
   * Export match report (PDF/Shareable link) or save locally.

4. **Patch Updates:**

   * Press the **“Fetch Latest Patch”** button in the main menu.
   * The app will automatically scrape official patch notes, parse changes, and update hero/build meta.
   * Once complete, AI models retrain (if necessary) and new data is ready for in-app use.

---

## Performance & Optimization

* **Quantized AI Models:** Significantly reduced model size (by \~75%) and inference latency.
* **Selective Screen Processing:** Only critical regions (mini-map, health bars) are captured at 5–10 FPS for real-time analysis.
* **Lightweight Overlays:** Vector graphics for minimal GPU/CPU usage.
* **Lazy Loading:** Load modules (e.g., replay analysis) only when invoked.
* **Resource Toggles:** Users can disable real-time features if they detect any performance impact.
* **Continuous Testing:** Automated profiling on low-end devices (2 GB RAM, mid-tier CPU) to ensure < 10% CPU usage overhead.

---

## Roadmap

### Phase 1: MVP

* Hero Guides & Tier Lists (static data).
* Basic Real-Time Assistant (cooldown tracking, “Fight or Flee”).
* Post-Match Match Analysis (damage, gold graphs).
* Patch Note Fetcher + NLP Summarization.

### Phase 2: Advanced AI Tools

* Skill & Damage Calculators (AI-driven).
* Draft Simulator with role synergy suggestions.
* Mistake Detection & In-Game Alert System.
* Power Spike & Gold Efficiency Trackers.

### Phase 3: Pro-Level Analytics

* Replay Analysis & Team Fight Analyzer.
* Detailed Role Efficiency Reports.
* Meta Trend Visualizations (win/pick rates over time).

### Phase 4: Future Enhancements

* **AR Overlays:** Skill range visualization and danger zone holograms.
* **Voice Assistant:** Real-time voice cues (“Enemy ultimate ready, retreat!”).
* **User-Uploaded Tutorials:** AI indexing of user content for on-demand navigation.
* **Cloud Training Service:**  Automated AI retraining pipeline after every major patch.

---

## Contributing

We welcome contributions! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch**

   ```bash
   git checkout -b feature/YourFeatureName
   ```
3. **Commit your changes**

   ```bash
   git commit -m "Add YourFeatureName"
   ```
4. **Push to your fork**

   ```bash
   git push origin feature/YourFeatureName
   ```
5. **Open a Pull Request** against `develop` branch.

**Guidelines:**

* Follow existing code style (Dart/TypeScript lint rules).
* Write unit tests for any new logic (AI modules, UI components).
* Document new features in this README and in-code comments.

---

## License

This project is licensed under the **MIT License**. See [LICENSE](LICENSE) for details.

---

## Contact

* **Project Maintainer:** Your Name
* **Email:** [your.email@example.com](mailto:your.email@example.com)
* **GitHub Issues:** [Submit issues and feature requests](https://github.com/your-username/MobaAssistant/issues)

Thank you for checking out **MobaAssistant**! Let’s empower every MLBB player to achieve pro-level gameplay with minimal overhead.
