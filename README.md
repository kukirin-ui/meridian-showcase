<div align="center">

# Meridian Family

**An offline-first suite of Android apps with local AI, developed entirely on a phone.**

![Android](https://img.shields.io/badge/Android-3DDC84?style=for-the-badge&logo=android&logoColor=white)
![Termux](https://img.shields.io/badge/Termux-000000?style=for-the-badge&logo=gnubash&logoColor=white)
![llama.cpp](https://img.shields.io/badge/llama.cpp-Vulkan-AC162C?style=for-the-badge&logo=vulkan&logoColor=white)
![Offline-first](https://img.shields.io/badge/offline--first-local_AI-4B32C3?style=for-the-badge)

[Architecture](docs/ARCHITECTURE.md) · [Benchmarks](docs/BENCHMARKS.md)

</div>

---

No PC, no laptop. Everything here was designed, built, patched, signed and tested on an Android phone (Galaxy S26, Exynos 2600 / Xclipse 960) using Termux.

This repository documents the project and what it achieved. The apps themselves are not published here; they are available on request.

## Video

Real screen recording on a Galaxy S26, 143 s, no edits. It shows Meridian Core (helper and family link), Meridian Gaming (live sensors and clocks, network speed test, task killer, heat stop, part of tuning) and Parallel: Build options, Plan (writes the steps, Run creates them), and a Console linked to Termux that turns a wrong command into a suggested fix, with the option to ask a local model or an online model through your own API key. Built in Kotlin and C++.

Watch it on X: https://x.com/termuxSolutions/status/2116310251070714073

## What I accomplished

### Five apps that work as one system
- Built a family of five Android apps (Core, Chat, Parallel, Gaming, NullCloud) that share one signing key, connect to each other and to Termux, and still work on their own.
- Kept the whole system **offline-first**: models run on the phone, and online providers are optional and only used with the user's own key.

### Root-free system access (Meridian Core)
- Built an elevation service that connects to the phone's own adb daemon, launches a shell-level helper on loopback, and lets the other apps run privileged actions through a bound service.
- Made it **survive Wi-Fi off and app restarts**: the helper runs in its own session, Core re-attaches to it with a one-time token, and it can use local `adb tcpip` instead of Wireless debugging.
- Debugged and fixed a hang where the helper started but Core never got the "finished" signal, by reading the launch output for a marker and saving the helper's address before launch.

### Local AI on the phone (Meridian Chat)
- Runs **Qwen3.5-4B with vision** through `llama-server` in Termux, on the GPU via Vulkan.
- Split the work between two roles: the local model talks to the user, and an optional online agent turns a large skill tree into short "how to do it" recipes in a shared library.
- Added a skill and recipe library, web search with citations, attachments, and Termux command blocks that run from the chat.

### Measured performance, not guesses
- **313 tokens/sec** prompt processing and **28.9 tokens/sec** generation (Llama 3.2 3B, GPU only).
- **232 / 23 tokens/sec** on Qwen3 4B.
- Found that **skin temperature at 45 °C** is what throttles the GPU on this phone, and that flash attention is slower on this GPU. Details in [docs/BENCHMARKS.md](docs/BENCHMARKS.md).

### Root-free monitoring
- Wrote a live terminal monitor that shows CPU and GPU clocks, GPU load, RAM, chip/GPU/battery/skin temperatures and power draw, using only local adb.
- Learned which sources are live and which are cached on Samsung phones, and which sensors adb is allowed to read.

### Patching and debugging my own apps
- Patched and rebuilt my own APKs with apktool and smali, injected changed dex files into signed builds, and verified every build by decompiling it and diffing against the previous version.

## How it fits together

See [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md).

## Author

Alen Požun · [XDA: termuxSolutions](https://xdaforums.com/m/termuxsolutions.13482532/) · [X: @termuxSolutions](https://x.com/termuxSolutions)
