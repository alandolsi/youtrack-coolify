# YouTrack on Coolify

Self-hosted [JetBrains YouTrack](https://www.jetbrains.com/youtrack/) deployed via [Coolify](https://coolify.io/) using Docker Compose.

## Voraussetzungen

- **Coolify** (v4+) auf einem Server installiert
- **Domain / Subdomain** (z. B. `youtrack.example.com`)
- **DNS A/AAAA-Record** zeigt auf den Coolify-Server
- Coolify übernimmt **Reverse Proxy & SSL** (Traefik / Caddy)

## Quickstart

1. **Repository klonen**
   ```bash
   git clone https://github.com/alandolsi/youtrack-coolify.git
   ```
2. **`.env.example` kopieren** und anpassen:
   ```bash
   cp .env.example .env
   ```
3. In **Coolify** eine neue Ressource anlegen → _Docker Compose_ wählen.
4. Das Repository (oder den Inhalt von `docker-compose.yml`) in Coolify einfügen.
5. **Domain** in den Coolify-Einstellungen setzen (z. B. `youtrack.example.com`).
6. **HTTPS** aktivieren – Coolify stellt automatisch ein Let's Encrypt-Zertifikat aus.
7. **Deploy** klicken.
8. Nach dem Start den **Setup-Wizard** im Browser öffnen (`https://youtrack.example.com`).
9. Admin-Account anlegen und **2FA aktivieren**.
10. In YouTrack unter _Administration → General → Base URL_ die Domain eintragen.

## Update-Strategie

1. Neue Version auf [Docker Hub](https://hub.docker.com/r/jetbrains/youtrack/tags/) prüfen.
2. `YOUTRACK_IMAGE_TAG` in `.env` (oder `docker-compose.yml`) auf die neue Version setzen.
3. In Coolify **Redeploy** auslösen.
4. **Rollback:** Alten Tag wieder eintragen und erneut deployen.

## Backups

- Das Volume `youtrack_backups` enthält von YouTrack erstellte Backups.
- **Empfehlung:** Regelmäßig das Backup-Volume exportieren oder per Cron-Job sichern.
- Wichtige Volumes: `youtrack_data`, `youtrack_conf`, `youtrack_backups`.
- Details: [docs/backups-and-updates.md](docs/backups-and-updates.md)

## Sicherheit

- **Admin-Account** mit starkem Passwort und **2FA** absichern.
- YouTrack und Coolify regelmäßig **updaten**.
- Zugriff auf das Coolify-Dashboard **einschränken** (IP-Whitelist, VPN o. Ä.).
- Keine Secrets in dieses Repository committen – `.env` ist in `.gitignore` gelistet.

## Dokumentation

| Datei | Inhalt |
|---|---|
| [docs/coolify-setup.md](docs/coolify-setup.md) | Schritt-für-Schritt Coolify-Einrichtung |
| [docs/dns-and-ssl.md](docs/dns-and-ssl.md) | DNS-Einträge & SSL-Konfiguration |
| [docs/backups-and-updates.md](docs/backups-and-updates.md) | Backups, Updates & Rollback |

## Lizenz

[MIT](LICENSE)
