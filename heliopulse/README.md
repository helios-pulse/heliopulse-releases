# HelioPulse for Home Assistant

Experimental distribution of HelioPulse for Home Assistant OS.

## 0.1.30 — HelioPulse core 1.23.8

- No changes for Home Assistant: this version keeps the core aligned with HelioPulse 1.23.8, whose only change affects updates on HelioPulse OS.

## 0.1.29 — HelioPulse core 1.23.7

- A collector that stops unexpectedly restarts by itself (after 5 s, backing off up to 60 s) instead of staying down until the app restarts.
- Automation time windows follow the site location's time zone, like daily totals and reports.
- Telemetry is queued, not dropped, while InfluxDB rejects the token, and is sent once it is fixed.
- Quieter logs: successful collector updates and health checks are logged only at debug level.

## 0.1.28 — HelioPulse core 1.23.4

- The dashboard reconnects its live connection by itself when it stops receiving updates (for example after a restart behind a proxy), so live views no longer freeze until a reload.

## 0.1.27 — HelioPulse core 1.23.3

- Daily and interval energy and long-range history (summaries of 15 min and 1 h) are kept in SQLite when InfluxDB is used; long History ranges load much faster.
- A slow telemetry store at startup no longer restarts the day's integrated energy from zero.

## 0.1.26 — HelioPulse core 1.23.2

- Support requests attach a full, sanitized diagnostic bundle in the background after sending.
- Faster SQLite reads and site battery SOC averaged per installation.

## 0.1.25 — HelioPulse core 1.23.1

- System › General keeps Information and Resources open side by side; Maintenance opens Diagnosis first.
- Support shows "Priority support" and no longer asks for an email when one is linked to the system.

## 0.1.24 — HelioPulse core 1.23.0

- Guided onboarding: adding a device now goes model → connection → details, with model search, BETA badges, per-method help, a pre-save serial test and a first-reading check with diagnosis.
- Setup checklist on Energy and in System › Help; state-aware welcome; short walkthroughs per area and a "How does it work?" entry on each screen.
- System settings are grouped as accordions; one anonymous notice is sent when a new installation starts for the first time.

## 0.1.23 — HelioPulse core 1.22.1

- Equipos › Drivers has a "Request driver" form: brand and model, optional connection, notes and email for follow-up. Requests go through the existing support channel.

## 0.1.22 — HelioPulse core 1.22.0

- Automations can write inverter settings, including whole time slots, through the same validated, read-back and audited path as manual changes. Disabled by default: an administrator enables it globally and per device, choosing the allowed parameters, limits and write cadence.
- The panel asks for the site location and warns while it is missing.
- New beta drivers for MUST PV18/PV19 and Felicity T-REX, and the EG4 GridBOSS as a meter. The local MCP server for AI agents is not shown inside Home Assistant.

## 0.1.21 — HelioPulse core 1.21.1

- Refresh the Home Assistant distribution with core 1.21.1. Its new local Shelly integration is not shown inside Home Assistant, which already ships its own Shelly integration.

## 0.1.20 — HelioPulse core 1.21.0

- New beta read-only driver for the INVT iMars XD-TL hybrid inverters (XD3–6KTL), over a Solarman logger or RS485.
- Drivers can declare derived metrics (a sum of metrics read in the same cycle). The INVT driver uses it for house consumption: inverter AC output plus grid meter.

## 0.1.19 — HelioPulse core 1.20.51

- Refresh the Home Assistant distribution with core 1.20.51. Its new System › Maintenance password change applies only to local HelioPulse sign-ins; inside Home Assistant the identity comes from Home Assistant, so the option is not shown.

## 0.1.18 — HelioPulse core 1.20.50

- The site time zone now follows the map location instead of staying on America/Bogota; it can also be chosen in System › Location.
- Existing installations are corrected on startup and the change is recorded in Events (a time zone chosen manually is kept).
- Fixed: outside Colombia the solar forecast disappeared after local midnight and its curve was shifted.

## 0.1.17 — HelioPulse core 1.20.49

- Refresh the Home Assistant distribution with the latest core release.
- Full encrypted backups now run inside the App: a root supervisor with `no_new_privs` handles them while the API keeps running as UID 10001.
- The interface shows only what applies inside Home Assistant: Security, Installer, Kasa, SmartThings, Tuya, AI and the host network rows are hidden.
- Fixed a blank screen in System › Maintenance and database restores that left WAL files behind.
- The App starts automatically after a reboot.
- Known issue: outside Colombia the solar forecast is hidden from 00:00 to 07:00 because the site time zone is fixed to America/Bogota.

## 0.1.16 — HelioPulse core 1.20.40

- Refresh the Home Assistant distribution with the latest core release.
- After a week of use, a discreet card lets you rate HelioPulse and leave optional feedback.

## 0.1.15 — HelioPulse core 1.20.39

- Refresh the Home Assistant distribution with the latest core release.
- The system DNS indicator no longer reports a false failure.

## 0.1.14 — HelioPulse core 1.20.38

- Refresh the Home Assistant distribution with the latest core release.
- Device parameters keep loading when one register does not answer.

## 0.1.13 — HelioPulse core 1.20.37

- Refresh the Home Assistant distribution with the latest core release.
- Updates a network library to fix a high-severity vulnerability (CVE-2026-78669).

## 0.1.12 — HelioPulse core 1.20.35

