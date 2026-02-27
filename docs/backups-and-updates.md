# Backups & Updates

## Wichtige Volumes

| Volume | Pfad im Container | Inhalt |
|--------|-------------------|--------|
| `youtrack_data` | `/opt/youtrack/data` | Datenbank, Indizes, Anhänge |
| `youtrack_conf` | `/opt/youtrack/conf` | Konfiguration, Lizenzdaten |
| `youtrack_logs` | `/opt/youtrack/logs` | Logdateien (weniger kritisch) |
| `youtrack_backups` | `/opt/youtrack/backups` | Von YouTrack erstellte Backups |

## Backup-Strategie

### Automatische Backups in YouTrack

YouTrack erstellt standardmäßig regelmäßige Backups im Verzeichnis `/opt/youtrack/backups`. Diese enthalten die Datenbank und Konfiguration.

### Zusätzliche Sicherung (empfohlen)

Das Backup-Volume sollte **regelmäßig extern gesichert** werden:

```bash
# Beispiel: Backup-Volume auf den Host kopieren
docker run --rm \
  -v youtrack_backups:/source:ro \
  -v /path/to/host/backup:/target \
  alpine cp -a /source/. /target/

# Oder per Cron-Job (z. B. täglich um 03:00):
# 0 3 * * * /path/to/backup-script.sh
```

### Offsite-Backup

Für maximale Sicherheit die Backups zusätzlich auf einen externen Speicher übertragen (S3, SFTP, NAS o. Ä.).

## Updates

### Vorgehensweise

1. **Vor dem Update ein Backup erstellen** (oder prüfen, dass ein aktuelles vorhanden ist).
2. Neue Version auf [Docker Hub](https://hub.docker.com/r/jetbrains/youtrack/tags/) prüfen.
3. `YOUTRACK_IMAGE_TAG` in der `.env` oder in den Coolify-Umgebungsvariablen anpassen.
4. In Coolify **Redeploy** auslösen.
5. Logs prüfen – YouTrack migriert beim Start automatisch die Datenbank.

### Rollback

Falls nach einem Update Probleme auftreten:

1. Den **alten Image-Tag** wieder in `YOUTRACK_IMAGE_TAG` eintragen.
2. Erneut **Redeploy** in Coolify.
3. Falls die Datenbank bereits migriert wurde: Backup aus dem `youtrack_backups`-Volume wiederherstellen.

> **Hinweis:** Major-Version-Upgrades können Datenbankmigrationen auslösen, die nicht rückgängig gemacht werden können. In diesem Fall ist ein Backup-Restore erforderlich.
