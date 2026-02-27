# Coolify Setup – YouTrack

## 1. Neue Ressource anlegen

1. Im Coolify-Dashboard auf **„New Resource"** klicken.
2. Den Ziel-Server auswählen.
3. Als Typ **„Docker Compose"** wählen.

## 2. Docker Compose einfügen

- Entweder das **Git-Repository** verknüpfen (empfohlen) oder den Inhalt von `docker-compose.yml` direkt einfügen.
- Coolify erkennt die Services automatisch.

## 3. Umgebungsvariablen

- Im Tab **„Environment Variables"** die Werte aus `.env.example` eintragen:
  - `YOUTRACK_IMAGE_TAG` – gewünschte YouTrack-Version
  - `TZ` – Zeitzone (z. B. `Europe/Berlin`)
- Alternativ: `.env`-Datei in der Coolify-Oberfläche hochladen.

## 4. Domain setzen

1. In den Service-Einstellungen die **Domain** eintragen (z. B. `youtrack.example.com`).
2. Sicherstellen, dass der DNS-Eintrag auf den Server zeigt (siehe [dns-and-ssl.md](dns-and-ssl.md)).

## 5. HTTPS aktivieren

- Coolify generiert über **Let's Encrypt** automatisch ein SSL-Zertifikat.
- Option „Force HTTPS" aktivieren, damit HTTP → HTTPS umgeleitet wird.

## 6. Deploy

- Auf **„Deploy"** klicken und warten, bis der Container gestartet ist.
- Logs im Coolify-Dashboard prüfen – YouTrack braucht beim ersten Start 1–2 Minuten.

## 7. Healthcheck (optional)

In Coolify kann ein Healthcheck konfiguriert werden:

- **URL:** `http://localhost:8080/api/config`
- **Interval:** 30s
- **Timeout:** 10s
- **Retries:** 3

So erkennt Coolify, ob YouTrack korrekt läuft.
