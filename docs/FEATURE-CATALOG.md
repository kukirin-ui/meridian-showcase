# Meridian Family — complete implemented feature catalog (2.6.55)

This is an inventory of the documented 2.6.55 product state, not a roadmap. It is based on the private source tree, checked-in screen inventory, Core documentation, generated port topology, release scripts and current tests. A listed control may depend on device support, permissions, Core pairing, Termux or a configured model.

## Product map

| App | Responsibility | Owns |
|---|---|---|
| Core | System hub | ADB bridge, shared data/ports, family state and durable knowledge |
| Chat | Intelligence workspace | Model configuration, conversation UX, projects, prompts and knowledge tools |
| Gaming | Device operations | Monitoring, benchmarks, game profiles, task isolation and tuning |
| Parallel | Termux workstation | Console, files, plans, tools, Doctor, Diagnose, Debugger, CodeGen and Sandbox |
| NullCloud | Reading/research | Link/PDF/text ingestion, transformations and reading library |

## 1. Meridian Core

### Pairing and shell-level elevation
- Guided Android Developer options and Wireless debugging setup.
- Pairing-code flow and discovery of the ADB pairing endpoint.
- Connects to the phone's ADB daemon; local ADB TCP mode can be used where explicitly configured.
- Starts a helper as the Android shell user with app_process.
- Helper binds to a random loopback port and authenticates with a one-time token.
- Helper runs in its own session; Core can reattach after its own process restarts.
- Family apps request supported actions through Core's bound service.
- Local activity/event records for actions and outcomes.

This is shell-user elevation through Android debugging, not root. Android may turn Wireless debugging off after reboot; the user must enable it and reconnect. The app does not silently enable debugging.

### Family services and shared state
- Shared content provider: content://com.meridian.core.data.
- Shared family preferences and app check-ins/version state.
- App-targeted command/result channels.
- Shared event log with severity and event text.
- Long-running work/progress records for model calls, Termux jobs and other app work.
- Shared language/theme/reduced-motion/haptics settings.
- Capability probe that reports available access level (none, shell or root).

### Typed app ports
The topology is declared in docs/ports.json and generated into Core rules and app-side bus contracts. Port families:
- tlm: telemetry/status.
- prm: owner-written settings/parameters.
- cmd: targeted request/result channel.
- evr: family events.

Ports are owner-scoped and schema-validated; keyed work records are bounded. CI checks generated contract parity.

### Shared knowledge
- Core owns durable shared card/lesson/library storage.
- Model-free local retrieval does not require an embedding model, neural runtime or resident LLM.
- Retrieval indexes error text and ICM intent/context/method.
- Error-signature match is primary; structural similarity is a secondary reranking signal.
- Independent confirmations and recency help order equally relevant candidates.
- Multiple distinct successful solutions remain distinct cards; retrieval can preserve more than one valid path for the same problem.
- Model output is only a candidate; Core's evidence and promotion policy decide durable status.

### Core app surfaces
Setup/pairing guide, family status, activity log, shared settings, update/release information, About, licenses and support/report entry points.

## 2. Meridian Chat

### Conversation and project workspace
- Main chat with model selection.
- Conversation memory and project-specific context.
- Custom instructions, response tone and ICM Inputs/Process/Outputs formatting option.
- Reusable prompt library.
- File attachments, file summaries and code/file review actions.
- Termux home/file access when linked and permitted.

### Local models
- Discover GGUF model files on the phone.
- Import/select model files and manage model entries.
- Optional model download flows.
- Connect to llama.cpp / llama-server through an OpenAI-compatible local API.
- Global defaults and per-model overrides.
- GPU (Vulkan), CPU-only, CPU+GPU split and supported automatic backend options.
- Threads, CPU affinity, context, GPU layers, batch, micro-batch, maximum reply, Flash Attention and KV-cache options.
- Thinking mode where supported.
- Model fit estimate, load/unload, speed test and runtime status.
- Optional local model mesh and user-controlled model membership/settings.
- NullCloud can reuse Chat's configured model engine.

### Three model seats
- Fixer proposes the first repair candidates.
- Helper independently investigates alternatives and missing evidence.
- Judge reviews candidates against actual test/Sandbox evidence.
- Optional seats can be absent; model-free retrieval and deterministic tools remain available.

### Online BYOK
- User-supplied provider, model ID, endpoint and API key.
- Documented providers: Groq, Gemini, OpenRouter, Mistral, Cerebras, NVIDIA NIM, OpenAI, Grok/xAI, Anthropic and custom.
- Multiple online seats, quality/step budget and per-answer cost cap.
- Explicit online-answer toggle; requests are not sent until enabled.
- Optional VPN requirement/status/configuration surface.
- Local and online modes remain distinct.

### Knowledge and learning
- Skill tree with 12 top-level domains and nested branches/cards.
- Skill-card workspace, lessons/dictionary, recipe pack browser and library sync.
- Shared Core knowledge access.
- Optional online recipe-building agent, separate from the local answering model.
- Web search with citations.

## 3. Meridian Gaming

### Dashboard and monitoring
- Home summaries for battery, RAM, CPU and activity.
- Hardware/system views and copyable hardware report.
- Live readings where Android/vendor interfaces expose them.
- CPU cluster/GPU readings, clocks/load and temperature surfaces.
- Battery, security/network-posture and device-care screens.
- Network speed test.

### Game profiles and isolation
- Detect installed games/apps.
- Add profiles manually or auto-add new installs when enabled.
- Start/stop watch mode.
- Profile permissions for write-settings, Do Not Disturb and overlay features.
- Task killer/isolation with app search and selection.
- Keep Google Play services option.
- Optional handling of Samsung/Google extras.
- Optional isolation while the selected game is open.
- Driver discovery action where supported.

