# Meridian architecture — five apps, one family core

## System view
Meridian is five standalone Android apps connected through Core. Chat owns model-facing interaction and the family's API keys; Parallel owns Termux workflows and building programs; Gaming owns device operations; NullCloud owns source reading; Core owns family contracts, durable shared knowledge and the record of verified work. Since 3.0.00 Core is the only process that runs all the time: the other apps open when there is work for them and close again.

## Core bridge and elevation
1. User enables Android Developer options and Wireless debugging.
2. Core pairs through Android's pairing-code flow and discovers the ADB endpoint.
3. Core launches a helper as the Android shell user with app_process.
4. Helper listens on a random loopback port and requires a one-time token.
5. Family apps request supported operations through Core's bound service.
6. Core can reattach after its own process restarts.

This is shell-user access through Android debugging, not root. Android may disable Wireless debugging after reboot; reconnect is a user action.

## Shared data and typed ports
The family provider is content://com.meridian.core.data. Port topology is declared in the private source at docs/ports.json and generated into Core and app-side bus contracts.

- tlm: telemetry/status.
- prm: owner-written parameters/settings.
- cmd: targeted request/result.
- evr: family events.

Ports are owner-scoped, schema-validated and size-bounded. CI checks generated parity.

## Core's Mind (3.0.00)
- One SQLite database compiled into Core (FTS5): documents in passages, recipe cards, proven fixes, lessons, learned cards and episodes.
- Learning Kernel: trust labels and moves, Beta-Bernoulli arms with forgetting and Thompson sampling, EWMA + CUSUM change detection, BM25, SimHash.
- Trust Ledger: a hash chain of every trust change, verified incrementally and in full in the rest window. Trust is scoped to the environment it was earned in.
- Episodes: `mind.episode` / `mind.episodes`. A writer never labels itself above SOURCE; reward 1 with evidence is VERIFIED. Retrieval by similarity (verified first) gives every model worked examples; paging in stored order feeds the adapters' training export.
- Mirror: a read-only shared memory region with sections (cards, fixes, lessons, learned, docs, arms, trust, care), sequence-locked with a CRC32 per section.
- Constitution (eight rules), Proof Engine (`mind.proof` / `mind.verify`) and Survival Mode (`tlm.health`).

## Wake: Core opens the apps (3.0.00)
1. An app sends work to another app's `cmd` port through Core with `wake: true` (`MeridianBus.work`).
2. Core opens the target app unless it is on screen: its helper's `am start` as the shell user (not limited by Android's background-start rule), else Android's own start, else a notice the owner taps.
3. The target takes the message from its port, does the work and answers on the sender's `cmd` port with `wake` (the sender comes back) and `release`.
4. Core closes the app that did the work, only when Core opened it and the owner is not using it.
5. `cap.now` says whether this Core can wake apps; with an older Core the apps open each other the old way.

## Job adapters (3.0.00)
Chat's llama-server loads up to fourteen LoRA adapters on one base model. Every request names all loaded adapters with the job's slot at scale 1 and the rest at 0; the slot comes from the job (file language, a failed command, judging, the topic). Training data comes from Core's verified episodes, Chat's rows, the teacher's fixes and Parallel's proven repairs.

## Model-free knowledge path
Problem/query → ICM intent/context/method → Core local full-text index → candidate pool → error-signature ranking plus secondary structural reranking → multiple distinct proven examples → deterministic result/recipe.

Optional models can propose candidates. Sandbox evidence and Core's promotion policy determine whether a candidate becomes durable knowledge. Retrieval does not require an embedding model, neural runtime or resident LLM.

## Optional Model Intelligence
- Fixer, Helper and Judge remain separate roles.
- Complexity and seat recommendations are advisory.
- Context budgeting may compact optional debugger detail but must preserve required source, ICM, failed-attempt evidence and output contract.
- Calibration is bounded, records eligible model-produced candidates with real Sandbox outcomes and remains advisory.
- Calibration is not Core knowledge and does not silently replace the user's model selection.

## Termux and execution
Parallel calls Termux for commands, files, package tools, build recipes, jobs, scheduler and local model services. Any app can ask Parallel for a program through Core (`codegen`): it is written with its tests, proven in the Sandbox, repaired and saved in `~/meridian-builds/<id>/`. CodeGen/Sandbox is a structured project workflow, not a hardened hostile-code jail.

## Build and release
Private Clean-Meridian source builds five unsigned APKs in GitHub Actions. The owner signs on-device in Termux, verifies the common family certificate, installs and publishes APKs/checksums to meridian-releases, then updates the public website. A release is stable by default (tag `v<version>`, marked Latest); a beta is a pre-release (`MF_CHANNEL=beta`). The private key never enters source or CI.
