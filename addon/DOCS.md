# Soalex — Add-on Dokumentation

Diese Datei ist die offizielle In-HA-Dokumentation des Add-ons. Der HA-Supervisor
rendert sie im Add-on-Detail-View.

## Installation

1. **Einstellungen → Add-ons → Add-on-Store** öffnen.
2. Oben rechts **⋮ → Repositories**.
3. URL eintragen: `https://github.com/thealkly/SoalexBeta`
4. Nach dem Refresh erscheint **Soalex** in der Liste. **Installieren**.
5. Nach dem Start öffnest du Soalex über die Seitenleiste; ist noch nichts
   eingerichtet, beginnt dort die Einrichtung
   ([Anleitung](https://soalex.de/anleitung/einrichtung/)).

## Einrichtung und Funktionstest

Die Einrichtung beginnt mit deinem Gerät: Marke antippen, drei Fragen
beantworten. Kennt Soalex das Gerät, kommen alle Einträge aus seinem
Gerätewissen; du bestätigst deinen Stromzähler. Der Funktionstest fährt dann
Laden, Anhalten und Entladen kurz an und prüft an deinem Stromzähler, ob es
wirklich ankommt — erst danach startet die Steuerung. Was sich gerade nicht
prüfen lässt (z. B. Entladen bei leerem Akku), steht als „Jetzt nicht
prüfbar" da — das prüft Soalex später im Betrieb selbst. Unter **Einstellungen → Anlage**
zeigt jedes Gerät danach seine Prüfpunkte.
→ [Anleitung: Soalex einrichten](https://soalex.de/anleitung/einrichtung/) ·
[Funktionstest](https://soalex.de/funktionen/funktionstest/)

**Was ist neu?** Jedes Release mit Erklärung und Bildern:
<https://soalex.de/neu/>

## Voraussetzungen

- **Home Assistant OS** (ausschließlich — siehe Abschnitt „Unterstützte
  HA-Versionen" für Details zu nicht unterstützten Varianten).
- Mindestens einen unterstützten Wechselrichter oder Akku im HA-Netzwerk.
- Für die Beta brauchst du keinen Lizenzschlüssel. Eine Beta-Version läuft
  30 Tage ab ihrem Erscheinen; danach hält Soalex die Steuerung an, bis du das
  nächste Update installierst. Eine Woche vorher weist Soalex dich darauf hin.

## Unterstützte HA-Versionen

- **Minimum:** 2026.4.0 (im `addon/config.yaml` via `homeassistant:`-Feld
  gepinnt; niedrigere Versionen erhalten eine Install-Warning im Add-on-Store).
- **Getestet bis:** 2026.4.3 (aktuelle stable zum Release-Zeitpunkt).
- **Unterstützt:** ausschließlich **Home Assistant OS**.
- **Nicht unterstützt:** Home Assistant Supervised, Home Assistant Container,
  Home Assistant Core.

Du weißt nicht, welche Variante du hast? Öffne in HA:
**Einstellungen → System → Info**.

## Unterstützte Hardware (Day 1)

- **Wechselrichter:** Hoymiles / OpenDTU, Trucki, ESPHome, MQTT-bridged — Limit-Regelung für Nulleinspeisung (Generic-Adapter über HA-Capabilities).
- **Akku:** Marstek Venus, Zendure SolarFlow, SolakonONE, Anker Solix, Hoymiles MS A2, Growatt Noah — Lade-/Entlade-Steuerung (Generic-Battery-Adapter, Topologie automatisch erkannt).
- **Smart Meter:** Shelly 3EM, ESPHome SML, Tibber, MQTT-bridged — Einspeisungs-Messung (Generic-Adapter).

Vendor-spezifische Tuning-Profile (z. B. Hoymiles-Drossel-Deadband) folgen in v1.5.

## Ressourcen-Budget (Raspberry Pi 4 Referenz)

- **Idle-RSS Ziel:** ≤ 150 MB
- **Idle-CPU Ziel:** ≤ 2 %
- **Aktiver Regelzyklus:** kurze Peaks bis ~10 % CPU

### Messung (Story 1.1 Skeleton, lokal via Docker)

| Messgröße | Gemessen | Ziel | Status |
|---|---|---|---|
| Idle-RSS | 64.9 MiB | ≤ 150 MB | ✅ 43 % des Budgets |
| Idle-CPU | 0.49 % | ≤ 2 % | ✅ 25 % des Budgets |

> Gemessen auf Docker Desktop (macOS, Apple Silicon) mit dem amd64-Image
> via Rosetta-Emulation. Auf einem echten Pi 4 (aarch64 nativ) sind die
> Werte tendenziell niedriger. Finale Validation erfolgt in der Beta-Phase
> auf echter Pi-4-Hardware.

## Daten-Persistenz

Alle dauerhaften Daten (SQLite-DB, Logs) liegen unter `/data/` und
überleben Add-on-Restart sowie Update.

```
/data/
├── soalex.db         # Betriebsdaten (KPIs, Config, Audit)
└── logs/
    └── soalex.log    # JSON-Zeilen, 10 MB × 5 Rotation
```

**Backup:** Soalex legt selbst keine Sicherungskopie an. Alles unter `/data/`
ist Teil des Add-on-Backups von Home Assistant (Einstellungen → System →
Backups). Willst du vor einem Update zurück können, erstell vorher ein Backup
oder hak beim Update „Backup erstellen“ an. Ab Soalex 0.1.187 werden
Logs und Diagnose-Kopien aus dem Backup ausgeschlossen, damit es klein bleibt.

## Keine externen Ports

Soalex kommuniziert ausschließlich über den Home-Assistant-Ingress-Proxy.
Es gibt keine externen Port-Expositionen. Dies ist eine harte Policy
(AC 7 Story 1.1, NFR28) und wird im `addon/config.yaml` via `ports: {}`
durchgesetzt.

## Datenschutz

Soalex sendet nie von selbst. Die Regelung läuft vollständig lokal, es gibt
keine Telemetrie. Nur wenn du „Diagnose an Alex senden" drückst (in Soalex
unten auf der Startseite unter „Feedback geben"), geht ein Diagnose-Paket an
Alex' Server in Deutschland (`inbox.soalex.de`). Es enthält den Verlauf deiner
Regelung, deine Geräte-Einstellungen mit Gerätenamen, das Protokoll, deine
letzten Bedienschritte in Soalex und deine Antworten — nie Lizenz oder
Passwörter. Alex sucht damit den Fehler und vergleicht die Auswertung über
Versionen, um Soalex zu verbessern; er löscht das Paket nach 90 Tagen, die
Auswertung nach 24 Monaten. Die Bedienschritte speichert Soalex nur bei dir;
sie gehen nur mit, wenn du sendest oder die Datei selbst herunterlädst. Löschen
lassen oder widersprechen: Mail an info@alkly.de mit Fallcode oder
Installations-ID.

Lieber von Hand? Unter „Lieber von Hand?" lädst du die Diagnose-Datei herunter
und lädst sie selbst ins Feedback-Formular hoch. Details:
[Diagnose an Alex senden](https://soalex.de/funktionen/diagnose-senden/) und
die [Datenschutzhinweise](https://alkly.de/datenschutzerklaerung/#soalex-diagnose).

## Akku-Regelung — wie Soalex misst und einstellt

Soalex liest deinen Smart Meter und verschiebt den Soll-Wert deines Akkus bei
jeder Anpassung um einen Teil der Abweichung vom Ziel — nie mit einem Sprung
über das Ziel hinaus. Einstellen musst du dafür nichts: Soalex misst im Betrieb
selbst, wie schnell deine Hardware antwortet, und passt sein Tempo daran an.
Unter **Einstellungen → Verhalten → 1 · Nulleinspeisung** klappst du die Zeile
deines Akkus auf: Dort steht, wie schnell er antwortet und wie oft Soalex den
Soll-Wert anpasst. Dort wählst du auch das
Regelungs-Profil (Schonend, Standard, Reaktiv); feinere Werte liegen in den
Profi-Einstellungen des Akkus.

## Cloud-Akkus (Anker Solix & Co)

Akkus, die ihre Steuerbefehle über die Hersteller-Cloud verarbeiten — Anker Solix
Solarbank ist der typische Vertreter — haben eine Reaktionszeit von rund 30 s
(Roundtrip Home Assistant → Cloud → Akku → Smart Meter). Das ist deutlich länger
als bei lokalen Akkus (Marstek Venus, Zendure SolarFlow, SolakonONE liegen bei
1–3 s). Soalex misst die Reaktionszeit selbst im laufenden Betrieb und passt
sein Tempo daran an — du musst dafür nichts einstellen und keinen Test starten.
Die 30-s-Sperre der Anker-Cloud (eine höhere Lastvorgabe wird erst nach 30 s
angenommen, eine niedrigere jederzeit) wartet Soalex seit Version 0.1.186 ab. Wähl bei Cloud-Akkus als
Rückmeldung „Nur Befehl prüfen“ und erwarte kein sekundengenaues Nachregeln.

## Grundregeln für Sensoren

Die meisten Einrichtungsprobleme kommen von einem falsch gewählten Sensor. Die
ausführliche Anleitung mit Bildern pro Gerät steht unter
<https://soalex.de/anleitung/akkus/>.

- **Netzzähler:** ein Sensor in Watt für deinen Anschluss, Plus = Bezug. Er
  muss mindestens alle 10 Sekunden einen Wert melden (Tasmota-Lesekopf:
  `TelePeriod 10`; Fronius-Zähler über Modbus TCP statt Solar API, die nur
  etwa alle 60 s liefert). Er muss den Strom messen, den dein Akku beeinflusst,
  alle Phasen zusammen — meist am Hausanschluss, im Mehrfamilienhaus also
  deinen Wohnungszähler. Ein einzelner Phasen-Kanal oder eine Steckdose reicht
  nicht.
- **Akku-Leistungssensor:** ein Sensor am Akku selbst. Nie der Netz- oder
  Hauszähler, nie ein PV- oder Balkonkraftwerk-Sensor. Gibt es keinen
  passenden, lass das Feld leer.
- **Wallbox-Sperre („Akku nicht entladen, während die Wallbox lädt“):** als
  Auslöser die Ladeleistung der Wallbox in Watt oder den EVCC-Ladepunkt-Status
  — nie den Netzzähler, nie einen kWh-Zähler.
- **Zweiter Haus-Akku:** nur für einen fremden Speicher mit eigener Regelung,
  nie für die eigenen Soalex-Akkus (z. B. nicht EVCCs `battery_power`, wenn
  EVCC die Soalex-Akkus führt).
- **EVCC:** die Batteriesteuerung von EVCC für die Soalex-Akkus ausschalten und
  stattdessen die Wallbox-Sperre von Soalex nutzen.

## Sonne übrig, günstig laden und andere Geräte im Haus

Was früher gesammelt unter „Verhalten → Deine Anlage" stand, ist seit 0.1.188
dort, wo es hingehört. Alles gilt für alle Akkus gemeinsam und speichert sich
sofort beim Ändern (kein Speichern-Button).

- **Entladen erlaubt** (Einstellungen → Verhalten → 1 · Nulleinspeisung): ein
  tägliches Zeitfenster, in dem deine Akkus überhaupt entladen dürfen — z. B.
  um nachts einen Mindest-Ladestand als Blackout-Puffer zu behalten.
  Standard: der ganze Tag.
- **Sonne übrig nutzen** (Einstellungen → Verhalten → 2 · Sonne übrig nutzen):
  Geräte wie Heizstab, Klimaanlage oder Waschmaschine bei Überschuss
  einschalten und mit mehreren Akkus den Überschuss erst an die anderen Akkus
  weitergeben. Die Solar-Prognose dafür wählst du je Gerät unter
  Einstellungen → Anlage.
  → [Sonne übrig](https://soalex.de/funktionen/sonne-uebrig/) ·
  [Solar-Prognose](https://soalex.de/funktionen/solar-prognose/)
- **Günstig laden** *(Alpha, ab Werk aus)* (Einstellungen → Verhalten →
  3 · Günstig laden): Mit dynamischem Stromtarif lädt Soalex den Akku aus dem
  Netz, wenn es sich gegenüber dem späteren Preis lohnt, und kann ihn für
  teure Stunden aufheben. → [Günstig laden](https://soalex.de/funktionen/guenstig-laden/)
- **Wallbox** (Einstellungen → Anlage → „Im Haus, aber nicht von Soalex
  gesteuert"): Wählst du den Lade-Sensor deiner Wallbox bzw. den
  Ladepunkt-Status von EVCC, hält Soalex den Akku zurück, solange das Auto
  lädt — der Akku-Strom soll nicht den Umweg über die Wallbox nehmen. Laden
  und Nulleinspeisung laufen normal weiter. Für EVCC empfiehlt sich der
  Status-Sensor mit Wert „C" (lädt), nicht der „freigegeben"-Schalter.
- **Zweiter Haus-Akku** (ebenda): für einen zusätzlichen, großen Haus-Akku
  mit eigener Nulleinspeisung (z. B. Huawei, Fronius, Sonnen, E3/DC). Soalex
  lädt nicht, während der Haus-Akku entlädt, und entlädt nicht, während er
  lädt — so schiebt kein Akku Strom in den anderen. Dafür den
  Leistungssensor des Haus-Akkus wählen (positiv = entlädt); zeigt dein
  Sensor es andersherum, hilft „Vorzeichen umkehren". Meldet der Sensor
  länger nichts (z. B. `unavailable`), regelt Soalex bewusst normal weiter,
  statt eine Nacht lang stillzustehen.

## Robustheit

- **Rückmeldung nach jedem Befehl:** Jeder Steuerbefehl an die Hardware
  wird nach dem Senden aus Home Assistant zurückgelesen. Stimmen Soll- und
  Ist-Wert nicht überein, verwirft Soalex die Anpassung, und die Liste
  „Was Soalex tut" auf der Startseite zeigt den Grund.
- **Sensor nicht verfügbar:** Bevor Soalex einen Wert schreibt, prüft es,
  ob der Sensor für die Rückmeldung in Home Assistant gerade einen Wert
  liefert. Ist er `unavailable` / `unknown` (z. B. Marstek-Modbus zwischen
  zwei Abfragen), überspringt Soalex die Anpassung und vermerkt „Sensor
  nicht verfügbar". Das verhindert blinde Befehle und Log-Rauschen in HA.
- **Schutzpause pro Gerät:** 30 s Mindestabstand zwischen zwei Anpassungen
  pro Gerät, gespeichert in der Datenbank (überlebt einen Neustart). Antwortet
  deine Hardware nachweislich schneller, verkürzt Soalex die Pause selbst auf
  bis zu 10 s.
- **Wie Soalex die Befehle prüft:** pro Gerät unter **Einstellungen → Anlage**,
  Karte aufklappen → Anschluss → „So prüft Soalex die Befehle". Soalex wählt
  die passende Stufe selbst; ändern nur, wenn deine Hardware keinen
  brauchbaren Sensor hat:
  - *Mit Rückmeldung* — Soalex prüft nach jedem Befehl den
    Leistungs- bzw. Echo-Sensor.
  - *Nur Befehl prüfen (langsamer Sensor)* — Soalex prüft nur, ob die Soll-Wert-Zahl
    übernommen wurde, nicht die tatsächliche Leistung. Sinnvoll für
    Akkus mit langsamem oder grob gerundetem Leistungs-Sensor
    (SolakonONE, Anker Solix, Zendure-Cloud): deren Sensor meldet
    minutenlang denselben Wert und löste sonst einen falschen
    Sicherheits-Stopp aus.
  - *Ohne Rückmeldung* — Soalex prüft **nicht**, ob die Hardware den
    Befehl tatsächlich ausführt. Nur wählen, wenn die Hardware keinen
    brauchbaren Leistungs- oder Rückmelde-Sensor hat. Was wegfällt:
    keine Bestätigung, dass der Befehl ankam, und (ohne hinterlegten
    Leistungs-Sensor) auch kein „Vermutlich Akku leer/voll"-Schutz.
    Was bleibt: Schreibpause, Hardware-Grenzen und der Verbindungs-
    Fail-Safe greifen weiterhin. Diese Stufe ist bewusst hinter eine
    Bestätigungs-Checkbox gelegt. Empfehlung: nach Möglichkeit einen
    Leistungs-Sensor am Gerät hinterlegen — dann fängt der
    verzögerte Effektivitäts-Schutz auch hier eine tote Hardware ab.

## Soalex Status in Home Assistant

Nach der Einrichtung legt Soalex acht Input-Helper in Home Assistant an,
die den internen Steuer-Status jederzeit per HA-Card oder Statistik-Graph
sichtbar machen. Sie liegen unter **Einstellungen → Geräte & Dienste →
Helfer** mit dem Filter `soalex_*`.

| Entity | Typ | Bedeutung |
| --- | --- | --- |
| `input_text.soalex_active_mode` | input_text | Aktuell aktiver Modus: `drossel`, `speicher`, `multi`, `export`, `paused`, `fail_safe`, `unknown` |
| `input_text.soalex_last_cycle_reason` | input_text | Letzter Cycle-Reason aus dem Audit-Trail (z. B. `noop: deadband`, `dispatched`, `fail_safe: range_check_violation`) |
| `input_text.soalex_last_command_at` | input_text | UTC-ISO-8601-Zeitstempel des letzten Schreibvorgangs |
| `input_text.soalex_fail_safe_state` | input_text | `inactive` (alles ok), `active_hold` (Fail-Safe greift), `active_release` (Erholung gerade aktiv) |
| `input_number.soalex_cycle_age_seconds` | input_number (`state_class=measurement`) | Sekunden seit dem letzten Cycle (0 = gerade jetzt; > 60 = Controller hängt) |
| `input_number.soalex_recent_cycles_count` | input_number (`state_class=measurement`) | Anzahl Cycles in der letzten Stunde |
| `input_number.soalex_fail_safes_today` | input_number (`state_class=measurement`) | Anzahl Fail-Safe-Events seit lokal-Mitternacht |
| `input_number.soalex_mode_switches_today` | input_number (`state_class=measurement`) | Anzahl Mode-Wechsel (z. B. DROSSEL → SPEICHER) seit lokal-Mitternacht |

**Nur Anzeige — keine Steuer-Eingänge:** Die `soalex_*`-Helfer zeigen
nur an, was Soalex gerade tut. Soalex liest sie nie und überschreibt sie
beim nächsten Update wieder. Setzt du z. B. `input_text.soalex_active_mode`
per Automation auf `paused`, pausiert das die Steuerung **nicht**: Soalex
regelt weiter. Neu angelegte Helfer tragen deshalb den Zusatz
„(nur Anzeige)" im Namen; bei bestehenden Installationen bleibt der alte
Name stehen. Zum Pausieren tippst du in der Soalex-Oberfläche oben auf
„Läuft …" (grüner Punkt) und bestätigst mit „Ja, pausieren"; „Fortsetzen" startet die
Steuerung wieder. Aus Home Assistant heraus geht das über den Schalter
„Soalex Steuerung" (siehe unten).

**Update-Verhalten:** Soalex aktualisiert die Helper nach jedem Cycle, gedrosselt auf max. 1 Update pro Helper pro 30 s. Bei Mode-Wechsel, Fail-Safe-Übergang oder Wechsel des Reason-Prefixes wird der Update sofort durchgereicht.

**Tages-Counter:** `fail_safes_today` und `mode_switches_today` sind in-memory; sie resetten bei lokal-Mitternacht und beim Add-on-Restart. Den vollständigen Tagesverlauf hält der HA-Recorder via `state_class: measurement` — Mid-Day-Restarts erscheinen als Sprung-zu-0 + Wieder-Anstieg.

**Helper manuell gelöscht?** Soalex schreibt eine Warnung ins Log (`status_helper_publish_failed`) und macht weiter — die Steuerung ist davon nicht betroffen. Den Helper kannst du wieder anlegen, indem du die Einrichtung erneut durchläufst (Einstellungen → Über Soalex → „Konfiguration zurücksetzen“, dann einrichten und aktivieren).

### Steuerung aus Home Assistant pausieren: `input_boolean.soalex_steuerung`

Der Schalter **„Soalex Steuerung"** ist der eine Helfer, den Soalex liest.
**An** heißt: Soalex steuert. **Aus** heißt: Soalex pausiert (bzw. fährt
gerade herunter). Du kannst ihn auf jedes Dashboard legen oder per
Automation schalten (`input_boolean.turn_off` / `turn_on`); er wirkt genau wie
„Pausieren" und „Fortsetzen" in der Soalex-Oberfläche, mit denselben
Einträgen im Verlauf.

- Soalex legt den Schalter nach dem Aktivieren an, bei bestehenden
  Installationen beim ersten Start nach dem Update. Löschst du ihn, legt
  Soalex ihn nicht wieder an; die Steuerung läuft davon unberührt weiter.
  Möchtest du ihn zurück, legst du unter **Helfer** einen Schalter mit dem
  Namen „Soalex Steuerung" an.
- Der Schalter zeigt immer den echten Zustand: Pausierst du in der
  Soalex-Oberfläche oder pausiert Soalex zum Schutz selbst, steht er auf aus.
- Lehnt Soalex das Umschalten ab (z. B. während eines Reaktionstests, oder
  „Fortsetzen" nach Ablauf der Beta-Phase), springt der Schalter zurück.
- Nach einem Neustart von Home Assistant oder Soalex gilt, was Soalex
  zuletzt gespeichert hat. Ein Neustart setzt eine pausierte Anlage nie fort
  und pausiert eine laufende nie.
- Ist der Schalter nicht verfügbar (`unavailable`/`unknown`), wertet Soalex
  das nicht als „aus".

### Diagnose-Endpoint `/api/v1/diagnostics/devices`

Für tiefere QA-Inspektion liefert das Add-on über die Ingress-API einen direkten Snapshot pro angelegtem Device. Beispiel-Response:

```json
{
  "devices": [
    {
      "id": 1,
      "type": "generic_battery",
      "role": "wr_charge",
      "entity_id": "number.akku_charge",
      "adapter_key": "generic_battery",
      "topology": "multi_entity",
      "battery_control": { "topology": "multi_entity", "discharge_setpoint_entity": "...", "...": "..." },
      "wizard_completed": true,
      "last_write_at": "2026-05-04T03:42:11Z",
      "last_cycle_reason": "dispatched",
      "writes_24h": 2881,
      "fail_safes_24h": 0,
      "noops_24h": 84219,
      "noop_reason_top3": [
        { "reason": "noop: deadband", "count": 45112 },
        { "reason": "noop: rate_limited", "count": 23001 },
        { "reason": "noop: wr_limit_state_cache_miss", "count": 16106 }
      ]
    }
  ],
  "generated_at": "2026-05-04T05:50:00Z"
}
```

`window_h` (Query-Parameter, Default 24, Max 168) wählt das Aggregat-Fenster. Der Endpoint ist auf p99 ≤ 200 ms ausgelegt (4 Devices × 100 000 Cycles).

## Support & Issues

- **Bug-Reports:** In Soalex unten auf der Startseite „Feedback geben" →
  „Diagnose an Alex senden" — ein Klick, du bekommst einen Fallcode. Oder
  über [GitHub Issues](https://github.com/thealkly/SoalexBeta/issues).
- **Kontakt:** info@alkly.de

---

Soalex — ein **Alex Kly** Produkt.