### Heat, tuning and benchmarks
- Heat-stop threshold and stop-heavy-work action.
- Advanced CPU/GPU/battery temperature limits and when-hot action.
- Read/apply/copy controls for device settings.
- Performance-related controls (performance mode, CPU clusters, GOS-related actions, phantom-process handling) where device firmware and permissions permit.
- Model benchmark: CPU, GPU/Vulkan and split backend; GPU layers, threads, CPU affinity, Flash Attention, KV cache, prompt/generation lengths, batch, micro-batch, repeats, history and result verification.

A visible tuning control does not guarantee that every Android vendor permits the requested operation.

## 4. Meridian Parallel

### Termux and console
- Termux setup checklist and connection check.
- Termux:API setup guidance.
- Console with command entry, run action and session selector.
- Direct open-Termux action.
- Battery/storage context and long-running job status.

### Files and projects
- Browse Home, Downloads, Shared, DCIM, Models, Projects, Notes, Logs, Bin and Meridian.
- Navigate, select and refresh.
- Create project, folder and file.
- File operations are limited by Android storage grants and Termux permissions.

### Plans and build recipes
- Searchable plans across phone, Termux basics, AI, web/servers, developer tools, languages/builds, files/media, phone/system and Linux desktop.
- Describe a task and generate a step plan.
- Build recipes for Node.js, Rust, Go, Ruby, PHP, Lua, Java, C/C++ and common shell/JSON utilities.

### Package and developer tools
- Installed packages, update, upgrade, search, package details, apt cache, repair and reinstall-core actions.
- Python/Pip, Node.js/NPM, Rust, Go, Ruby, PHP, Lua, Java JDK, Clang, CMake, Make and C/C++ build-essential.
- Git and Docker CLI.
- Folders/storage/home files, find, disk use, Vim, Neovim, Micro, ripgrep, jq, tree, unzip, rsync, curl and wget.
- Local model, on-device AI, llama-server, GPU compute, Python jobs, Node services, web page, media box and remote shell recipes.
- Debian and Ubuntu entry points through proot-distro.

### APIs and scheduler
- Optional BYOK provider and custom endpoint configuration.
- User-defined task and cadence, refresh and stop-all controls.
- Android background execution and Termux availability still govern whether scheduled work runs.

### Doctor, Diagnose and fixes
- Doctor categories: network, storage, memory, heat, battery, Termux, packages, local model, Core and permissions.
- Diagnose from pasted error or last failed command.
- Evidence-oriented error-family diagnosis.
- Fix recipes for package/repository, permission, storage, missing tool, Vulkan, command cache and other common Android/Termux faults.
- User-controlled repair actions and outcome recording.

### Debugger, CodeGen and Sandbox
- Debugger can open files and discover source files.
- CodeGen plans multi-file tasks and validates paths, duplicate names, extensions, language contracts and line budgets.
- Generated files are saved into the selected project/Termux workspace.
- Sandbox runs configured checks and records outcomes.
- Diagnose/repair loop can use configured Fixer/Helper/Judge seats.
- Save workflow preserves generated project output and its contracts/evidence.

Sandbox is a controlled execution workflow, not a hardened hostile-code jail. CodeGen is a structured coding/repair workflow, not a claim of unlimited autonomous engineering.

## 5. NullCloud

### Sources and library
- Read web pages/links.
- Import PDF documents.
- Paste plain text.
- Save processed reads to a local library.

### Reading actions
Summarize, bullet points, key points, explain subject, extract knowledge/facts, create recipe/how-to steps, check claims, simplify language, translate and ask follow-up questions.

### Model modes
- Reuse Chat's configured model when available.
- Standalone model mode when Chat is not installed or the user chooses it.
- Select GGUF file and configure threads, GPU layers and context.
- Install/start the model engine from the model screen when using standalone mode.

## 6. Release and support
- Private source: kukirin-ui/Clean-Meridian.
- GitHub Actions builds five unsigned APKs for a source commit.
- Owner release script checks source state, exact remote commit, authentication, permissions and signing prerequisites.
- Owner's private key stays on the phone; all five signatures are checked against the pinned family certificate.
- Release repo stores five APKs and SHA256SUMS.txt.
- Website What's New is updated from release notes and Pages deployment is verified.
- In-app Report a problem previews app/version/device context before the user submits.

## 7. Dependencies and boundaries

| Capability | Dependency / limit |
|---|---|
| Core elevation | User-enabled Wireless debugging; shell-user, not root; reconnect after reboot may be required |
| Device tuning | Vendor firmware, Android version, permissions and exposed interfaces |
| Termux features | Termux, external-app access, storage permission and relevant packages |
| Termux:API | Required by selected device functions |
| Local AI | GGUF file, llama.cpp/llama-server and enough RAM/compute |
| Vulkan | Compatible GPU driver/backend |
| Online AI | User API key, network and explicit online enablement |
| Scheduler | Android background-execution policy |
| Sandbox | Controlled runner, not hostile-code isolation |
| Model Intelligence | Advisory complexity/context/calibration layer; not an embedding engine or automatic model selector |
| Benchmarks | Specific to phone, model, backend, flags and thermal state |

## 8. Explicit non-claims
- ADB shell elevation is not root.
- Model-free retrieval does not mean every generative feature works without a model.
- No neural embedding model is claimed by the model-free foundation.
- Model confidence is not proof.
- A generated candidate is not automatically a proven card.
- One successful solution does not erase other distinct proven solutions.
- The Sandbox is not a complete security boundary.
- UI presence does not guarantee vendor support.
- Benchmark results are not universal Android performance claims.
