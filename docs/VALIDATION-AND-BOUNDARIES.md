# Validation, dependencies and boundaries

## Evidence baseline
This documentation describes the 3.0.00 source state and uses the checked-in screen inventory, Core Android documentation, typed port topology, model-free retrieval notes, Model Intelligence notes, tests and release scripts. A UI control is not proof that every Android vendor exposes its underlying operation.

## Environment requirements
| Area | Requirement |
|---|---|
| Android | Android 11 / API 30 is the documented minimum |
| Core elevation | User-enabled Wireless debugging and pairing; shell-user, not root |
| Termux | Termux, external-app permission and relevant packages |
| Termux:API | Required for selected device functions |
| Device tuning | Vendor/firmware support and Android permissions |
| Local inference | GGUF model and working llama.cpp/llama-server |
| Vulkan | Compatible GPU driver/backend |
| Online inference | User API key, enabled online mode and network |
| Files | Android storage grants and Termux path permissions |
| Scheduler | Android background-execution and battery policies |
| Core opening apps | Core's helper running (Wireless debugging); otherwise the apps open each other or a notice asks for a tap |
| Job adapters | Trained adapter files loaded on Chat's llama-server |
| Hard offline | Android's VPN slot |

## Security and trust boundaries
- ADB elevation is not root and does not bypass Android's user-facing debugging controls.
- The helper is loopback-bound and token-authenticated; this is not a claim that the device is invulnerable.
- API keys and private APK signing key must never be committed to source or public docs.
- Public issues are visible; do not include secrets, tokens, private logs or personal data.
- Sandbox is a controlled command/test workflow, not a hostile-code jail. Do not run untrusted code expecting filesystem or network isolation.
- Model output is untrusted input. Confidence and explanation are not test evidence.
- Generated repairs are candidates until Core's evidence/promotion policy accepts them.
- Local model calibration is advisory, not the Core knowledge base.
- A writer never labels its own knowledge above SOURCE; only evidence (a passing run or check) makes it VERIFIED, and trust is scoped to the phone and Android version it was earned on.
- Core closes only apps it opened itself, never one the owner is using.

## Model-free vs model-assisted
Model-free means deterministic Core card indexing, retrieval and ranking do not need an LLM or embedding model resident in RAM. It does not mean every generative task can be completed without a model.

Model-assisted means an optional model can draft, analyze or propose candidates. Fixer/Helper/Judge remain separate. Actual validation depends on tests and Sandbox evidence.

## Benchmark interpretation
Numbers in BENCHMARKS.md apply to the recorded device, model, backend, flags, thermal state and test lengths. They must not be generalized to all Android devices or all llama.cpp versions.
