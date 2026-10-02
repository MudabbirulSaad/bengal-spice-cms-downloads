# Bengal Spice Restaurant CMS for Windows

An offline restaurant management application for one Windows PC.

**[Download the Windows installer](https://github.com/MudabbirulSaad/bengal-spice-cms-downloads/releases/download/v1.3.1/Bengal-Spice-CMS-Setup-1.3.1-x64.exe)** · **[View the latest release](https://github.com/MudabbirulSaad/bengal-spice-cms-downloads/releases/latest)**

Current version: **1.3.1**. Requires **Windows 11 x64**. No GitHub account is needed to download the public release.

## Install

1. Download and run `Bengal-Spice-CMS-Setup-1.3.1-x64.exe` from the release assets. The Source code ZIP/TAR files contain documentation, not the installer.
2. Follow Windows' installation prompts. The installer is unsigned, so an unknown-publisher message may appear.
3. The app opens automatically. Choose **Set up this restaurant** for a new restaurant or **Restore a backup** for existing data.
4. Follow the eight guided steps to create the owner account, save its recovery code, review restaurant details, service/payment settings, menu and opening stock, and verify an encrypted backup.

All required application runtimes and the private database are included. The app works offline and installs for your current Windows user.

When upgrading, close the app before running the new installer. Existing restaurant data is retained. Configured restaurants can continue immediately and open **Settings → Review setup** whenever needed.

## Software updates

Install 1.3.1 manually once over an older installation. The owner can then use **Software updates** to check releases, read changes and enable optional overnight installation. Automatic updates start off. Updates verify their signed release and a local encrypted recovery backup before installation; leave Windows signed in and the PC on mains power for overnight updates.

See the [update lifecycle and publishing guide](desktop-updates.md).

## Restaurant operations

- Counter orders, parked tickets, cash/change, external card and manually verified PayID records.
- Menu, prepared food stock, ingredients, recipes and cooking batches.
- Owner, manager and cashier accounts; sales reports, PDF export and A4 output.
- Optional customer details, local Contacts and permission-based CSV export.
- Encrypted backups and validated restoration.

Payments record staff confirmation; the app does not contact a bank or payment terminal. It is designed for one PC. Online ordering and campaign email delivery are outside this application.

## Help and verification

- [Operating guide](desktop-user-guide.md)
- [Release notes](desktop-release-notes.md)
- [Verification record and test boundaries](desktop-verification.md)
- [Installer SHA256 checksum](SHA256SUMS.txt)

This public repository contains downloads and documentation only. Application source code remains in a separate private repository. The installer contains the supplied menu and artwork, but no restaurant sales, staff credentials or cloud secrets. Third-party license notices are included in the installed application.
