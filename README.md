<!-- VA Pharmacy Automation v3.4.3 -->
# VA Pharmacy Automation

**v3.4.3-rc.7 - Pharmacist-supervised prerelease integrating normal Smart Refill, the compact four-tab Console, JSONL diagnostics and operation-specific timing. Live Oracle/Citrix acceptance remains unverified.**

AutoHotkey v2 automation supporting selected Oracle Health / Cerner retail pharmacy workflows through Citrix.

## Runtime and Smart workflow status

Routing Option opens the dropdown, selects twice with Ctrl+A, types the complete configured value once as literal text, waits 500 ms, commits with Tab and waits 1000 ms. It observes Health plan and handles Routing Option Override with Alt+U/default reason once per episode, then proceeds to the next unfinished operation without reacquiring or copying the route just to compare the value sent. This removes the shared post-write failure gate; it does not establish independent route persistence. Dispense Priority selects once, types its complete configured value once and retains its necessary commit without routine readback. These two writes do not use clipboard paste. Route reads that supply clinical decisions retain their source and clipboard protections. Manual mCDS/Discern review does not expire active workflow budgets; cancellation and explicit Resume remain available. Comments, Routing Option Override and Copy Order may return through a new window; the next required field is acquired there. Copy sends Alt+C once and waits up to 15 seconds for the copied order, returning early when ready. Uncertain mutations are never replayed automatically.

Configured VA Routing Option, Dispense Date/Time and Health plan anchors use their reviewed Window-relative search bands, converted and clipped to the current Citrix client. Complete native templates and competing complete matches are checked within those bands; a miss does not expand the search to the rest of the client. Other reviewed labels retain their supported client regions. A current acquisition may serve its immediate action and a valid same-prescription handoff; actual surface changes require fresh evidence. Health plan transition observation, clinical decision route reads and retained Bridge quantity checks remain distinct required operations.

Smart Refill from Ctrl+Alt+X or the Console starts on the intended Discern Duplicate Order alert. The pharmacist chooses C2, C3-5 or Non-Controlled Medication once. Complete captured actual-fill history for the same medication and regimen supplies rolling coverage across historical prescription numbers. The workflow selects Modify Order/OK and reviews the plan before field changes. C2 accepts only observed Window or Local Regular Mail; unexpected C2 CMOP stops for review. C3-5 mail uses Local Regular Mail at due minus one day; NC mail preserves its supported subtype at due minus ten days. Window uses C2 On Hold or C3-5/NC On File without Date/Time acquisition. C2 documentation preserves existing text and provider restrictions; top Comments are appended once and reopened for readback. Final pharmacist approval authorizes the once-only forwarding sequence and matching returned Duplicate Order continuation. Uncertain actions never replay. See CANDIDATE-STATUS.md for startup and review boundaries.

Smart SIG supports the four supplied weekly mg and bedtime insulin mappings through its shared resolver, preview and field-plan application. When PRN is positively unchecked and no PRN change is parsed, the optional reason is left unread and untouched. Required PRN observations, conflict detection and unknown SIG empty-destination confirmation remain. Support for these examples does not reproduce the original reported workplace insulin incident.

The Pharmacy Console uses native Windows controls, subtle headings and system colors with a fixed 820 x 540 logical layout, or a complete 780 x 540 compact layout selected for the monitor's actual usable area and native frame. Both profiles share the 540-unit vertical arrangement. A slim row shows Oracle/Citrix availability and the active workflow/step. Version remains in Settings and the title bar. Minimize, close-to-hide, keyboard access and Always on Top remain. The main window has no resizing, maximize or scrollbars; an area smaller than the readable compact layout is reported instead of hiding controls. Native rendering of the latest height/overlay polish remains pending; live workstation behavior remains UNVERIFIED. Prior layout results do not establish acceptance of this revision.

