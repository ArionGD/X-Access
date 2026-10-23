# X-Access 🚀

> **High-Performance, Self-Hosted, WebRTC Remote Desktop Platform with Dynamic Auto-Scaling & Custom Aspect Ratios.**

X-Access is an open-source, clientless remote desktop system designed to deliver the seamless, low-latency responsiveness of **Chrome Remote Desktop** while giving you 100% control over your data, signaling, and display geometry.

---

## 🌟 Key Highlights

* **Universal Clientless Access**: Connect from any modern browser (Chrome, Edge, Safari, Firefox) with zero client installations.
* **On-The-Fly Auto-Scaling & Custom Ratios**: Seamlessly adapts to non-standard resolutions like `720×640` (split-screen), `1080×1280` (vertical mobile), or native 1080p/4K without stretching or black bars.
* **Direct WebRTC P2P (Sub-20ms Latency)**: End-to-end encrypted video streaming with adaptive bitrate control and hardware-accelerated decoding.
* **Runs 100% Free**: Designed to run on zero-cost cloud tiers (like Oracle Cloud Always Free AMD x86 micro-VMs using under 50 MB RAM).
* **Multi-Platform Ecosystem**: Works on Web, Desktop, Mobile, and **Android TV** (via React Native).

---

## 📚 Documentation Index

All core architectural documents and technical specifications are located in the [`docs/`](./docs) directory:

1. [**Core Vision & Idea (`docs/IDEA.md`)**](./docs/IDEA.md): Problem statement, motivation, and comparison with Chrome Remote Desktop & RustDesk.
2. [**Technology Stack & Architecture (`docs/TECH_STACK.md`)**](./docs/TECH_STACK.md): Component breakdown (Signaling Server, Host Agent, Web & TV Clients, and Display Engine).
3. [**Implementation Plan (`docs/IMPLEMENTATION_PLAN.md`)**](./docs/IMPLEMENTATION_PLAN.md): Phase-by-phase implementation roadmap, milestone tasks, and testing guide.

---

## 🛠️ Quick Architecture Overview

```
[ Client (Browser / React Native TV) ]
            │
            ├──── 1. WebSocket Signaling (SDP / ICE) ────> [ x86 Signaling Server ] (~20 MB RAM)
            │                                                      │
            │                                                      │
            │<─── 2. Direct WebRTC Media Stream (UDP Video/Audio) ──┤ [ Host Agent (VM) ]
            │                                                      │  (X11 / PipeWire / uinput)
            ├──── 3. WebRTC DataChannel (Mouse, Keys, Resizes) ───>┤
```

---

## 📜 License
MIT License. Free for personal and commercial self-hosting.
