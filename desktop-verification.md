# Windows CMS — release verification

## Version 1.2.0: guided installation and setup, 1 October 2026

- Installer: `Bengal-Spice-CMS-Setup-1.2.0-x64.exe`, 186,849,149 bytes.
- SHA256: `79bfc75139fec57f21681f2ceff4df891b5d80aafc03eade299ffdff7765d33a`.
- Formatting, ESLint, TypeScript, 27 unit tests across seven files, OpenAPI validation for 59 paths, the Next standalone build and NSIS packaging passed. The package gate compared 3,739 resource files and verified dependency resolution inside the package. No environment files are included in its resource directory.
- The complete bundled-runtime suite passed the new setup checks, 19 restaurant integration checks, 10 contact checks, encrypted backup/restore checks and recovery/fault checks against a fresh isolated database.
- Setup integration verified automatic owner sign-in, password-confirmed recovery replacement, strict rejection of the old boolean completion body, direct Counter API gating, owner-only review operations, stale review rejection and transactional/idempotent completion. Editing reviewed settings invalidated backup proof; revisiting unchanged menu/stock reviews preserved it. A proof from another installation was rejected.
- Backup setup performed real authenticated decryption, archive checksum validation and PostgreSQL restoration into a disposable database. Tests rejected an incorrect passphrase, damaged archives and stale proof without replacing live data. Existing fault tests covered injected disk-full failures, database crashes/WAL recovery, occupied ports, worker recovery and downgrade rejection.
- The installed application was tested outside the checkout with a fresh Windows data profile, cleared Node lookup overrides, Windows-only PATH and blocked external renderer DNS/proxies. The wizard passed all eight stages, Back navigation, restart at each stage, expired-session sign-in, recovery-code replacement, cancelled folder selection, encrypted backup verification and server-checked completion. Setup draft storage rejected a secret field.
- An opening-stock request committed successfully before its response was replaced with an HTML error. Restarting and replaying the saved request left the exact original portion count, with no second addition. Optional Review setup loaded the existing menu and stock without reimporting or resetting them, and omitted the ordinary staff sidebar.
- Keyboard focus, live progress, labelled fields, reduced motion, narrow-window overflow and 150% Electron zoom were checked. Automated accessibility audits reported no violations on the tested setup pages; screenshots of the menu and final review were inspected. The audit waits for fonts and finite page transitions to settle, avoiding transient contrast measurements during fades. This is not a manual screen-reader session or a Windows system-wide display-scaling test.
- A disposable packaged copy was closed during database startup, shut down cleanly and reopened with its initialized database preserved. A deliberately missing worker produced the Retry/Exit startup error; exiting retained the data. No normal installation files were removed for this fault test.
- Actual installed Counter journeys passed parking/resuming, cash/change, a committed HTML-response interruption without duplicate sales, independent worker invoice generation, PDF/A4 rendering and restart preservation. Portable restoration into a second fresh profile retained menu, orders, reports and contacts; access remained gated until the new backup location was configured and verified.
- The user's normal installed 1.1.0 application was upgraded with the actual 1.2.0 installer. Before/after read-only counts and complete-row digests matched across 18 staff, settings, catalogue, inventory, recipe, order, receipt, refund, invoice and contact tables. The upgrade created its pre-upgrade archive, preserved the private PostgreSQL cluster and retained immediate legacy access. No synthetic restaurant records were inserted into that profile.
- Both final installer modes passed against the normal registered installation. Interactive installation launched the app automatically, reached database/server readiness and shut down gracefully. Silent `/S` installation did not launch it. Desktop and Start menu shortcuts still pointed to the standard per-user installation.

Installer launch acceptance exposed a failure in the standard shell-mediated shortcut launch on this PC. The per-user installer now uses a versioned NSIS hook to launch the installed executable directly for interactive installation only. Silent `/S` installation bypasses that hook. Installer testing preserves the normal program location and desktop/Start menu shortcuts.

Test-harness corrections: bundled verification now starts with a unique synthetic database so contacts from an earlier run cannot affect empty-directory assertions. Installed lifecycle tests support a runtime-only executable override and reject installation/uninstallation with that override. Installer process waiting observes the installer itself rather than waiting for its automatically launched app to exit. Windows executable metadata reports product version `1.2.0.0`; the installer check uses file version `1.2.0`.