Four permanent tabs provide Medication Manager, SIG Library, Diagnostics and Settings. Medication Manager groups actual refill facts, one availability explanation, a Single/Batch route matrix with narrower 166-unit buttons, status actions and one compact Smart workflow row. Smart Refill's qualification caption reflects its existing qualification service independently of temporary launch availability. Bridge uses inline schedule/quantity/route controls, shortcut reminders beneath Run/Batch, and a last-run summary with a heading shown only when relevant; existing helper detail remains in the full result. Run Bridge uses inline settings, Ctrl+Alt+B opens the separate chooser, and Ctrl+Alt+Shift+B opens Batch Bridge setup. PDMP Note moves to Documentation on this page and retains its original PowerChart handler and source requirements. Last Action occupies one or two lines, with **Copy** of the complete sanitized snapshot and **View Full** for longer results. Copy respects a workflow's clipboard lease and leaves an explicit successful copy on the clipboard. Abort, conditional Resume/Wait Longer and Hide remain reachable in the shared footer, without repeating Last Action there. The native Abort button has a red outline while active, including paused or cancellation-requested workflows, and returns to neutral/disabled when idle; high contrast uses system colors. Styling changes only with state and does not change cooperative cancellation.

SIG Library shows actual catalog identity, family/component counts, load state and last successful load. Normal Reload/Retry remains available. Side-by-side source/result editors update offline through the existing resolver after one cancellable debounce of about 300 ms; Clear and ointment context remain. Preview never activates Oracle, sends prescription input or writes the clipboard. Open Catalog File and Open User Mappings are developer-only.

Settings groups Window, Safety, Display, Developer and About controls. Individual changes apply and persist immediately using the existing preference keys and file; a persistence failure is reported without claiming the setting was saved. Confirm Before Starting a Batch defaults to ON for a missing setting, while explicit saved choices remain. Version, Help, clear update status and Retry are available here. Developer Mode reveals technical environment information and advanced target tools; normal Diagnostics remains available when it is off.

Priority Mail Batch now has Ctrl+Alt+Shift+P. Batch Bridge opens setup with Ctrl+Alt+Shift+B or the Bridge area's Batch Bridge button. Declare a finite prescription count for queued Copy actions from one patient. The default confirms quantity and route for each copied order; uniform mode requires an explicit confirmation of the settings for every queued prescription. Single Bridge remains Ctrl+Alt+B, with decimal Custom quantities and its existing 15-second copied-order wait. Clinical meaning, residual Instructions, CMOP and existing refill policies remain unchanged.

Batch Bridge sends queue Apply at most once, or zero times when explicitly starting with Copy Order already open. Each item reserves Copy and submit once and reuses the existing Bridge field sequence. Transition observation uses a proposed 30-second normal budget plus one 15-second grace interval; it advances as soon as the target appears. At expiry, Resume/Wait Longer observes the same phase without replaying input. Clinical review remains manual. Submission sends and observed departures are reported separately. The batch stops at the declared count and leaves any extra queued action untouched. These timings and Oracle's automatic queue continuation require supervised live validation.

The replacement CMOP catalog accounts for all 114 supplied rows and includes broad insulin and NSAID class membership with complete-token ingredient and reviewed brand matching. The read-only Drug gesture uses one native copy. Its popup reports a supported 90/84-day initiative match, a complete negative result or an unresolved read; it never changes quantity, duration or the prescription.

Genuine failures append sanitized UTF-8 records to the local Reports directory's `incidents.jsonl`, regardless of Developer Mode. The permanent **Diagnostics** tab displays bounded recent failures with local occurrence times, workflow/code and the selected incident's failed/completed steps, actual input-dispatch evidence and sanitized technical details. Copy Report and explicit TXT Export Report are disabled without a selection; Open Reports Folder remains available. Empty history displays **No failures recorded** centered in the list body with blank details; the message disappears when an incident arrives. History loads when the tab opens, and successful new incidents update a visible list from their existing snapshot without a manual Refresh button or continuous disk polling. The JSONL schema, sanitization and existing reports remain unchanged. The included companion observes the exact application process and records unexpected exits and the last action. It never restarts the application or replays a workflow. Keep `ExitMonitor.ahk` beside `Scripts.ahk`; the application launches it automatically.

