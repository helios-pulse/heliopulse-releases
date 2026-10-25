# HelioPulse

**Free, local-first monitoring for solar inverters and batteries.** HelioPulse reads your
inverter, BMS and meters directly over RS485/Modbus or your network and shows solar,
battery, home and grid in one live view, with history you keep on your own hardware.
No vendor cloud required.

Runs on **Home Assistant OS**, a **Raspberry Pi 4/5** image or **Docker**.

[Website](https://www.heliopulse.io) · [Getting started](https://www.heliopulse.io/en/getting-started) · [Compatible hardware](https://www.heliopulse.io/en#drivers) · [Support](https://www.heliopulse.io/en/soporte) · [Guía en español](https://www.heliopulse.io/es/getting-started)

![HelioPulse energy view: solar, battery, home and grid](https://www.heliopulse.io/capturas/heliopulse-live-en/01-energy.png)

## What it does

- Live energy flow for solar, batteries, home and grid, plus history, savings, alarms and monthly reports.
- Reads inverters, batteries and meters directly: a USB–RS485 adapter, the Wi-Fi logger many
  inverters already ship with, Modbus TCP, or an ESP32 collector on your network.
- Battery detail down to each cell when the BMS reports it: spread, lowest and highest cell, temperatures, SOC and SOH.
- Several inverters and battery banks on one site, including parallel systems.
- Rules and automations, with a dry run before anything is written to your equipment.
- Home Assistant integration through MQTT discovery, so the readings show up as entities.
- Everything runs locally. Readings and settings stay on your device and keep working without internet.

## Install

### Home Assistant OS (experimental)

[![Open your Home Assistant instance and show the add add-on repository dialog with a specific repository URL pre-filled.](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fhelios-pulse%2Fheliopulse-releases)

Or add it by hand: **Settings → Apps → App store → ⋮ → Repositories**, and paste:

```text
https://github.com/helios-pulse/heliopulse-releases
```

Then install **HelioPulse**, start it and turn on **Show in sidebar**. You sign in with your
Home Assistant administrator account. To get sensors in Home Assistant, set up the Mosquitto
broker and the MQTT integration; the app finds the Supervisor broker on its own.

`aarch64` and `amd64`. Read the [app guide and known issues](heliopulse/DOCS.md) and the
[changelog](heliopulse/README.md).

### Raspberry Pi 4/5 image

Download the latest `heliopulse-os-*.img.xz` from [Releases](https://github.com/helios-pulse/heliopulse-releases/releases)
(tags starting with `os-`), flash it to a microSD card or SSD and follow the
[step-by-step guide](https://www.heliopulse.io/en/getting-started#instalar-os). Setup is a
guided captive portal from your phone, no SSH. Signed updates install from the panel.

### Docker

```sh
docker run -d --name heliopulse \
  -p 8080:8080 -v heliopulse-data:/data \
  -e HP_RUNTIME=docker --restart unless-stopped \
  --log-driver json-file --log-opt max-size=10m --log-opt max-file=3 \
  public.ecr.aws/j7s7r2j5/heliopulse:latest
```

Open `http://<host>:8080`. Multi-arch image (`amd64`/`arm64`); to update, pull the new image
and recreate the container. The
[Docker guide](https://www.heliopulse.io/en/getting-started#instalar-docker) also has a
hardened Compose file and covers passing a USB–RS485 adapter to the container.

## Compatible hardware

Built-in drivers in v1.23.52. **Beta** drivers are tested in software against the
manufacturer's register map but have not been confirmed on that exact hardware yet. If you
run one, a report helps a lot.

| Brand | Models | Status |
|---|---|---|
| Deye | SUN-12K-SG04LP3-EU | Supported |
| Deye / Sunsynk | Single-phase hybrid SG0xLP1, 3.6–8 kW | Beta |
| SRNE | Hybrid inverter 48 V | Supported |
| Growatt | MIC TL-X; SPA / SPH storage hybrid | Supported |
| Growatt | SPF 4000–12000T DVM off-grid | Beta |
| EG4 | 18kPV / 12kPV / FlexBOSS; 6000XP / 12000XP; GridBOSS meter | Beta |
| Sol-Ark | 15K-2P-N split-phase (read-only) | Beta |
| Victron Energy | GX system, single-phase (Modbus TCP) | Beta |
| Huawei | SUN2000 L1 / M1 / M2 + LUNA2000 | Beta |
| Sungrow | SH hybrid; SG RS / RT string | Beta |
| Solis | RHI / S6 hybrid; grid-tied string | Beta |
| GoodWe | ET / EM / ES hybrid | Beta |
| Felicity Solar | T-REX 5/10K LP 48 V | Beta |
| INVT | iMars XD-TL hybrid | Beta |
| MUST | PV1800 / PH1800; PV19 (PV1900 EXP) 48 V | Beta |
| Voltronic | Axpert King, including parallel stacks | Beta |
| JK BMS | Native broadcast; V19 Modbus RTU 16S | Supported |
| Pylontech / Must | LV 16S over RS485 | Supported |
| Generic | 16S BMS and EV charger over Modbus RTU | Supported |

Your inverter is not listed? Drivers are JSON files, so a new one can be written from the
manufacturer's register map ([how](https://www.heliopulse.io/en/getting-started#crear-driver)).
See [compatible hardware](https://www.heliopulse.io/en#drivers) or ask through
[support](https://www.heliopulse.io/en/soporte).

## About this repository

HelioPulse is free to use. Its source code is not public: this repository is where the
signed builds are published. It is public on purpose, because security comes from the
Ed25519 signatures, not from hiding the files.

| Tag or folder | What it is |
|---|---|
| `vX.Y.Z` | Over-the-air app update: `heliopulse-app-vX.Y.Z.tar.zst` plus the signed `update.json` manifest |
| `os-X.Y.Z` | Raspberry Pi image (`.img.xz`) |
| `ha-v0.1.x` | Home Assistant app release, with the image digest and security scan reports |
| `app-windows-v*` | HelioPulse for Windows (preview) |
| `influxdb3-portable-v*` | Pinned database runtime that appliances download; do not remove |
| `heliopulse/`, `repository.yaml` | Home Assistant app repository metadata |
| `firmware/` | ESP32 collector firmware |

Releases are published automatically by the build pipeline. Home Assistant images are
public on Amazon ECR and signed with Cosign.