- Refresh the Home Assistant distribution with the latest core release.
- The core adds installer driver editing inside an owner commissioning window.
  Home Assistant hides the Installer tab, so this has no visible change for HA
  installations.

## 0.1.11 — HelioPulse core 1.20.32

- Refresh the Home Assistant distribution with the latest core release.
- Security hardening: viewers can no longer change automations, serial driver
  settings are validated before use, collectors can only report their own
  devices, and webhooks cannot reach loopback or cloud metadata addresses.
- Faster, coordinated loading of the dashboard.

## 0.1.10 — HelioPulse core 1.20.29

- Refresh the Home Assistant distribution with the latest core release.
- The core now groups installer access in a System › Installer tab. Home Assistant
  hides that tab, so this release has no visible change for HA installations.

## 0.1.9 — HelioPulse core 1.20.28

- Refresh the Home Assistant distribution with the latest core release.
- Include grid export energy on the overview, inverter detail and history.
- Include the installer platform's OTA request queue. In Home Assistant the
  installer card is hidden and OTA stays managed by Supervisor, so this changes
  nothing for HA installations.

## 0.1.8 — HelioPulse core 1.20.21

- Refresh the Home Assistant distribution with the latest core release.
- Include energy-history query fixes and consumption forecasts on inverter pages.
- Include read-only device details and sanitized diagnostic exports for installers.

Home Assistant updates remain managed by Supervisor. This release does not
change the Solarman profile or the freshness policy for imported HA entities.

## 0.1.7 — HelioPulse core 1.20.9

- Include signing test fixtures in native container builds (0.1.6 did not publish).

- Improve error handling, history ranges, device selection and mobile layouts.
- Update the vulnerable frontend source-map dependency.
- Include the new encrypted recovery format in the core. Coordinated full backups
  require the appliance worker or an external Docker helper; Home Assistant App
  recovery continues to use Supervisor cold backups.
- Preserve Home Assistant ingress, source mapping and managed MQTT.

## 0.1.5 — HelioPulse core 1.20.6

- Expanded onboarding: 35-step orientation and 13-step getting-started guide.
- Jump between sections, pause to use the screen and resume after reloading.
- Mobile highlights, contextual availability notices and seven translated languages.
- Home Assistant retains its source mapping, managed MQTT and host restrictions.

The guide explains controls without executing device actions. Home Assistant
updates continue to be managed from its App page.

## 0.1.4 — HelioPulse core 1.20.5

- Savings with time-of-use tariffs and export pricing.
- Off-grid devices are valued in savings even without a grid meter.
- Energy intervals are no longer overwritten; savings reconcile with daily
  counters, and historical impact totals and energy counters are protected.
- Faster History: grouped telemetry queries and independent chart loading.

Built from core 1.20.5. The release pipeline validates amd64/arm64 builds,
startup, UID10001, NoNewPrivs and the vulnerability gate; the new core
features have not yet been exercised inside a Home Assistant lab.

## 0.1.3 — Complete Home Assistant source setup

- Map frequency and AC voltage, and identify a single-phase installation.
- Configure panel capacity, tilt and azimuth in the source editor. Saving the
  solar array refreshes the forecast using the location set in System.
- Optionally estimate battery current from power ÷ voltage when no current
  sensor is mapped. Calculated values are labelled as estimated and disappear
  when input readings are invalid or too far apart in time.
- Clear labels for production and consumption today; known lifetime counters
  are rejected as daily energy. Unassigned daily counters use integrated power.
- Complete snapshots remove obsolete readings from the live display.

Validated in QEMU with a real solar forecast request, restart persistence,
measured/estimated current, zero-voltage handling and seven UI languages.

## Existing Home Assistant entities

In **Devices → Add from Home Assistant**, select an existing inverter device
and explicitly map its sensors to HelioPulse metrics. Readings feed the live
dashboard and history, without polling the inverter a second time. The source
reads Core every five seconds and supports editing, pausing and deletion.

Units are normalized automatically. Positive grid power means import; positive
battery power/current means discharge. Use **Invert sign** when the source uses
the opposite convention. Unknown, unavailable, stale and out-of-range readings
are skipped. Imported readings are not republished through HelioPulse MQTT.
This works with existing integrations such as Solarman and requires no broker
configuration changes. Mapping and restart recovery were validated in QEMU.

## Installation

Add `https://github.com/helios-pulse/heliopulse-releases` under
Settings → Apps → App store → Repositories, install **HelioPulse**, then open
its Web UI. Enable **Show in sidebar** for the solar-power icon. Only active
Home Assistant administrators can use the App UI; no separate login is needed.

This public repository contains installation metadata and release artifacts.
The core source repository is private. Container images are distributed through
public ECR and require no registry credentials.

For sensors in Home Assistant, install/configure Mosquitto and the MQTT
integration. The default `mqtt_mode: auto` uses the Supervisor MQTT service.
Configure your devices in HelioPulse, using a distinct topic prefix if you run
more than one instance. Updates are managed from the Home Assistant App page.

Supported image architectures: **aarch64** and **amd64** on Home Assistant OS.
Ingress/admin SSO, simulated telemetry, MQTT Discovery and cold backup/restore
have been exercised in QEMU. USB/RS485, ESP32 and physical Pi/x86 acceptance
remain pending. This is an App, not a HACS integration; the App store is not
available in Home Assistant Container.

The App has independent versions (`ha-v*`). Every image identifies its App
version, core base version and exact source commit. Stable hardware support is
pending; the initial release remains **experimental**.
