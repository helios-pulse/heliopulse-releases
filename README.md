# HelioPulse — Releases

Artefactos OTA firmados de HelioPulse OS (binarios ARM64 + web).
Este repo es **público** a propósito: la seguridad la aporta la firma Ed25519,
no la privacidad. El código fuente vive en el repo privado `heliopulse`.

Cada release OTA contiene:
- `heliopulse-app-vX.Y.Z.tar.zst` — artefacto de aplicación (bin + web + VERSION)
- `update.json` — manifiesto firmado (versión, sha256, firma, canal, rollout, changelog)

Publicado automáticamente por el workflow `release.yml` del repo de código.

## Home Assistant — experimental

Este repositorio también se puede añadir a **Home Assistant OS** como repositorio
de Apps: **Ajustes → Apps → Tienda de Apps → ⋮ → Repositorios**.

```text
https://github.com/helios-pulse/heliopulse-releases
```

Instala **HelioPulse**, inícialo y activa **Mostrar en la barra lateral**. Accede
con tu sesión de administrador de Home Assistant. Para sensores, configura
Mosquitto y la integración MQTT; el App usa el broker del Supervisor en modo auto.

- [Guía del App y límites del soporte](heliopulse/README.md)
- [Versión experimental 0.1.1](https://github.com/helios-pulse/heliopulse-releases/releases/tag/ha-v0.1.1)
- [Guía ilustrada del sitio](https://www.heliopulse.io/es/getting-started#home-assistant)

Imágenes públicas `aarch64`/`amd64` en ECR, firmadas con Cosign. Las versiones
`ha-v*` son independientes de OTA/OS. Validado en QEMU; aceptación física
USB/RS485, ESP32 y Pi/x86 pendiente. No es una integración HACS.
