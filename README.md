# 📸 PS-Telegram-Request-Screenshot

### A PowerShell script that let group members request screenshots of a shift planner via a Telegram bot — authenticated with stored passwords.

[![GitHub Stars](https://img.shields.io/github/stars/CheswickDEV/PS-Telegram-Request-Screenshot?color=00d4ff&labelColor=16161f)](https://github.com/CheswickDEV/PS-Telegram-Request-Screenshot)
[![Last Commit](https://img.shields.io/github/last-commit/CheswickDEV/PS-Telegram-Request-Screenshot?color=a855f7&labelColor=16161f)](https://github.com/CheswickDEV/PS-Telegram-Request-Screenshot/commits/main)
![Version](https://img.shields.io/badge/version-1.0-00d4ff?labelColor=16161f)
![Status](https://img.shields.io/badge/status-Archived-6c757d?labelColor=16161f)
![License](https://img.shields.io/badge/license-Unlicensed-6c757d?labelColor=16161f)
![PowerShell](https://img.shields.io/badge/PowerShell-5.1-a855f7?logo=powershell&logoColor=white&labelColor=16161f)

---

> ⚠️ **This is an archived project.** It was built for a specific use case at a previous job and is no longer actively maintained. The code is preserved here as a reference and portfolio piece.

---

## 💡 What It Did

The shift planner at work was a desktop application with no API and no remote access. Team members who needed to check their shifts while away from the office had no way to see the schedule.

This script solved that by running on the machine where the shift planner was installed. It:

1. **Listened** for incoming Telegram messages via the Bot API (polling loop)
2. **Authenticated** the user by checking their stored password
3. **Brought the shift planner window to the foreground** using Win32 API calls (`ShowWindowAsync`)
4. **Captured a screenshot** of a defined screen region using `System.Drawing`
5. **Sent the screenshot** back to the user via the Telegram Bot API

The entire flow happened within ~60 seconds of the initial request.

---

## 🔄 How It Worked

```
┌──────────────┐     ┌──────────────────────┐     ┌──────────────────┐
│  Team Member │     │  PowerShell Script    │     │  Shift Planner   │
│  on Telegram │────▶│  (running on PC)      │────▶│  (local app)     │
│              │     │                       │     │                  │
│  "Beispiel1" │     │  1. Match username    │     │  Window brought  │
│              │◀────│  2. Ask for password  │◀────│  to foreground   │
│  "mypass123" │────▶│  3. Verify password   │     │                  │
│              │     │  4. Screenshot region  │     │  Screenshot      │
│  📷 Image   │◀────│  5. Send via Bot API  │     │  captured        │
└──────────────┘     └──────────────────────┘     └──────────────────┘
```

---

## 🛠️ Tech Stack

![PowerShell](https://img.shields.io/badge/PowerShell-16161f?logo=powershell&logoColor=00d4ff)

```
PS-Telegram-Request-Screenshot/
├── screenshot-bot.ps1    # Main script (polling loop, auth, capture, send)
└── README.md
```

- **PowerShell 5.1** with `System.Drawing` for screen capture
- **Win32 API** (`user32.dll`) for window management
- **Telegram Bot API** for messaging and photo delivery
- **curl** for multipart file uploads to Telegram

---

## ⚠️ Notes

- The script used hardcoded passwords per user — this was an internal tool on a trusted network, not a production security model
- Screen coordinates for the capture region were hardcoded to match the specific shift planner window layout
- The polling loop ran indefinitely with 120-second sleep intervals between checks

---

## 📝 Changelog

### v1.0
- 🚀 Initial release
- ✨ Telegram Bot API polling loop
- ✨ Password-based user authentication
- ✨ Win32 window management and screen capture
- ✨ Automatic screenshot delivery via Telegram

---

## 📄 License

Unlicensed — provided as-is for reference.

---

<p align="center">
  <a href="https://cheswick.dev">
    <img src="https://img.shields.io/badge/CHESWICK.DEV-00d4ff?logo=firefox&logoColor=0a0a0f&labelColor=a855f7" alt="cheswick.dev" />
  </a>
</p>

<p align="center">
  Made with 🖤 by <a href="https://cheswick.dev">cheswick.dev</a>
</p>
