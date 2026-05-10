# Changelog — Solalex Add-on

Dieses Changelog betrifft nur das HA-Add-on-Artefakt (Container + Manifest).
Repo-weites Changelog: `/CHANGELOG.md`.

## 0.1.108 — 2026-05-10

- feat(3.10b): grid_target_w für Akku-only (wr_charge) + Pool-Lead-Fallback

## 0.1.107 — 2026-05-10

- fix(3.10a): grid_target_w in MULTI-Gates und Drossel-Feed-in-Check

## 0.1.106 — 2026-05-10

- feat(3.10a): symmetrischer Mindestbezug, PI-Soll in Verhalten

## 0.1.105 — 2026-05-10

- feat(3.17): Rate-Limit-Anti-Windup PI-Speicher + Reaktionstest-Wartezeit

## 0.1.104 — 2026-05-09

- fix(4.11): Sparkline-Bar-Breite, History-Skeleton 400ms, Retry bei Fehler

## 0.1.103 — 2026-05-09

- docs: Sprint-Status 4.11 review, Story 3.17 ready, Artefakt 4.11 erweitert
- feat: Stories 4.9–4.11 Schreibhistorie, Retention und Sparkline
- fix: reaktionstest done+unzuverlässig zeigt warning + diagnose-logs

## 0.1.102 — 2026-05-09

- qa: Diagnose-Export Marstek Testsystem 2026-05-09 (meta + DB)
- fix: setpoint-echo-readback toleriert stale state bei matching value

## 0.1.101 — 2026-05-09

- fix: subscribe mode-select + permission-switch aus battery_control blob

## 0.1.100 — 2026-05-09

- Reaktionstest: idempotenter Mode-Echo; PI-Edit ohne volles Mess-Blob

## 0.1.99 — 2026-05-09

- Story 3.16c: Review-Fixes PI-Tuning, Reaktionstest und Speicher-PI

## 0.1.98 — 2026-05-09

- fix: akku-cadence-ui und reaktionstest nutzt live-battery-pool

## 0.1.97 — 2026-05-09

- fix: reaktionstest-ui bei unzuverlässigem ergebnis und tests

## 0.1.96 — 2026-05-09

- feat: implementiere PI-regelung mit reaktionstest end-to-end

## 0.1.95 — 2026-05-08

- chore: snapshot vor großer pid-regelungsänderung

## 0.1.94 — 2026-05-08

- fix: halte hero-evidence auch bei failed/timeout dispatch aktuell

## 0.1.93 — 2026-05-08

- feat: ergänze heute-gesteuert-kpi und strompreis-settings

## 0.1.92 — 2026-05-08

- docs(test): markiere review-fixes als erledigt und schärfe custom-rate-limit-test

## 0.1.91 — 2026-05-08

- fix: stabilisiere rate-limit opt-out und config-preset-verhalten

## 0.1.90 — 2026-05-08

- fix: härte speicher-range-clamp und funktionstest-diagnostik

## 0.1.89 — 2026-05-07

- fix: räume running-statusanzeige auf und ergänze footer-meta

## 0.1.88 — 2026-05-07

- fix: stabilisiere akku-funktionstest und clamp speicher-setpoints

## 0.1.87 — 2026-05-07

- fix: vereinfache narrative passiv-logik und verbessere config-edit flow

## 0.1.86 — 2026-05-07

- feat: Adapter-Defaults & Akku-Topologie-Feinschliff + neue QA-Diags

## 0.1.85 — 2026-05-06

- fix: Night-Hero-Logik und Settings-Rate-Limit-Feld nachziehen

## 0.1.84 — 2026-05-06

- fix: Solakon Numeric-Mode-Pflicht im Wizard absichern

## 0.1.83 — 2026-05-06

- fix: Mode-Option-Autodetect gegen Slot-Kollisionen härten

## 0.1.82 — 2026-05-06

- fix: Wizard-Optionen und Akku-Cooldown-Defaults nachschärfen

## 0.1.81 — 2026-05-06

- feat: Battery-Topology-Wizard und Mode-Option-Handling erweitern

## 0.1.80 — 2026-05-06

- feat: Sticky Header/Footer für Settings- und Diagnose-Seiten

## 0.1.79 — 2026-05-06

- fix: Passive-Akku-Flow und Running-UI nachschärfen

## 0.1.78 — 2026-05-05

- fix: iOS-Nav-Fallbacks in Running/Setup-Routen absichern

## 0.1.77 — 2026-05-05

- fix: SettingsVerhalten-Review-Patches und Story-Status abschließen

## 0.1.76 — 2026-05-05

- feat: Settings-Verhalten auf eine Sammel-Page konsolidieren

## 0.1.75 — 2026-05-05

- feat: Narrative-, Settings- und Diagnose-Refinements bündeln

## 0.1.74 — 2026-05-05

- feat: Settings-IA-Refactor, Verbindungsdiagnose und Health-Status erweitern

## 0.1.73 — 2026-05-05

- feat: Topologie-Default für Akku-Cooldown absichern

## 0.1.72 — 2026-05-05

- feat: Sign-Flip-Cooldown, Helper-Slugs und Klartext-Mapping

## 0.1.71 — 2026-05-04

- fix: QA-Status-Helper über HA-WebSocket anlegen
- ci: Add-on-Changelog bei Auto-Release aus Git-Log ergänzen

## 0.1.1-beta.7 — 2026-04-25

- Manifest/Release-Stand auf `0.1.1-beta.7` aktualisiert.
- Runtime- und Debug-Logging-Verbesserungen aus Story-4.0-Zyklus integriert.
- Speicher-/Controller-Stabilisierung inklusive begleitender Test-Erweiterungen.

## 0.1.0-beta.1 — 2026-04-23

- Initiales Add-on-Skeleton (Multi-Arch, amd64 + aarch64).
- FastAPI-Backend unter Ingress-Port 8099.
- Health-Endpoint `/api/health`.
- SQLite-Init unter `/data/solalex.db` (WAL-Mode).
- Minimum HA Core: 2026.4.0 deklariert (via `addon/config.yaml`
  `homeassistant:`-Feld; niedrigere Versionen erhalten Install-Warning).
- Support-Matrix auf **Home Assistant OS** beschränkt. Home Assistant
  Supervised, Container und Core werden nicht unterstützt.
- Landing-Page-Voraussetzungen (`docs/landing/voraussetzungen.md`) und
  In-Store-Doku (`addon/DOCS.md` Abschnitt „Unterstützte HA-Versionen")
  ergänzt.
