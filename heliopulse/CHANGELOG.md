# 0.1.59 — HelioPulse core 1.23.41

- Help: a new short guide to AI in System › General › Help covers your providers, the assistant settings and the assistant button (chat with your real data, attachments and memory).
- The full guided tour now also explains expected consumption, fullscreen (kiosk) mode and the Energy plan's batteries, vehicle and flexible loads, and its texts were updated in all 7 languages. The assistant button is now shown on its own tour step instead of staying hidden.

# 0.1.58 — HelioPulse core 1.23.40

- Diagnostics: the diagnostic attached to Support requests and the one your installer downloads now include recent logs of HelioPulse and of each collector, the state of every process (restarts and last exit), system data from the host and an Internet/DNS check. Before, the app only exported the version and disk usage.
- Diagnostics on every installation also include each device's communication status, the state of Voltronic parallel groups and the result of the last group detection, without personal data, serial numbers or credentials. A failed detection is now written to the log with its error code.
- System › General shows how long the host has been powered on and the memory in use.

# 0.1.57 — HelioPulse core 1.23.38

- Solar forecast: the card on Energy and on each inverter now has Today and Tomorrow, so you can check the next day's expected production before midnight.
- Home Assistant sensors: each inverter with panels publishes “Solar forecast today” and “Solar forecast tomorrow” (kWh) through MQTT Discovery, for automations such as setting the next day's battery charge target. They stay available at night while the inverter is off.
- Panel: the forecast card keeps its size while it loads, Energy reads the savings settings once, and with “reduce motion” on, content shows as soon as it has loaded.

# 0.1.56 — HelioPulse core 1.23.37

- SRNE inverters: the over-discharge voltage and maximum charge current are back in Devices › Device configuration. The inverter did not answer them when parameters were read in blocks, which blocked every change; they are now read one by one.
- Device configuration: when the device refuses a change, the panel says so with the Modbus code it returned instead of “Write error”. Values are rounded to their step and options show their name.

# 0.1.55 — HelioPulse core 1.23.36

- Device configuration: if the device doesn't answer a parameter, Devices › Device configuration names it and explains why no change can be applied. If the driver was modified on this installation, you can restore the official one right there.
- Batteries: on the Energy screen, a battery group with more than 4 batteries shows as one card; open it to see each battery. In Devices › Parallel systems, a shared battery can take several battery banks (BMS) on the same bus, with the level averaged by capacity.
- System: Communications and Maintenance load once. Every card no longer requests its data twice, and a click made while the tab loads is no longer lost.
- Phone: the “More” sheet now closes when you pick the screen you are already on.

# 0.1.54 — HelioPulse core 1.23.35

- Energy plan: enter each battery bank's capacity and maximum charge and discharge power in Energy plan › Batteries, set the charge your vehicle needs by its departure time and add appliances that can wait, like the washing machine or the pool pump. The plan suggests when to run them, on solar or in the cheapest hours, and never controls your devices.
- Energy plan: it uses your time-of-use tariff, including time bands and export price, and shows the estimated money saving.
- Energy plan: it refreshes at least every hour, “Regenerate” no longer goes back to the previous plan, it keeps your battery reserve and shows times in your time zone. Saving the policies no longer resets the objective, mode or reserve.
- Dashboard: with every battery's capacity entered, the total state of charge weights each bank by its capacity.
- Expected consumption: a peak seen on a single day, like charging the car once, no longer inflates the following weeks.
- History: the “Calibrate with real production” switch works again.
- Security: hardened backup restore and the panel's browser security headers.

# 0.1.53 — HelioPulse core 1.23.34

- Expected consumption: on an inverter's page, with several inverters, the chart now shows that inverter's own expected consumption, based on its own history, instead of the whole installation. The overview still shows the total.

# 0.1.52 — HelioPulse core 1.23.33

- Expected consumption: hours and weekends now follow your site's clock. They used UTC, so on sites behind UTC a Friday evening counted as the weekend.
- What's new: following a link keeps the highlighted card in view while the rest of the page loads.
- The rest of this core release is for HelioPulse OS (the neural consumption model and its nightly training); nothing else changes in this App.

# 0.1.51 — HelioPulse core 1.23.32

- Devices: USB adapters under Detected serial ports show their maker and model instead of "Unknown".
- The rest of this core release is for the Docker distribution (USB adapters, remote access); nothing else changes in this App.

