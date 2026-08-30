# HelioPulse — Releases

Artefactos OTA firmados de HelioPulse OS (binarios ARM64 + web).
Este repo es **público** a propósito: la seguridad la aporta la firma Ed25519,
no la privacidad. El código fuente vive en el repo privado `heliopulse`.

Cada release contiene:
- `heliopulse-app-vX.Y.Z.tar.zst` — artefacto de aplicación (bin + web + VERSION)
- `update.json` — manifiesto firmado (versión, sha256, firma, canal, rollout, changelog)

Publicado automáticamente por el workflow `release.yml` del repo de código.
