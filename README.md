# Fahrzeugakte – Downloads

Diagnose- und Reparaturdokumentation pro Fahrzeug für Werkstätten und Autohäuser: Fahrzeuge, Aufträge, Einträge mit
Fehlercodes, durchgeführten Arbeiten und Teilen, Fotos und Dokumente, Materialbestellliste, Benutzer mit Rollen und Rechten.
Bedienung im Browser (PC, Tablet, Handy); alle Daten bleiben im Betrieb.

Die Dateien stehen unter [Releases](https://github.com/areadox/Fahrzeugakte-Downloads/releases/latest).

## Windows

`Fahrzeugakte-Setup-<Version>.exe` herunterladen und ausführen. Das Programmfenster zeigt die Adressen, unter denen
die Fahrzeugakte im Netzwerk erreichbar ist (Standard-Port 8090). `Fahrzeugakte-portable.exe` läuft ohne Installation.

## Linux (Dienst)

```
curl -fsSL https://github.com/areadox/Fahrzeugakte-Downloads/releases/latest/download/install.sh | sudo sh
```

Legt den Dienst `fahrzeugakte` an (startet mit dem Rechner) und fragt nach Name und Passwort für den ersten Admin.
Programm in `/opt/fahrzeugakte`, Daten in `/var/lib/fahrzeugakte`, Log: `journalctl -u fahrzeugakte`.

Optionen hinter `sh -s --`, z.B. `… | sudo sh -s -- --port 8095`:

| Option | Wirkung |
|---|---|
| `--port N` | anderer Port (auch später im Browser unter *Admin → Einstellungen*) |
| `--docker` | als Docker-Container statt als Dienst |
| `--deinstallieren` | Dienst und Programm entfernen, Daten bleiben erhalten |

Ein erneuter Aufruf aktualisiert bzw. repariert die Installation. Läuft auf jeder x86_64-Distribution.

## Linux (Docker)

```
curl -fsSL https://github.com/areadox/Fahrzeugakte-Downloads/releases/latest/download/install.sh | sudo sh -s -- --docker
```

oder von Hand: `Dockerfile`, `start.sh` und `compose.yml` aus dem Release in einen Ordner legen und
`docker compose up -d --build`. Daten im Unterordner `daten`.

## Erster Start

Im Browser `http://<Rechner>:8090` öffnen. Gibt es noch keinen Benutzer, unter *Admin → Benutzer* den ersten Admin
anlegen – danach meldet sich jeder mit eigenem Namen und Passwort an.

## Funktionen (Auswahl)

- Fahrzeuge mit FIN, Kennzeichen und **Schlüsselnummer (HSN/TSN)**: Hersteller, Modell und Motor werden aus dem eingebauten
  KBA-Verzeichnis „Hersteller und Typen – Pkw“ übernommen – offline, ohne Zugang zu einem Portal.
- Aufträge mit eigener Auftragsnummer; darin Aufgaben mit eigenem Formular: **Diagnose** (Arbeitsschritte mit Soll/Ist/Ergebnis,
  Dauer, Fehlercodes), **Reparatur** (direkt aus der Diagnose, mit Probefahrt und „Fehlerspeicher gelöscht“),
  **Wartung/Inspektion** (Checkliste, nächster Service), **Dokument** und **Sonstiges**; Auftrag abschließen, wenn alles erledigt ist.
- Bei Renault und Dacia im Auftrag zusätzlich **MCS-Code**, **Katalogfunktion** und **Garantie-Code** (auch im Druck und auf der Diagnosekarte).
- **Diagnosekarte** zum Ausdrucken, bei Renault und Dacia zusätzlich die Renault „Allgemeine Diagnosekarte“;
  Fotos und PDFs der Diagnose werden als Anlagen mitgedruckt.
- **Auftrag drucken** mit allen Aufgaben, Diagnosekarten und Dokumenten (Fotos, PDFs als Anlagen) – alles einzeln auswählbar.
- Dokumente aus dem Posteingang direkt an die passende Aufgabe im Auftrag (z.B. an die Diagnose) zuordnen.
- „← Zurück“ auf jeder Seite führt immer auf die zuletzt angesehene Seite.
- Benutzer mit Rollen und Rechten, Materialbestellliste, Artikel und Preise, Posteingang.

## Drucken in die Fahrzeugakte

Aus jedem Programm (DMS, Prüfprotokolle, Diagnoseberichte …) auf den Drucker **„Fahrzeugakte“** drucken – das Dokument
landet im **Posteingang**, und das passende Fahrzeug wird anhand von FIN oder Kennzeichen vorgeschlagen.

- **Windows-Programm:** Drucker im Programmfenster unter *Drucker* einrichten.
- **Andere PCs / Linux-Server:** im Browser unter *Posteingang* auf *Drucker für diesen PC herunterladen* klicken,
  die Datei auf dem PC doppelklicken und die Administrator-Abfrage bestätigen. Gedruckt wird über das Netzwerk
  (Port 9100, ein- und ausschalten unter *Admin → Einstellungen*). Bei aktiver Firewall: `sudo ufw allow 9100/tcp`;
  bei Docker `"9100:9100"` unter `ports` in der `compose.yml`.

## Updates

Im Browser unter *Admin → Update*: *Nach Updates suchen*, dann *Jetzt installieren*. Die Datenbank wird vorher
gesichert, die Prüfsumme geprüft; danach startet die Fahrzeugakte von selbst neu.

## Prüfsummen

Zu jeder Programmdatei gibt es eine `.sha256`-Datei, z.B. `sha256sum -c fahrzeugakte-server-linux-x86_64.sha256`.

## Lizenzen Dritter

Die Fahrzeugakte enthält Open-Source-Bibliotheken unter freizügigen Lizenzen. Ihre Lizenzhinweise stehen in
`LIZENZEN-DRITTER.html` (liegt jedem Release bei), im Programm unten auf jeder Seite unter *Lizenzen Dritter* und im
Startmenü (Windows).

Alle Rechte vorbehalten.
