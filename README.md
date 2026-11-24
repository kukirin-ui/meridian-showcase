<div align="center">

# MERIDIAN FAMILY
### Five Android apps. One mind. Built from a phone.
**An offline-first, model-agnostic Android environment for local AI, Termux engineering, device operations and shared knowledge that learns from its own verified work.**

[![Android 11+](https://img.shields.io/badge/Android-11%2B-3DDC84?style=for-the-badge&logo=android&logoColor=white)](https://www.android.com/) [![Termux](https://img.shields.io/badge/Termux-native-111111?style=for-the-badge&logo=gnubash&logoColor=white)](https://termux.dev/) [![Local AI](https://img.shields.io/badge/AI-local_first-6046D8?style=for-the-badge)](https://github.com/kukirin-ui/meridian-releases) [![Current](https://img.shields.io/badge/release-3.0.00-blue?style=for-the-badge)](https://github.com/kukirin-ui/meridian-releases/releases/latest)

[Get the apps](https://github.com/kukirin-ui/meridian-releases) · [Website](https://kukirin-ui.github.io/meridian-site/) · [Architecture](docs/ARCHITECTURE.md) · [Complete feature catalog](docs/FEATURE-CATALOG.md) · [Benchmarks](docs/BENCHMARKS.md) · [Install & release](docs/INSTALL-AND-RELEASE.md)
</div>

---

## Inside the apps — real interface captures

These are captures from the published Meridian interface (2.6 series), not concept mockups; 3.0.00 screens add to them. Open an image to inspect it at full size.

| Meridian Chat | Meridian Core |
|---|---|
| ![Chat home](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/chat-home.webp) | ![Core connected](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/core-connected.webp) |
| [Chat home](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/chat-home.webp) · [Model and tools](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/chat-menu.webp) · [Device controls](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/chat-tweaks.webp) | [Core connected](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/core-connected.webp) · [Wireless debugging](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/core-wireless.webp) · [Pairing](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/core-pair.webp) · [Paired](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/core-paired.webp) · [Shell bridge](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/core-code.webp) |

| Meridian Gaming | Meridian Parallel |
|---|---|
| ![Gaming dashboard](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/gaming-dashboard.webp) | ![Parallel findings](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/parallel-findings.webp) |
| [Dashboard](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/gaming-dashboard.webp) · [Advanced tuning](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/gaming-advanced.webp) · [Task isolation](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/gaming-isolate.webp) | [Findings](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/parallel-findings.webp) · [Diagnose input](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/parallel-paste.webp) · [Fix workflow](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/parallel-fix.webp) · [Pattern match](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/parallel-pattern.webp) · [Verified result](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/parallel-verified.webp) |

| NullCloud |
|---|
| ![NullCloud source reading](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/nullcloud-source.webp) |
| [Source](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/nullcloud-source.webp) · [Summary](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/nullcloud-summary.webp) · [Extracted facts](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/nullcloud-facts.webp) · [Ask source](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/nullcloud-ask.webp) · [Presets](https://raw.githubusercontent.com/kukirin-ui/meridian-site/main/img/explore/nullcloud-presets.webp) |

[Open the full website](https://kukirin-ui.github.io/meridian-site/) for the complete gallery and product walkthroughs.

---

## The idea

Meridian is not one oversized chatbot with five tabs. It is a family of five standalone Android applications, each with a defined responsibility. They can run independently; when installed together, they communicate through Core and typed contracts, and Core is their shared mind: one memory, trust that only evidence raises, and the one process that always runs, opening each app when there is work for it.

## New in 3.0.00

- **Core is the family's mind:** one library and memory in one database, ranked by what really worked on this phone, with every trust change on the Trust Ledger.
- **Every app's verified work is shared:** commands that ran, files that passed their check, fixes the Sandbox proved and programs whose tests passed are kept in Core, and every model gets the closest verified work as an example before it answers.
- **Core opens the apps for their work** and closes them again: only Core and the app on screen use memory.
- **Any model can have a program built:** Parallel writes it with its tests, proves it in the Sandbox and saves it in Termux.
- **14 LoRA adapters made only for Qwen3.5-4B**, **Teacher mode**, **Me mode**, **tools for local models**, **Model Lab**, **Forge**, **Recipe Compiler**, **Repro Lab**, **NullCloud Studio**, **Smart gaming**, **Theme Studio**, the **Caretaker**, the **internet switch** and **Core · Translator**.

The complete list: [3.0.00 release notes](https://github.com/kukirin-ui/meridian-releases/releases/tag/v3.0.00) · [feature catalog](docs/FEATURE-CATALOG.md).

| App | Responsibility |
|---|---|
| **Meridian Core** | The family's mind: shared memory, the Trust Ledger, verified work, app wake-up, device bridge |
| **Meridian Chat** | Local/online models, job adapters, Me mode, Teacher mode, Model Lab, projects and knowledge |
| **Meridian Gaming** | Device telemetry, Smart gaming, performance tools, game profiles and benchmarks |
| **Meridian Parallel** | Termux workstation, Forge, programs on request for the family, diagnosis and the Sandbox |
| **NullCloud** | Reading links, PDFs and text, and Studio: learn, scrape and write from sources |

**Architectural rule:** each capability has an owner. Other apps request it or display its shared state; they should not grow competing copies of the same subsystem.

## Built on a phone

The documented development and release workflow was carried out on an Android phone using Termux and GitHub Actions: design, source changes, assembly, build, local signing and release. The reference device used for published benchmark notes is a Samsung Galaxy S26 (Exynos 2600 / Xclipse 960). Those measurements are device-specific, not universal Android claims.

## The five apps

### 01 — Meridian Core · the hub

Core coordinates the family and owns shared services and durable knowledge.
- Android Wireless debugging pairing and reconnect flow.
- ADB shell-user helper launched with app_process, bound to loopback and protected by a one-time token.
- Bound-service bridge through which family apps request supported elevated operations.
- Shared content provider, preferences, app check-ins, targeted command/result channels and family event log.
- Typed, owner-scoped data ports generated from one topology definition and checked in CI.
- Shared work/progress records for model calls, Termux jobs and app operations.
- Core-owned card/lesson/library storage and deterministic model-free retrieval.
- ICM intent/context/method indexing; distinct successful solutions remain distinct.
- Setup, activity, settings, update, About and support/report surfaces.
- **3.0.00:** the Mind (one library and memory, Learning Kernel, Trust Ledger, episodes of verified work), a read-only shared mirror for every app, Wake (opens apps for their work and closes them again), the Caretaker, Constitution, Proof Engine, Survival Mode, the Reasoner, Theme Studio, the internet master switch and Core · Translator.

**Privilege boundary:** this is Android shell-user access through the debugging interface, not root. Android can disable Wireless debugging after reboot; the user must reconnect.

### 02 — Meridian Chat · models and knowledge

- Local GGUF model discovery, import, optional downloads and per-model configuration.
- llama.cpp / llama-server connection through an OpenAI-compatible local API.
- CPU, Vulkan GPU and mixed execution settings; threads, CPU affinity, context, GPU layers, batch, micro-batch, max reply, Flash Attention and KV-cache options.
- Model fit estimates, load/unload and speed-test controls.
- Optional model mesh and distinct Fixer / Helper / Judge seats.
- Optional online BYOK providers: Groq, Gemini, OpenRouter, Mistral, Cerebras, NVIDIA NIM, OpenAI, Grok/xAI, Anthropic and custom endpoints.
- Separate online seats, user-provided model IDs and API keys, step/cost controls, explicit online toggle and optional VPN requirement.
- Projects, conversations, memory, custom instructions, tone, reusable prompts and attachments.
- Termux file access and command handoff when connected.
- Skill trees, skill cards, lessons, recipes, shared knowledge library and web search with citations.
- **3.0.00:** 14 LoRA adapters made only for Qwen3.5-4B; Me mode; Teacher mode; builds through Parallel; Meridian's tools for models measured as reliable; Model Lab and the Store; Tweaks with llama.cpp built from source, Vulkan drivers and presets; Storage; Croatian through Core's Translator; Chat holds the family's API keys.

Online use is opt-in and uses the user's own provider key. Local model use does not require an online account.

### 03 — Meridian Gaming · device operations

- Home dashboard for battery, memory, CPU and activity summaries.
- Hardware/system views, live readings and shareable hardware reports.
- Battery, security/network-posture and device-care surfaces.
- Game detection, per-game profiles, optional auto-add and watch mode.
- Task isolation/task killer with keep-lists for Google Play services and optional Samsung/Google extras.
- Heat-stop controls and advanced CPU/GPU/device tuning surfaces.
- Local-model benchmark runner: CPU, GPU/Vulkan and mixed backend; GPU layers, threads, CPU affinity, Flash Attention, KV cache, prompt/generation lengths, batch, micro-batch, repeats, history and result verification.
- Core, Termux and permission setup guidance.
- **3.0.00:** Smart gaming: per-game posture, Sweet Spot Finder, the chip's efficiency fingerprint, Throttle Forecast, a frame-time recorder and an exact restore.

Device operations depend on Android version, manufacturer firmware and granted permissions. A visible control is not a guarantee that every phone exposes that operation.

### 04 — Meridian Parallel · the Termux workbench

- Termux setup, connection check, console, command execution and session controls.
- File browser for Home, Downloads, Shared, DCIM, Models, Projects, Notes, Logs, Bin and Meridian paths.
- Create projects/files/folders; navigate and inspect files; operations follow Android/Termux permissions.
- Searchable plans and command recipes across phone, Termux, AI, servers, developer tools, languages/builds, files/media and system operations.
- Build recipes and language/tool support for JavaScript/Node.js, Rust, Go, Ruby, PHP, Lua, Java, C/C++ and shell/JSON utilities.
- Package tools, compilers, CMake, Make, Git, Docker CLI, Vim, Neovim, Micro, ripgrep, jq, tree, unzip, rsync, curl and wget.
- Python jobs, Node services, local model/llama-server, GPU compute, SSH/remote shell and Debian/Ubuntu through proot-distro.
- User-defined scheduler; online providers come through Chat, which holds the keys for the family.
- Meridian Doctor categories for network, storage, memory, heat, battery, Termux, packages, local model, Core and permissions.
- Diagnose from pasted errors or the last failed command; evidence-oriented fix recipes.
- Debugger with file/source discovery.
- Multi-file CodeGen with file contracts, path/extension/budget checks, Sandbox tests and bounded repair workflow.
- Sandbox audit records and explicit test outcomes.
- **3.0.00:** Forge (from an idea to a proven product), programs on request from any app and any model, the Recipe Compiler and the Repro Lab; every proven fix and part is kept in Core as verified work.

Sandbox is a controlled test workflow, not a hardened hostile-code jail or a guarantee of filesystem/network isolation.

### 05 — NullCloud · reading and research

- Read web pages/links, PDFs and pasted text.
- Summaries, bullets, key points, explanations, knowledge/fact extraction, recipes, how-to steps, claim checks, simplification and translation.
- Ask follow-up questions about the source.
- Local reading library.
- Reuse Chat's configured model or use a standalone model path with GGUF selection, threads, GPU layers and context.
- **3.0.00:** Studio (learn a topic into Core's library, scrape a site with robots.txt respected, write from sources only); only the public web is read, checked on every redirect; no size caps.

## The shared foundation

### Core-owned knowledge
Core is the authority for durable shared knowledge; models are replaceable contributors.
- Deterministic indexing, retrieval and ranking work without a resident LLM or embedding model.
- Error-signature matching is primary; structural similarity is secondary.
- ICM intent, context and method are indexed.
- Several distinct proven examples can be retrieved for the same issue; they are not collapsed into one answer.
- Model-generated output remains a candidate until Core's evidence and promotion policy accepts it.

### Three-seat repair workflow
| Seat | Responsibility |
|---|---|
| **Fixer** | Proposes repair candidates |
| **Helper** | Independently explores alternatives and missing evidence |
| **Judge** | Reviews candidates against actual Sandbox outcomes |

Missing model seats do not disable model-free diagnosis, retrieval or existing fix recipes. Model Intelligence adds advisory complexity routing, context budgeting and bounded outcome calibration; it does not silently replace user-selected models.

### Inter-app communication
Apps communicate through Core's shared data provider and declared typed ports. Ports define an owner, schema and direction (telemetry, parameters, commands or events). CI checks generated Core/app contract parity to prevent ad-hoc cross-app dependencies. Since 3.0.00 a command can carry `wake`: Core opens the app it is for, and closes it again after its answer.

### Verified work that teaches every model
Every app's work is an episode in Core with its result and evidence. A writer never labels its own work above SOURCE; a passing run or check makes it VERIFIED and puts it on the Trust Ledger. Before a task, every model, local or online, gets the most similar verified episodes as worked examples, and the adapters are trained from them.

## Download and install

**[Download the latest five-app release](https://github.com/kukirin-ui/meridian-releases/releases/latest)**

1. Install **Meridian Core** first for the connected family experience.
2. Install any combination of Chat, Gaming, Parallel and NullCloud.
3. Follow in-app setup for Wireless debugging, Termux and Termux:API only when the chosen feature needs them.
4. Verify each downloaded APK with the SHA256SUMS.txt attached to that same release.

Android 11+ is the documented minimum. Device feature availability depends on vendor, OS, permissions, ADB pairing, Termux packages and model availability.

## Build and release

The private source repository is [Clean-Meridian](https://github.com/kukirin-ui/Clean-Meridian). GitHub Actions builds unsigned APKs. The owner signs locally in Termux with the private family key, verifies the common certificate, installs the apps and publishes the release assets. The private signing key and password are not stored in GitHub.

- Source: [Clean-Meridian](https://github.com/kukirin-ui/Clean-Meridian)
- APKs: [meridian-releases](https://github.com/kukirin-ui/meridian-releases)
- Website: [Meridian Suite](https://kukirin-ui.github.io/meridian-site/)

See [Install & release](docs/INSTALL-AND-RELEASE.md) and [Validation & boundaries](docs/VALIDATION-AND-BOUNDARIES.md).

## Evidence and boundaries

This showcase describes the documented 3.0.00 source state and checked-in screen inventory. It does not claim every phone exposes every device control, that shell elevation is root, that the Sandbox is a hostile-code security boundary, or that every generative task works without a model.

Benchmark results are device/configuration-specific. See [Benchmarks](docs/BENCHMARKS.md). The complete implemented surface and its dependencies are recorded in the [feature catalog](docs/FEATURE-CATALOG.md).

## Author

**Alen Požun** · Founder & Lead Architect, Meridian Family  
[X / @termuxSolutions](https://x.com/termuxSolutions) · [XDA](https://xdaforums.com/m/termuxsolutions.13482532/)

---
*Meridian Family © 2026 Alen Požun. See the source repository for component-level notices and third-party licenses.*