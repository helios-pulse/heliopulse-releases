# HelioPulse for Home Assistant

Experimental distribution of HelioPulse for Home Assistant OS.

## 0.1.2 — Existing Home Assistant entities

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