The v3.4.3 candidate starts in normal runtime. Extract every file together, including Images/Runtime, Images/Squirrel.jpg and Sounds/SquirrelChitter.wav. Missing templates, ambiguous matches or unsupported target geometry stop the dependent operation. Operation-local acquisition and short foreground/session guards protect input; diagnostic observations do not qualify field access. Only `--target-probe` selects read-only diagnostics. Smart Route remains unavailable without selected-prescription data acquisition. Smart Refill uses its pharmacist-reviewed Discern entry, plan and forwarding path. A submission action does not establish Oracle acceptance. Live Oracle/Citrix acceptance has NOT RUN.

The supervised public work-test candidate is v3.4.3-rc.7. Published rc.6, earlier candidates and stable v3.3.1 remain unchanged. Use the checksum and manifest to identify the complete ZIP and exact source commit.

Required merged-source CI passed, including repository and package-integrity checks. Existing SIG behavior is retained. Local clinical simulations, Oracle workflows and live prescription completion were NOT RUN for this candidate. Workplace Citrix recognition, clipboard delivery, routing, Bridge/batch and Smart Refill completion remain UNVERIFIED. Comments observation now starts immediately; Script Origin uses a 250 ms settle and the final failed date readback has no extra settle. Image retries use 250 ms with immediate first observation; this can increase detection latency. The 50 ms cancellation cadence, routing-specific waits, SIG/clipboard delivery and untimed pharmacist review remain. Package sanitation, include closure, checksums and asset review remain required.

## Read-only visual preflight

Launch `Scripts.ahk --target-probe`, open Diagnostics / Target Probe, then manually focus Oracle Order Entry. Click **Run Visual Preflight (read only)**. Its button preserves Oracle foreground; results appear in the existing scrollable report panel. Select **Sweep failed anchors (0..75)** before refocusing Oracle to compare tolerances. The probe sends no input, reads no clipboard, saves no screenshots and does not change production profiles. Report the anchor names, outcomes, variations, attempts, client size and DPI. Matching is separate from live workflow acceptance.

## Download

