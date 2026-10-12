# Bluey for iPhone + Windows

This project keeps the original native SwiftUI iPhone app from [rileybrown101010/bluey-by-riley](https://github.com/rbrown101010/bluey-by-riley) and adds a Windows companion that speaks its Bonjour and newline-delimited JSON protocol. The phone discovers the PC automatically; there is no manual IP or pairing-token screen.

## Start here

1. Install [GitHub Desktop](https://desktop.github.com/) if needed. On GitHub, create a private repository in your account (recommended), or make a public fork if you are comfortable with that copy being visible. The original repository belongs to its author; do not push to it.
2. Clone that repository with GitHub Desktop, extract this ZIP directly into the cloned repository folder (replace matching files), then use GitHub Desktop to commit and push the changes to **your repository**.
3. In your repository, open **Actions → Build Bluey iPhone IPA → Run workflow**. A GitHub-hosted macOS runner builds an **unsigned** iPhone IPA. No Apple ID or signing key is stored in GitHub.
4. Download the workflow artifact and follow [the Windows + iPhone sideload guide](docs/ios-sideloading.md) to install AltStore and Bluey.
5. On the Windows PC, stop the earlier Pip demo server with Ctrl+C if it is running, then open `Windows/run_bluey.bat`. Keep this console window open. On the iPhone, open Bluey and allow Local Network and Microphone access.

The Windows host advertises `_googly._tcp`, streams mouse gaze to the phone, mints short-lived OpenAI Realtime client secrets, receives tool requests, and saves Bluey session notes under `Documents\Bluey Notes`.

## Requirements and privacy

- Windows 10/11 and Python 3.11 or newer.
- PC and iPhone on the same trusted private Wi-Fi.
- Your own OpenAI API key for voice, screen assistance, web research, and audio transcription (a ChatGPT sign-in alone is not an API key; OpenAI API usage may be billed separately). On first launch, the console offers to save it to Windows Credential Manager. Never put the key in this repo or send it in chat.

If Windows Firewall asks, allow the host on **Private networks only**. Do not forward its port on your router, and do not run it on public or untrusted Wi-Fi. The original Bluey wire protocol has no pairing password or transport encryption; local-network trust is the boundary. Microphone audio and screenshots requested by Bluey are sent to OpenAI for the relevant features. The phone records audio while awake; the PC saves audio chunks and session notes locally under `Documents\Bluey Notes`.

The native iPhone face, voice UI, transcripts, sessions, and Bonjour discovery remain from the original app. The Windows port supports cursor following, screenshot-based screen help, coordinate-based click/type/scroll/drag, app/URL opening, web research, diarized transcription, and notes. This first Windows port does **not** provide OCR labels for screen words or the macOS version's floating animated Bluey cursor overlay; it uses the Windows pointer and screen-grid coordinates instead. Typing fails closed if Windows UI Automation cannot verify that the focused field is not a password field.

To disable computer actions, set `BLUEY_DISABLE_CONTROL=1` before starting Bluey. To pause actions for six seconds, type `STOP` in the companion console. `Ctrl+C` or `EXIT` stops the host.

See [Windows host details](Windows/README.md) and [iPhone build/sideload steps](docs/ios-sideloading.md).

## Source and license

The iPhone UI and shared protocol are from the original Bluey project, released under the Unlicense. The Windows host and CI workflow in this package are additions. The original macOS host remains in `Mac/` for reference; it is not used by the Windows setup.
