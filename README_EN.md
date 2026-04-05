<div align="center">

# PhoneClaw

**Your phone. Your AI. Entirely on-device.**

[中文](README.md) · [Report an Issue](https://github.com/kellyvv/phoneclaw/issues) · [Request a Feature](https://github.com/kellyvv/phoneclaw/issues)

</div>

---

PhoneClaw is a local AI assistant that runs entirely on your iPhone. No internet connection. No data uploads. No cloud dependency — all inference happens on-device.

Say one sentence, and it can schedule a meeting, save a contact, and set a reminder — all at once, silently, with no confirmation dialogs.

## What It Can Do

### 🗓️ Calendar · Reminders · Contacts

One sentence. Three things done:

> "Tomorrow at 2pm, meet with Alex from Bytedance at Hightech Park. His number is 138xxxx. Also remind me tonight at 8 to send the architecture doc."

PhoneClaw breaks it down and executes — a calendar event is created, a contact is saved silently, and a reminder fires at exactly 8pm.

### 📋 Clipboard · Device Info · Text Tools

Read or write the clipboard, query your device specs, run text transformations — without leaving the app.

### 🖼️ Image Understanding

Take a photo or choose one from your library, then ask questions about it.

### 🧩 Custom Skills

Define new capabilities using a single Markdown file. No code changes. Hot-reload inside the app.

---

## Privacy Guarantee

| | PhoneClaw | Cloud AI |
|--|--|--|
| Network requests | ❌ Never | ✅ Every message |
| Data uploads | ❌ Never | ✅ Always |
| Works offline | ✅ Fully | ❌ No |
| Your data belongs to | You | The vendor |

---

## Getting Started

### Requirements

- iPhone with Apple Silicon (A16 or later; E4B model requires A17 Pro)
- Xcode 16+, iOS 17.0+
- CocoaPods: `gem install cocoapods`

### Step 1 — Download a Model

Place the model under the `Models/` folder in the project root. **You only need one** — place what you want to use.

**Recommended · E2B (~1.5 GB, works on all A16+ devices)**
```
Models/
└── gemma-4-e2b-it-4bit/     ← Download mlx-community/gemma-4-2b-it-4bit from Hugging Face
```

**Advanced · E4B (~3 GB, requires iPhone 15 Pro or later)**
```
Models/
└── gemma-4-e4b-it-4bit/     ← Download mlx-community/gemma-4-4b-it-4bit from Hugging Face
```

> `Models/` is gitignored. Model files are never committed to the repository.

### Step 2 — Install & Open

```bash
pod install
open PhoneClaw.xcworkspace
```

> ⚠️ Always open `.xcworkspace`, not `.xcodeproj`

### Step 3 — Sign & Run

1. In Xcode: select the **PhoneClaw** target → **Signing & Capabilities**
2. Set your **Team** (Apple ID)
3. Change the **Bundle Identifier** (e.g. `com.yourname.phoneclaw`)
4. Connect your iPhone via USB and press **⌘R**

On first install, trust the certificate on your iPhone:  
**Settings → General → VPN & Device Management → Trust**

---

## Built-in Skills

| Skill | Description |
|-------|-------------|
| 📅 Calendar | Create calendar events with title, time, and location |
| ⏰ Reminders | Create reminders with push notifications at the due time |
| 👤 Contacts | Create or update contacts, deduped by phone number |
| 📋 Clipboard | Read and write the system clipboard |
| 📱 Device Info | Query device name, OS version, memory, and more |
| 🔤 Text Tools | Hash calculation, text reversal, and more |

---

## Adding Custom Skills

Create a `SKILL.md` file in the app's data directory and hot-reload in-app:

```
ApplicationSupport/PhoneClaw/skills/<skill-name>/SKILL.md
```

```yaml
---
name: My Skill
description: 'What this skill does'
version: "1.0.0"
icon: star
disabled: false

triggers:
  - keyword

allowed-tools:
  - my-tool-name
---

# Instructions

Tell the AI when and how to use this skill and its tools.
```

To call native iOS APIs, register your tool in `Skills/ToolRegistry.swift`.

---

## License

MIT — free to use, modify, and distribute.
