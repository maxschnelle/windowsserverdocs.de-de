---
title: Vorbereiten der Migration eines eigenständigen AD FS Verbund Servers
description: Enthält Informationen zum Vorbereiten der Migration eines eigenständigen AD FS Servers zu Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 09b8cbd9097a95cd00b1413ce9e32ff9bf2f44c3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359323"
---
#  <a name="prepare-to-migrate-a-stand-alone-ad-fs-federation-server-or-a-single-node-ad-fs-farm"></a>Vorbereiten der Migration eines eigenständigen AD FS Verbund Servers oder einer AD FS Farm mit einem einzelnen Knoten  
 
Zum Vorbereiten der Migration (dieselbe Servermigration) eines eigenständigen AD FS 2,0-Verbund Servers oder einer AD FS-Farm mit einem einzelnen Knoten zu Windows Server 2012 müssen Sie die AD FS Konfigurationsdaten von diesem Server exportieren und sichern.  
  
Führen Sie zum Exportieren der AD FS-Konfigurationsdaten die folgenden Schritte aus:  
  
-   [Schritt 1:  Dienst Einstellungen exportieren @ no__t-0  
  
-   [Schritt 2:  Exportieren von Anspruchs Anbieter-Vertrauens Stellungen @ no__t-0  
  
-   [Schritt 3:  Vertrauens Stellungen der vertrauenden Seite exportieren @ no__t-0  
  
-   [Schritt 4:  Sichern der benutzerdefinierten Attribut Speicher @ no__t-0  
  
-   [Schritt 5:  Sichern von Webseiten Anpassungen @ no__t-0  
  
## <a name="step-1-export-service-settings"></a>Schritt 1: Exportieren der Diensteinstellungen  
 Gehen Sie wie folgt vor, um die Diensteinstellungen zu exportieren:  
  
### <a name="to-export-service-settings"></a>So exportieren Sie Diensteinstellungen  
  
1.  Notieren Sie den Antragstellernamen des Zertifikats sowie den Fingerabdruckwert des SSL-Zertifikats, die vom Verbunddienst verwendet werden. Öffnen Sie zum Aufrufen des SSL-Zertifikats die IIS (Internetinformationsdienste)-Verwaltungskonsole, wählen Sie im linken Bereich **Standardwebsite** aus, und klicken Sie im Bereich **Aktion** auf **Bindungen…** . Navigieren Sie zur HTTPS-Bindung, wählen Sie sie aus, und klicken Sie auf **Bearbeiten**und anschließend auf **Anzeigen**.  
  
> [!NOTE]
>  Optional können Sie auch das vom Verbunddienst verwendete SSL-Zertifikat und seinen privaten Schlüssel in eine PFX-Datei exportieren. Weitere Informationen finden Sie unter [Exportieren des Bereichs mit dem privaten Schlüssel eines Serverauthentifizierungszertifikats](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md).  
>   
>  Das Exportieren des SSL-Zertifikats ist optional, da dieses Zertifikat auf dem lokalen Computer im privaten Zertifikatspeicher gespeichert wird und beim Upgrade des Betriebssystems erhalten bleibt.  
  
2. Notieren Sie sich die Konfiguration der Zertifikate für die AD FS-Dienstkommunikation, Tokenverschlüsselung und Tokensignatur.  Öffnen Sie zum Anzeigen aller verwendeten Zertifikate Windows PowerShell, und führen Sie den folgenden Befehl aus, um der Windows PowerShell-Sitzung die AD FS Cmdlets hinzuzufügen: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um eine Liste aller in einer Datei verwendeten Zertifikate zu erstellen `PSH:>Get-ADFSCertificate | Out-File “.\certificates.txt”`  
  
> [!NOTE]
>  Sie können optional auch zusätzlich zu allen selbstsignierten Zertifikaten alle Zertifikate und Schlüssel für die Tokensignatur, Tokenverschlüsselung oder Dienstkommunikation exportieren, die nicht intern generiert werden. Sie können alle auf Ihrem Server verwendeten Zertifikate mithilfe von Windows PowerShell anzeigen. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung aus: `PSH:>add-pssnapin “Microsoft.adfs.powershell`. Führen Sie dann den folgenden Befehl aus, um alle Zertifikate anzuzeigen, die auf dem Server verwendet werden `PSH:>Get-ADFSCertificate`. Die Ausgabe dieses Befehls umfasst StoreLocation- und StoreName-Werte, die den Speicherort für die einzelnen Zertifikate angeben. Sie können dann die Anleitung in [Exportieren des Bereichs mit dem privaten Schlüssel eines Serverauthentifizierungszertifikats](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md) verwenden, um die einzelnen Zertifikate und den entsprechenden privaten Schlüssel in eine PFX-Datei zu exportieren.  
>   
>  Das Exportieren dieser Zertifikate ist optional, da alle externen Zertifikate während des Betriebssystemupgrades erhalten bleiben.  
  
3. Exportieren Sie AD FS 2,0-Verbund Dienst Eigenschaften, z. b. den Verbund Dienstnamen, den anzeigen amen des Verbund Diensts und den Verbund Server Bezeichner in eine Datei.  
  
Öffnen Sie zum Exportieren der Verbund Dienst Eigenschaften Windows PowerShell, und führen Sie den folgenden Befehl aus, um der Windows PowerShell-Sitzung die AD FS Cmdlets hinzuzufügen: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl zum Exportieren der Verbund Dienst Eigenschaften aus: `PSH:> Get-ADFSProperties | Out-File “.\properties.txt”`.  
  
Die Ausgabedatei enthält die folgenden wichtigen Konfigurationswerte:  
  
    
|**Verbunddienst Eigenschaftsnamen wie von Get-ADF sproperties gemeldet**|**Eigenschaften Name Verbunddienst in AD FS Verwaltungskonsole**|
|------|------|
|HostName|Verbunddienstname|  
|Bezeichner|Bezeichner des Verbunddiensts|  
|DisplayName|Anzeigename des Verbunddiensts|  
  
4. Sichern Sie die Anwendungskonfigurationsdatei. Neben anderen Einstellungen enthält diese Datei die Verbindungszeichenfolge der Richtliniendatenbank.  
  
Zum Sichern der Anwendungskonfigurationsdatei muss die Datei `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` manuell an einen sicheren Speicherort auf einem Sicherungsserver kopiert werden.  
  
> [!NOTE]
>  Notieren Sie sich die Datenbankverbindungszeichenfolge in dieser Datei. Sie befindet sich direkt hinter %%amp;quot;“policystore connectionstring=”)%%amp;quot;. Gibt die Verbindungszeichenfolge eine SQL Server-Datenbank an, ist der Wert beim Wiederherstellen der ursprünglichen AD FS-Konfiguration auf dem Verbundserver erforderlich.  
>   
>  Im Folgenden sehen Sie ein Beispiel für eine WID-Verbindungszeichenfolge: `“Data Source=\\.\pipe\mssql$microsoft##ssee\sql\query;Initial Catalog=AdfsConfiguration;Integrated Security=True"`. Im Folgenden sehen Sie ein Beispiel für eine SQL Server-Verbindungszeichenfolge: `"Data Source=databasehostname;Integrated Security=True"`.  
  
5. Notieren Sie die Identität des AD FS 2,0-Verbund Dienst Kontos und das Kennwort für dieses Konto.  
  
Der Identitätswert befindet sich in der Konsole **Dienste** in der Spalte **Anmelden als** unter **AD FS 2.0-Windows-Dienst** . Zeichnen Sie diesen Wert manuell auf.  
  
> [!NOTE]
>  Für einen eigenständigen Verbunddienst wird das integrierte Konto NETZWERKDIENST verwendet.  In diesem Fall benötigen Sie kein Kennwort.  
  
6. Exportieren Sie die Liste aktivierter AD FS-Endpunkte in eine Datei.  
  
Öffnen Sie hierzu Windows PowerShell, und führen Sie den folgenden Befehl aus, um der Windows PowerShell-Sitzung die AD FS Cmdlets hinzuzufügen: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um die Liste der aktivierten AD FS Endpunkte in eine Datei zu exportieren: `PSH:> Get-ADFSEndpoint | Out-File “.\endpoints.txt”`.  
  
7. Exportieren Sie alle benutzerdefinierten Anspruchbeschreibungen in eine Datei.  
  
Öffnen Sie hierzu Windows PowerShell, und führen Sie den folgenden Befehl aus, um der Windows PowerShell-Sitzung die AD FS Cmdlets hinzuzufügen: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um alle benutzerdefinierten Anspruchs Beschreibungen in eine Datei zu exportieren: `Get-ADFSClaimDescription | Out-File “.\claimtypes.txt”`.  
  
##  <a name="step-2-export-claims-provider-trusts"></a>Schritt 2: Exportieren der Anspruchsanbieter-Vertrauensstellungen  
 Gehen Sie wie folgt vor, um die Anspruchsanbieter-Vertrauensstellungen zu exportieren:  
  
### <a name="to-export-claims-provider-trusts"></a>So exportieren Sie Anspruchsanbieter-Vertrauensstellungen  
  
1.  Sie können alle Anspruchsanbieter-Vertrauensstellungen mithilfe von Windows PowerShell exportieren. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung aus: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um alle Anspruchs Anbieter-Vertrauens Stellungen zu exportieren: `PSH:>Get-ADFSClaimsProviderTrust | Out-File “.\cptrusts.txt”`.  
  
## <a name="step-3-export-relying-party-trusts"></a>Schritt 3: Exportieren der Vertrauensstellungen der vertrauenden Seite  
 Gehen Sie wie folgt vor, um die Vertrauensstellungen der vertrauenden Seite zu exportieren:  
  
### <a name="to-export-relying-party-trusts"></a>So exportieren Sie Vertrauensstellungen der vertrauenden Seite  
  
1.  Wenn Sie alle Vertrauens Stellungen der vertrauenden Seite exportieren möchten, öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl aus, um der Windows PowerShell-Sitzung die AD FS Cmdlets hinzuzufügen: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um alle Vertrauens Stellungen der vertrauenden Seite zu exportieren: `PSH:>Get-ADFSRelyingPartyTrust | Out-File “.\rptrusts.txt”`.  
  
## <a name="step-4-back-up-custom-attribute-stores"></a>Schritt 4: Sichern der benutzerdefinierten Attributspeicher  
 Informationen zu von AD FS verwendeten benutzerdefinierten Attributspeichern erhalten Sie mithilfe von Windows PowerShell. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung aus: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um Informationen zu den benutzerdefinierten Attribut speichern zu suchen: `PSH:>Get-ADFSAttributeStore`. Die Schritte zum Aktualisieren oder Migrieren von Attributspeichern variieren.  
  
## <a name="step-5-back-up-webpage-customizations"></a>Schritt 5: Sichern der Webseitenanpassungen  
 Um Webseiten Anpassungen zu sichern, kopieren Sie die AD FS Webseiten und die Datei **Web. config** aus dem Verzeichnis, das dem virtuellen Pfad **"/ADFS/ls"** in IIS zugeordnet ist. Standardmäßig befindet sie sich im Verzeichnis **%systemdrive%\inetpub\adfs\ls**.  

## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md)-Verbund Servers    
 [Vorbereiten der Migration des AD FS 2,0-Verbund Server Proxys](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren Sie den AD FS 2,0](migrate-the-ad-fs-fed-server.md)-Verbund Server  .  
 [Migrieren Sie den AD FS 2,0-Verbund Server Proxy](migrate-the-ad-fs-2-fed-server-proxy.md) .  
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)