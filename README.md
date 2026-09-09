# VA Pharmacy Automation

AutoHotkey v2 automation supporting selected Oracle Health / Cerner retail pharmacy workflows through Citrix.

## Download

Open the [latest GitHub Release](https://github.com/aaronbridges128/VA-Pharmacy-Automation/releases/latest) and download the attached file named `VA-Pharmacy-Automation-vX.Y.Z.zip`.

Do **not** download GitHub's automatically generated **Source code (zip)** or **Source code (tar.gz)** files. Those are not the tested installation package.

## Requirements

- Windows
- [AutoHotkey v2.0.18 or later](https://www.autohotkey.com/)
- A compatible Oracle Health / Cerner Medication Manager Retail environment delivered through Citrix
- The locally validated Oracle layout, display scaling, and permissions required by your pharmacy

## Installation

1. Open the latest release page.
2. Download the attached `VA-Pharmacy-Automation-vX.Y.Z.zip` file.
3. Extract the ZIP into a permanent folder where you have write access.
4. Keep the extracted folder structure intact.
5. Run `Scripts.ahk` with AutoHotkey v2.

Do not copy `Scripts.ahk` by itself. It loads required modules from the `Core`, `Citrix`, `Domain`, `MMR`, `Workflows`, and `UI` folders.

## Updating

The Pharmacy Console checks this public repository for a newer stable GitHub Release after the Console first opens. It performs at most one automatic check per application session, and an offline computer or unavailable GitHub service does not affect pharmacy workflows.

When a newer release exists, the Console shows **Update available** and a **View Update** button. That button only opens the exact release page in your normal browser. The automation never silently downloads, installs, replaces, or executes files from the Internet. Download the new attached release ZIP and install it manually.

## Major features

- Single-prescription Window, USPS, Priority Mail, UPSG, Discharge, On File, and On Hold actions
- Bridge Supply quantity and routing workflows
- Smart Refill date and disposition assistance
- Smart SIG conversion for explicitly supported instruction patterns
- Window, USPS, and UPSG batch refill processing
- Pharmacy Console for workflow launch, status, diagnostics, and update notification
- PowerChart PDMP documentation workflow that leaves the note open for pharmacist review and signing
- Deterministic Smart Route rule infrastructure that remains fail-closed until its local selected-refill acquisition mapping is configured and validated

All Oracle input is guarded by the application's validated Citrix context and workflow boundaries. The operator remains responsible for confirming the correct patient, prescription, values, and final Oracle result.

## Hotkeys

These bindings come from the distributed `UI/Hotkeys.ahk` module.

| Hotkey | Action |
| --- | --- |
| `Ctrl+Alt+B` | Open the Bridge Supply chooser |
| `Ctrl+Alt+D` | Run Discharge |
| `Ctrl+Alt+W` | Run Window |
| `Ctrl+Alt+F` | Set On File |
| `Ctrl+Alt+H` | Set On Hold |
| `Ctrl+Alt+M` | Run USPS |
| `Ctrl+Alt+P` | Run Priority Mail (Local Regular Mail + Priority) |
| `Ctrl+Alt+U` | Run UPSG |
| `Ctrl+Alt+R` | Run Smart Route (only when locally configured) |
| `Ctrl+Alt+S` | Run Smart SIG |
| `Ctrl+Alt+X` | Run Smart Refill |
| `Ctrl+Alt+Shift+W` | Batch queued refills as Window |
| `Ctrl+Alt+Shift+M` | Batch queued refills as USPS |
| `Ctrl+Alt+Shift+U` | Batch queued refills as UPSG |
| `Ctrl+Alt+Pause` | Request cooperative workflow abort |
| `Ctrl+Alt+I` | Open read-only diagnostics |
| `Ctrl+Alt+Space` | Open or raise the Pharmacy Console |
| `Ctrl+Alt+Esc` | Exit the application |

## Troubleshooting

- If a hotkey is blocked, return to the expected Oracle/Citrix screen and confirm no other workflow is active.
- If a workflow stops, read the stable error code shown by the application and use **Diagnostics** from the Console or tray menu. Do not include patient information in an issue report.
- If the Pharmacy Console says `Latest: unavailable`, continue working normally and try the release page later. Update availability never controls prescription automation.
- If the script does not start, confirm AutoHotkey v2.0.18 or later is installed and that the complete extracted folder is present.
- If your Oracle layout, Citrix scaling, or field positions differ, do not guess new coordinates. Stop using the affected workflow until it has been validated for that environment.

## Project status

This is an independently maintained pharmacy workflow automation project. It is not an official product of the U.S. Department of Veterans Affairs, Oracle, Oracle Health, or Citrix. It does not provide clinical decision-making, and local authorization and validation remain required before production use.

This public repository is the download and issue-reporting surface. Development occurs in a separate private source repository; development history is intentionally not published here.
