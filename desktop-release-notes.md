# Bengal Spice CMS 1.3.1

Software updates adds owner-controlled downloads and optional overnight installation, signed release verification, local recovery backups, an independent Windows maintenance companion, release notes and per-staff notifications. Managers can check releases; only owners change installation policy. Counter transactions and unsaved work block update preparation. Existing hosted services are unchanged.

Install 1.3.1 manually once. Automatic updates are initially off. See the [operating guide](desktop-user-guide.md) and [update lifecycle](desktop-updates.md). Windows publisher warnings remain possible because no paid signing certificate is used.

The verification record documents packaged UI, Windows scheduling, recovery and installer acceptance, including their test boundaries. Stable publication requires acceptance of the exact installer bytes.

## Bengal Spice CMS 1.2.0

- Simplified per-user Windows installation with automatic launch after interactive installation; silent installation stays silent.
- Eight guided setup steps with progress, reversible slide transitions, keyboard focus management and reduced-motion support.
- Owner creation signs in immediately. Interrupted setup resumes from saved checkpoints and owner-scoped encrypted non-secret drafts.
- Inline business, payment, menu and opening-stock review. Replayed stock submissions preserve idempotency and revision checks.
- Backup setup now verifies an actual temporary database restoration before granting completion; proof is tied to the installation and reviewed data.
- Server-enforced setup completion for new restaurants; existing completed/trading installations remain accessible. Review setup from Settings never resets data.
- Startup shows real preparation stages and offers retry/exit on failure. Additive migration 0006 preserves existing records.

## Version 1.1.0

- Name, email and phone are optional for every Counter order, including empty/whitespace API values. Blank names display as Walk-in. Coupons have a separate section.
- Optional email marketing agreement is saved with drafts and confirmed orders; old drafts default to no new agreement.
- Local Contacts directory for owners/managers: search, permission/status filters, editing, archiving and append-only permission history. Cashiers collect details through orders only.
- Transactional contact capture merges normalized email addresses and deduplicates retried orders. Phone-only captures remain separate per confirmed order. Existing historical orders are not imported.
- Subscribed-only CSV export includes permission evidence, spreadsheet formula protection and audit records. No email sending or external synchronization is added.
- Additive desktop migration 0005 creates contacts, captures and permission history; encrypted backups include all three. Install over 1.0.2 with restaurant data preserved and an automatic pre-upgrade backup.

## Version 1.0.2

Fixes startup after installation outside the source checkout. Version 1.0.1 omitted the Next.js server's dependencies from the installer because electron-builder excludes a file set's root `node_modules` directory. Earlier acceptance tests ran underneath the checkout and unintentionally resolved those missing packages from the development installation.

The installer now copies the complete traced server from a shared resource parent. Worker-only libraries are bundled explicitly, and shared authorization rules are separated from web cookie access so the worker does not load Next.js request APIs. Startup waits for the worker to confirm it loaded and connected to the database. A packaging gate compares all required resource files with their staged originals and rejects dependencies resolving outside the packaged server. Installer acceptance runs outside the source checkout, rejects ancestor dependency folders and clears Node lookup overrides. It checks worker health and invoice processing before any web PDF request.

This update changes packaging, startup supervision and dependency boundaries, with no application schema or restaurant-data changes. Install it over 1.0.1; existing business data remains separate and is preserved.

## Version 1.0.1 (superseded)

First Windows desktop release from the separate `codex/local-restaurant-cms` branch.

- Bundles the website server, durable worker, private PostgreSQL database, Node/Electron runtimes, required Microsoft DLLs, fonts and brand artwork.
- Replaces cloud authentication/storage/jobs with local staff accounts, private files and recoverable invoice jobs.
- Retains Counter interruption recovery and adds cash tendered/change, external-card records and manually verified PayID.
- Adds ingredient receipts/counts/wastage, explicit unit/pack conversions, immutable recipe versions and atomic cooking batches.
- Provides sales/refund reports, cashier restrictions, CSV/PDF export and A4 output.
- Includes first-run setup, the existing menu with fresh operational data, Windows-protected installation secrets and encrypted portable backups/restoration.
- Removes public ordering/account/marketing/integration routes and cloud deployments from this branch.
- Includes installer lifecycle, migration, API, concurrency, recovery and UI verification on the user's Windows PC.

Version 1.0.0 was the internal packaging acceptance build. Version 1.0.1 includes desktop history/session indexes, verified upgrade backup handling and the final local workflow/UI corrections.

Read [the operating guide](desktop-user-guide.md) before setup. See [the verification record](desktop-verification.md) for actual results and test boundaries. The installer is unsigned; Windows can display an unknown-publisher warning. Existing Windows app data is preserved by normal uninstall and upgrade.
