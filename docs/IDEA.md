# X-Access: Core Vision & Motivation

## 1. Executive Summary

**X-Access** is an open-source, ultra-low-latency remote desktop system engineered as an open, self-hosted equivalent to **Google Chrome Remote Desktop (CRD)**.

While solutions like RustDesk, AnyDesk, and VNC exist, they suffer from critical flaws when deployed on cloud VMs:
* **Over-reliance on public relays**: When direct peer-to-peer connection fails, tools like RustDesk fall back to overseas relay servers (e.g. New York), spiking latency from 20ms to 300+ ms.
* **Rigid display resolutions**: Traditional remote desktops assume fixed landscape resolutions (1920×1080). When viewed inside a compact browser window, a split-screen layout, or a vertical mobile device, the remote desktop is squashed down, rendering text unreadable.
* **Proprietary cloud lock-in**: Google Chrome Remote Desktop has exceptional streaming performance, but Google only builds host packages for `x86_64` (completely ignoring ARM64 cloud architectures) and locks users into Google's proprietary authentication.

**X-Access solves all of these problems** by providing a clean WebRTC pipeline with dynamic client-to-host resolution negotiation and zero-cost cloud deployment.

---

## 2. Core Pillars & Value Proposition

### 1. Dynamic Auto-Scaling & Custom Aspect Ratios
* **The Problem**: Opening a 1080p remote desktop inside a half-screen window (e.g. 720×640) shrinks UI elements by 50%.
* **The X-Access Solution**: The client browser observes its exact container dimensions via `ResizeObserver` and sends live resolution change requests over a WebRTC DataChannel. The host Linux machine dynamically generates and applies custom modelines on the fly (`xrandr` / virtual display driver), ensuring the remote screen matches your viewport **pixel-for-pixel with zero black borders**.

### 2. Sub-20ms Direct WebRTC Streaming
* **The Problem**: Third-party relays introduce jitter and overseas packet hops.
* **The X-Access Solution**: Direct peer-to-peer WebRTC streaming with STUN/TURN hole punching directly within your local cloud region (e.g. Mumbai). Video streams over optimized UDP using VP9 or H.264 with adaptive bitrate throttling.

### 3. Clientless Web Experience + Native Mobile / TV Apps
* **Browser First**: Open a link, authenticate, and control your computer right inside Google Chrome, Safari, Edge, or Firefox.
* **React Native Companion**: Native clients for iOS, Android, and **Android TV** (with 10-foot D-Pad remote control support).

### 4. 100% Free Self-Hosting
* Designed to run permanently on free cloud tiers:
  * **Signaling Server**: Runs on a 1 GB RAM x86 micro-VM (consuming ~20 MB RAM).
  * **Target Host**: Runs on any Linux workstation (ARM64 Ampere or x86_64).

---

## 3. Comparison with Existing Solutions

| Feature | Google Chrome Remote Desktop | RustDesk | Traditional VNC / RDP | **X-Access** |
| :--- | :--- | :--- | :--- | :--- |
| **Clientless Web Access** | ✅ Yes (in Chrome) | ⚠️ Experimental | ❌ Needs Client / Guacamole | **✅ Yes (Any Modern Browser)** |
| **Dynamic Auto-Resize** | ✅ Yes | ❌ Fixed Presets | ❌ Rigid / Reconnect needed | **✅ Yes (Arbitrary: 720×640, 1080×1280)** |
| **ARM64 Linux Host Support** | ❌ AMD64 Only | ✅ Yes | ✅ Yes | **✅ Yes (ARM64 & x86_64)** |
| **Self-Hosted Infrastructure** | ❌ Google Only | ⚠️ Requires dedicated ports | ⚠️ Complex VNC setup | **✅ 100% Self-Hosted & Lightweight** |
| **P2P Relay Latency Control** | ❌ Google Network | ⚠️ Prone to US relay hop | ❌ No P2P | **✅ Local Cloud Gateway (15–20ms)** |
| **Android TV D-Pad Support** | ❌ No | ❌ Touch-focused | ❌ Hard to navigate | **✅ Native React Native TV support** |
