---
title: "Vorbereiten der Migration eines eigenständigen AD FS-Verbundservers"
description: "Enthält Informationen zum Vorbereiten der Migration von einem eigenständigen AD FS-Server zu Windows Server 2012."
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0c1fd2bc1026d9aee25c591cf5c91a1c59f66ee0
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
#  <a name="prepare-to-migrate-a-stand-alone-ad-fs-federation-server-or-a-single-node-ad-fs-farm"></a>Vorbereiten der Migration eines eigenständigen AD FS-Verbundservers oder einer AD FS-Farm mit einzelnem Knoten  
 
Zum Vorbereiten der Migration (dieselbe Servermigration) eines eigenständigen AD FS 2.0-Verbundservers oder einer Farm mit einzelnem Knoten AD FS zu Windows Server2012, Sie müssen exportieren und Sichern Sie die AD FS-Konfigurationsdaten von diesem Server.  
  
Führen Sie zum Exportieren der AD FS-Konfigurationsdaten die folgenden Aufgaben aus:  
  
-   [Schritt1: Exportieren der diensteinstellungen](#step-1-export-service-settings)  
  
-   [Schritt2: Exportieren der Anspruchsanbieter-Vertrauensstellungen](#step-2-export-claims-provider-trusts)  
  
-   [Schritt3: Exportieren der Vertrauensstellungen der vertrauenden Seite](#step-3-export-relying-party-trusts)  
  
-   [Schritt4: Sichern der benutzerdefinierten Attributspeicher](#step-4-back-up-custom-attribute-stores)  
  
-   [Schritt5: Sichern der webseitenanpassungen](#step-5-back-up-webpage-customizations)  
  
## <a name="step-1-export-service-settings"></a>Schritt1: Exportieren der diensteinstellungen  
 Führen Sie die folgenden Schritte, um die diensteinstellungen zu exportieren:  
  
### <a name="to-export-service-settings"></a>So exportieren Sie diensteinstellungen  
  
1.  Notieren Sie die Namen und den Fingerabdruck Wert für den Zertifikatantragsteller der vom Verbunddienst verwendete SSL-Zertifikat. Um das SSL-Zertifikat zu suchen, öffnen Sie die Internetinformationsdienste (Internet Information Services, IIS)-Verwaltungskonsole, wählen **Default Web Site** klicken Sie im linken Bereich auf **Bindungen...** in der **Aktion** Bereich, suchen und wählen Sie die Https-Bindung, klicken Sie auf **bearbeiten**, und klicken Sie dann auf **Ansicht**.  
  
> [!NOTE]
>  Optional können Sie auch das SSL-Zertifikat verwendet, indem Sie den Verbunddienst und seinen privaten Schlüssel in eine PFX-Datei exportieren. Weitere Informationen finden Sie unter [Exportieren des Bereichs der privaten Schlüssel eines Serverauthentifizierungszertifikats ](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md).  
>   
>  Exportieren des SSL-Zertifikats ist optional, da dieses Zertifikat in der persönliche Zertifikatspeicher des lokalen Computers gespeichert wird und bleibt im Upgrade Betriebssystems erhalten.  
  
2.  Notieren Sie die Konfiguration der Kommunikation zwischen den AD FS-Dienst, tokenentschlüsselungs- und Tokensignaturzertifikate Zertifikate.  Um alle Zertifikate anzuzeigen, die verwendet werden, öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung:`PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl zum Erstellen einer Liste aller Zertifikate in einer Datei verwendet `PSH:>Get-ADFSCertificate | Out-File “.\certificates.txt”`  
  
> [!NOTE]
>  Sie können optional auch Exportieren alle Tokensignatur, tokenverschlüsselung oder Dienstkommunikation Zertifikate und Schlüssel, die nicht intern, zusätzlich zu allen selbstsignierten Zertifikaten generiert werden. Sie können alle Zertifikate anzeigen, die auf dem Server werden mithilfe von Windows PowerShell. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung:`PSH:>add-pssnapin “Microsoft.adfs.powershell`. Führen Sie dann den folgenden Befehl aus, um alle Zertifikate anzuzeigen, die auf dem Server werden `PSH:>Get-ADFSCertificate`. Die Ausgabe dieses Befehls umfasst StoreLocation- und StoreName-Werte, die den Speicherort für die einzelnen Zertifikate angeben. Anschließend können Sie die Anleitung im [Exportieren des Bereichs der privaten Schlüssel eines Serverauthentifizierungszertifikats](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md) jedes Zertifikat und seinen privaten Schlüssel in eine PFX-Datei exportieren.  
>   
>  Das Exportieren dieser Zertifikate ist optional, da alle externen Zertifikate während der Aktualisierung des Betriebssystems beibehalten werden.  
  
3.  Exportieren Sie AD FS 2.0-verbunddiensteigenschaften wie etwa den verbunddienstnamen, Anzeigename des Verbunddiensts und den Bezeichner des Verbunddiensts in eine Datei.  
  
Um die verbunddiensteigenschaften zu exportieren, öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung:`PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl zum Exportieren der verbunddiensteigenschaften:`PSH:> Get-ADFSProperties | Out-File “.\properties.txt”`.  
  
Die Ausgabedatei enthält die folgenden wichtigen Konfigurationswerte:  
  
    
|**Den Namen der verbunddiensteigenschaft von Get-ADFSProperties gemeldet**|**Den Namen der verbunddiensteigenschaft in AD FS-Verwaltungskonsole**|
|------|------|
|HostName|Verbunddienstname|  
|Bezeichner|Bezeichner des Verbunddiensts|  
|"DisplayName"|Anzeigename des Verbunddiensts|  
  
4.  Sichern der Anwendungskonfigurationsdatei. Neben anderen Einstellungen enthält diese Datei die Verbindungszeichenfolge der Richtliniendatenbank.  
  
Sie müssen manuell kopieren, zum Sichern der Anwendungskonfigurationsdatei der `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` Datei an einem sicheren Speicherort auf einem Sicherungsserver.  
  
> [!NOTE]
>  Notieren Sie sich die Datenbankverbindungszeichenfolge in dieser Datei befindet sich direkt hinter "Policystore Connectionstring ="). Wenn die Verbindungszeichenfolge eine SQL Server-Datenbank angegeben ist, wird der Wert beim Wiederherstellen der ursprünglichen AD FS-Konfigurations auf dem Verbundserver benötigt.  
>   
>  Im folgenden finden Sie ein Beispiel für eine WID-Verbindungszeichenfolge: `“Data Source=\\.\pipe\mssql$microsoft##ssee\sql\query;Initial Catalog=AdfsConfiguration;Integrated Security=True"`. Im folgenden finden Sie ein Beispiel für eine SQL Server-Verbindungszeichenfolge: `"Data Source=databasehostname;Integrated Security=True"`.  
  
5.  Notieren Sie die Identität des AD FS 2.0-Verbunddienstkontos und das Kennwort für dieses Konto.  
  
Der Identitätswert befindet, überprüfen Sie die **Anmelden als** Spalte **AD FS 2.0-Windows-Dienst** in der **Dienste** Konsole und zeichnen Sie diesen Wert manuell.  
  
> [!NOTE]
>  Für einen eigenständigen Verbunddienst wird das integrierte Konto Netzwerkdienst verwendet.  In diesem Fall müssen Sie nicht über ein Kennwort verfügen.  
  
6.  Exportieren Sie die Liste der aktivierten AD FS-Endpunkte in eine Datei.  
  
Zu diesem Zweck öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung:`PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um die Liste der aktivierten AD FS-Endpunkte in eine Datei zu exportieren:`PSH:> Get-ADFSEndpoint | Out-File “.\endpoints.txt”`.  
  
7.  Exportieren Sie alle benutzerdefinierten anspruchbeschreibungen in eine Datei.  
  
Zu diesem Zweck öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung:`PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um alle benutzerdefinierten anspruchbeschreibungen in eine Datei zu exportieren:`Get-ADFSClaimDescription | Out-File “.\claimtypes.txt”`.  
  
##  <a name="step-2-export-claims-provider-trusts"></a>Schritt2: Exportieren der Anspruchsanbieter-Vertrauensstellungen  
 Um die Anspruchsanbieter-Vertrauensstellungen zu exportieren, führen Sie die folgenden Schritteaus:  
  
### <a name="to-export-claims-provider-trusts"></a>So exportieren Sie Anspruchsanbieter-Vertrauensstellungen  
  
1.  Sie können Windows PowerShell verwenden, um alle Anspruchsanbieter-Vertrauensstellungen zu exportieren. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um alle Anspruchsanbieter-Vertrauensstellungen zu exportieren:`PSH:>Get-ADFSClaimsProviderTrust | Out-File “.\cptrusts.txt”`.  
  
## <a name="step-3-export-relying-party-trusts"></a>Schritt3: Exportieren der Vertrauensstellungen der vertrauenden Seite  
 Um die Vertrauensstellungen der vertrauenden Seite exportieren möchten, führen Sie die folgenden Schritteaus:  
  
### <a name="to-export-relying-party-trusts"></a>So exportieren Sie Vertrauensstellungen der vertrauenden Seite  
  
1.  Öffnen Sie zum Exportieren der Vertrauensstellungen alle vertrauenden Seite Windows PowerShell und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung:`PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl zum Exportieren der Vertrauensstellungen alle vertrauenden Seite:`PSH:>Get-ADFSRelyingPartyTrust | Out-File “.\rptrusts.txt”`.  
  
## <a name="step-4-back-up-custom-attribute-stores"></a>Schritt4: Sichern der benutzerdefinierten Attributspeicher  
 Finden Sie Informationen zu benutzerdefinierten attributspeichern von AD FS verwendeten mithilfe von Windows PowerShell. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie den folgenden Befehl Informationen zu benutzerdefinierten Attributspeicher:`PSH:>Get-ADFSAttributeStore`. Die Schritte zum Aktualisieren oder Migrieren von attributspeichern variieren.  
  
## <a name="step-5-back-up-webpage-customizations"></a>Schritt5: Sichern der webseitenanpassungen  
 Um alle webseitenanpassungen zu sichern, kopieren Sie die AD FS-Webseiten und die **"Web.config"** Datei aus dem Verzeichnis, das den virtuellen Pfad zugeordnet ist **"/ Adfs/ls"** in IIS. Es wird standardmäßig der **%systemdrive%\inetpub\adfs\ls** Verzeichnis.  

## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration der AD FS 2.0-Verbundserver-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren der AD FS 2.0-Verbundserver-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)