# Wakuron Dock

Your personal toolbox in the terminal. Type `wakuron` and use the tools you picked: email,
notes, todos, passwords and more. The Dock itself is small; every tool comes as a **bundle**
you download only if you want it.

> **Windows 10 / 11 (64-bit) for now.** Linux and macOS builds are coming.

## Install

1. Open **[Releases](../../releases/latest)** and download `wakuron-dock-<version>-win-amd64.zip`.
2. Extract the ZIP anywhere (right-click → *Extract All…*).
3. Double-click **`install.cmd`**.
   - No Python yet? The installer offers to install it for you (Python 3.10 or newer is needed).
   - Windows may show *"Windows protected your PC"*: click **More info → Run anyway**.
4. The installer lists the available bundles. Type the ones you want, e.g. `mail notes`, and
   press Enter. (Enter alone = none; you can add them any time later.)
5. Open a **new** terminal (PowerShell, Command Prompt or Windows Terminal) and type:

   ```
   wakuron bundles
   ```

Done. The extracted folder can be deleted: Wakuron lives in
`%LOCALAPPDATA%\Programs\wakuron`.

**Without questions** (e.g. from a script), run in the extracted folder:

```
install.cmd -Bundles mail,notes     the Dock + these bundles
install.cmd -Bundles none           the Dock only
```

Set `WAKURON_INSTALL_DIR` before installing to put Wakuron somewhere else.

## Bundles

| Bundle | Commands | What it does |
|--------|----------|--------------|
| `mail`  | `wakuron mail`  | All your email accounts (Gmail, Outlook / Microsoft 365, Seznam, any IMAP) in one inbox |
| `notes` | `wakuron todo`, `wakuron note` | A todo list with due dates, and quick notes |
| `vault` | `wakuron vault` | Passwords and 2FA codes, stored in Windows Credential Manager |

```
wakuron bundles                   what you have installed
wakuron bundles available         everything you can install
wakuron bundles add vault         download and install a bundle
wakuron bundles remove vault      uninstall it (its data is kept)
```

Every command has help: `wakuron --help`, `wakuron todo --help`, `wakuron mail send --help`.

## Quick start

**Todos and notes**

```
wakuron todo add Buy milk -t shop -p high
wakuron todo add Finish report -d fri       due: 2026-11-03, today, tomorrow, fri, +3d, +2w
wakuron todo                                open todos, most urgent first
wakuron todo done 1
wakuron note add Call the dentist           a one-line note
wakuron note add                            your editor opens for a longer one
wakuron note                                all notes; wakuron note find dentist
```

**Passwords and 2FA**

```
wakuron vault add github -g        make up a strong password and copy it
wakuron vault get github           copy the password to the clipboard
wakuron vault totp github          save the 2FA key ("enter key manually" under the QR code)
wakuron vault code                 current 2FA codes
```

**Email**

```
wakuron mail account add           asks for everything, one account at a time
wakuron mail inbox                 all accounts, newest first
wakuron mail read 12
wakuron mail send -t friend@example.com -s "Hi"
```

- **Gmail:** use an [app password](https://myaccount.google.com/apppasswords)
  (needs 2-Step Verification), not your normal password.
- **Seznam.cz:** allow IMAP in Seznam's settings first.
- **Outlook / Microsoft 365** (most school and work accounts) sign in through the browser and
  need a one-time setup: register an app at <https://entra.microsoft.com> (*App registrations →
  New registration*, any organizational directory and personal accounts), turn on *Allow public
  client flows*, add the delegated permissions `IMAP.AccessAsUser.All` and `SMTP.Send`
  (*Office 365 Exchange Online*), then run
  `wakuron config set microsoft_client_id <Application (client) ID>`.
  Some schools block outside apps; then their admin has to approve it.

## Updates

Once a day `wakuron` checks for a new version of the Dock and of your bundles and asks
`Update now? [Y/n]`. Or do it yourself:

```
wakuron update                     the Dock and all your bundles
wakuron update --core              only the Dock
wakuron bundles update             only the bundles
wakuron bundles update notes       only this bundle
wakuron update --check             just look, don't install
```

Your accounts, notes, passwords and settings are kept. If an update fails, the previous version
is restored.

## Uninstall

**Settings → Apps → Wakuron Dock → Uninstall**, or `wakuron uninstall`.

It asks whether to delete your data too. Keep it and a later reinstall picks up where you left
off.

## Your data

- Settings, notes, todos and the mail cache: `%APPDATA%\wakuron`
- Passwords, 2FA keys and sign-in tokens: Windows Credential Manager, never in plain files
- Wakuron only talks to your own mail servers (and Microsoft's sign-in for Outlook accounts),
  to GitHub for updates and bundles, and to the Python package index when installing

## Problems?

- **`wakuron` is not recognized:** open a *new* terminal. The installer adds Wakuron to your
  PATH, but terminals that were already open don't see it.
- **The installer can't find or install Python:** install Python 3.10+ from
  <https://www.python.org/downloads/> (tick *Add python.exe to PATH*) and run `install.cmd` again.
- **Something else:** run the command with `--help`, or open an issue in this repository.
