# DEVBOYZ IDM DOWNLOADER

An independent, open-source desktop download manager with segmented HTTP(S)
transfers and optional browser video capture. It is maintained by **Devboyz**.

This application is **not** affiliated with Internet Download Manager and is
**not** a complete feature-for-feature replacement. It is inspired by features
commonly found in download managers such as IDM.

**Preview software:** Private/sign-in-required, DRM, and live media are
unsupported. Please report bugs without sharing session tokens or signed media
links.

## Contact & Support

Need help using DEVBOYZ IDM DOWNLOADER, want to report a problem, or interested
in customization? Contact Devboyz through WhatsApp.

**Maintained by:** Devboyz

**WhatsApp:** +91 81580 36375

**Contact link:** [https://wa.me/918158036375](https://wa.me/918158036375)

The app does not send download history, browser credentials, filenames, or other
private data to Devboyz. WhatsApp opens only when you choose the support link.

## Features

- HTTP(S) downloads with parallel ranges where the server supports them.
- Pause/resume for supported transfers, history, scheduling, and speed limits.
- Chrome/Edge media detection and quality selection; selected video/audio tracks
  are combined locally with FFmpeg.
- Download File Info with save location, category, Download Later, Start, and Cancel.
- Separate progress and completion windows, duplicate-active-download prevention.
- Linux x64 desktop packages (`.deb` and AppImage).
- Windows x64 NSIS installer and Electron portable `.exe` (packaging is configured; launch testing still requires Windows).

YouTube uses captured browser-session data and the GoogleVideo SABR transport
library. It is not a promise of universal site support or DRM circumvention.
The legacy manual watch-URL resolver optionally uses yt-dlp; browser quality
selection does not invoke it. Firefox YouTube capture has not reached parity.

## Supported systems

| Platform | Architecture | Status |
| --- | --- | --- |
| Ubuntu 22.04 | x86_64 / amd64 | Desktop app and Linux packages are developed and tested here |
| Other Linux x64 | x86_64 | `.deb`/AppImage may run; only Ubuntu 22.04 is the documented test target |
| Windows 10/11 | x64 / amd64 | NSIS installer and portable `.exe` can be packaged; they still need Windows launch testing |
| macOS, ARM | — | Not part of this distribution |

## Install on Ubuntu 22.04 (amd64)

You do not need Node.js or npm to use a packaged build.

### Debian package

After a local or CI Linux build, the installer is:

`release/DEVBOYZ-IDM-DOWNLOADER-<version>-amd64.deb`

```bash
sudo apt install ./DEVBOYZ-IDM-DOWNLOADER-0.2.0-preview.1-amd64.deb
```

Then launch **DEVBOYZ IDM DOWNLOADER** from the application menu, or run
`devboyz-idm-downloader`.

Remove with:

```bash
sudo apt remove devboyz-idm-downloader
```

Uninstall does not delete `~/.awesome-downloader` or files you downloaded.

### AppImage

After a local or CI Linux build, the AppImage is:

`release/DEVBOYZ-IDM-DOWNLOADER-<version>-x86_64.AppImage`

```bash
chmod +x DEVBOYZ-IDM-DOWNLOADER-0.2.0-preview.1-x86_64.AppImage
./DEVBOYZ-IDM-DOWNLOADER-0.2.0-preview.1-x86_64.AppImage
```

Running an AppImage typically needs FUSE (`libfuse2` on Ubuntu 22.04). If FUSE
is unavailable, extract and run the payload with
`./DEVBOYZ-IDM-DOWNLOADER-*.AppImage --appimage-extract-and-run`.

### Downloading release assets

After you publish a GitHub Release on the intended repository
(`https://github.com/devboyz/idm-downloader`, once that repository exists),
download these files from the release page:

- Ubuntu users: `DEVBOYZ-IDM-DOWNLOADER-<version>-amd64.deb`
- Portable Linux: `DEVBOYZ-IDM-DOWNLOADER-<version>-x86_64.AppImage`
- Windows installer: `DEVBOYZ-IDM-DOWNLOADER-Setup.exe`
- Windows portable: `DEVBOYZ-IDM-DOWNLOADER-Portable.exe`
- Checksums: `SHA256SUMS.txt`

Do not assume those GitHub download URLs exist until you upload the assets
yourself. This project does not auto-publish releases.

See [docs/INSTALL.md](docs/INSTALL.md) for usage and browser setup.

## Browser integration

Browser integration is **optional**. The desktop app downloads HTTP(S) files
without any extension.

Chrome/Edge unpacked-extension setup writes Linux native-messaging manifests.
**Linux Chrome/Edge/Firefox end-to-end capture has not been verified in a full
browser session in this distribution.** Do not treat store listing, silent
install, or Firefox YouTube parity as available.

Native messaging still uses the host name `com.awesome.downloader` so existing
connectors keep working. Application data remains in `~/.awesome-downloader`.

## Develop

On Ubuntu 22.04 x64 with Node.js 22+:

```bash
npm ci
npm test
npm start
```

`npm start` launches the Electron desktop app. Linux startup does not invoke
the Windows C# compiler. Browser integration is optional.

```bash
npm run package:linux        # unpacked Linux directory
npm run dist:linux           # AppImage and .deb (x64), does not publish
bash scripts/build-linux.sh  # npm ci, tests, then Linux packages
bash scripts/prepare-windows-resources.sh
npm run dist:win             # NSIS + portable .exe into release-windows/
bash scripts/assemble-windows-release.sh
bash scripts/pack-github-source.sh
bash scripts/assemble-release.sh
```

See [docs/RELEASING.md](docs/RELEASING.md) before distributing binaries.
Current builds are unsigned and have no auto-updater.

The optional legacy extractor is described in [THIRD-PARTY.md](THIRD-PARTY.md).
Do not commit its executable.

## Known limitations

- Preview software: DRM, private/sign-in-required media, and live streams are
  unsupported.
- Linux browser video capture is implemented but not fully verified here.
- Firefox YouTube capture has not reached Chrome/Edge parity.
- Packages are unsigned. There is no automatic updater.
- AppImage launch on Ubuntu 22.04 typically needs `libfuse2`.
- Website grabber projects are not available; use Add URL for HTTP(S) links.
- Windows packages are unsigned and have not been launch-tested from Ubuntu.
- macOS installers are not shipped.

## Privacy and security

Media request credentials are held in memory, not stored in download history.
History and browser-integration configuration are stored locally in
`~/.awesome-downloader`. The bridge is
authenticated and loopback-only. Do not publish this directory or browser
profiles in issues.

Vulnerability reports: see [SECURITY.md](SECURITY.md).

## Original Project and Attribution

This project originated from
[Ahmadkhattak1’s Awesome Downloader](https://github.com/Ahmadkhattak1/awesome-downloader).

The Devboyz distribution includes subsequent modifications: Linux compatibility,
packaging, branding, documentation, WhatsApp support entry points, and other
changes made in this working tree. The original authors and contributors retain
credit for their respective work. This distribution is independently maintained
by Devboyz.

Do not push Devboyz changes to the original author’s repository.

## Contribute

Start with [docs/CONTRIBUTOR-START-HERE.md](docs/CONTRIBUTOR-START-HERE.md),
[CONTRIBUTING.md](CONTRIBUTING.md), and [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).

Bug reports and pull requests are welcome once a public Devboyz repository is
published. Use the GitHub issue templates in `.github/ISSUE_TEMPLATE/`. Do not
include cookies, tokens, signed media URLs, browser profiles, or
`~/.awesome-downloader` contents.

The intended publication target is
`https://github.com/devboyz/idm-downloader` — that repository is **not**
assumed to exist until the maintainer creates and publishes it.

## License

Original project code is [MIT licensed](LICENSE). Third-party components retain
their own licenses, including GPL-covered FFmpeg components; see
[THIRD-PARTY.md](THIRD-PARTY.md). Proprietary binaries, extracted evidence, local
research and test screenshots are not part of the public source.
Only download content you are permitted to save.
# devboyz-idm-downloader
