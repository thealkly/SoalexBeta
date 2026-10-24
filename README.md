# Soalex

**Sekundengenaue aktive Nulleinspeisung und Akku-Pool-Steuerung als Home-Assistant-Add-on.**

Soalex steuert Wechselrichter und Akkus sekundengenau über die Home-Assistant-WebSocket-API.
Die Regelung läuft 100 % lokal, keine Telemetrie, kein Cloud-Zwang. Soalex sendet nie von
selbst — nur wenn Du „Diagnose an Alex senden" drückst oder eine Diagnose selbst exportierst,
verlassen Daten Dein System.

> **Status:** Beta. Aktive Erprobung mit ausgewählten Beta-Tester:innen.

## Was ist neu?

**0.1.188** — Neue Einrichtung „Gerät zuerst": Du wählst dein Gerät, Soalex füllt alles aus
seinem Gerätewissen vor, und der Funktionstest beweist am Stromzähler, dass Laden, Anhalten
und Entladen wirklich ankommen. Dazu „Diagnose an Alex senden" mit einem Klick,
Prüfpunkte je Gerät, eine selbst gewählte Solar-Prognose für „Sonne übrig" und als Alpha
„Günstig laden" bei dynamischem Stromtarif.
→ **[Alles Neue mit Erklärung und Bildern](https://soalex.de/neu/0-1-188/)**

- **0.1.187** — Soalex sagt, was wirklich passiert (stiller Zähler, zurückgesetzter Sollwert,
  falscher Sensor), Geräte bei Sonnenüberschuss einschalten, „Sonne vor Akku".
- **0.1.186** — Soalex sagt, wenn dein Akku nicht mehr antwortet; drei Einrichtungs-Fallen
  behoben, Diagnose-Export startet zuverlässig.

Alle Releases: [soalex.de/neu](https://soalex.de/neu/) · vollständige Historie im
[Changelog](./addon/CHANGELOG.md).

## Installation

Voraussetzung: **Home Assistant OS** auf `amd64` oder `aarch64`. Andere HA-Varianten
(Supervised, Container, Core) werden in der Beta nicht unterstützt.

1. In Home Assistant: **Einstellungen → Add-ons → Add-on-Store**.
2. Oben rechts **⋮ → Repositories**.
3. URL eintragen: `https://github.com/thealkly/SoalexBeta`
4. Nach dem Refresh erscheint **Soalex** in der Add-on-Liste.
5. **Installieren**, dann starten. Du öffnest Soalex über die Seitenleiste; ist noch nichts
   eingerichtet, beginnt dort die Einrichtung
   ([Anleitung](https://soalex.de/anleitung/einrichtung/)).

**Update:** Einstellungen → Add-ons → Soalex → **Update**, sobald eine neue Version
angeboten wird — ohne neue Einrichtung, deine Konfiguration bleibt erhalten.

**Beta-Laufzeit:** jede Beta-Version ist ab dem Build-Zeitpunkt 30 Tage lang aktiv.
Ab 7 Tagen vor Ablauf zeigt der Live-Screen einen Hinweis-Banner, danach einen
deutlichen „Beta-Phase beendet"-Banner und die Steuerung pausiert, bis du auf die
nächste Version updatest. Kein Datenverlust, keine Neueinrichtung nötig — einfach
updaten.

## Was Soalex kann

### Nulleinspeisung & Akku-Steuerung

Soalex hält deine Einspeisung sekundengenau auf null (oder auf einen von dir
gewählten kleinen Toleranz-Wert) und lädt/entlädt deinen Akku passend zum
gerade verfügbaren Überschuss bzw. Bezug. Wie schnell deine Hardware antwortet,
misst Soalex im Betrieb selbst und passt sein Tempo daran an — du musst nichts
von Hand einstellen. Jeder Befehl an die Hardware wird nachgeprüft (Closed-Loop-
Readback), bevor der nächste Zyklus läuft.

### Einrichtung mit Beweis

Die Einrichtung beginnt mit deinem Gerät: Marke antippen, drei Fragen
beantworten — kennt Soalex das Gerät, kommen alle Einträge aus seinem
Gerätewissen. Der Funktionstest fährt Laden, Anhalten und Entladen kurz an und
prüft an deinem Stromzähler, ob es ankommt. Unter **Einstellungen → Anlage**
zeigt jedes Gerät danach seine Prüfpunkte.
[Anleitung: Soalex einrichten](https://soalex.de/anleitung/einrichtung/)

### Mehrere Akkus gleichzeitig (Multi-Akku)

Hast du mehr als einen Akku, verwaltet Soalex alle als gemeinsamen Pool: Laden
und Entladen wird sinnvoll über alle Akkus verteilt, jeder Akku lässt sich
einzeln einrichten, ändern oder nachträglich hinzufügen. Ein nicht mehr
reagierender Akku (z. B. wegen einer toten Verbindung) bekommt seinen Anteil
entzogen — der Rest des Pools regelt normal weiter.

### Ohne Ladestand-Sensor (SoC-los)

Hat dein Akku-Setup keinen auslesbaren Ladestand (z. B. eine CAN-/BMS-Bridge
ohne SoC-Wert), kann Soalex trotzdem regeln — über die Leistung; „voll" und
„leer" erkennt dann die Hardware selbst.

### Sonne übrig nutzen und günstig laden

Unter **Einstellungen → Verhalten** stehen die Regeln als Stufen:
**1 · Nulleinspeisung** (u. a. „Entladen erlaubt" als tägliches Zeitfenster),
**2 · Sonne übrig nutzen** (Geräte wie Heizstab oder Klimaanlage bei
Überschuss einschalten, Überschuss an andere Akkus weitergeben) und **3 · Günstig laden** *(Alpha)* — bei dynamischem Tarif lädt
Soalex den Akku aus dem Netz, wenn es sich gegenüber dem späteren Preis lohnt.
Die Solar-Prognose dafür wählst du je Gerät unter **Einstellungen → Anlage**.
Mehr: [Sonne übrig](https://soalex.de/funktionen/sonne-uebrig/) ·
[Solar-Prognose](https://soalex.de/funktionen/solar-prognose/) ·
[Günstig laden](https://soalex.de/funktionen/guenstig-laden/)

### Andere Geräte im Haus

Wallbox und ein zweiter Haus-Akku mit eigener Regelung (Huawei, Fronius,
Sonnen, E3/DC) stehen unter **Einstellungen → Anlage → „Im Haus, aber nicht von
Soalex gesteuert"**. Soalex entlädt deinen Akku nicht, während das Auto lädt,
und arbeitet nie gegen den Haus-Akku. Beides gilt für alle Akkus gemeinsam.

### Diagnose & Support

Acht Home-Assistant-Helfer (`input_text.soalex_*` / `input_number.soalex_*`)
zeigen den internen Status jederzeit als Karte oder Statistik-Graph; über
`input_boolean.soalex_steuerung` pausierst du die Steuerung aus Home Assistant.
Klemmt etwas, drückst du in Soalex **„Diagnose an Alex senden"** — ein Klick,
du bekommst einen Fallcode. Wer lieber von Hand arbeitet, lädt die
Diagnose-Datei herunter und schickt sie selbst.
[Was im Paket ist](https://soalex.de/funktionen/diagnose-senden/)

## Unterstützte Hardware (Day 1)

- **Wechselrichter:** Hoymiles / OpenDTU, Trucki, ESPHome, MQTT-bridged (Generic-Adapter
  über HA-Capabilities — Domain + `unit_of_measurement`)
- **Akku:** Marstek Venus, Zendure SolarFlow, SolakonONE, Anker Solix, Hoymiles MS A2,
  Growatt Noah (Generic-Battery-Adapter — Topologie automatisch erkannt)
- **Smart Meter:** Shelly 3EM, ESPHome SML, Tibber, MQTT-bridged (Generic-Adapter)

Vendor-spezifische Tuning-Profile (z. B. Hoymiles-Drossel-Deadband) sind für
Folge-Releases geplant.

## Sicherheits- und Datenschutz-Grundsätze

- **Regelt 100 % lokal:** keine Cloud-Roundtrips für Steuerung oder Monitoring. Soalex sendet
  nie von selbst; nur wenn Du „Diagnose an Alex senden" drückst oder eine Diagnose selbst
  exportierst, verlassen Daten Dein System
  ([Datenschutzhinweise](https://alkly.de/datenschutzerklaerung/#soalex-diagnose)).
- **Closed-Loop-Readback:** jeder Schreib-Befehl an die Hardware wird verifiziert,
  bevor der nächste Zyklus läuft.
- **Rate-Limit + Fail-Safe:** persistierte Schreib-Limits pro Gerät; bei
  Kommunikations-Ausfall hält Soalex das letzte bekannte Limit, statt freizugeben.
- **Kein Online-Check, keine Telemetrie:** Soalex ruft keinen Lizenz- oder
  Statistik-Server auf. Die einzige Verbindung nach außen ist das Diagnose-Paket an
  `inbox.soalex.de` — und nur, wenn Du es selbst sendest.

## Weiterführende Dokumentation

- **[soalex.de](https://soalex.de/)** — Anleitungen, Funktionen und
  [was in jedem Release neu ist](https://soalex.de/neu/).
- **[Changelog](./addon/CHANGELOG.md)** — vollständige Versionshistorie.
- **[DOCS.md](./addon/DOCS.md)** — ausführliche Nutzungs-Doku: Installation,
  unterstützte HA-Versionen, Ressourcen-Budget, Daten-Persistenz, Akku-Regelung
  im Detail, Cloud-Akkus, Robustheit/Fail-Safes, Status-Helper in Home Assistant.

## Lizenz

Proprietär — siehe [LICENSE](LICENSE). Source ist zur Auditierbarkeit offen, aber
nicht freie Software.

## Kontakt & Support

Alex Kly — info@alkly.de
