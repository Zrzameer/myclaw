# 🦞 MyClaw

OpenClaw + Codex CLI on Android — ek self-contained APK me. Embedded Linux bootstrap,
pehle run pe packages install, phir WebView UI.

Package: `com.myclaw.assistant` · minSdk 24 (Android 7) · targetSdk 28 (W^X bypass, Termux jaisa)

## Build

```bash
cd myclaw
./scripts/download-bootstrap.sh aarch64   # ~30 MB Termux bootstrap
./gradlew assembleDebug                    # ya: gradle assembleDebug
```

APK: `app/build/outputs/apk/debug/app-debug.apk`

## Architecture

```
┌─────────────────────────────────────────┐
│              MyClaw APK                 │
│                                         │
│  ┌──────────────┐  ┌────────────────┐   │
│  │   WebView    │  │  Bootstrap     │   │
│  │              │  │  Installer     │   │
│  │ localhost:   │  │                │   │
│  │   18923      │  │  Extracts      │   │
│  │              │  │  Termux env    │   │
│  └──────┬───────┘  └───────┬────────┘   │
│         │                  │            │
│         ▼                  ▼            │
│  ┌──────────────────────────────────┐   │
│  │  /data/data/com.myclaw.assistant/│   │
│  │    files/usr/  (Termux prefix)   │   │
│  │    ├── bin/node                   │   │
│  │    ├── bin/codex                  │   │
│  │    └── lib/node_modules/          │   │
│  │        └── codex-web-local/       │   │
│  └──────────────────────────────────┘   │
└─────────────────────────────────────────┘
```

## First run

1. Termux bootstrap extract hota hai (~30 MB compressed, ~100 MB extracted)
2. `apt-get install nodejs-lts` (~30 MB)
3. `npm install -g @openai/codex codex-web-local`
4. OpenAI API key puchha jata hai (device pe encrypted)
5. Server start, WebView khulti hai

Steps 1-3 ek hi baar hote hain.

## Requirements

- Android 7.0+ (API 24), arm64-v8a
- ~500 MB free storage
- Internet (pehle run ke package installs ke liye)

## Build from source (CI)

`.github/workflows/build-apk.yml` — GitHub Actions bootstrap download karke
APK banata hai. Actions tab se artifact download karo.

## License & credits

Original implementation: **AnyClaw** by the OpenClaw community
(<https://github.com/OpenClawAndroid/openclaw-android-assistant>), MIT License,
Copyright (c) 2026 OpenClaw Foundation.

MyClaw is a rebranded fork of that project. Original MIT license terms apply;
see `LICENSE-ORIGINAL` for the upstream notice.
