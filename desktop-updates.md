# Desktop software update lifecycle

The desktop branch owns Windows updates. The hosted application, customer database and cloud deployment workflows are separate.

## Owner experience

Install 1.3.1 manually once. Software updates then shows the installed version, approved release, download progress, last successful check, release notes, schedule and history. A failed/offline check is distinct from being up to date. Managers may check and read updates; only owners may download, install, select Preview or change machine preferences. Cashiers can read changes and acknowledge their own notifications.

Automatic updates require the owner's explicit opt-in on each installation. Defaults: Stable, 03:00–05:00 Australia/Melbourne, wake disabled, mains power, and 20 minutes without Windows or CMS activity. The last 30 minutes of a window cannot start an installation. Checks run on startup, every six hours while open, manually, and through the enabled Windows schedule. Missed Windows triggers always recheck the Melbourne window. A signed-out or switched-off PC cannot update. Optional wake requests depend on Windows and hardware support.

Counter work and normal exits do not trigger installation. Save or park tickets and finish edits, printing and backup/restore operations first. During preparation the app temporarily prevents interaction, drains requests, creates a local encrypted backup and restores it into a temporary database to verify it. External backup drives are not required. The previous UI state is restored after success; an app that was closed stays closed. The next staff session can read cached changes. Owner failures remain visible until acknowledged.

## Trust and coordination

- `electron-updater` 6.8.9 handles full installer downloads using a custom provider populated exclusively from an Ed25519-verified manifest. Implicit installation on exit and differential downloads are disabled.
- The manifest binds version, channel, monotonic sequence, approval dates, URL, byte length, SHA-256/SHA-512, supported application/database range, PostgreSQL major, automatic/manual classification and structured notes. Downloads allow only the configured public GitHub repository and its release asset redirect hosts. No GitHub token is shipped.
- The release approval is fetched again immediately before replacing files. Failed validation, withdrawal, unavailable approval or insufficient disk space cancels preparation. Restaurant data is preserved.
- Per-user InteractiveToken scheduled tasks run a separate Electron maintenance companion. It has its own executable/runtime, a Windows-encrypted installation binding, an independently tested startup, and a kernel-owned named-pipe lock. It does not store Windows passwords or require administrator rights.
- Policy, consent and the durable journal live outside the replaceable program folder, encrypted using Windows protection. The renderer has narrow typed IPC; it cannot supply executable paths, claim successful verification, or bypass server roles. Authorized API requests enter a transactional audited queue, and the desktop rechecks membership before dispatch.
- All API operations and workers take a shared maintenance barrier. The gate is checked after lock acquisition so a queued request cannot slip through a drain. The existing database/file backup lock remains separate to avoid nested advisory-lock deadlocks.
- Drizzle migration 0007 adds request, history and per-staff acknowledgement tables. Trusted machine events are mirrored idempotently into database history and audit. Portable restores rotate installation identity and disable machine scheduling consent.

## Recovery

The durable phases are Preparing, Prepared, Installing, Validating, Completed/Cancelled and Recovery required. A restart before replacement cancels the interrupted attempt. After replacement, recovery retries the verified target. If startup still fails, a previous signed installer can be used only when the actual database schema matches its compatibility declaration. A database backup is never silently restored over later business writes. An incompatible downgrade remains blocked. Failed databases, logs and referenced recovery archives are preserved for owner-assisted recovery.

Keep the current and previous verified installer and the latest three update backups. Ordinary uninstall removes the Windows schedules and maintenance programs; business data and backups remain. Windows publisher warnings may still appear because release-manifest signatures are separate from paid Authenticode signing.

## Publishing from the private desktop checkout

1. Update both package versions, `desktop/release-notes.json` and `desktop/release-policy.json`. Use additive Drizzle migrations and classify destructive changes or PostgreSQL major upgrades as manual-only. Update the operating guide and record actual tests.
2. Commit the source. `pnpm desktop:release build preview` requires a clean desktop branch and runs formatting, lint, types, unit/API checks, packaging and bundled integration checks. It prepares an EXE, checksums, metadata, structured notes, guides and source commit receipt in ignored `output/releases/<version>`.
3. `pnpm desktop:release draft preview` creates a public downloads draft. Existing version assets cannot be overwritten. `pnpm desktop:release preview preview` publishes it as a prerelease and signs/pushes the Preview channel approval.
4. Exercise the real installer and automatic update lifecycle with isolated data. Record `acceptance.json` beside the release with the exact installer `sha256`, `installerPassed: true` and `updateLifecyclePassed: true` only after those checks pass.
5. `pnpm desktop:release promote stable` promotes the same installer bytes and publishes signed Stable approval. The source repository stays private. Do not rebuild a tested version before promotion.
6. To withdraw an offer, use `pnpm desktop:release withdraw stable` (or preview). Existing installations continue working. Publish a higher corrective version; never replace an existing EXE. Channel approval expires after 90 days and can be renewed by signing/publishing a fresh approval of the same verified artifacts.

The release scripts target only `MudabbirulSaad/bengal-spice-cms-downloads`. Push source commits/tags to the private source repository separately. They do not deploy the hosted application or use a paid runner.

## Signing-key custody

The release private key is stored under the Windows publisher profile in `%LOCALAPPDATA%\Bengal Spice Publisher\release-signing.enc`. Only public trust keys enter the source and installers. The accompanying recovery PEM is encrypted; its generated recovery passphrase is Windows-protected separately. Keep a portable encrypted key and its passphrase on separate offline media before relying on another PC for releases. A physical offline backup is an operator task and is not established by creating these local files.

For rotation, first ship a release trusted by the old key that embeds both old and new public keys; only then sign future releases with the new key. Raise minimum upgrade versions where needed. Key loss or compromise requires a manually trusted recovery installer. Never place publisher secrets in GitHub release assets, repository files or a customer installer.
