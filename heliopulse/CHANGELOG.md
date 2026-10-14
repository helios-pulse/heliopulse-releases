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
