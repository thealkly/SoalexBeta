# Changelog — Solalex Add-on

Dieses Changelog betrifft nur das HA-Add-on-Artefakt (Container + Manifest).
Repo-weites Changelog: `/CHANGELOG.md`.

## 0.1.146 — 2026-05-26

- feat(5.11): Reaktionstest-Journal, Diagnose-APIs und Profil-Vergleich

## 0.1.145 — 2026-05-26

- chore: Marstek-local-Defaults + bundled WIP
- feat(5.10): Identity-Sprache + Setup-Steckbrief P0 (Gamification)
- feat(deps): add html-to-image for setup steckbrief PNG export

## 0.1.144 — 2026-05-21

- feat(3.30): Pause zwischen Richtungswechseln + Settings-UI
- chore: Ingress-Port 8099→8777, Alex-Kly-Hersteller in Add-on-Beschreibung
- fix(3.15): Readback-Availability-Guard sieht `unavailable` nach WS-Outage

## 0.1.143 — 2026-05-20

- chore(5.1l): Sprint-Status und FunctionalTest-Tests nachgezogen
- feat(5.1l): Onboarding-Wiedererkennung, FunctionalTest/Running-Tests
- docs(5.1l): Story-Artefakt ergänzt, Marstek-Nachmittag-QA
- feat: Story 5.1l Onboarding-Wiedererkennung + Reaktionstest als Gefallen
- feat(live): Live-Screen vereinheitlichen — h1/Enum-Chip raus, eine Wirkungs-Euro-Wahrheit, Watt-only-Bilanz
- feat(live): Netz-Leistung-Tile zeigt wieder Watt-Wert mit Vorzeichen

## 0.1.142 — 2026-05-19

- feat: finalize 5.1j config drawer model

## 0.1.141 — 2026-05-19

- feat: Heute-Bilanz, Live-Diagramm-Symmetrie und Reaktionstest-Hinweise
- docs(5.1j): Schubladen-Modell-Konsolidierung — Kp-Max ratifiziert, Quell-Refs gefixt, Sextett-Korrektur

## 0.1.140 — 2026-05-19

- feat(5.5a): Hero letzte Aktion, open-loop-Fixes, Dev-Port 8777
- chore: Ingress-Port 8099→8777, Alex-Kly-Hersteller in Add-on-Beschreibung
- feat(5.5a): Hero-Footer zeigt letzte Aktion mit Werten (Neu-Impl gegen main)

## 0.1.139 — 2026-05-19

- fix: ERROR_ADVICE für Reaktionstest Pre-Check-Log-Keys

## 0.1.138 — 2026-05-19

- feat: SPEICHER PI-Defaults nach Akku-Hardware-Klasse
- docs(qa): Tagesanalyse 2026-05-18 Trucki+Victron + Runbook-Grid-Meter-Filter-Härtung
- feat: Live-Diagramm-Symmetrie Akku/WR (Story 5.8) + chartSeries
- fix(speicher): Integrator-Windup am SoC-Cap — voller Akku entlädt jetzt bei Netzbezug

## 0.1.137 — 2026-05-16

- docs: QA-Validierung SolakonONE Story 3.28 open_loop
- feat(brand): Setup-CTAs auf Marken-Rot + Sektions-Signatur-System

## 0.1.136 — 2026-05-16

- fix: Klartext „Anpassung zu klein" für min_step und Hysterese
- feat(brand): Marken-Rot Chrome-only + Rebrand Add-on-Name auf "Solalex"

## 0.1.135 — 2026-05-16

- fix: WR-Reaktionstest PV-Headroom und abbrechbares Readback
- docs: Story 3.23 — drei offene WR-Reaktionstest-Review-Punkte ergänzt

## 0.1.134 — 2026-05-16

- feat: Story 3.28 open_loop, Migration 009 und Readback-UI

## 0.1.133 — 2026-05-16

- feat: readback_mode für WR und Akku (Story 3.28)
- fix: Marstek Venus E RS485-Steuermodus-Select als Permission-Entity priorisieren

