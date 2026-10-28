# DEVBOYZ IDM DOWNLOADER

An independent, open-source desktop download manager with segmented HTTP(S) transfers and optional browser video capture. It is maintained by **Devboyz**.

This application is **not affiliated with Internet Download Manager** and is not a complete feature-for-feature replacement. It is inspired by features commonly found in download managers such as IDM.

> **Preview software:** Private/sign-in-required, DRM, and live media are unsupported. Please report bugs without sharing session tokens or signed media links.

## 📥 Download DEVBOYZ IDM DOWNLOADER

**Latest published version referenced here: `v0.2.0-preview.1`**

### Direct download

**[⬇️ Download DEVBOYZ IDM DOWNLOADER for Ubuntu/Linux (.deb)](https://github.com/sarkarabhay64/devboyz-idm-downloader/releases/download/v0.2.0-preview.1/DEVBOYZ-IDM-DOWNLOADER-0.2.0-preview.1-amd64.deb)**

| Platform | Package | Download |
|---|---|---|
| Ubuntu 22.04 / Debian, 64-bit | `.deb` installer | [Download Linux package](https://github.com/sarkarabhay64/devboyz-idm-downloader/releases/download/v0.2.0-preview.1/DEVBOYZ-IDM-DOWNLOADER-0.2.0-preview.1-amd64.deb) |
| Linux, 64-bit | AppImage | [Browse release assets](https://github.com/sarkarabhay64/devboyz-idm-downloader/releases/tag/v0.2.0-preview.1) |
| Windows 10/11, 64-bit | Installer / portable executable | [Browse release assets](https://github.com/sarkarabhay64/devboyz-idm-downloader/releases/tag/v0.2.0-preview.1) |
| All supported platforms | Checksums, if published | [Browse release assets](https://github.com/sarkarabhay64/devboyz-idm-downloader/releases/tag/v0.2.0-preview.1) |

The `.deb` link above is the direct URL supplied for the published release. AppImage, Windows, and checksum downloads are linked to the release page because their exact asset URLs have not been confirmed.

## Contact & Support

Need help using DEVBOYZ IDM DOWNLOADER, want to report a problem, or interested in customization? Contact Devboyz through WhatsApp.

**Maintained by:** Devboyz

**WhatsApp:** +91 81580 36375

**[Contact Devboyz on WhatsApp](https://wa.me/918158036375)**

The app does not send download history, browser credentials, filenames, or other private data to Devboyz. WhatsApp opens only when you choose the support link.

## Features

- HTTP(S) downloads with parallel ranges where the server supports them.
- Pause/resume for supported transfers, history, scheduling, and speed limits.
- Chrome/Edge media detection and quality selection; selected video/audio tracks are combined locally with FFmpeg.
- Download File Info with save location, category, Download Later, Start, and Cancel.
- Separate progress and completion windows, duplicate-active-download prevention.
- Linux x64 desktop packages (`.deb` and AppImage).
- Windows x64 NSIS installer and Electron portable `.exe`. Packaging is configured, but launch testing still requires Windows.

YouTube uses captured browser-session data and the GoogleVideo SABR transport library. This does not guarantee universal site support or DRM circumvention.

The legacy manual watch-URL resolver optionally uses `yt-dlp`; browser quality selection does not invoke it. Firefox YouTube capture has not reached parity.

## Supported systems

| Platform | Architecture | Status |
|---|---|---|
| Ubuntu 22.04 | x86_64 / amd64 | Desktop app and Linux packages are developed and tested here |
| Other Linux x64 | x86_64 | `.deb`/AppImage may run; only Ubuntu 22.04 is the documented test target |
| Windows 10/11 | x64 / amd64 | NSIS installer and portable `.exe` can be packaged; Windows launch testing is still required |
| macOS, ARM | — | Not part of this distribution |

## Install on Ubuntu 22.04 (amd64)

You do not need Node.js or npm to use a packaged build.

### Option 1: Download the Debian package

**[Download DEVBOYZ IDM DOWNLOADER (.deb)](https://github.com/sarkarabhay64/devboyz-idm-downloader/releases/download/v0.2.0-preview.1/DEVBOYZ-IDM-DOWNLOADER-0.2.0-preview.1-amd64.deb)**

After downloading, open a terminal in the download directory and run:

```bash
sudo apt install ./DEVBOYZ-IDM-DOWNLOADER-0.2.0-preview.1-amd64.deb
```

Launch **DEVBOYZ IDM DOWNLOADER** from the applications menu, or run:

```bash
devboyz-idm-downloader
```

To uninstall:

```bash
sudo apt remove devboyz-idm-downloader
```

Uninstalling does not delete `~/.awesome-downloader` or files you downloaded.

### Option 2: AppImage

Visit the [GitHub release page](https://github.com/sarkarabhay64/devboyz-idm-downloader/releases/tag/v0.2.0-preview.1) to check whether an AppImage is available.

After downloading the file, run:

```bash
chmod +x DEVBOYZ-IDM-DOWNLOADER-0.2.0-preview.1-x86_64.AppImage
./DEVBOYZ-IDM-DOWNLOADER-0.2.0-preview.1-x86_64.AppImage
```

Running an AppImage typically needs FUSE (`libfuse2` on Ubuntu 22.04). If FUSE is unavailable, extract and run the payload with:

```bash
./DEVBOYZ-IDM-DOWNLOADER-*.AppImage --appimage-extract-and-run
```

### Downloading other release assets

Visit the [v0.2.0-preview.1 release page](https://github.com/sarkarabhay64/devboyz-idm-downloader/releases/tag/v0.2.0-preview.1) for available downloads.

Expected asset names, if published:

- Ubuntu/Linux: `DEVBOYZ-IDM-DOWNLOADER-0.2.0-preview.1-amd64.deb`
- Portable Linux: `DEVBOYZ-IDM-DOWNLOADER-0.2.0-preview.1-x86_64.AppImage`
- Windows installer: `DEVBOYZ-IDM-DOWNLOADER-Setup.exe`
- Windows portable: `DEVBOYZ-IDM-DOWNLOADER-Portable.exe`
- Checksums: `SHA256SUMS.txt`

See [docs/INSTALL.md](docs/INSTALL.md) for usage and browser setup.

## Browser integration

Browser integration is **optional**. The desktop app downloads HTTP(S) files without any extension.

Chrome/Edge unpacked-extension setup writes Linux native-messaging manifests.

**Linux Chrome/Edge/Firefox end-to-end capture has not been verified in a full browser session in this distribution.** Do not treat store listings, silent installation, or Firefox YouTube parity as available.

Native messaging still uses the host name `com.awesome.downloader` so existing connectors keep working. Application data remains in `~/.awesome-downloader`.

## Develop

On Ubuntu 22.04 x64 with Node.js 22+:

```bash
npm ci
npm test
npm start
```

`npm start` launches the Electron desktop app. Linux startup does not invoke the Windows C# compiler. Browser integration is optional.

```bash
npm run package:linux
npm run dist:linux
bash scripts/build-linux.sh
bash scripts/prepare-windows-resources.sh
npm run dist:win
bash scripts/assemble-windows-release.sh
bash scripts/pack-github-source.sh
bash scripts/assemble-release.sh
```

See [docs/RELEASING.md](docs/RELEASING.md) before distributing binaries.

Current builds are unsigned and have no auto-updater.

The optional legacy extractor is described in [THIRD-PARTY.md](THIRD-PARTY.md). Do not commit its executable.

## Known limitations

- Preview software: DRM, private/sign-in-required media, and live streams are unsupported.
- Linux browser video capture is implemented but not fully verified here.
- Firefox YouTube capture has not reached Chrome/Edge parity.
- Packages are unsigned. There is no automatic updater.
- AppImage launch on Ubuntu 22.04 typically needs `libfuse2`.
- Website grabber projects are not available; use Add URL for HTTP(S) links.
- Windows packages are unsigned and have not been launch-tested from Ubuntu.
- macOS installers are not shipped.

## Privacy and security

Media request credentials are held in memory, not stored in download history.

History and browser-integration configuration are stored locally in `~/.awesome-downloader`. The bridge is authenticated and loopback-only.

Do not publish this directory or browser profiles in issues.

Vulnerability reports: see [SECURITY.md](SECURITY.md).

## Original Project and Attribution

This project originated from [Ahmadkhattak1's Awesome Downloader](https://github.com/Ahmadkhattak1/awesome-downloader).

The Devboyz distribution includes subsequent modifications: Linux compatibility, packaging, branding, documentation, WhatsApp support entry points, and other changes made in this working tree. The original authors and contributors retain credit for their respective work. This distribution is independently maintained by Devboyz.

Do not push Devboyz changes to the original author's repository.

## Contribute

Start with [docs/CONTRIBUTOR-START-HERE.md](docs/CONTRIBUTOR-START-HERE.md), [CONTRIBUTING.md](CONTRIBUTING.md), and [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).

Bug reports and pull requests are welcome. Use the GitHub issue templates in `.github/ISSUE_TEMPLATE/`.

Do not include cookies, tokens, signed media URLs, browser profiles, or `~/.awesome-downloader` contents.

## License

Original project code is [MIT licensed](LICENSE). Third-party components retain their own licenses, including GPL-covered FFmpeg components; see [THIRD-PARTY.md](THIRD-PARTY.md).

Proprietary binaries, extracted evidence, local research, and test screenshots are not part of the public source.

Only download content you are permitted to save.
