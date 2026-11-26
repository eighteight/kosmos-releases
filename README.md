# Kosmos for testers

Kosmos is an editor and media server for live shows. This page explains how to install it, start it, keep it up to date and report problems.

## What you need

- A Mac with Apple silicon (M1 or later). Intel Macs are not supported yet.
- macOS 12 Monterey or later.
- A tester licence. Each licence works on one Mac; how to get yours is below.

## Install

1. Open the [latest release](https://github.com/eighteight/kosmos-releases/releases/latest) and download `Kosmos-VERSION.dmg` from its Assets.
2. Double-click the dmg. A window opens with Kosmos and an Applications folder.
3. Drag **Kosmos** onto **Applications**, then eject the Kosmos disk (the ⏏ next to it in Finder's sidebar). Start Kosmos from Applications, not from the disk.
4. Open Kosmos. Apple has checked and notarised the build, so macOS asks once whether to open an app downloaded from the internet. Choose Open.

If macOS says Kosmos is damaged or cannot be checked, do not override it in System Settings. Delete the download, download it again from the release page, and tell the developer if the message comes back.

To check a download by hand, compare its checksum with the `.sha256` file next to it on the release page:

```bash
shasum -a 256 ~/Downloads/Kosmos-*.dmg
```

## Get a licence

The first time Kosmos starts, it shows a licence window instead of the editor.

1. Click **Copy Machine ID** and send the ID to the developer.
2. You will get back a file named like `licence.yaml`. Save it anywhere.
3. Start Kosmos, click **Open Licence File…** and choose that file. Kosmos keeps its own copy, so you can delete yours afterwards.

To see your licence later, or to replace it with a new one, choose **Help ▸ Kosmos Licence…**. Licences are tied to one Mac. If you move to a new Mac, send its machine ID and ask for a new licence.

## First steps

Kosmos opens with the **Operator Designer**, an example **Cue Graph** and the Kosmos navigator on the left.

- **Movies:** HAP is the best choice for clips you scrub or trim. ProRes plays through macOS's own decoder. H.264 plays, but scrubbing it is slow.
- **Cameras:** the first time a Video Input uses a camera, macOS asks whether *Kosmos Hardware* may use it. If you said no, allow it in System Settings ▸ Privacy & Security ▸ Camera, then choose **Check Camera Access** on the node.
- **NDI:** install the NDI Runtime from ndi.video. Kosmos looks for it in `/usr/local/lib` and in the NDI SDK folder, or you can point **Locate Backend** at `libndi.dylib`.
- **Syphon:** works with the Syphon framework in `/Library/Frameworks` and with any app that publishes a Syphon server.

Some features need Apple's developer tools. To install them, open Terminal and run:

```bash
xcode-select --install
```

- **Generate Show App** needs them.
- So do operators written in Python.
- Operators written in C++ also need CMake (`brew install cmake`).

Operators in JavaScript need nothing extra.

## Updates

Each new build appears on the [release page](https://github.com/eighteight/kosmos-releases/releases) with a list of what changed. To update:

1. Quit Kosmos.
2. Download the new dmg and open it.
3. Drag **Kosmos** onto **Applications** and choose Replace.

Your settings, licence and shows are kept, because they live outside the app.

Kosmos will later be able to check for updates and install them itself, from **Help ▸ Check for Updates…**.

## Reporting a problem

Please include:

- the Kosmos version, which is in the release's name and in the dmg's name;
- your Mac model and macOS version, from  ▸ About This Mac;
- what you did, what you expected and what happened instead;
- a screenshot, and the show file if you can share it;
- the logs, if possible: in Kosmos, open the command palette (⇧⌘P), run **Developer: Open Logs Folder**, and zip the newest folder.

## Where Kosmos keeps its files

| What | Where |
|---|---|
| Settings, window state, logs | `~/Library/Application Support/Kosmos` |
| Licence | `~/Library/Application Support/io.eight.eightpp/licence.yaml` |
| Editor extensions | `~/.kosmos-ide` |

To remove Kosmos completely, quit it, move Kosmos.app to the Trash, and remove these three items.