Testing was performed on this Windows PC, as requested. No clean VM, second physical PC, physical network disconnection or physical printer is claimed. Picker selections were automated; the installer, application, local PostgreSQL, encryption, files and restore operations were real. Storage faults were injected rather than filling the user's drive. The hosted application, cloud configuration and unfinished cloud checkout were not changed.

## Version 1.1.0: optional details and contacts, 1 October 2026

- Installer: `Bengal-Spice-CMS-Setup-1.1.0-x64.exe`, 186,906,597 bytes.
- SHA256: `021b41530466dee2e84a8cd6b749e337ceea6c411f85d93055b91225c48d2c4e`.
- Formatting, ESLint, TypeScript, 27 unit tests across seven files, OpenAPI validation for 57 paths, Next standalone build and NSIS packaging passed. The packaging gate verified 3,735 unchanged resource files and local dependency resolution.
- The final bundled runtime passed 19 existing workflow checks, 10 contact integration checks, five encrypted backup/restore checks and eight recovery/fault checks. Contact tests cover omitted/empty/whitespace and independently supplied fields, invalid input, phone-only captures, concurrent confirmations using independent stock pools, repeated email matching, duplicate confirmation, stale contact edits, literal search, permission filters, direct role restrictions, CSV evidence/formula protection/audit, withdrawal/resubscription, email changes and archiving.
- A synthetic database trigger forced contact capture to fail after order approval. The order/contact savepoint rolled back, the received-payment fact remained durable, and retry completed one order/capture. Database triggers rejected history/capture mutation.
- Encrypted backup restoration compared every field of every contact, capture and permission-history record. Original database records and PDF files were preserved.
- The actual installer ran outside the checkout in `%TEMP%/Bengal Spice CMS acceptance 1.1.0`, with restricted PATH, cleared Node lookup overrides and external renderer DNS/proxies blocked. Installed UI tests passed empty names, consent gating/clearing, legacy draft defaults, park/resume, two restarts, committed HTML-response interruption, automatic recovery without duplicate sale/contact, Contacts search, explicit withdrawal/fresh agreement and the authenticated CSV save dialog. Counter cash/change, PDF/A4 rendering and independent invoice generation also passed.
- Normal uninstall/reinstall preserved the independent restaurant data and owner access.
- The final installer restored a backup into a second fresh Windows data profile and compared the contact and its complete permission history, sales and existing order against the source profile.
- The released 1.0.2 installer (verified SHA256) was installed and launched against its existing synthetic restaurant profile, followed by 1.1.0. Menu, stock, ingredients, recipes, batches, sales summary and an immutable order/invoice projection matched exactly. A pre-upgrade archive was created. Contacts started empty; an old saved ticket defaulted to no new consent, and a committed 1.0.2 create request replayed without duplication.

The user's normal installation in `%LOCALAPPDATA%/Programs/Bengal Spice CMS` was upgraded from 1.0.2 to 1.1.0 after isolated acceptance. Read-only before/after checks matched the PostgreSQL cluster identifier and fingerprints of staff, settings, catalogue, orders, receipts, refunds, stock, ingredients, recipes, batches and invoice snapshots. The pre-upgrade archive exists, Contacts starts empty, and the installed server/worker both passed readiness. No synthetic records were written to the normal data directory.

Test setup corrections: all imported menu dishes track stock, so the contact test now supplies explicit prepared stock. Recovery fault tests wait for the added invoice backlog to drain first. UI tests wait for parking to finish, allow automatic committed-order recovery, and use a unique export filename to avoid reading an earlier run's CSV. One final rebuild exited with native Windows status `-1073741819` before compiler diagnostics; the unchanged retry completed successfully. These observations are recorded without claiming a diagnosed compiler cause.

Tests used synthetic records and local profiles on this PC. No clean VM, second physical PC, physically disconnected network or physical printer is claimed. Native file-picker selections were automated; the installer, application, PostgreSQL, encryption, files and restore operations were real. Email sending remains outside the application. Cloud work and hosted data were not changed.

## Version 1.0.2: startup repair, 1 October 2026

