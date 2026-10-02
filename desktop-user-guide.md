# Bengal Spice CMS — operating guide

## Install and set up

Run the x64 setup executable on Windows 11. It installs for your Windows user in the standard location and opens Bengal Spice CMS when finished. The installer is unsigned, so Windows may show an unknown-publisher warning. All runtimes, PostgreSQL, fonts and artwork are included; no internet connection or development tools are needed.

Choose **Set up this restaurant**, or **Restore a backup** if you already have restaurant data. The eight-step wizard creates your owner account, helps you save its recovery code, reviews receipt/tax details, service/payment settings, the included menu and opening prepared portions, then creates and verifies an encrypted backup before the final review. Use **Back** to correct details. Completed steps and non-secret drafts are saved; **Save and sign out** lets you resume later. Passwords, recovery codes and backup passphrases are never saved as form drafts.

Use a password of at least 12 characters. Save the one-time owner recovery code somewhere safe. If setup was interrupted before you saved it, sign in with your chosen username/password and generate a replacement from the recovery step. The replacement invalidates the previous recovery code; no restaurant data is erased.

Review the bundled menu's 44 dishes and 9 categories. Dishes without prices stay unavailable. Enter only food already prepared; zero portions is valid. Staff accounts, ingredients and recipes can be added later. Cash and externally processed card payments need no online integration; PayID details are optional. Staff still check each external payment before confirming it.

At **Backups**, enter and confirm a recovery passphrase and choose a folder or USB drive. The app creates an encrypted backup and verifies it by restoring into a temporary database without replacing your restaurant data. Cancelling the picker or a failed verification leaves setup unfinished. Save the passphrase separately: it serves a different purpose from the owner recovery code.

On the final page, **Finish setup** checks the saved requirements, then **Open Counter** begins service. Direct order requests cannot bypass unfinished setup. Existing configured or already trading installations continue working after an upgrade; owners can use **Settings → Review setup** to review their current data without resetting it.

The owner adds manager and cashier accounts under **Team & access**. Sign out/lock when changing staff. Suspending staff or resetting their password immediately revokes their sessions. Owners control staff, business/tax settings, imports and restoration. Managers control restaurant operations and refunds. Cashiers see their own tickets, orders and sales and cannot refund or cancel paid orders.

Sessions last eight hours. If your session ends, sign in again with the same local username and password. Your saved Counter draft remains available. Sign out also works after expiry. Reinstalling keeps restaurant data and does not reset accounts or passwords.

## Daily work

1. Receive ingredients, record wastage or use a stocktake to set the observed balance. Use compatible units: g/kg, ml/l, or whole count. Configure packs explicitly.
2. Create a recipe version with quantities and expected yield. Record each cooking batch with its actual ingredient usage and actual portions. This deducts ingredients and adds prepared stock atomically.
3. Create an order in **Counter**. Choose takeaway or dine-in, add dishes/options and optionally a name, contact, table reference or kitchen note. **Save for later** and **Park ticket** keep an unpaid ticket for resumption.
4. Select **Take payment**. Cash calculates change from the tendered amount. External card and PayID require staff confirmation and a reference. The app records these transfers; it does not contact a bank or terminal.
5. If a request is interrupted, keep that ticket and use **Retry request**. Do not start another sale to recover it. Reopening the app retains pending desktop actions and queries their result.
6. Advance the order through preparation and pickup/service. Preparation consumes its reserved portions once. It never deducts the recipe ingredients again. Managers/owners record actual refunds separately; refunds do not put food back into stock.

Correct stock through new, explained movements. Historical receipts, invoices, recipe versions, batches, refunds and audit entries are preserved. Options use the parent dish’s portion pool; independently stocked sizes must be separate menu items.

## Optional customer details and Contacts

At Counter, expand **Customer details (optional)** to collect name, email or phone. Leave any or all blank; the order can still be confirmed and displays **Walk-in** if no name is supplied. Correct an invalid email or clear it. Coupons have their own section.

Check **Customer agreed to receive marketing emails** only after receiving agreement. It starts unchecked, needs a valid email, and clears when that email is edited. Details and recorded agreement survive parking, resuming and restarting the app. Old drafts start without new permission.

After a successful confirmation, an email or phone creates a local contact. Repeated email addresses merge regardless of case; phone-only entries stay separate per sale. Names alone create no directory entry. Previous sales are not automatically imported.

