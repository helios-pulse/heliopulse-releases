# HelioPulse

HelioPulse monitors your solar installation from Home Assistant: what the panels
produce, what the house uses, the battery and the grid, live and over time.

## What it does

- Shows live production, consumption, battery and grid in one energy-flow view,
  plus history, savings, alarms and monthly reports.
- Reads inverters, batteries and meters directly (USB/RS485 serial or network),
  or from sensors you already have in Home Assistant — inverters, batteries
  (several packs and cells) and EV chargers (**Devices → Add from Home
  Assistant**), without polling the equipment twice.
- Publishes its readings to Home Assistant through MQTT, so you can use them in
  dashboards and automations.
- Runs locally: readings and settings stay on your Home Assistant host.

## Open it

1. Install **HelioPulse** from the App store and start it.
2. Turn on **Show in sidebar** and open **HelioPulse** from the sidebar
   (or press **Open Web UI**). There is no separate HelioPulse sign-in.
3. Only Home Assistant administrators can open it.
4. Add your first device in **Devices → Add**. To send readings to Home
   Assistant, install the Mosquitto broker App and the MQTT integration first.

## Known issues

- The App is experimental: USB/RS485 adapters, ESP32 collectors and physical
  Raspberry Pi or x86 hardware have not finished acceptance testing.
- After plugging in a new USB adapter, restart the App so it can use it.
- Some panel sections are hidden here because Home Assistant handles them or
  they do not apply: Security, Installer, Kasa, SmartThings, Tuya, Shelly, AI,
  the MCP server and the host network rows.
- Update the App from its page in Home Assistant; HelioPulse's own update
  screen does not apply.
- Devices deleted before the discovery registry existed may leave old MQTT
  entities behind; remove them manually.

When asking for help, use **Support** in the panel and include the App and core
versions. Never share tokens, passwords or Ingress URLs.

# Configuration (technical details)

## Access and MQTT

Open the App through Home Assistant Ingress. HelioPulse verifies administrator
membership against Core; `panel_admin` alone does not provide authorization.
If Core is unavailable or permission cannot be verified, access is denied.
Local setup and local-user administration are unavailable through Ingress.

MQTT defaults to `auto`: install and start the official Mosquitto App. Supervisor
supplies credentials in memory; they are not saved to HelioPulse's database.
Without a broker, monitoring continues and MQTT reports disconnected.

Set `mqtt_mode: manual` in App configuration and restart to configure an external
broker from HelioPulse. There is no automatic fallback to stored credentials.
`disabled` turns publishing off. Pending discovery cleanup remains visible at
`/api/v1/integrations/mqtt/status`; disabling or losing access to an old broker
does not prove that retained entities were removed.

Use distinct `topic_prefix` values when several installations share a broker.
`discovery_prefix` defaults to `homeassistant` and must match HA's MQTT settings.

Each inverter with a solar array also gets two forecast sensors, "Solar forecast
today" and "Solar forecast tomorrow" (kWh, the same total the panel shows). They
stay available at night while the inverter is off. Tomorrow's sensor is
unavailable for up to 3 hours after midnight, until the next forecast download.
Use it in an evening automation, for example to set the next day's battery
charge target.

## Serial and ESP32

UART devices are mapped by Supervisor. The API and child collectors run as UID
10001 with numeric supplementary groups for mapped serial devices. Prefer
`/dev/serial/by-id` (or by-path for adapters without an identifier). Restart the
App after hotplug if a new group is required. No privileged/full-access mode is
requested. Physical USB/RS485 and ESP32 acceptance testing is still pending.

The LAN API is off by default; loopback ingestion and health remain available.
For ESP32, enable `lan_api_enabled`, map container port 8080 in the App Network
settings, and configure the collector with the HA host address and mapped port.
mDNS is disabled in this runtime. Ingress port 8099 must not be published.

## Backups and updates

Create a Home Assistant backup including HelioPulse before updating. The App
uses **cold backup**: Supervisor stops it before copying `/data`. That includes
SQLite, driver/configuration files, discovery registry and the local vault key.
The Supervisor token is supplied anew on startup and is not backed up by the App.

For automatic and off-site copies, use Home Assistant's own backups:
**Settings → System → Backups** schedules them, keeps a number of copies and can
store them with Home Assistant Cloud or the Google Drive and OneDrive backup
integrations. Select HelioPulse among the Apps included. HelioPulse does not run
its own schedule or cloud uploads inside Home Assistant, so the two never back
up the same night.

HelioPulse can also create an encrypted full backup on demand from **System →
Maintenance** (database, configuration, drivers, keys and models). The first one
sets the backup password (12+ characters); later backups use it without asking,
and it is only needed to restore. The App briefly stops its API for a consistent
copy and restarts it; monitoring pauses for a few seconds. Restore accepts only a
backup made by the same App version, with the password or the downloadable
recovery key; it rolls back automatically if the restored API does not start.
The Supervisor-managed App options are never included or overwritten. Keep the
password or the recovery key: without them the archive cannot be restored.

Update through Supervisor. Do not use appliance OTA or systemd commands.
Downgrade only when the schema is compatible; otherwise restore the matching
pre-upgrade backup. Experimental installations based on an isolated development
branch are not evidence of compatible production upgrade/rollback.

## Anonymous notices

HelioPulse tells heliopulse.io when it is installed and, once per version, when
it is updated. Each notice carries only a random installation id created by the
App, the runtime, the architecture, the HelioPulse core version and, for
updates, the previous version. The site adds the country. No user, hostname,
IP address, network, device or energy data is sent, and nothing else is
reported while you use the App.

## Current experimental limits

QEMU ARM64 validation is distinct from physical Pi/x86/USB/ESP32 beta coverage.
Discovery registry adoption cannot reconstruct devices deleted before the
registry existed; those retained topics may require explicit manual cleanup.
Full driver-metric reconciliation, metadata, performance and failure-injection
matrices must be completed before stable. Ingress latency includes a live Core
administrator lookup; resources and revocation behavior need beta measurements.

Report the App/core versions, architecture and sanitized error codes. Never
include tokens, passwords, Ingress URLs or complete browser storage.
