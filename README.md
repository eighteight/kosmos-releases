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

To try Kosmos before you have a licence, click **Start 30-Day Trial**. The trial has every feature and lasts 30 days from today, today included, or 60 launches of Kosmos, whichever comes first. Reloading a window does not count as a launch. Each Mac gets one trial, which cannot be restarted. Kosmos shows the days and launches left each time it starts. While on trial and online, Kosmos asks api.github.com for today's date, so changing your Mac's clock does not extend it. When the trial ends, the licence window comes back. A show that is running is never stopped. Show apps made with Kosmos open on this Mac during the trial; on another Mac they need a licence.

To get a licence:

1. Click **Copy Machine ID** and send the ID to the developer.
2. You will get back a file named like `licence.yaml`. Save it anywhere.
3. Start Kosmos, click **Open Licence File…** and choose that file. Kosmos keeps its own copy, so you can delete yours afterwards.

To see your licence later, or to replace it with a new one, choose **Help ▸ Kosmos Licence…**. Licences are tied to one Mac. If you move to a new Mac, send its machine ID and ask for a new licence.

## First steps

Kosmos opens with the **Operator Designer**, the **Rocket Science Demo** and the Kosmos navigator on the left. The demo has four cues: **Movie**, **Audio**, **GLSL** (a space shader) and **Camera**. The first time it opens, Kosmos makes the demo's movie and sound on your Mac, which takes a few seconds. Press **Run**, then **Space** for the next cue. In the Camera cue, choose your camera in the Video Input node's **Source**.

- **Movies:** HAP is the best choice for clips you scrub or trim. ProRes plays through macOS's own decoder. H.264 plays, but scrubbing it is slow.
- **Cameras:** the first time a Video Input uses a camera, macOS asks whether *Kosmos Hardware* may use it. If you said no, allow it in System Settings ▸ Privacy & Security ▸ Camera, then choose **Check Camera Access** on the node.
- **NDI®:** works without installing anything, because Kosmos includes the NDI runtime. To use a different NDI runtime, point **Locate Backend** on the Video Input node at its `libndi.dylib`. More about NDI, and NDI's free tools, at [ndi.video](https://ndi.video/).
- **Syphon:** works without installing anything, because Kosmos includes the Syphon framework; it receives from any app that publishes a Syphon server. To use a different Syphon.framework, point **Locate Backend** at it.

Some features need Apple's developer tools. To install them, open Terminal and run:

```bash
xcode-select --install
```

- **Generate Show App** needs them.
- So do operators written in Python.
- Operators written in C++ also need CMake (`brew install cmake`).

Operators in JavaScript need nothing extra.

## Terms of use

Kosmos is pre-release software lent to you for testing. By installing it you agree to these terms.

- Kosmos includes the NDI® runtime by Vizrt NDI AB, under the NDI SDK licence. Its copyright and licence notices are in **Help ▸ About Kosmos… ▸ Third-Party Notices**.
- Kosmos includes Syphon.framework, copyright 2010 bangnoise (Tom Butterworth) & vade (Anton Marini), under its BSD licence, whose full text, with its disclaimer, is in the same place.
- You may not modify, reverse engineer, disassemble or recompile the NDI software in Kosmos, or the protocols it uses over a network or on the computer, and you may not try to. You may not get around its technical limitations, or remove, hide or change its proprietary notices and labels.
- Kosmos, and the NDI software in it, are provided "as is", without any warranty from the developer, from Vizrt NDI AB or from their licensors. As far as the law allows, none of them is liable for any damage, direct, indirect, incidental or consequential, that comes from using Kosmos.
- You will comply with the export laws and regulations of the United States and will not export Kosmos, or any part of it, in breach of them.
- If you write software that uses NDI through Kosmos, it must comply with the NDI SDK licence, work fully with current NDI, and pass these terms on in its own licence agreement.

## Updates

Kosmos checks for a new version once a day while it is open, and tells you when one is ready. To check now, choose **Help ▸ Check for Updates…**. Choose **Install and Restart**: Kosmos downloads the new version, checks that it is the genuine, notarised Kosmos, asks to save any unsaved work, quits, replaces itself and opens again. **Release Notes** shows what changed, and **Skip This Version** stops the reminders until a newer one appears.

Kosmos can only replace itself when it is in a folder you can change, such as Applications, and not when it was opened from the dmg; if it cannot, it says what to do. To stop the daily check, open Preferences, search for **Kosmos: Check For Updates** and turn it off.

You can also update by hand from the [release page](https://github.com/eighteight/kosmos-releases/releases), where each build is listed with what changed:

1. Quit Kosmos.
2. Download the new dmg and open it.
3. Drag **Kosmos** onto **Applications** and choose Replace.

Your settings, licence and shows are kept either way, because they live outside the app. If an update goes wrong, `~/Library/Logs/Kosmos/update.log` says why; please include it in your report.

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
| Licence, trial record | `~/Library/Application Support/io.eight.eightpp` |
| Second copy of the trial record | `~/Library/Preferences/io.eight.eightpp.trial.yaml` |
| Editor extensions | `~/.kosmos-ide` |

To remove Kosmos completely, quit it, move Kosmos.app to the Trash, and remove these four items.

---

NDI® is a registered trademark of Vizrt NDI AB.
