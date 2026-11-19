# Meridian architecture — five apps, one family core

## System view
Meridian is five standalone Android apps connected through Core. Chat owns model-facing interaction; Parallel owns Termux workflows; Gaming owns device operations; NullCloud owns source reading; Core owns family contracts and durable shared knowledge.

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
Parallel calls Termux for commands, files, package tools, build recipes, jobs, scheduler and local model services. CodeGen/Sandbox is a structured project workflow, not a hardened hostile-code jail.

## Build and release
Private Clean-Meridian source builds five unsigned APKs in GitHub Actions. The owner signs on-device in Termux, verifies the common family certificate, installs and publishes APKs/checksums to meridian-releases, then updates the public website. The private key never enters source or CI.
