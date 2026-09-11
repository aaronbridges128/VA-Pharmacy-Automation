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

Do not copy `Scripts.ahk` by itself. It loads required modules from the `Core`, `Citrix`, `Domain`, `MMR`, `Workflows`, `UI`, and `Data` folders.

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

## Smart SIG

Smart SIG (`Ctrl+Alt+S`) recognizes a complete dosing prefix and looks up its exact semantic key in a validated external library. The only shipped approved mapping is **TAKE 1 TABLET BY MOUTH DAILY -> `T1 PO D`**, Source `USER_CONFIRMED`. Spaces are part of the literal output. There is no token composition, form-character emission, template expansion, wildcard, or fallback. BID, PRN, half-dose, capsule, nasal, bedtime and other recognized combinations have no approved default and make no changes.

The existing New Order/Refill entry, bound prescription and commit guards remain. SIG uses qualified client coordinate `74,118`; Instructions uses `270,386`. The workflow captures Instructions, resolves one pinned library generation, offers genuine residual text through **Include Instructions / Do Not Include Instructions / Cancel**, revalidates the bound prescription, writes the exact SIG and commits with Tab, then updates or clears Instructions. Cancel, Escape, close, no mapping, ambiguity, invalid active library or a changed generation before writing leave both fields unchanged. Smart SIG does not submit the order or populate other fields. A partially transmitted SIG operation cannot be rolled back: failure stops processing and preserves Instructions. A subsequent Instructions failure reports `SMART_SIG_INSTRUCTIONS_UPDATE_FAILED`.

Residual source offsets, parentheses, whitespace handling and sentence-case conversion of all-uppercase residual text are preserved. Unconsumed dosing qualifiers such as may increase/decrease, hold if, breakthrough dosing, unresolved as directed, alternate schedules, late PRN/duration and unknown PRN indications fail closed. Ordinary strength-change notes and bridge markers may use the chooser. The finite parser does not understand arbitrary prose.

### Editing and reloading

**Open Console -> SIG Library -> Open Library -> add an approved row -> save -> Reload Library -> read the result.** Oracle need not be running. Open Library creates only a header if the user file is absent, never replaces an existing file, and opens its associated application (Notepad fallback). Both utilities are blocked during a workflow/reload. New mappings for already recognized semantics require no source edit or restart; new parser vocabulary requires a separate code change.

- Distributed, reviewed defaults: `Data/SmartSigLibrary.default.tsv`.
- Local additions: `Data/SmartSigLibrary.user.tsv`, ignored by Git and excluded from releases.
- Paths are relative to the installation folder, independent of the working directory.
- Save UTF-8 (with or without BOM), or BOM-marked UTF-16LE, tab-delimited text. Import all spreadsheet columns as text. Do not save XLSX or CSV under a TSV filename. Dates such as a spreadsheet-converted `1-2`, scientific notation and formulas are rejected.
- Preserve the exact 14-column header and empty cells. LF/CRLF and a missing final newline are supported; empty lines after the header are ignored. Optional quoted cells may use doubled quotes. Embedded tabs/newlines and control characters are rejected. Limits: 1 MiB and 10,000 data rows per file.

### Schema version 1

| Column | Contract |
| --- | --- |
| SchemaVersion | Exactly `1` |
| Enabled | Exactly `0` or `1` |
| Id | Unique lowercase ASCII identifier, `[a-z][a-z0-9_]*`, maximum 64 characters |
| Action, Quantity, Form, Route, Frequency | Exact canonical semantic values from the vocabulary below; quantity is literal text |
| PRN | Exactly `0` or `1` |
| Indication | Canonical indication, or blank for absence; non-PRN rows cannot carry an indication |
| DurationDays | Positive integer days, or blank for absence |
| SigCode | Exact opaque literal; required for enabled rows; spaces/case/punctuation are preserved |
| Description | Nonempty human explanation for enabled rows |
| Source | `USER_CONFIRMED`, `USER_CONFIRMED:<reference>`, or `DOCUMENTED_UNAMBIGUOUSLY:<exact field-specific reference>` |

