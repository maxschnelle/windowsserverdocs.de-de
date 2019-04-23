Rufen Sie zunächst ein SSL-Zertifikat für Host-Überwachungsdienst, von Ihrer Zertifizierungsstelle. Jeden Hostcomputer muss das SSL-Zertifikat vertrauen, daher wird empfohlen, dass Sie das SSL-Zertifikat von Ihres Unternehmens public Key-Infrastruktur oder Drittanbietern Zertifizierungsstelle ausgeben. Beliebiges SSL-Zertifikat, das von IIS unterstützt wird jedoch vom Host-Überwachungsdienst bietet unterstützt **Name des Antragstellers des Zertifikats muss der vollqualifizierte Name des Host-Überwachungsdienst-Dienst entsprechen** (verteilter Netzwerkname Cluster). Beispielsweise sollte die Host-Überwachungsdienst-Domäne ist "bastion.local" und den Namen des Host-Überwachungsdienst-Diensts ist "Host-Überwachungsdienst", das SSL-Zertifikat für "hgs.bastion.local" ausgegeben werden. Sie können das Zertifikat der alternative Antragstellername bei Bedarf zusätzliche DNS-Namen hinzufügen.

Nachdem Sie die SSL-Zertifikat, öffnen Sie eine PowerShell-Sitzung mit erhöhten Rechten verfügen, und geben Sie entweder den Zertifikatpfad beim Ausführen von [Set-HgsServer](https://technet.microsoft.com/itpro/powershell/windows/host-guardian-service/server/set-hgsserver):


```powershell
$sslPassword = Read-Host -AsSecureString -Prompt "SSL Certificate Password"
Set-HgsServer -Http -Https -HttpsCertificatePath 'C:\temp\HgsSSLCertificate.pfx' -HttpsCertificatePassword $sslPassword
```

Oder, wenn Sie das Zertifikat bereits im lokalen Zertifikatspeicher installiert haben, können Sie es durch Fingerabdruck verweisen:

```powershell
Set-HgsServer -Http -Https -HttpsCertificateThumbprint 'A1B2C3D4E5F6...'
```

> [!IMPORTANT]
> Konfigurieren von Host-Überwachungsdienst mit einem SSL-Zertifikat wird den HTTP-Endpunkt nicht deaktiviert werden.
> Wenn Sie nur die Verwendung von HTTPS-Endpunkt zulassen möchten, konfigurieren Sie Windows-Firewall so, dass eingehende Verbindungen an Port 80 blockiert.
> **Ändern Sie die IIS-Bindungen nicht** für Host-Überwachungsdienst Websites So entfernen Sie den HTTP-Endpunkt an; es wird nicht unterstützt. zu diesem Zweck.
