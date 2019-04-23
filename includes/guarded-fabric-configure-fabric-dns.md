Es gibt viele Möglichkeiten zum Konfigurieren der namensauflösung für die Fabric-Domäne. Eine einfache Möglichkeit besteht darin, eine bedingte Weiterleitung-Zone im DNS für das Fabric zu einzurichten. Führen Sie die folgenden Befehle zum Einrichten dieser Zone in einer Windows PowerShell-Konsole mit erhöhten Rechten auf einem Fabric-DNS-Server. Ersetzen Sie den Namen und Adressen in der Windows PowerShell-Syntax finden Sie unten nach Bedarf für Ihre Umgebung. Fügen Sie der Masterserver für die zusätzlichen HGS-Knoten hinzu.

```
Add-DnsServerConditionalForwarderZone -Name 'bastion.local' -ReplicationScope "Forest" -MasterServers <IP addresses of HGS server>
```

<!-- Appears in guarded-fabric-configuring-fabric-dns-ad.md and guarded-fabric-configuring-fabric-dns.md and set-up-hgs-for-always-encrypted-in-sql-server.md
-->    