# HelioPulse for Home Assistant

Experimental distribution of HelioPulse for Home Assistant OS.

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
