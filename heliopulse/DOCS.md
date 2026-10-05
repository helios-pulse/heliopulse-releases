# Configuration

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
Logical exports have a separate sanitization contract and are not equivalent to
a cold backup of secrets. Restore portable exports according to HelioPulse docs.

Update through Supervisor. Do not use appliance OTA or systemd commands.
Downgrade only when the schema is compatible; otherwise restore the matching
pre-upgrade backup. Experimental installations based on an isolated development
branch are not evidence of compatible production upgrade/rollback.

## Current experimental limits

QEMU ARM64 validation is distinct from physical Pi/x86/USB/ESP32 beta coverage.
Discovery registry adoption cannot reconstruct devices deleted before the
registry existed; those retained topics may require explicit manual cleanup.
Full driver-metric reconciliation, metadata, performance and failure-injection
matrices must be completed before stable. Ingress latency includes a live Core
administrator lookup; resources and revocation behavior need beta measurements.

Report the App/core versions, architecture and sanitized error codes. Never
include tokens, passwords, Ingress URLs or complete browser storage.