- Installer: `Bengal-Spice-CMS-Setup-1.0.2-x64.exe`, 186,883,960 bytes.
- SHA256: `d4aaeeee97dc4eb544cb418efaecce15fdb25ca1b03bc1d7a8830b7817f600de`.
- The user's normal installation reproduced `Cannot find module 'next'`. The new payload regression check failed against 1.0.1 with `Installer payload is missing server\\node_modules`.
- Electron-builder excluded each resource file set's root dependency folder. Copying from the common parent preserves the server's traced dependencies. Worker-only libraries are now bundled; shared authorization policy no longer imports web cookies, and startup requires a worker readiness signal after a database connection.
- After-pack and installed-file verification compare 3,733 resource files and enforce local resolution for the server and worker's external imports. The check also caught missing worker-only dependencies and a CommonJS/ESM dependency mismatch before release.
- Formatting, lint, typecheck, 18 tests across 6 files, 53-path API validation, Next standalone build, runtime staging and NSIS packaging passed. Startup tests cover actual child-process readiness, a missing dependency and a readiness deadline.
- Against the final staged runtime, all 19 integration, 4 encrypted-backup and 8 recovery checks passed, including role revocation, concurrent transactions, worker failure/retry, independent worker processes, database crash recovery and restored financial records.
- The actual installer was exercised under `%TEMP%/Bengal Spice CMS acceptance 1.0.2 final`, outside the checkout and without ancestor `node_modules`, `NODE_PATH` or `NODE_OPTIONS`. Startup, owner setup, menu import, Counter interruption recovery, cash/change, independent background invoice generation, PDF/A4 rendering, restart, discounts, partial refund, native image processing, ingredients/cooking, server-crash recovery, single-instance protection, daily backup catch-up and portable restoration into another fresh profile passed.
- The restored snapshot was created after the test mutations. Native file picker selections were automated; actual database, file, encryption, backup and restoration code ran. No synthetic accounts or orders were inserted into the user's normal data directory.
- Version 1.0.2 was installed over the user's normal installation in `%LOCALAPPDATA%/Programs/Bengal Spice CMS`. A read-only startup check reached **Set up your restaurant** with both server and worker alive. PostgreSQL's system identifier matched the pre-repair value, confirming the existing cluster was retained. The ordinary upgrade path created its pre-upgrade backup.
- One additional fresh synthetic-cluster test encountered Windows `EPERM` while renaming the newly initialized database folder. A retry of the test succeeded without changing or resetting the user's database. This was separate from the missing-dependency failure; the test does not establish coverage of every Windows file-locking condition.

Testing remains on this Windows PC, as requested. No clean VM, physical printer or physically disconnected network is claimed. The 1.0.1 record below is retained with its verification error explicitly corrected.

## Version 1.0.1: superseded record

**Correction after the user's installation failure:** the 1.0.1 installer omitted the server's `node_modules`. Its recorded installed-application checks were performed below the source checkout, allowing Node to resolve missing dependencies from that checkout. These checks established application behavior but did not establish an independently runnable installer. The claim of self-contained installer acceptance for 1.0.1 is withdrawn. Version 1.0.2 corrects the package and moves installation acceptance outside the checkout; its results are recorded above.

Verified on 1 October 2026 on the user's Windows 11 Pro for Workstations x64 PC, build 26300. The user explicitly selected this PC instead of a clean VM or second physical PC. All test restaurant records are synthetic and isolated from hosted data and the normal Windows application-data directory.

## Release artifact

- Installer: `Bengal-Spice-CMS-Setup-1.0.1-x64.exe`
- Size: 175,609,236 bytes
- SHA256: `7ca059fe7b382bd1fbd49ce92e4c65ca23f23b1ac873ecc7c297c1f4281987e8`
- Electron 44.5.1, Node 24.21.0, pnpm 12.4.2, PostgreSQL 17.11; signed app-local Microsoft runtime inputs are pinned in `desktop/runtime-lock.json`.
- Unsigned NSIS installer, per-user installation, no remote updater or deployment.
- Supplied catalogue: 44 dishes, 9 categories, zero hosted dish-image files. Original branding and licensed fonts retained. No hosted staff, credentials, customers, orders or stock were imported.

## Executed checks

The versioned test commands and their actual results are:

