This is a Flutter laboratory showcase that opens with a cinematic animated home screen, then branches into four desktop-style activities: a custom music player, the Grimm Runner mini-game, and two full-page chapter illustrations. The experience leans heavily on rich artwork, ambient audio, and tactile micro-interactions.

## 🎮 What’s Inside
1. **HOME** – A Material 3 landing screen with layered parallax clouds, animated grass, looping background music (`assets/opening.mp3`), and floating “Music Player” / “Grimm Runner” pills that mute the intro audio before navigation.
2. **Activity 1 – Music Player** – A playlist-driven interface that uses `just_audio` to stream local horror-soundtrack MP3s, show current track artwork, and toggle between compact now-playing and full playlist views with shuffle/skip controls.
3. **Activity 2 – Grimm Runner** – A runner-style module with persistent high scores, three handcrafted levels, animated sprites, and win/lose screens, all sourced from `lib/activity2` and the `assets/images/activity2/…` directories.
4. **Activity 3 & 4 – Chapter Images** – Fullscreen image previews (`assets/activity3.png` / `assets/activity4.png`) rendered through the reusable `FullImagePage` widget (used by `lib/pages/activity3_page.dart` and `activity4_page.dart`).

## 🧱 Repo Layout
- `lib/main.dart` – boots the MaterialApp, configures routes, and initializes Flame audio.
- `lib/pages/` – contains the home page plus each numbered activity entry point.
- `lib/widgets/` – shared UI (e.g., `FullImagePage`) and styling helpers (`styles.dart`).
- `lib/activity2/` – Grimm Runner implementation (level logic, win/lose screens, maps).
- `assets/` – imagery, music, fonts, and themed sprites declared in `pubspec.yaml`.
- `styles.dart` – centralizes colors, typography, and decorative painters used across the experience.

## ⚙️ Prerequisites
Ensure your machine meets the Flutter SDK requirements (this project targets Dart 3.5.3). Then:

```bash
flutter pub get
```

Optionally run the analyzer/linter:

```bash
flutter analyze
```

## ▶️ Running the App
1. Plug in a device or launch an emulator/simulator.
2. Start the app with:

```bash
flutter run
```

For a specific platform:

```bash
flutter run -d windows
flutter run -d chrome
```

The default route (`HomePage`) plays `assets/opening.mp3` through `flame_audio`. Use the floating mute button at the top-right if you need silence before hopping into an activity.

## 🧰 Dependencies
- `flutter` (Material & widgets)
- `flame` + `flame_audio` (intro audio initialization)
- `just_audio` / `just_audio_windows` (Activity 1 playlist)
- `google_fonts` (Playfair Display, Poppins)
- `shared_preferences` (high-score persistence for Grimm Runner)
- `vector_math` (custom animations)

## 🧭 Navigation Summary
- `/` – `HomePage`
- `/a1` – `Activity1Page` (music player)
- `/a2` – `Activity2Page` (Grimm Runner home)
- `/a3` – `Activity3Page` (Chapter 3 imagery)
- `/a4` – `Activity4Page` (Chapter 4 imagery)

## 🎧 Audio & Assets
All audio lives under `assets/music/`, `assets/audio/`, or the single-file `assets/opening.mp3`. When adding new files, update `pubspec.yaml` and keep file sizes reasonable for faster hot reloads. The music player also uses album-cover art inside `assets/album-cover/`.

## 🔧 Development Notes
- The home screen uses multiple `AnimationController`s (`_intro`, `_clouds`, `_grassWind`, `_titleGlow`, `_buttonFloat`) to choreograph its animated layers—tweaking durations in `lib/pages/home_page.dart` affects the entire scene.
- Grimm Runner persists the best score via `SharedPreferences` under the key `grimm_runner_high_score`. Clearing preferences resets the leaderboard.
- If a route fails to load (e.g., due to missing assets), `ErrorWidget.builder` in `main.dart` currently swallows the crash with an empty `SizedBox`.

## 📝 Next Steps
1. Add new tracks/images? Drop them into `assets/` and register them in `pubspec.yaml` (especially the playlist metadata in `lib/pages/activity1_page.dart`).
2. Expand Grimm Runner with extra levels in `lib/activity2/levelN_screen.dart` and corresponding spawn data.
3. Build platform-specific release binaries with `flutter build <platform>`.