[Latest Smart Refill test build](https://github.com/aaronbridges128/VA-Pharmacy-Automation/releases/tag/v3.4.3-rc.7) - **v3.4.3-rc.7 supervised public work-test prerelease**. Integrates normal Smart Refill, the compact four-tab Console, JSONL diagnostics and operation-specific timing. Download the complete application ZIP with its checksum and manifest. Workplace acceptance remains unverified.

[Previously released work-test candidate](https://github.com/aaronbridges128/VA-Pharmacy-Automation/releases/tag/v3.3.2-rc.2) — v3.3.2-rc.2 remains unchanged; it does not contain queued Batch Bridge or the header polish.

[Download v3.3.1](https://github.com/aaronbridges128/VA-Pharmacy-Automation/releases/tag/v3.3.1) — complete normal application. Extract every file together. Public availability does not establish live workflow acceptance or Smart Refill production qualification.

The stable download and updater remain on the stable latest-release endpoint below.

Open the [latest GitHub Release](https://github.com/aaronbridges128/VA-Pharmacy-Automation/releases/latest) and download the attached file named `VA-Pharmacy-Automation-vX.Y.Z.zip`.

Do **not** download GitHub's automatically generated **Source code (zip)** or **Source code (tar.gz)** files. Those are not the installation package.

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

- Single-prescription Window, Local Mail, Priority Mail, Discharge, On File, and On Hold actions
- Bridge Supply quantity and routing workflows
- Smart Refill date and disposition assistance
- Smart SIG conversion for explicitly supported instruction patterns
- Window, Local Mail and Priority Mail batch refill processing
- Pharmacy Console for workflow launch, status, diagnostics, and update notification
- PowerChart PDMP documentation workflow that leaves the note open for pharmacist review and signing
- Deterministic Smart Route rule infrastructure that remains fail-closed until its local selected-refill acquisition mapping is configured and validated

All Oracle input is guarded by the application's validated Citrix context and workflow boundaries. The operator remains responsible for confirming the correct patient, prescription, values, and final Oracle result.

## Hotkeys

CMOP Supply Check: hold plain Ctrl, double-left-click the Drug value below
`Drug:` in the foreground Oracle/Citrix order-entry form, then release Ctrl and the mouse.
The reader locates the Drug label and copies the operator's native selection once.
The read-only popup displays `90 day item` for catalog Days 90 or 84,
`Not on CMOP 90 day initiative` for a complete negative determination, and
`Unable to determine` for invalid, clipped, multiline, mixed-ingredient or
otherwise ambiguous input. No prescription changes are made. Supervised live
acceptance is required before clinical deployment.

These bindings come from the distributed `UI/Hotkeys.ahk` module.

| Hotkey | Action |
| --- | --- |
| `Ctrl+Alt+B` | Open the Bridge Supply chooser |
| `Ctrl+Alt+D` | Run Discharge |
| `Ctrl+Alt+W` | Run Window |
| `Ctrl+Alt+F` | Set On File |
| `Ctrl+Alt+H` | Set On Hold |
| `Ctrl+Alt+M` | Run Local Mail |
| `Ctrl+Alt+P` | Run Priority Mail (Local Regular Mail + Priority) |
| `Ctrl+Alt+R` | Run Smart Route (only when locally configured) |
| `Ctrl+Alt+S` | Run Smart SIG |
| `Ctrl+Alt+X` | Run Smart Refill |
| `Ctrl+Alt+Shift+W` | Batch queued refills as Window |
| `Ctrl+Alt+Shift+M` | Batch queued refills as Local Mail |
| `Ctrl+Alt+Shift+P` | Batch queued refills as Priority Mail |
| `Ctrl+Alt+Shift+B` | Open Batch Bridge setup for queued Copy actions |
| `Ctrl+Alt+Enter` | Resume a paused workflow or wait longer for its pending transition |
| `Ctrl+Alt+Pause` | Request cooperative workflow abort |
| `Ctrl+Alt+I` | Open read-only diagnostics |
| `Ctrl+Alt+Space` | Open or raise the Pharmacy Console |
| `Ctrl+Alt+Esc` | Exit the application |

## Troubleshooting

- If a hotkey is blocked, return to the expected Oracle/Citrix screen and confirm no other workflow is active.
- If a workflow stops, read the stable error code shown by the application and use **Diagnostics** from the Console or tray menu. Do not include patient information in an issue report.
- If an update check fails, Settings shows its reason and offers Retry when another check can start. Continue working normally; update availability never controls prescription automation.
- If the script does not start, confirm AutoHotkey v2.0.18 or later is installed and that the complete extracted folder is present.
- If your Oracle layout, Citrix scaling, or field positions differ, do not guess new coordinates. Stop using the affected workflow until it has been validated for that environment.

## Project status

This is an independently maintained pharmacy workflow automation project. It is not an official product of the U.S. Department of Veterans Affairs, Oracle, Oracle Health, or Citrix. It does not provide clinical decision-making, and local authorization and validation remain required before production use.

This public repository is the download and issue-reporting surface. Development occurs in a separate private source repository; development history is intentionally not published here.

## Smart SIG

Smart SIG (`Ctrl+Alt+S`) uses the reviewed 167-entry administration-only catalog and 173 recognition rules across ten constrained families: `{Verb}{Quantity} {Formulation} {Route} {Frequency}`. Provenance retains the historical 765-row import separately. Bedtime produces `T1 TAB PO QHS`; two-capsule daily produces `T2 CAP PO D`; half-tablet daily produces `T0.5 TAB PO D`. Both “three times daily” and “three times a day” produce `T1 TAB PO TID` for the supplied oral-tablet example; explicit every-eight-hours remains Q8H. Fixed whole-unit morning injection retains `INJ{units} UN SQ QAM`; the supplied bedtime insulin family uses `INJ{units} INJECTION-INSULIN SC QHS`. Weekly mg injections use `INJ{dose} INJECTION-MG SC 1XWK` for “one time a week” and `INJ{dose} INJECTION-MG SC QWK` for “every week”. The explicit “subcutaneously (under the skin)” route is consumed once. The demonstrated `APP1 OINT TOP BID` remains supported. PRN state/reason and residual Instructions remain separate from SIG. No route is inferred from dosage form, no concentrations are converted, and unsupported essential qualifiers reject without replacement.

For positively unchecked scheduled instructions, an irrelevant PRN Reason is left unread and untouched; the review identifies it as unchanged rather than observed empty. Required PRN content/conflict checks, unknown SIG empty-destination confirmation and pharmacist field-plan review remain. Correction scales, titration, hold parameters and unsupported complex regimens are not flattened into these fixed-dose mappings; meaningful supported residual text remains in Instructions.

Live Smart SIG acquires the reviewed lower Instructions label and associated field for one fresh full-field select/copy transaction. It preserves source text when capture or composition fails. The legacy SIG `74,118` and Instructions `270,386` coordinates do not authorize input. Physical launch/modifier release, clipboard ownership and detectable concurrent updates remain. SIG/PRN fields retain their meaningful commit/readback contracts before Instructions changes. Live Oracle/Citrix acceptance remains NOT RUN. The editable **Include Instructions / Do Not Include Instructions / Cancel** chooser preserves pharmacist edits exactly. Include-empty and Exclude clear source Instructions only after SIG Tab commit. Tabs/newlines are visibly flattened and require another Include click; other controls are rejected. Cancel, Escape and close perform no intentional replacement. A later Instructions failure reports `SMART_SIG_INSTRUCTIONS_UPDATE_FAILED`.

Residual source offsets, parentheses, whitespace handling and sentence-case conversion of all-uppercase residual text are preserved. Unconsumed dosing qualifiers such as may increase/decrease, hold if, breakthrough dosing, unresolved as directed, alternate schedules, late PRN/duration and unknown PRN indications fail closed. Ordinary strength-change notes and bridge markers may use the chooser. The finite parser does not understand arbitrary prose.

### Editing and reloading

**Enable Developer Mode in Settings -> SIG Library -> Open User Mappings -> add an approved row -> save -> Reload Catalog -> read the result.** Oracle need not be running. Open User Mappings creates only a header if the user file is absent, never replaces an existing file, and opens its associated application (Notepad fallback). File access is developer-only; normal Reload/Retry remains available. Existing workflow/reload ownership checks remain. New mappings for already recognized semantics require no source edit or restart; new parser vocabulary requires a separate code change.

- Distributed, reviewed defaults: `Data/SmartSigLibrary.default.tsv`.
- Local additions: `Data/SmartSigLibrary.user.tsv`, ignored by Git and excluded from releases.
- Paths are relative to the installation folder, independent of the working directory.
- Save UTF-8 (with or without BOM), or BOM-marked UTF-16LE, tab-delimited text. Import all spreadsheet columns as text. Do not save XLSX or CSV under a TSV filename. Dates such as a spreadsheet-converted `1-2`, scientific notation and formulas are rejected.
- Preserve the exact 14-column header and empty cells. LF/CRLF and a missing final newline are supported; empty lines after the header are ignored. Optional quoted cells may use doubled quotes. Embedded tabs/newlines and control characters are rejected. Limits: 1 MiB and 10,000 data rows per file.

Existing schema-1 user files remain unchanged. Mixed schema-1/schema-2 files retain the 14-column header. Schema 2 supports only the injection row described above, with approved provenance; duplicate templates (including disabled definitions), arbitrary placeholders and other versions are rejected. Deploy code and default data together: older executables cannot load schema 2.

### Schema version 1

| Column | Contract |
| --- | --- |
| SchemaVersion | Exactly `1` |
| Enabled | Exactly `0` or `1` |
| Id | Unique lowercase ASCII identifier, `[a-z][a-z0-9_]*`, maximum 64 characters |
| Action, Quantity, Form, Route, Frequency | Exact canonical semantic values from the vocabulary below; quantity is literal text |
| PRN | Exactly `0` or `1` |
| Indication | Canonical indication, or blank for absence; scheduled and PRN indications are distinct |
| DurationDays | Positive integer days, or blank for absence |
| SigCode | Exact opaque literal; required for enabled rows; spaces/case/punctuation are preserved |
| Description | Nonempty human explanation for enabled rows |
| Source | `USER_CONFIRMED`, `USER_CONFIRMED:<reference>`, or `DOCUMENTED_UNAMBIGUOUSLY:<exact field-specific reference>` |

The complete key is Action, Quantity, Form, Route, Frequency, PRN, Indication and DurationDays. Blank qualifiers mean absence, never wildcard. All fields must describe a parser-supported combination. Source is a pharmacist attestation, not independent proof of Oracle syntax. Never enter patient data. References are plain text and are never fetched or executed. TEST_ONLY, UNVERIFIED_HISTORICAL and CONTRADICTED do not authorize production output.

IDs must be unique within each file, including disabled rows. Duplicate enabled semantic keys within one file are errors even when their output strings agree. In a catalog snapshot, an explicitly approved local full-SIG row overrides the same complete key from bundled defaults/composition, so an intentional legacy `T1 PO D` user row remains usable. Conflicting same-priority outputs fail; identical defensive matches deduplicate. A plain custom key cannot erase meal/awake qualifiers. Bundled canonical defaults cannot silently shadow composition with a conflicting output. A header-only, missing or optional zero-byte user file is valid with no custom mappings. Whitespace-only, BOM-only, malformed or locked files are preserved for correction. The application never rewrites user mappings to resolve overlaps.

### Load status and updates

The SIG Library tab displays actual catalog identity, active family/definition/component information, last successful load and a concise load result. A failed reload retains the previous snapshot, counts, generation and loaded timestamp. On startup, invalid user data activates only independently valid catalog/defaults with a visible warning. Missing/invalid defaults, catalog or composition rules disable Smart SIG resolution while other valid workflows remain available. Missing user data on explicit reload returns to defaults. Structural validity does not certify Oracle acceptance. Offline preview remains usable when Oracle is not active and updates after a single cancellable debounce; it uses the same approved snapshot as live Smart SIG.

For updates in the existing installation folder, close the script before extraction, retain the local user TSV, and restart after complete extraction. For a new installation folder, keep the old installation and deliberately copy its user TSV into the new Data folder before use/reload. The package contains no user file. Update discovery remains notification-only; no automatic installation, migration or mapping download occurs.

### Supported semantic vocabulary

The following legacy literal-schema vocabulary remains for local-file compatibility; its presence does not enable every combination. Production composition additionally uses the fingerprinted Data/OracleSigCatalog.tsv and Data/OracleSigRules.tsv, with provenance in Data/OracleSigProvenance.json. Component approval and typed compatibility govern production output; unsupported legacy vocabulary cannot bypass completeness checks.

- **Actions:** INHALE_CONTENTS, TAKE, USE, APPLY, INHALE, INSTILL, INSERT, INJECT, PUT, DISSOLVE, CHEW, SWALLOW, GIVE.

- **Quantities:** 1.5, 0.5, 1-2, 2-3, 3-4, 4-5, 4-6, 5-6, 12, 11, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1.

- **Forms:** ML, TABLESPOON, TEASPOON, APPLICATORFUL, SUPPOSITORY, INHALATION, CAPSULE, TABLET, LOZENGE, PACKET, PATCH, SPRAY, PUFF, DROP, UNIT, GRAM, FILM, STRIP.

- **Routes:** EYE_LEFT, EYE_RIGHT, EYE_BOTH, EYE_AFFECTED, EYE_UNSPECIFIED, EAR_LEFT, EAR_RIGHT, EAR_BOTH, EAR_AFFECTED, EAR_UNSPECIFIED, NASAL_EACH_NOSTRIL, BUCCAL_BOTH, SUBLINGUAL, BUCCAL, ORAL, SUBCUTANEOUS, INTRAMUSCULAR, RECTAL, VAGINAL, INHALATION, TOPICAL, NASAL.

- **Frequencies:** EVERY_10_TO_12_HOURS, EVERY_8_TO_12_HOURS, EVERY_6_TO_8_HOURS, EVERY_4_TO_6_HOURS, EVERY_3_TO_4_HOURS, EVERY_2_TO_3_HOURS, EVERY_12_HOURS, EVERY_8_HOURS, EVERY_6_HOURS, EVERY_4_HOURS, EVERY_3_HOURS, EVERY_2_HOURS, EVERY_1_HOUR, EVERY_HALF_HOUR, FOUR_TIMES_DAILY, THREE_TIMES_DAILY, TWICE_DAILY, BEDTIME, MORNING, EVENING, WEEKLY, DAILY.

- **Conditions:** NAUSEA_AND_VOMITING, SHORTNESS_OF_BREATH, MIGRAINE_HEADACHE, SEVERE_PAIN, CONSTIPATION, WHEEZING, ANXIETY, NAUSEA, SLEEP, PAIN, HEADACHE, COUGH.


Validation for v2.6.0: deterministic source/data/package checks only. AutoHotkey runtime: NOT RUN. Oracle/Citrix live: NOT RUN.

## Local visual rendering profiles

Version 3.2.0 separates runtime image decoding from release integrity checks. Keep the distributed defaults intact and place reviewed replacement label crops under `Images/LocalVisual/`. Only templates explicitly registered in `VisualProfiles.local.ini` are loaded. These local files are never included in release packages. Restart the application at an idle boundary after changing them.

For a workstation whose label **and editable-field layout** have been verified to scale uniformly from the bundled reference frame, a local profile can select a bounded ratio list:

```ini
[Profile]
Version=1
UniformLayout=1
Ratios=1,1.25,1.5,1.75,2
```

Ratios are relative to each template, not Windows display settings. Do not declare uniform layout based on label dimensions alone. Without that declaration, non-native geometry is refused. Resampling cannot reproduce every independently rendered font. Use Visual Preflight to inspect acquisition and field geometry before workflow acceptance.

Full-scene fixture testing qualifies the tested native and 200% nearest-neighbor renderings only. Fractional 125%, 150%, 175% transforms and JPEG-like text have observed failures; these require rendering-specific calibrated templates. The ratio list above is configuration syntax, not a compatibility guarantee.

A replacement section names an existing anchor and its local file. `Frame=preserved` declares that the reference origin and geometry remain valid; `GeometryScale` declares its layout scale. `CropX`/`CropY` locate the replacement crop origin in that reference frame. `Frame=calibrated` instead supplies `Rect.<target>` (four half-open bounds) and `Point.<target>` (two coordinates) in replacement-native pixels for every target using that anchor. Values must come from actual field calibration; no example click coordinates are supplied. `Frame=unknown` permits decoding but cannot authorize field input. `ReferenceScale` is optional (`unknown`, `100`, `125`, `150`, `175`, or `200`) and is descriptive only.

The profile permits at most two local variants per registered anchor, five configured ratios in 0.5–2, and BMP/PNG templates up to 2048×512 and 524,288 pixels (8 MiB encoded). Allowed ratios are 0.5, 0.625, 0.75, 0.875, 1, 1.25, 1.5, 1.75 and 2. Blockers also test the declared rendering scale; unsupported blocker transforms stop acquisition. Missing optional variants are reported and skipped; corrupt resources fail closed. Synthetic scale and geometry tests do not establish recognition rates or live workstation acceptance.