| Check                                                         | Result                                                                                            |
| ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| Formatting, ESLint, TypeScript                                | Passed                                                                                            |
| Vitest                                                        | 15 tests across 5 files passed                                                                    |
| OpenAPI                                                       | 53 paths validated; excluded online/account/tracking/integration routes absent                    |
| Next standalone build, native runtime staging, NSIS packaging | Passed; staged files have no external directory links                                             |
| `desktop-integration.mjs`                                     | 19 bundled-runtime API/database checks passed                                                     |
| `desktop-backup-check.mjs`                                    | 4 encrypted-archive/restore checks passed                                                         |
| `desktop-recovery-check.mjs`                                  | 8 worker, database, restoration and fault checks passed                                           |
| Packaged Electron acceptance                                  | Installation, first setup, UI workflows, restart, upgrade, uninstall/reinstall and restore passed |

Integration coverage includes local owner creation and hashed-password sessions; direct cashier authorization checks; idempotent menu import; concurrent cooking-batch retries; insufficient-stock rollback; incompatible-unit rejection; duplicate cash confirmation and server-calculated change; cash/card/PayID breakdowns; own-cashier reports; protected reservations; one-time portion consumption without a second ingredient deduction; manager-only, idempotent refunds; database-enforced immutable history; cross-staff ticket denial; immediate suspension revocation; 23-hour and 25-hour Melbourne report days; PDF/CSV generation; and optimistic ingredient revisions/threshold changes.

Backup/recovery checks use actual PostgreSQL `pg_dump`/`pg_restore` and actual encrypted files. They verify wrong-passphrase rejection, modified-archive authentication failure, restoration into a separate database and a fresh private cluster, original-data preservation, invoice file hashes, session revocation, eight failed worker attempts, blocked-job/manual retry, abandoned-lease recovery, two concurrent worker processes, an occupied default PostgreSQL port, abrupt database stop and WAL recovery, incompatible-schema downgrade rejection, and restoration of the backup lock after errors. A separate retention test preserves 30 newest daily archives plus manual/unrelated files.

`desktop-lifecycle.mjs` installs and launches the actual packaged executable, with Electron sandbox/context isolation enabled and renderer Node integration disabled. It verifies:

- First-run owner and recovery code, bundled menu import, opening stock and encrypted backup configuration.
- Counter park/resume and cash payment after returning an HTML error **after the real server commit**. Recovery produces one sale and the correct change.
- Authenticated PDF export and Chromium A4 print rendering; report and invoice pages were visually inspected, including a seven-page, 60-line invoice with Bengali text and long dish names.
- Ingredient entry, opening quantities, recipe creation and cooking through the installed UI.
- Server-calculated option surcharges/discounts, historical prices surviving later menu edits, a decimal AUD partial refund through the UI, and native Sharp processing/private serving of an uploaded local image.
- Graceful close/reopen with a different private port, staff-bound draft isolation, single-instance enforcement, server-process crash/reopen without losing committed records, and a missed daily backup caught up at launch.
- Upgrade from the initial 1.0.0 package to 1.0.1, with a pre-upgrade backup and the additive history/session-index migration.
- Normal uninstall/reinstall preserving restaurant data; portable restore through the desktop bridge into another fresh data profile on this PC.

Later packaged runs used a PATH containing only the Windows System32 directory, invalid external proxy endpoints and Chromium rules disabling external DNS. External renderer fetches were rejected. The installed services use bundled executables and loopback connections. No hosted services participated in these journeys.

## Test boundaries

- No clean Windows VM, second physical machine or second Windows account was available/tested. Fresh data profiles and PostgreSQL clusters were tested on this PC as requested. Existing system libraries on the PC mean this is not independent proof of a clean-OS installation.
- The PC's network adapter remained connected for the working session. External renderer traffic/DNS was blocked in tests; there was no physical network-disconnection test.
- No physical printer or bank/card terminal was used. A4 output was rendered to PDF. Card/PayID are intentionally staff-recorded facts, not payment-provider integrations.
- Native file-picker responses were automated by the test harness; real IPC, encryption, file I/O, migrations and restore operations ran. The release contains no test dialog overrides or synthetic credentials.
- Disk-full conditions were injected at free-space/copy boundaries; the user's actual disk was not filled. These tests cover safe error handling rather than every hardware/storage failure.
- The manual installer CI workflow is versioned but has not run on GitHub. It requires a dedicated, configured `cms-builder` Windows runner and the licensed runtime inputs. No runner, paid service or cloud deployment was created.

The implementation remains on `codex/local-restaurant-cms` in its own worktree. The dirty `codex/vercel-supabase-jobs` checkout was preserved, and the hosted application was not deployed or changed.
