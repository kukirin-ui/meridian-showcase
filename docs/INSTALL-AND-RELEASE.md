# Install, update and release

## Downloads
Canonical APKs are attached to [the latest Meridian release](https://github.com/kukirin-ui/meridian-releases/releases/latest). Verify files with the SHA256SUMS.txt attached to that same release.

## Install order
1. Install Meridian Core first for the connected family, shared data and Core-backed capabilities.
2. Install Chat, Gaming, Parallel and/or NullCloud as needed.
3. Open each app once and follow its setup.
4. For Core elevation, enable Developer options and Wireless debugging, then pair through the in-app code flow.
5. For Parallel/Termux, install Termux from its supported distribution source, allow external-app access as guided, grant storage access and install packages required by the task.
6. Install/configure Termux:API when a selected feature requires it.

Each app remains independently launchable. Connected functions depend on Core and relevant permissions/services.

## Updating safely
- Download APKs from the same release; do not mix builds from different tags.
- All five family APKs use the same signing certificate.
- Android updates an installed package only when package identity and signing lineage are compatible.
- If Android reports a signature mismatch, stop and verify the APK source and certificate. Do not uninstall or bypass the warning as a workaround.

## Owner release pipeline
The private source repository is [Clean-Meridian](https://github.com/kukirin-ui/Clean-Meridian).
1. GitHub Actions builds the five unsigned APKs for a specific source commit.
2. The owner runs the Termux release orchestrator from a clean, pushed main checkout.
3. Preflight checks Git state, remote identity, CI/authentication, repository permissions, certificate pin and local signing-key availability.
4. One interactive yes authorizes the complete workflow.
5. The phone downloads the exact CI artifact, signs all five APKs locally and verifies each signature against the pinned family certificate.
6. The owner installs the five apps (ADB installation where available; otherwise Android installer confirmation).
7. The release script publishes the five APKs and SHA-256 checksums to meridian-releases.
8. Release notes update the public site's What's New page; the script waits for and verifies the live Pages deployment.

The private key and password stay on the phone. Android installer prompts and the local key password remain separate security requirements; the single release confirmation does not bypass OS or cryptographic controls.

## Repositories
- Source (private): [Clean-Meridian](https://github.com/kukirin-ui/Clean-Meridian)
- APKs/releases (public): [meridian-releases](https://github.com/kukirin-ui/meridian-releases)
- Showcase (public): [meridian-showcase](https://github.com/kukirin-ui/meridian-showcase)
- Website: [meridian-site](https://kukirin-ui.github.io/meridian-site/)
