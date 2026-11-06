<p align="center">
  <img src="assets/icon.svg" width="72" alt="">
</p>
<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/logo-on-dark.svg">
    <img src="assets/logo-on-light.svg" width="300" alt="GAMPEON">
  </picture>
</p>

<p align="center">
  <b>The GAMPEON launcher for Windows.</b><br>
  Play GAMPEON games and talk with your communities.
</p>

<p align="center">
  <a href="https://github.com/gampeon/launcher-releases/releases/latest"><b>Download the latest version</b></a>
  ·
  <a href="https://gampeon.com">gampeon.com</a>
  ·
  <a href="https://gampeon.com/changelog/">Changelog</a>
</p>

---

> **Early preview.** The launcher is in an early test phase. Things change quickly and some features are still missing. For example, the launcher doesn't download games yet: the first time you press Play, you choose the GAMPEON client (`GampeonClient.exe`) from the folder you installed it in.

This repository only hosts the release builds of the launcher. Once installed, the launcher keeps itself up to date from here.

## Install

You need Windows 10 or 11 (64-bit) and an internet connection.

1. Open the [latest release](https://github.com/gampeon/launcher-releases/releases/latest) and download `GAMPEON_<version>_x64-setup.exe`.
2. Run it. The launcher installs for your Windows user only, so you don't need administrator rights. If the WebView2 runtime is missing on your PC, the installer downloads it for you.
3. Windows may show **"Windows protected your PC"**. This happens because the installer doesn't have a Windows code signature yet. We're working on it. If you downloaded the file from this page, click **More info**, then **Run anyway**.
4. Start GAMPEON and sign in. The launcher opens gampeon.com in your browser. Sign in there (or create an account), and your browser sends you back to the launcher.

## What's inside

- **Home:** continue playing, your library, popular games, and a page for every game with its servers and a big Play button.
- **Communities:** studios and projects can have their own community right inside the launcher, with channels, roles, permissions, invites and moderation tools.
- **Links:** `gampeon://` links and invites like `gampeon.com/invite/<code>` open the right place in the launcher. A link never starts a game on its own.
- **Automatic updates:** see below.

## Updates

The launcher checks for a new version when it starts and every 6 hours, and downloads it in the background. When it's ready, a **Restart to update** button appears at the bottom of the left bar. Click it whenever it suits you: the launcher closes, installs the update and starts again. You can also check by hand in **Settings → Updates → Check now**.

Every update is signed with the GAMPEON update key. The launcher checks that signature before it installs anything and never runs a file that doesn't match.

Each release contains three files:

| File | What it is |
|---|---|
| `GAMPEON_<version>_x64-setup.exe` | The installer. Use it for a new install. |
| `GAMPEON_<version>_x64-setup.exe.sig` | The signature of the installer. |
| `latest.json` | The update feed the launcher reads. |

## Check a download (optional)

You can check that an installer really comes from GAMPEON with [minisign](https://jedisct1.github.io/minisign/). The `.sig` file is a base64-encoded minisign signature. Our public update key is in [`gampeon-updates.pub`](gampeon-updates.pub):

```
untrusted comment: minisign public key: E004C14CAE13D187
RWSH0ROuTMEE4Bl4SCy8jab5DAgDHrHr6WFtra5LvWO8gi4YFJJsxRrC
```

Download the installer and its `.sig` into the same folder, then run:

**Windows (PowerShell)**

```powershell
$exe = "GAMPEON_0.2.1_x64-setup.exe"   # the file you downloaded
[IO.File]::WriteAllBytes("$PWD\$exe.minisig", [Convert]::FromBase64String((Get-Content "$exe.sig" -Raw)))
minisign -Vm $exe -x "$exe.minisig" -P RWSH0ROuTMEE4Bl4SCy8jab5DAgDHrHr6WFtra5LvWO8gi4YFJJsxRrC
```

**Linux or macOS**

```sh
exe=GAMPEON_0.2.1_x64-setup.exe   # the file you downloaded
base64 -d "$exe.sig" > "$exe.minisig"
minisign -Vm "$exe" -x "$exe.minisig" -P RWSH0ROuTMEE4Bl4SCy8jab5DAgDHrHr6WFtra5LvWO8gi4YFJJsxRrC
```

A good file prints `Signature and comment signature verified`, followed by a trusted comment with the file name and version. Anything else means: don't run it.

This signature is separate from the Windows code signature mentioned above, which is still to come.

## Your data

The launcher keeps your sign-in in the Windows Credential Manager. It talks to the GAMPEON servers and checks this repository on GitHub for updates. Details are in our [Privacy Policy](https://gampeon.com/privacy).

## Uninstall

Go to Windows **Settings → Apps → Installed apps**, find **GAMPEON** and choose **Uninstall**. Your GAMPEON account isn't affected. To remove your saved sign-in as well, choose **Log out** in the launcher settings first.

## Help and feedback

- News, help and your account: [gampeon.com](https://gampeon.com)
- Bugs and feedback: [hello@gampeon.com](mailto:hello@gampeon.com)
- Security problems: please email [security@gampeon.com](mailto:security@gampeon.com) instead of posting them in public.

## License

Copyright © 2026 Gampeon, Inc. All rights reserved. The launcher is not open source. Its use is subject to the GAMPEON [Terms of Service](https://gampeon.com/terms).

<p align="center"><sub>Created by <a href="https://gampeon-studios.com">GAMPEON Studios</a></sub></p>