Owners and managers use **Contacts** to search, filter, edit and archive contacts. **Not recorded**, **Subscribed** and **Withdrawn** describe email permission. An unchecked later order does not withdraw existing permission. Use **Withdraw email permission** for a withdrawal; check fresh agreement and click **Record fresh agreement** to resubscribe. A changed email resets permission for that address. History records who recorded each change, when, its source and any associated order. Past orders and invoices stay unchanged.

**Export subscribed contacts** saves a CSV with all active subscribed email contacts and their permission evidence, regardless of directory filters. Archived contacts and other permission states are excluded. Exports are audited and included contact values are protected against spreadsheet formulas. Email delivery happens outside the app; imported/exported mailing lists are not synchronized. All contact records and permission history are included in encrypted backups.

## Reports and printing

**Sales & reports** provides today, week, month and custom periods in Australia/Melbourne, including daylight-saving changes. Amounts are AUD. Sales are after discounts, refunds use their own recorded dates, and net sales subtract those refunds. Cashier attribution, payment methods, best sellers and unresolved records are shown. These are sales figures, not profit or accounting reports. There is no required end-of-day close.

Export CSV or PDF to a chosen folder. Open an order to save its immutable invoice PDF and open it in the Windows PDF reader for A4 printing. **Print A4** prints the report using Windows printing. Choose A4 in the printer dialogue. PDF export does not require a printer.

## Back up, restore and update

Use **Backups & recovery** to choose a backup folder (preferably a separate drive) and a recovery passphrase of at least 12 characters. Store the passphrase separately. The app creates daily encrypted backups while open and catches up when reopened; it retains 30 automatic daily files. Manual and pre-upgrade backups are retained separately. Check the visible last-backup time and any failure message. A disconnected USB or full drive cannot receive a backup.

**Create portable backup** saves an encrypted PostgreSQL logical dump, private files and version information. Writes pause briefly while the consistent snapshot is captured. Do not copy the live `postgres` directory as a backup.

To move to another PC, install the app there and choose **Restore backup** before creating an owner. Select the `.bscms` file and enter its passphrase. An existing installation requires owner access. Restore validates a separate database before switching; previous data remains preserved. Sign in with an account from the backup. Complete the backup-location step after restoration. Its verification belongs to this installation; the restored menu and stock are retained. The owner recovery code and backup passphrase serve different purposes; keep both.

Quit the app before running a newer installer. Application data survives normal upgrades and uninstall/reinstall. An upgrade takes a backup before applying new desktop migrations. Incompatible database downgrades are blocked. Business data lives in `%LOCALAPPDATA%\Bengal Spice CMS\`, separately from program files. Windows-encrypted installation secrets work with the same Windows account; use portable backups when moving machines/accounts.

## Recovery and limitations

The app and its jobs run while open or minimized. Quitting stops the local services. After an unexpected restart, reopen it and review any interrupted Counter action, blocked PDF job or backup warning. **Local jobs** lets managers retry blocked invoices after resolving disk-space problems. Keep adequate free disk space and a separate backup copy.

This release is for one Windows PC and one shared Windows account. It does not provide online ordering, customer accounts, email, thermal printing, payment-terminal integration, split payments, purchasing/accounting or multi-PC access. Do not expose its loopback services to a network.

# Software updates (1.3.1)

Open **Software updates** from the Management menu. The owner can check, download, read changes and choose **Install now**. Save or park Counter work first. The app verifies a local recovery backup, closes safely and checks the new version before reopening.

To update overnight, enable **Allow automatic overnight updates on this PC** and save preferences. The default window is 3–5 am Melbourne time. Leave Windows signed in (it can be locked), keep the PC on mains power, and finish current edits. Optional wake support depends on Windows settings. Nothing installs simply because you close the app. Internet is needed to find/download/approve updates; normal restaurant work remains offline.

Use **Install tonight**, **Remind me tomorrow**, or turn automatic updates off. Managers can check and read releases; installation and scheduling belong to the owner. New-version notes are cached, and update history records success or failures. If an update needs recovery, follow its message and reopen the CMS. Never delete restaurant data to fix an update.

Install 1.3.3 manually if you currently use 1.2.0 or earlier. Download the EXE, close the CMS, run it and reopen. Data is preserved. Version 1.3.1 can use Software updates. See [update lifecycle and publishing](desktop-updates.md) for administration and recovery.
