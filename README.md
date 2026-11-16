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

## Updates

Im Browser unter *Admin → Update*: *Nach Updates suchen*, dann *Jetzt installieren*. Die Datenbank wird vorher
gesichert, die Prüfsumme geprüft; danach startet die Fahrzeugakte von selbst neu.

## Prüfsummen

Zu jeder Programmdatei gibt es eine `.sha256`-Datei, z.B. `sha256sum -c fahrzeugakte-server-linux-x86_64.sha256`.

Alle Rechte vorbehalten.
