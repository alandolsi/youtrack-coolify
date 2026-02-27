# DNS & SSL

## DNS-Einträge

Damit die Domain auf den Coolify-Server zeigt, werden folgende DNS-Records benötigt:

| Typ | Name | Wert | TTL |
|------|------|------|-----|
| A | `youtrack.example.com` | `<SERVER_IPv4>` | 300 |
| AAAA | `youtrack.example.com` | `<SERVER_IPv6>` | 300 |

> Ersetze `youtrack.example.com` durch deine tatsächliche (Sub-)Domain und die IP-Adressen durch die deines Servers.

## Cloudflare-Proxy (optional)

Falls du **Cloudflare** als DNS-Provider nutzt:

- **Proxied (orangene Wolke):** Möglich, aber Cloudflare terminiert dann TLS. Coolify muss ggf. auf HTTP-Only gestellt werden, damit kein doppeltes TLS entsteht.
- **DNS-only (graue Wolke):** Empfohlen für einfache Setups. Coolify verwaltet SSL komplett über Let's Encrypt.

> **Tipp:** Bei Cloudflare-Proxy und Coolify-SSL kann es zu Redirect-Loops kommen. Im Zweifel Cloudflare auf „Full (Strict)" stellen oder den Proxy deaktivieren.

## SSL über Coolify

Coolify bringt **automatische SSL-Zertifikate** via Let's Encrypt mit:

1. Domain in den Service-Einstellungen eintragen.
2. „HTTPS" aktivieren.
3. Coolify fordert automatisch ein Zertifikat an und erneuert es vor Ablauf.

Keine manuelle Zertifikatsverwaltung nötig.

## Base URL in YouTrack

Nach dem ersten Login in YouTrack:

1. **Administration → General Settings** öffnen.
2. Die **Base URL** auf `https://youtrack.example.com` setzen.
3. Speichern.

Dies stellt sicher, dass YouTrack korrekte Links in E-Mails, Webhooks und der Oberfläche generiert.