# 0.1.50 — HelioPulse core 1.23.31

- Assistant: attach photos, screenshots, PDFs (such as a manufacturer's Modbus map) and text files such as CSV to your questions, with the paperclip, by pasting or by dragging (up to 4). Photos are shrunk before sending, files go only to your AI provider, and they are deleted with the conversation.

# 0.1.49 — HelioPulse core 1.23.30

- Assistant: with Claude it sometimes used its tools and ended without writing anything. It now has more room to reason, asks again for the answer when none arrives, and says so in the chat if there is still no text.

# 0.1.48 — HelioPulse core 1.23.29

- AI: Anthropic keys that are not tied to a workspace (sk-ant-usr...) failed every request. Their profile now takes the workspace ID, and the error explains what is missing. The assistant also no longer ends with an empty or cut answer after showing a page button.

# 0.1.47 — HelioPulse core 1.23.28

- New System → AI tab: connect your own AI provider (Anthropic, OpenAI-compatible such as OpenRouter or Groq, or Ollama on your network). Keys are encrypted and never shown again; nothing is sent to any provider until you turn AI on and accept the data notice; daily call and token limits.
- AI assistant with memory: when AI is on, the small button at the bottom right of every page opens a chat that answers with your installation's real data, opens HelioPulse guides when needed, links you to the right page and remembers earlier conversations (you can review, search or erase what it remembers). If an administrator allows it, it proposes setting changes, new automations (saved disabled) and new drivers as cards you apply with a button.
- Claude: works with the newest models such as Claude Opus 5.5; use the model id (claude-opus-5-5), and a failed connection test shows the provider's own message.
- 0.1.46 was never published (its image build failed); this release includes its changes.

# 0.1.45 — HelioPulse core 1.23.26

- Tuya: automations run over the local network again. Devices that name their switch "switch" on the LAN (such as some dual power transfer switches) now get rule commands saved as "switch_1" over the LAN instead of the cloud, which could reject them with error 2008. That error is now explained on screen.
- Rules → Execution log: each action shows whether it was confirmed, left unconfirmed or failed, with the reason, and a run whose action was not applied is marked "Actions not applied" instead of looking like a success.

# 0.1.44 — HelioPulse core 1.23.25

- SRNE inverters: changing a setting no longer fails every time. The ASP48100U200-H never answers reads of the over-discharge voltage (0xE00D) or the maximum charge current (0xE20A), and each change first rereads every setting, so those two blocked all the others. They are no longer listed; set them on the inverter's own display.

# 0.1.43 — HelioPulse core 1.23.24

- Support requests: after you send a request, the full compressed diagnostic of the app is generated in the background and added to it, so support can look into the problem without asking you for files. It includes no personal data or credentials; if it cannot be added, the request is still sent as before.
- Panel: after an update, a one-time "What's new" notice lists the new features of the installed version, each with a direct link. In this version it points to the support diagnostic.

# 0.1.42 — HelioPulse core 1.23.23

- Automations: a condition that compares metrics of several devices now shows every metric with its device, and editing a row keeps the right device. Wait and sustained nodes show their full list of conditions.

# 0.1.41 — HelioPulse core 1.23.22

- Core 1.23.22: fixes for the Tuya integration (local search on HelioPulse OS, clearer setup errors, removing Tuya circuits). Tuya stays hidden in Home Assistant, so this app has no visible change.

# 0.1.40 — HelioPulse core 1.23.21

- Firmware version on the device cards: each inverter shows the firmware version it reports in its own registers (SRNE: app version; Deye three-phase and single-phase: control and communication boards). HelioPulse only reads it, every 12 hours, and never updates an inverter's firmware.
- If you edited the SRNE or Deye driver, restore the official one in System → Drivers to get the firmware registers.

# 0.1.39 — HelioPulse core 1.23.18

- Backups: a failed backup now says where it failed (pre-backup checks, copy, disk space, resume or verification) instead of a generic message.
- Backups no longer count InfluxDB rows with full-table queries, which failed on large histories; the check reads the Parquet metadata instead.

# 0.1.38 — HelioPulse core 1.23.16

- Includes the changes of 0.1.37, whose image build failed and was never published.
- Backup password: the first full backup sets it; later backups use it without asking and it is only needed to restore. A recovery key can be downloaded and used instead of the password, and changing the password keeps older backups readable with the one they were made with.
- Backups can be deleted from the list.
- Scheduled and off-site copies of the App are made with Home Assistant's own backups (Settings → System → Backups, which can store them in Google Drive or OneDrive); the backups card says so.
- Growatt SPA (beta driver): grid frequency, AC output voltage and power, and inverter temperatures are read.

# 0.1.37 — HelioPulse core 1.23.15

- Backup password: the first full backup sets it; later backups use it without asking and it is only needed to restore. A recovery key can be downloaded and used instead of the password, and changing the password keeps older backups readable with the one they were made with.
- Backups can be deleted from the list.
- Scheduled and off-site copies of the App are made with Home Assistant's own backups (Settings → System → Backups, which can store them in Google Drive or OneDrive); the backups card says so.
- Growatt SPA (beta driver): grid frequency, AC output voltage and power, and inverter temperatures are read.

# 0.1.36 — HelioPulse core 1.23.14

- Driver diagnostics: each device has a page listing every value its driver reads, with the last reading, its status (reading, stale, not reading or calculated) and where it comes from. Writable parameters are read only on demand; the table can be copied or downloaded as CSV. Home Assistant sources have a Diagnostics button too.
- Forecast history: History compares what the solar forecast predicted with the real production, by hour or by day, with the average daily error and bias. The history starts filling from this version.
- Calibrated forecast: after a few days of history, the forecast is corrected with the real production of the last 14 days, ignoring hours with reading gaps or a full battery. It is used by the Overview and the energy plan, and can be switched off in History.
- Several panel orientations: an inverter, including a Home Assistant inverter source, can have up to four planes with their own power, tilt and azimuth; the forecast adds them up.

# 0.1.35 — HelioPulse core 1.23.13

- Battery state of charge and other steady values read from Home Assistant no longer disappear after five minutes: HelioPulse keeps a value while Home Assistant reports the sensor as available. Each mapped sensor shows whether it is reading, holding its last value or skipped, and why; the optional maximum age is now per sensor.
- Add batteries and EV chargers from Home Assistant, not only inverters. Choose the type (HelioPulse suggests it from the sensors), map one or more battery packs, from one or several devices such as one ESP32 per BMS, with their cells, and link a battery or charger to its inverter. Batteries no longer count as extra inverters.
- The site location, time zone and currency are taken from Home Assistant, so the location prompt no longer asks again.
- Entities published to Home Assistant use the device name, readable names in the panel language and rounded values; cell voltages and status values are listed as diagnostics. Entity IDs do not change, but their visible names do.
- Users who are not Home Assistant administrators see a clear message instead of an error code. The anonymous installation notice now works in the App: existing installations report once as "existing".
- Flash collector explains the LAN API and port mapping an ESP32 needs in Home Assistant.

# 0.1.34 — HelioPulse core 1.23.12

- Energy on phones: the "Now" summary starts with solar production (power and whether the panels are producing) instead of a "Source" cell that repeated the battery or grid; long status words no longer overflow.
- History: production vs consumption, temperatures and per-phase charts use solid lines for every series.

# 0.1.33 — HelioPulse core 1.23.11

- First published Home Assistant build since 0.1.30: versions 0.1.31 and 0.1.32 failed to build and were never released, so their changes listed below arrive with this version.
- The "CO₂ avoided" and "Estimated savings" cards share one layout: the value lines up with the title next to the icon.

# 0.1.32 — HelioPulse core 1.23.10

- The battery screen's "State of charge (24h)" chart now shows its history for banks that group several packs on one cable (JK, Pylontech/Must and similar), and follows the pack you select.

# 0.1.31 — HelioPulse core 1.23.9

- The panel fits Home Assistant's frame better: a single compact header row without a second logo, and layouts that adapt to the space next to the sidebar.
- Readable everywhere: text and charts meet contrast in light and dark mode, numbers use your language's format, high-contrast mode keeps bars visible and animations respect reduced motion.
- Each device shows live, delayed or no communication and when it last reported; alarms say the likely cause and what to do.
- On phones, Energy opens with a "now" summary and the bottom bar has labels.
- Theme: System (the new default, follows your device), Light or Dark, with no flash of the wrong theme.
- Reports show the change against the previous period again; using less energy counts as an improvement.
- New beta drivers: Deye/Sunsynk single-phase, Huawei SUN2000 with LUNA2000, Victron GX over Modbus TCP, and Solis and Sungrow grid-tied string inverters. Solis RHI DC and meter power now read correctly.

# 0.1.30 — HelioPulse core 1.23.8

- No changes for Home Assistant: this version keeps the core aligned with HelioPulse 1.23.8, whose only change affects updates on HelioPulse OS.

# 0.1.29 — HelioPulse core 1.23.7

- A collector that stops unexpectedly restarts by itself (after 5 s, backing off up to 60 s) instead of staying down until the app restarts.
- Automation time windows follow the site location's time zone, like daily totals and reports.
- Telemetry is queued, not dropped, while InfluxDB rejects the token, and is sent once it is fixed.
- Quieter logs: successful collector updates and health checks are logged only at debug level.

# 0.1.28 — HelioPulse core 1.23.4

- The dashboard reconnects its live connection by itself when it stops receiving updates (for example after a restart behind a proxy), so live views no longer freeze until a reload.

# 0.1.27 — HelioPulse core 1.23.3

- Daily and interval energy and long-range history (summaries of 15 min and 1 h) are kept in SQLite when InfluxDB is used; long History ranges load much faster.
- A slow telemetry store at startup no longer restarts the day's integrated energy from zero.

# 0.1.26 — HelioPulse core 1.23.2

- Support requests attach a full, sanitized diagnostic bundle in the background after sending.
- Faster SQLite reads and site battery SOC averaged per installation.

# 0.1.25 — HelioPulse core 1.23.1

- System › General keeps Information and Resources open side by side; Maintenance opens Diagnosis first.
- Support shows "Priority support" and no longer asks for an email when one is linked to the system.

# 0.1.24 — HelioPulse core 1.23.0

- Guided onboarding: adding a device now goes model → connection → details, with model search, BETA badges, per-method help, a pre-save serial test and a first-reading check with diagnosis.
- Setup checklist on Energy and in System › Help; state-aware welcome; short walkthroughs per area and a "How does it work?" entry on each screen.
- System settings are grouped as accordions; one anonymous notice is sent when a new installation starts for the first time.

# 0.1.23 — HelioPulse core 1.22.1

- Equipos › Drivers has a "Request driver" form: brand and model, optional connection, notes and email for follow-up. Requests go through the existing support channel.

# 0.1.22 — HelioPulse core 1.22.0

- Automations can write inverter settings, including whole time slots, through the same validated, read-back and audited path as manual changes. Disabled by default: an administrator enables it globally and per device, choosing the allowed parameters, limits and write cadence.
- The panel asks for the site location and warns while it is missing.
- New beta drivers for MUST PV18/PV19 and Felicity T-REX, and the EG4 GridBOSS as a meter. The local MCP server for AI agents is not shown inside Home Assistant.

# 0.1.21 — HelioPulse core 1.21.1

- Refresh the Home Assistant distribution with core 1.21.1. Its new local Shelly integration is not shown inside Home Assistant, which already ships its own Shelly integration.

# 0.1.20 — HelioPulse core 1.21.0

- New beta read-only driver for the INVT iMars XD-TL hybrid inverters (XD3–6KTL), over a Solarman logger or RS485.
- Drivers can declare derived metrics (a sum of metrics read in the same cycle). The INVT driver uses it for house consumption: inverter AC output plus grid meter.

# 0.1.19 — HelioPulse core 1.20.51

- Refresh the Home Assistant distribution with core 1.20.51. Its new System › Maintenance password change applies only to local HelioPulse sign-ins; inside Home Assistant the identity comes from Home Assistant, so the option is not shown.

# 0.1.18 — HelioPulse core 1.20.50

- The site time zone now follows the map location instead of staying on America/Bogota; it can also be chosen in System › Location.
- Existing installations are corrected on startup and the change is recorded in Events (a time zone chosen manually is kept).
- Fixed: outside Colombia the solar forecast disappeared after local midnight and its curve was shifted.

# 0.1.17 — HelioPulse core 1.20.49

- Refresh the Home Assistant distribution with the latest core release.
- Full encrypted backups now run inside the App: a root supervisor with `no_new_privs` handles them while the API keeps running as UID 10001.
- The interface shows only what applies inside Home Assistant: Security, Installer, Kasa, SmartThings, Tuya, AI and the host network rows are hidden.
- Fixed a blank screen in System › Maintenance and database restores that left WAL files behind.
- The App starts automatically after a reboot.
- Known issue: outside Colombia the solar forecast is hidden from 00:00 to 07:00 because the site time zone is fixed to America/Bogota.

# 0.1.16 — HelioPulse core 1.20.40

- Refresh the Home Assistant distribution with the latest core release.
- After a week of use, a discreet card lets you rate HelioPulse and leave optional feedback.

# 0.1.15 — HelioPulse core 1.20.39

- Refresh the Home Assistant distribution with the latest core release.
- The system DNS indicator no longer reports a false failure.

# 0.1.14 — HelioPulse core 1.20.38

- Refresh the Home Assistant distribution with the latest core release.
- Device parameters keep loading when one register does not answer.

# 0.1.13 — HelioPulse core 1.20.37

- Refresh the Home Assistant distribution with the latest core release.
- Updates a network library to fix a high-severity vulnerability (CVE-2026-78669).

# 0.1.12 — HelioPulse core 1.20.35

- Refresh the Home Assistant distribution with the latest core release.
- The core adds installer driver editing inside an owner commissioning window.
  Home Assistant hides the Installer tab, so this has no visible change for HA
  installations.

# 0.1.11 — HelioPulse core 1.20.32

- Refresh the Home Assistant distribution with the latest core release.
- Security hardening: viewers can no longer change automations, serial driver
  settings are validated before use, collectors can only report their own
  devices, and webhooks cannot reach loopback or cloud metadata addresses.
- Faster, coordinated loading of the dashboard.

# 0.1.10 — HelioPulse core 1.20.29

- Refresh the Home Assistant distribution with the latest core release.
- The core now groups installer access in a System › Installer tab. Home Assistant
  hides that tab, so this release has no visible change for HA installations.

# 0.1.9 — HelioPulse core 1.20.28

- Refresh the Home Assistant distribution with the latest core release.
- Include grid export energy on the overview, inverter detail and history.
- Include the installer platform's OTA request queue. In Home Assistant the
  installer card is hidden and OTA stays managed by Supervisor, so this changes
  nothing for HA installations.

# 0.1.8 — HelioPulse core 1.20.21

- Refresh the Home Assistant distribution with the latest core release.
- Include energy-history query fixes and consumption forecasts on inverter pages.
- Include read-only device details and sanitized diagnostic exports for installers.

Home Assistant updates remain managed by Supervisor. This release does not
change the Solarman profile or the freshness policy for imported HA entities.

# 0.1.7

- Include signing test fixtures in the native container build.
- Ship the changes listed below with core 1.20.9.

# 0.1.6 — Not published (build failed)

- Include HelioPulse core 1.20.9 with functional fixes and the frontend security update.
- Improve history, API failure recovery, inverter selection and mobile layouts.
- Core encrypted recovery requires the appliance worker or external Docker helper;
  use Supervisor cold backups to recover the Home Assistant App.

# 0.1.5

- Include HelioPulse core 1.20.6 with a detailed 35-step tour and 13-step setup guide.
- Add section navigation, pause to explore and saved progress across reloads.
- Improve mobile highlights and translate the expanded guide into seven languages.
- Preserve Home Assistant source setup, managed MQTT and host-feature restrictions.

# 0.1.4

- Include HelioPulse core 1.20.5: time-of-use tariffs and export pricing,
  off-grid savings without a grid meter, protected energy history and faster
  History charts.

# 0.1.3

- Map frequency, AC voltage, single-phase installs and solar array geometry
  from Home Assistant sources; optional estimated battery current.

# 0.1.2

- Add existing Home Assistant entities as HelioPulse device sources.

# 0.1.1

- Replace the Debian runtime with a minimal Alpine/musl image.
- Validate native amd64/arm64 builds, SQLite, UID10001 and NoNewPrivs.
- Block publication on HIGH/CRITICAL vulnerabilities and retain scan reports.
- Distribute installation metadata through heliopulse-releases.

# 0.1.0 — Experimental (publication pending)

- Home Assistant runtime and non-root process collectors.
- Ingress with Core-backed administrator verification and prefix-aware UI.
- Supervisor MQTT credentials, bounded publishing queue and discovery registry.
- Explicit local Home Assistant service destination for automation actions.
- Cold-backup metadata and separate App versioning.

Hardware beta, complete Discovery v2 reconciliation, release verification and
stable qualification remain pending. This file is preparation, not publication evidence.
