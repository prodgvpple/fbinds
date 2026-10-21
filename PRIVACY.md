# Privacy

fbinds has to see your key presses to remap them. This page explains exactly what it does with them, and with everything else it touches.

**Short version:** fbinds never records, stores or sends what you type. It has no accounts, no analytics and no telemetry. The only network request it makes is a check for new versions on GitHub.

## Your key presses

- fbinds installs a global keyboard hook (SharpHook). Like every global shortcut tool, the hook receives every key press, in any app.
- fbinds only acts on a key press when FL Studio is focused and remapping is not paused. It then compares the press with your mappings in memory, and forgets it.
- To handle combos, fbinds keeps track of the keys currently held down. That list lives in memory only and is cleared when the keys are released or FL Studio loses focus.
- The keys currently held down are shown in the "INPUT" bar of the fbinds window as feedback. Nothing from it is saved.
- Key presses are never written to disk, never written to the log, and never sent anywhere.

## What fbinds stores on your computer

Everything lives in one folder: `%APPDATA%\fbinds` (Windows) or `~/Library/Application Support/fbinds` (macOS). "More → Open settings & logs folder" opens it.

| File | Contents |
| --- | --- |
| `settings.json` | Shortcuts you customized, the Override setting, and keyboard layout labels |
| `fbinds.log` | Startup lines (app version, OS version), pause/resume, and errors |

**Keyboard layout labels** are the characters your keyboard layout produces for each physical key (for example, that the key left of Enter types `ù` on your layout). fbinds learns them from unmodified key presses while its own window is focused, so it can display shortcuts the way your keyboard is labelled. They describe your layout, not anything you typed.

When "Launch at login" is on, fbinds also adds a standard login entry: the `fbinds` value under `HKCU\Software\Microsoft\Windows\CurrentVersion\Run` (Windows) or `~/Library/LaunchAgents/com.gapple.fbinds.plist` (macOS).

Exported profiles (`.fbinds` files) contain the same data as `settings.json` and are saved only where you choose.

## Detecting FL Studio

About once per second, fbinds asks the operating system which program owns the focused window and compares its process name with FL Studio's. It does not read window titles or window contents, and it does not store the result. On Windows this uses the standard foreground-window API; on macOS, `lsappinfo`.

## Network

- **Update check:** a few seconds after launch, fbinds requests `https://api.github.com/repos/prodgvpple/fbinds/releases/latest` to see whether a newer version exists. Like any web request, this exposes your IP address and the app version (in the `User-Agent` header) to GitHub. [GitHub's privacy statement](https://docs.github.com/site-policy/privacy-policies/github-general-privacy-statement) applies to that request. No other data is sent.
- **Links:** the website, download page and `@prodgvpple` links open in your browser only when you click them.

Nothing else leaves your computer.

## System permissions

- **macOS:** Accessibility access, which macOS requires for any app that reads or simulates key presses system-wide.
- **Windows:** no special permission.

## Contact

Questions about privacy: contact@prodgvpple.com
