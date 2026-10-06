# 0.1.4

- Include HelioPulse core 1.20.5: time-of-use tariffs and export pricing,
  off-grid savings without a grid meter, protected energy history and faster
  History charts.

# 0.1.3

- Map frequency, AC voltage, single-phase installs and solar array geometry
  from Home Assistant sources; optional estimated battery current.

# 0.1.2

- Add existing Home Assistant entities as HelioPulse device sources.

# 0.1.0 — Experimental (publication pending)

- Home Assistant runtime and non-root process collectors.
- Ingress with Core-backed administrator verification and prefix-aware UI.
- Supervisor MQTT credentials, bounded publishing queue and discovery registry.
- Explicit local Home Assistant service destination for automation actions.
- Cold-backup metadata and separate App versioning.

Hardware beta, complete Discovery v2 reconciliation, release verification and
stable qualification remain pending. This file is preparation, not publication evidence.
# 0.1.1

- Replace the Debian runtime with a minimal Alpine/musl image.
- Validate native amd64/arm64 builds, SQLite, UID10001 and NoNewPrivs.
- Block publication on HIGH/CRITICAL vulnerabilities and retain scan reports.
- Distribute installation metadata through heliopulse-releases.