## 0.1.132 — 2026-05-15

- feat: Story 5.1i Verhalten-Settings nach Besitz (4-Block)

## 0.1.131 — 2026-05-15

- docs: Story 5.1i Settings-Restrukturierung und UX-Spec ergänzen
- fix: Sticky-Setpoint-Schutz — Hysterese-Cap + Trend-Override (Story 3.19)

## 0.1.130 — 2026-05-15

- docs: Videoskript „Der klebende Setpoint" (Zendure Live-Befund)

## 0.1.129 — 2026-05-15

- fix: SoC-Cap nur Latch-Richtung sperren; Live-Zyklen lesbar

## 0.1.128 — 2026-05-15

- fix: Akku-Readback Single-Source und Magnituden-Vergleich (Zendure)
- fix: Funk-Bridge- und Cloud-API-Beispiele in Hardware-Klasse-Picker (Akku)

## 0.1.127 — 2026-05-15

- fix: Funktionstest Status-Stale-Recovery, Wizard-Skip und Akku-Leistungs-Anzeige

## 0.1.126 — 2026-05-15

- feat: Akku-Hardware-Klasse für Rate-Limit und Reaktionstest-Step-Timing
- fix: mode_switch_single Setpoint-Echo Sign-Vergleich gegen abs(target)

## 0.1.125 — 2026-05-14

- fix: Akku-Power-Feedback-LivePreview-Vorzeichen an Backend-Konvention

## 0.1.124 — 2026-05-14

- feat: Story 3.27 WR-Reaktionstest Bridge-Write bei niedrigem Start-Limit

## 0.1.123 — 2026-05-14

- fix: Setpoint-Echo Readback schneller + grid_target_w-Default 10 W

## 0.1.122 — 2026-05-14

- feat: Story 3.26 WR-Hardware-Klasse Funk (OpenDTU/AhoyDTU) + 2.9-Feedback-Feinschliff
- feat: Story 2.9 Wizard Power-Feedback-Picker (Akku Pflicht, WR optional)

## 0.1.121 — 2026-05-13

- fix: Akku-Rate-Limit 30s (Readback-Kopplung), passive_only PI + Min-SoC-Schutz

## 0.1.120 — 2026-05-13

- fix: Akku-Rate-Limit-Default 5s, max_soc 100, SoC-Staleness für Pool/passive

## 0.1.119 — 2026-05-13

- feat: Story 3.23 WR-UI-Symmetrie + Story 3.24 WR-Reaktionstest (API, Wizard)

## 0.1.118 — 2026-05-13

- feat: Story 2.10 Akku-Hardware-Swap, Story 3.22 Regelungs-Profile, Folge-Specs 3.23/3.24

## 0.1.117 — 2026-05-12

- fix: Story-3.20-Code-Review-Härtung, Sprint 3.20 done + Story 2.10 angelegt

## 0.1.116 — 2026-05-12

- feat: Story 3.20 Drossel-PI, Wizard-Defaults und Sprint-/Doku-Stand

## 0.1.115 — 2026-05-12

- chore: story 2.2a abgeschlossen (Setpoint-Echo readback_invert, Tests, Sprint)

## 0.1.114 — 2026-05-12

- chore: story 3.19 auf backlog (Heartbeat zugunsten UI-Tuning-Hypothese)

## 0.1.113 — 2026-05-12

- fix: story 3.21 soc-cap-gates wiederholen 0-w-stop bis echo

## 0.1.112 — 2026-05-12

- feat: funktionstest setpoint-echo fallback und hysterese-feintuning

## 0.1.111 — 2026-05-11

- fix: speicher soc-kappen erkennen bei latched setpoint und flachem meter

## 0.1.110 — 2026-05-11

- fix: story-3-18 review smoothing am grid-meter und noise-band-range

## 0.1.109 — 2026-05-11

- feat: schreib-reduktion mit hysterese und median-noise-band

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