The complete key is Action, Quantity, Form, Route, Frequency, PRN, Indication and DurationDays. Blank qualifiers mean absence, never wildcard. All fields must describe a parser-supported combination. Source is a pharmacist attestation, not independent proof of Oracle syntax. Never enter patient data. References are plain text and are never fetched or executed. TEST_ONLY, UNVERIFIED_HISTORICAL and CONTRADICTED do not authorize production output.

IDs must be unique across both files, including disabled rows. Duplicate enabled semantic keys are errors even when their output strings agree. User rows never override defaults. Disabled rows still need valid identity and semantics; their output, description and source may be empty. A header-only user file is valid. If a later release duplicates a local mapping, remove or disable the redundant local row with a distinct ID and reload; the application never rewrites the local library.

### Load status and updates

The tab displays active default/user counts, generation, last successful load, latest attempt and sanitized row/column errors. A failed reload retains the previous snapshot, counts, generation and loaded timestamp. On startup, invalid user data or cross-file conflicts activate only independently valid defaults with a visible warning. Missing/invalid defaults disable Smart SIG resolution while other valid workflows remain available. Missing user data on explicit reload returns to defaults. Structural validity does not certify Oracle acceptance.

For updates in the existing installation folder, close the script before extraction, retain the local user TSV, and restart after complete extraction. For a new installation folder, keep the old installation and deliberately copy its user TSV into the new Data folder before use/reload. The package contains no user file. Update discovery remains notification-only; no automatic installation, migration or mapping download occurs.

### Supported semantic vocabulary

These values come from the current recognizer; their presence does not approve an Oracle output or every cross-product combination.

- **Actions:** INHALE_CONTENTS, TAKE, USE, APPLY, INHALE, INSTILL, INSERT, INJECT, PUT, DISSOLVE, CHEW, SWALLOW, GIVE.

- **Quantities:** 1.5, 0.5, 1-2, 2-3, 3-4, 4-5, 4-6, 5-6, 12, 11, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1.

- **Forms:** ML, TABLESPOON, TEASPOON, APPLICATORFUL, SUPPOSITORY, INHALATION, CAPSULE, TABLET, LOZENGE, PACKET, PATCH, SPRAY, PUFF, DROP, UNIT, GRAM, FILM, STRIP.

- **Routes:** EYE_LEFT, EYE_RIGHT, EYE_BOTH, EYE_AFFECTED, EYE_UNSPECIFIED, EAR_LEFT, EAR_RIGHT, EAR_BOTH, EAR_AFFECTED, EAR_UNSPECIFIED, NASAL_EACH_NOSTRIL, BUCCAL_BOTH, SUBLINGUAL, BUCCAL, ORAL, SUBCUTANEOUS, INTRAMUSCULAR, RECTAL, VAGINAL, INHALATION, TOPICAL, NASAL.

- **Frequencies:** EVERY_10_TO_12_HOURS, EVERY_8_TO_12_HOURS, EVERY_6_TO_8_HOURS, EVERY_4_TO_6_HOURS, EVERY_3_TO_4_HOURS, EVERY_2_TO_3_HOURS, EVERY_12_HOURS, EVERY_8_HOURS, EVERY_6_HOURS, EVERY_4_HOURS, EVERY_3_HOURS, EVERY_2_HOURS, EVERY_1_HOUR, EVERY_HALF_HOUR, FOUR_TIMES_DAILY, THREE_TIMES_DAILY, TWICE_DAILY, BEDTIME, MORNING, EVENING, WEEKLY, DAILY.

- **Conditions:** NAUSEA_AND_VOMITING, SHORTNESS_OF_BREATH, MIGRAINE_HEADACHE, SEVERE_PAIN, CONSTIPATION, WHEEZING, ANXIETY, NAUSEA, SLEEP, PAIN, HEADACHE, COUGH.


Validation for v2.6.0: deterministic source/data/package checks only. AutoHotkey runtime: NOT RUN. Oracle/Citrix live: NOT RUN.
