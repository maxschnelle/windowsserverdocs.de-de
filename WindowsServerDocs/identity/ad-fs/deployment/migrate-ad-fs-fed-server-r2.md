---
title: Migrieren der AD FS 2.0-Verbundservers
description: Enthält Informationen zur Migration von AD FS-Server zu Windows Server 2012 R2.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 46d0b643d786443093e0dfeafe4cddde3278ff76
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444621"
---
# <a name="migrate-the-ad-fs-20-federation-server-to-ad-fs-on-windows-server-2012-r2"></a>Migrieren der AD FS 2.0-Verbundservers mit AD FS unter Windows Server 2012 R2

Zum Migrieren eines AD FS-Verbundservers, das eine AD FS-Farm mit einzelnem Knoten, einer WIF-Farm oder eine SQL Server Windows Server 2012 R2-Farm gehört, müssen Sie die folgenden Aufgaben ausführen:  
  
1.  [Exportieren und Sichern der AD FS-Konfigurationsdaten](migrate-ad-fs-fed-server-r2.md#export-and-backup-the-ad-fs-configuration-data)  
  
2.  [Erstellen einer Windows Server 2012 R2-Verbundserverfarm](migrate-ad-fs-fed-server-r2.md#create-a-windows-server-2012-r2-federation-server-farm)  
  
3.  [Importieren Sie die ursprünglichen Konfigurationsdaten in der Windows Server 2012 R2 AD FS-farm](migrate-ad-fs-fed-server-r2.md#import-the-original-configuration-data-into-the-windows-server-2012-r2-ad-fs-farm)  
  
##  <a name="export-and-backup-the-ad-fs-configuration-data"></a>Exportieren und Sichern der AD FS-Konfigurationsdaten  
 Führen Sie zum Exportieren der AD FS-Konfigurationseinstellungen die folgenden Schritte aus:  
  
###  <a name="to-export-service-settings"></a>So exportieren Sie Diensteinstellungen  
  
1.  Stellen Sie sicher, dass Sie über Zugriff auf die folgenden Zertifikate und ihre privaten Schlüssel in einer PFX-Datei verfügen:  
  
    -   Das SSL-Zertifikat, das von der zu migrierenden Verbundserverfarm verwendet wird  
  
    -   Das Dienstkommunikationszertifikat (falls es sich vom SSL-Zertifikat unterscheidet), das von der zu migrierenden Verbundserverfarm verwendet wird  
  
    -   Alle Tokensignaturzertifikate oder Tokenverschlüsselungs-/Tokenentschlüsselungszertifikate von Drittanbietern, die von der zu migrierenden Verbundserverfarm verwendet werden  
  
Öffnen Sie zum Aufrufen des SSL-Zertifikats die IIS (Internetinformationsdienste)-Verwaltungskonsole, wählen Sie im linken Bereich **Standardwebsite** aus, und klicken Sie im Bereich **Aktion** auf **Bindungen…** . Navigieren Sie zur HTTPS-Bindung, wählen Sie sie aus, und klicken Sie auf **Bearbeiten**und anschließend auf **Anzeigen**.  
  
Sie müssen das vom Verbunddienst verwendete SSL-Zertifikat und seinen privaten Schlüssel in eine PFX-Datei exportieren. Weitere Informationen finden Sie unter [Exportieren des Bereichs mit dem privaten Schlüssel eines Serverauthentifizierungszertifikats](export-the-private-key-portion-of-a-server-authentication-certificate.md).  
  
> [!NOTE]
>  Wenn Sie den Geräteregistrierungsdienst im Rahmen der Ausführung von AD FS in Windows Server 2012 R2 bereitstellen möchten, müssen Sie ein neues SSL-Zertifikat abrufen. Weitere Informationen finden Sie unter [Enroll an SSL Certificate for AD FS](enroll-an-ssl-certificate-for-ad-fs.md) und [Configure a federation server with Device Registration Service](configure-a-federation-server-with-device-registration-service.md).  
  
Führen Sie zum Anzeigen der verwendeten Tokensignatur-, Tokenentschlüsselungs- und Dienstkommunikationszertifikate den folgenden Windows PowerShell-Befehl aus, um eine Liste aller verwendeten Zertifikate in einer Datei zu erstellen:  
  
``` powershell
Get-ADFSCertificate | Out-File “.\certificates.txt”  
 ```  
  
2. Exportieren Sie AD FS-Verbunddiensteigenschaften wie etwa den Verbunddienstnamen, den Anzeigenamen des Verbunddiensts und den Bezeichner des Verbunddiensts in eine Datei.  
  
Öffnen Sie zum Exportieren der Verbunddiensteigenschaften Windows PowerShell und führen Sie den folgenden Befehl aus: 

``` powershell
Get-ADFSProperties | Out-File “.\properties.txt”`.  
``` 

Die Ausgabedatei enthält die folgenden wichtigen Konfigurationswerte:  
 
|**Den Namen der verbunddiensteigenschaft von Get-ADFSProperties gemeldeten**|**Den Namen der verbunddiensteigenschaft in AD FS-Verwaltungskonsole**|
|-----|-----|  
|HostName|Verbunddienstname|  
|Bezeichner|Bezeichner des Verbunddiensts|  
|DisplayName|Anzeigename des Verbunddiensts|  
  
3. Sichern Sie die Anwendungskonfigurationsdatei. Neben anderen Einstellungen enthält diese Datei die Verbindungszeichenfolge der Richtliniendatenbank.  
  
Zum Sichern der Anwendungskonfigurationsdatei muss die Datei `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` manuell an einen sicheren Speicherort auf einem Sicherungsserver kopiert werden.  
  
> [!NOTE]
>  Notieren Sie sich die Datenbankverbindungszeichenfolge in dieser Datei. Sie befindet sich direkt hinter "policystore connectionstring=". Gibt die Verbindungszeichenfolge eine SQL Server-Datenbank an, ist der Wert beim Wiederherstellen der ursprünglichen AD FS-Konfiguration auf dem Verbundserver erforderlich.  
>   
>  Im Folgenden sehen Sie ein Beispiel für eine WID-Verbindungszeichenfolge: `“Data Source=\\.\pipe\mssql$microsoft##ssee\sql\query;Initial Catalog=AdfsConfiguration;Integrated Security=True"`. Im Folgenden sehen Sie ein Beispiel für eine SQL Server-Verbindungszeichenfolge: `"Data Source=databasehostname;Integrated Security=True"`.  
  
4. Notieren Sie die Identität des AD FS-Verbunddienstkontos und das Kennwort für dieses Konto.  
  
Der Identitätswert befindet sich in der Konsole **Dienste** in der Spalte **Anmelden als** unter **AD FS 2.0-Windows-Dienst** . Zeichnen Sie diesen Wert manuell auf.  
  
> [!NOTE]
>  Für einen eigenständigen Verbunddienst wird das integrierte Konto NETZWERKDIENST verwendet.  In diesem Fall benötigen Sie kein Kennwort.  
  
5. Exportieren Sie die Liste aktivierter AD FS-Endpunkte in eine Datei.  
  
Öffnen Sie dazu Windows PowerShell, und führen Sie den folgenden Befehl aus: 

``` powershell
Get-ADFSEndpoint | Out-File “.\endpoints.txt”`.  
``` 

6. Exportieren Sie alle benutzerdefinierten Anspruchbeschreibungen in eine Datei.  
  
Öffnen Sie dazu Windows PowerShell, und führen Sie den folgenden Befehl aus: 

``` powershell
Get-ADFSClaimDescription | Out-File “.\claimtypes.txt”`.  
 ```

7. Falls in der Datei %%amp;quot;web.config%%amp;quot; benutzerdefinierte Einstellungen wie etwa %%amp;quot;useRelayStateForIdpInitiatedSignOn%%amp;quot; konfiguriert sind, muss die Datei %%amp;quot;web.config%%amp;quot; zu Referenzzwecken gesichert werden. Sie können die Datei aus dem Verzeichnis kopieren, das dem virtuellen Pfad **%%amp;quot;/adfs/ls%%amp;quot;** in IIS zuwiesen ist. Standardmäßig befindet sie sich im Verzeichnis **%systemdrive%\inetpub\adfs\ls**.  
  
###  <a name="to-export-claims-provider-trusts-and-relying-party-trusts"></a>So exportieren Sie Anspruchsanbieter-Vertrauensstellungen und Vertrauensstellungen der vertrauenden Seite  
  
1.  So exportieren Sie AD FS-Anspruchsanbieter-Vertrauensstellungen und Vertrauensstellungen wird verlassen, Sie müssen sich als Administrator an (jedoch nicht als Domänenadministrator) bei Ihrem Verbundserver Server, und führen Sie die folgenden Windows PowerShell-Skript im Verzeichnis der **Media / Server_support/AD FS** Ordner von der Windows Server 2012 R2-Installations-CD: `export-federationconfiguration.ps1`.  
  
> [!IMPORTANT]
>  Das Exportskript enthält die folgenden Parameter:  
> 
> - Export-federationconfiguration. ps1-Path < Zeichenfolge\> [-ComputerName < Zeichenfolge\>] [-Credential < Pscredential\>] [-Force] [-CertificatePassword < Securestring\>]  
>   -   Export-federationconfiguration. ps1-Path < Zeichenfolge\> [-ComputerName < Zeichenfolge\>] [-Credential < Pscredential\>] [-Force] [-CertificatePassword < Securestring\>] [- Weder < Zeichenfolge [] >] [-ClaimsProviderTrustIdentifier < Zeichenfolge [] >]  
>   -   Export-federationconfiguration. ps1-Path < Zeichenfolge\> [-ComputerName < Zeichenfolge\>] [-Credential < Pscredential\>] [-Force] [-CertificatePassword < Securestring\>] [- RelyingPartyTrustName < Zeichenfolge [] >] [-ClaimsProviderTrustName < Zeichenfolge [] >]  
> 
>   **-RelyingPartyTrustIdentifier < Zeichenfolge [] >** – das Cmdlet nur exportiert der vertrauenden Seite Vertrauensstellungen, deren Bezeichner im Zeichenfolgenarray angegeben sind. Standardmäßig werden KEINE Vertrauensstellungen der vertrauenden Seite exportiert. Wenn weder %%amp;quot;RelyingPartyTrustIdentifier%%amp;quot;, %%amp;quot;ClaimsProviderTrustIdentifier%%amp;quot;, %%amp;quot;RelyingPartyTrustName%%amp;quot; noch %%amp;quot;ClaimsProviderTrustName%%amp;quot; angegeben ist, werden vom Skript alle Vertrauensstellungen der vertrauenden Seite und Anspruchsanbieter-Vertrauensstellungen exportiert.  
> 
>   **-ClaimsProviderTrustIdentifier < Zeichenfolge [] >** -das-Cmdlet exportiert nur die Anspruchsanbieter-Vertrauensstellungen, deren Bezeichner im Zeichenfolgenarray angegeben sind. Standardmäßig werden KEINE Anspruchsanbieter-Vertrauensstellungen exportiert.  
> 
>   **-RelyingPartyTrustName < Zeichenfolge [] >** – das Cmdlet nur exportiert der vertrauenden Seite Vertrauensstellungen, deren Namen im Zeichenfolgenarray angegeben sind. Standardmäßig werden KEINE Vertrauensstellungen der vertrauenden Seite exportiert.  
> 
>   **-ClaimsProviderTrustName < Zeichenfolge [] >** -das-Cmdlet exportiert nur die Anspruchsanbieter-Vertrauensstellungen, deren Namen im Zeichenfolgenarray angegeben sind. Standardmäßig werden KEINE Anspruchsanbieter-Vertrauensstellungen exportiert.  
> 
>   **-Path < Zeichenfolge\>**  – der Pfad zu einem Ordner, die die exportierten Dateien enthält.  
> 
>   **ComputerName: < Zeichenfolge\>**  -gibt der STS-Serverhostnamen an. Der Standardwert ist der lokale Computer. Bei der Migration von AD FS 2.0 oder AD FS unter Windows Server 2012 zu AD FS unter Windows Server 2012 R2 ist dies der Hostname des AD FS-Legacyservers.  
> 
>   **-Credential < PSCredential\>**  -gibt ein Benutzerkonto an, die über die Berechtigung zum Ausführen dieser Aktion verfügt. Der Standardwert ist der aktuelle Benutzer.  
> 
>   **-Force** – Gibt an, dass keine Benutzerbestätigung angefordert wird.  
> 
>   **-CertificatePassword < SecureString\>**  -gibt ein Kennwort für das AD FS-Zertifikaten, privaten Schlüssel exportieren. Wird dieser Parameter nicht angegeben, wird vom Skript ein Kennwort angefordert, wenn ein AD FS-Zertifikat mit privatem Schlüssel exportiert werden muss.  
> 
>   **Eingaben**: Keine  
> 
>   Zeichenfolge **Outputs**: – Dieses Cmdlet gibt den Ordnerpfad für den Export an. Sie können das zurückgegebene Objekt über die Pipeline an %%amp;quot;Import-FederationConfiguration%%amp;quot; übergeben.  
  
###  <a name="to-back-up-custom-attribute-stores"></a>So sichern Sie benutzerdefinierte Attributspeicher  
  
1.  Alle benutzerdefinierten Attributspeicher, die Sie in der neuen AD FS-Farm unter Windows Server 2012 R2 beibehalten möchten, müssen manuell exportiert werden.  
  
> [!NOTE]
>  In Windows Server 2012 R2 erfordert AD FS benutzerdefinierte Attributspeicher, die auf .NET Framework 4.0 oder höher basieren. Folgen Sie zum Installieren und Einrichten von .Net Framework 4.5 den Anweisungen unter [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653) .  
  
Informationen zu von AD FS verwendeten benutzerdefinierten Attributspeichern erhalten Sie durch Ausführen des folgenden Windows PowerShell-Befehls: 

``` powershell
Get-ADFSAttributeStore
```  

Die Schritte zum Aktualisieren oder Migrieren von Attributspeichern variieren.  
  
2. Alle DLL-Dateien der benutzerdefinierten Attributspeicher, die Sie in der neuen AD FS-Farm unter Windows Server 2012 R2 beibehalten möchten, müssen ebenfalls manuell exportiert werden. Die Schritte zum Aktualisieren oder Migrieren von DLL-Dateien benutzerdefinierter Attributspeicher variieren.  
  
##  <a name="create-a-windows-server-2012-r2-federation-server-farm"></a>Erstellen einer Windows Server 2012 R2-Verbundserverfarm  
  
1.  Installieren Sie das Betriebssystem Windows Server 2012 R2 auf einem Computer, den als Verbundserver fungieren, und fügen Sie dann auf die AD FS-Serverrolle werden sollen. Weitere Informationen finden Sie unter [Install the AD FS Role Service](install-the-ad-fs-role-service.md). Konfigurieren Sie anschließend den neuen Verbunddienst entweder mithilfe des Konfigurations-Assistenten für Active Directory-Verbunddienste oder der Windows PowerShell. Weitere Informationen finden Sie unter [Konfigurieren eines Verbundservers](configure-a-federation-server.md) im Thema %%amp;quot;Konfigurieren des ersten Verbundservers in einer neuen Verbundserverfarm%%amp;quot;.  

Beachten Sie beim Ausführen dieses Schritts die folgenden Anweisungen:  
  
-   Zum Konfigurieren des Verbunddiensts sind Domänenadministratorberechtigungen erforderlich.  
  
-   Sie müssen denselben Verbunddienstnamen (Farmnamen) angeben wie in AD FS 2.0 oder AD FS unter Windows Server 2012. Wenn Sie nicht den gleichen verbunddienstnamen verwenden, funktionieren die Zertifikate, die Sie haben gesichert nicht in der Windows Server 2012 R2-Verbunddienst, die Sie konfigurieren möchten.  
  
-   Geben Sie an, ob es sich um eine WID- oder SQL Server-Verbundserverfarm handelt. Geben Sie im Falle einer SQL-Farm den Speicherort und den Instanznamen der SQL Server-Datenbank an.  
  
-   Sie müssen eine PFX-Datei mit dem SSL-Serverauthentifizierungszertifikat angeben, das Sie bei der Vorbereitung für die AD FS-Migration gesichert haben.  
  
-   Geben Sie dieselbe Dienstkontoidentität wie in der AD FS 2.0-Farm oder der Farm mit AD FS unter Windows Server 2012 an.  
  
2. Wenn der erste Knoten konfiguriert ist, können Sie der neuen Farm weitere Knoten hinzufügen. Weitere Informationen finden Sie unter [Konfigurieren eines Verbundservers](configure-a-federation-server.md) im Thema %%amp;quot;Hinzufügen eines Verbundservers zu einer vorhandenen Verbundserverfarm%%amp;quot;.  
  
##  <a name="import-the-original-configuration-data-into-the-windows-server-2012-r2-ad-fs-farm"></a>Importieren der ursprünglichen Konfigurationsdaten in die AD FS-Farm mit Windows Server 2012 R2  
 Nun, da Sie eine AD FS-Verbundserverfarm in Windows Server 2012 R2 ausgeführt haben, können Sie die ursprüngliche AD FS-Konfigurationsdaten in diese importieren.  
  
1.  Importieren und konfigurieren Sie weitere benutzerdefinierte AD FS-Zertifikate, u. a. extern registrierte Tokensignaturzertifikate und Tokenverschlüsselungs-/Tokenentschlüsselungszertifikate, und das Dienstkommunikationszertifikat, falls es vom SSL-Zertifikat abweicht.  
  
Wählen Sie in der AD FS-Verwaltungskonsole **Zertifikate** aus. Überprüfen Sie die Dienstkommunikations-, Tokenverschlüsselungs-/Tokenentschlüsselungs- und Tokensignaturzertifikate. Vergleichen Sie dazu die einzelnen Zertifikate mit den Werten, die Sie bei der Vorbereitung der Migration in die Datei %%amp;quot;certificates.txt%%amp;quot; exportiert haben.  
  
Wenn Sie die Tokenverschlüsselungs- oder Tokensignaturzertifikate von den standardmäßigen selbstsignierten Zertifikaten in externe Zertifikate ändern möchten, müssen Sie zuerst das standardmäßig aktivierte Feature für das automatische Zertifikatrollover deaktivieren. Hierzu können Sie den folgenden Windows PowerShell-Befehl verwenden:  
  
``` powershell 
Set-ADFSProperties –AutoCertificateRollover $false  
```  
  
2. Konfigurieren Sie mithilfe des Cmdlets %%amp;quot;Set-AdfsProperties%%amp;quot; beliebige benutzerdefinierte AD FS-Diensteinstellungen, z. B. %%amp;quot;AutoCertificateRollover%%amp;quot; oder SSO-Lebensdauer.  
  
3. Um AD FS Vertrauensstellungen vertrauenden Seite und Anspruchsanbieter-Vertrauensstellungen importieren möchten, Sie müssen angemeldet sein als Administrator (jedoch nicht als Domänenadministrator) Ihrem Verbundserver Server, und führen Sie die folgenden Windows PowerShell-Skript befindet sich im Ordner \support\adfs der Installations-CD von Windows Server 2012 R2:  
  
``` powershell 
import-federationconfiguration.ps1  
```  
  
> [!IMPORTANT]
>  Das Importskript enthält die folgenden Parameter:  
> 
> - Import-federationconfiguration. ps1-Path < Zeichenfolge\> [-ComputerName < Zeichenfolge\>] [-Credential < Pscredential\>] [-Force] [-LogPath < Zeichenfolge\>] [-CertificatePassword < Securestring \>]  
>   -   Import-federationconfiguration. ps1-Path < Zeichenfolge\> [-ComputerName < Zeichenfolge\>] [-Credential < Pscredential\>] [-Force] [-LogPath < Zeichenfolge\>] [-CertificatePassword < Securestring \>] [-RelyingPartyTrustIdentifier < Zeichenfolge [] >] [-ClaimsProviderTrustIdentifier < Zeichenfolge [] >  
>   -   Import-federationconfiguration. ps1-Path < Zeichenfolge\> [-ComputerName < Zeichenfolge\>] [-Credential < Pscredential\>] [-Force] [-LogPath < Zeichenfolge\>] [-CertificatePassword < Securestring \>] [-RelyingPartyTrustName < Zeichenfolge [] >] [-ClaimsProviderTrustName < Zeichenfolge [] >]  
> 
>   **-RelyingPartyTrustIdentifier < Zeichenfolge [] >** – das Cmdlet nur importiert der vertrauenden Seite Vertrauensstellungen, deren Bezeichner im Zeichenfolgenarray angegeben sind. Standardmäßig werden KEINE Vertrauensstellungen der vertrauenden Seite importiert. Wenn weder %%amp;quot;RelyingPartyTrustIdentifier%%amp;quot;, %%amp;quot;ClaimsProviderTrustIdentifier%%amp;quot;, %%amp;quot;RelyingPartyTrustName%%amp;quot; noch %%amp;quot;ClaimsProviderTrustName%%amp;quot; angegeben ist, werden vom Skript alle Vertrauensstellungen der vertrauenden Seite und Anspruchsanbieter-Vertrauensstellungen importiert.  
> 
>   **-ClaimsProviderTrustIdentifier < Zeichenfolge [] >** -das-Cmdlet importiert nur die Anspruchsanbieter-Vertrauensstellungen, deren Bezeichner im Zeichenfolgenarray angegeben sind. Standardmäßig werden KEINE Anspruchsanbieter-Vertrauensstellungen importiert.  
> 
>   **-RelyingPartyTrustName < Zeichenfolge [] >** – das Cmdlet nur importiert der vertrauenden Seite Vertrauensstellungen, deren Namen im Zeichenfolgenarray angegeben sind. Standardmäßig werden KEINE Vertrauensstellungen der vertrauenden Seite importiert.  
> 
>   **-ClaimsProviderTrustName < Zeichenfolge [] >** -das-Cmdlet importiert nur die Anspruchsanbieter-Vertrauensstellungen, deren Namen im Zeichenfolgenarray angegeben sind. Standardmäßig werden KEINE Anspruchsanbieter-Vertrauensstellungen importiert.  
> 
>   **-Path < Zeichenfolge\>**  – der Pfad zu einem Ordner, die zu importierenden Konfigurationsdateien enthält.  
> 
>   **-LogPath < Zeichenfolge\>**  – der Pfad zu einem Ordner, die die Protokoll-Importdatei enthalten soll. In diesem Ordner wird eine Protokolldatei mit dem Namen %%amp;quot;import.log%%amp;quot; erstellt.  
> 
>   **ComputerName: < Zeichenfolge\>**  -gibt den Hostnamen des STS-Servers. Der Standardwert ist der lokale Computer. Bei der Migration von AD FS 2.0 oder AD FS unter Windows Server 2012 zu AD FS unter Windows Server 2012 R2 muss für diesen Parameter der Hostname des AD FS-Legacyservers angegeben werden.  
> 
>   **-Credential < PSCredential\>** -gibt ein Benutzerkonto an, die über die Berechtigung zum Ausführen dieser Aktion verfügt. Der Standardwert ist der aktuelle Benutzer.  
> 
>   **-Force** – Gibt an, dass keine Benutzerbestätigung angefordert wird.  
> 
>   **-CertificatePassword < SecureString\>**  -gibt ein Kennwort für das Importieren von AD FS-Zertifikaten, privaten Schlüssel. Wird dieser Parameter nicht angegeben, wird vom Skript ein Kennwort angefordert, wenn ein AD FS-Zertifikat mit privatem Schlüssel importiert werden muss.  
> 
>   Zeichenfolge **Inputs:** – Dieser Befehl verwendet den Importordnerpfad als Eingabe. Sie können %%amp;quot;Export-FederationConfiguration%%amp;quot; über die Pipeline an diesen Befehl übergeben.  
> 
>   **Ausgaben:** Keine  
  
Nachgestellte Leerzeichen in der WSFedEndpoint-Eigenschaft einer Vertrauensstellung der vertrauenden Seite können Fehler im Importskript verursachen. Entfernen Sie in diesem Fall vor dem Import die Leerzeichen manuell aus der Datei. Die folgenden Einträge können beispielsweise Fehler verursachen:  
  
    ```  
    <URI N="WSFedEndpoint">https://127.0.0.1:444 /</URI>  
    ```  
  
    ```  
    <URI N="WSFedEndpoint">https://myapp.cloudapp.net:83 /</URI>  
    ```  
  
     They must be edited to:  
  
    ```  
    <URI N="WSFedEndpoint">https://127.0.0.1:444/</URI>  
    ```  
  
    ```  
    <URI N="WSFedEndpoint">https://myapp.cloudapp.net:83/</URI>  
    ```  
> [!IMPORTANT]
>  Falls die Active Directory-Anspruchsanbieter-Vertrauensstellung im Quellsystem benutzerdefinierte Anspruchsregeln (also nicht die AD FS-Standardregeln) enthält, werden diese von den Skripts nicht migriert. Dies ist, da Windows Server 2012 R2 neue Standardwerte aufweist. Benutzerdefinierten Regeln müssen zusammengeführt werden, indem sie manuell die Active Directory Anspruchsanbieter-Vertrauensstellung in der neuen Windows Server 2012 R2-Farm hinzugefügt.  
  
4. Konfigurieren Sie alle benutzerdefinierten AD FS-Endpunkteinstellungen. Wählen Sie in der AD FS-Verwaltungskonsole **Endpunkte** aus. Vergleichen Sie die aktivierten AD FS-Endpunkte mit der Liste der aktivierten AD FS-Endpunkte, die Sie beim Vorbereiten der AD FS-Migration in eine Datei exportiert haben.  
  
    \- "und" -  
  
    Konfigurieren Sie alle benutzerdefinierten Anspruchbeschreibungen. Wählen Sie in der AD FS-Verwaltungskonsole **Anspruchbeschreibungen**aus. Vergleichen Sie die Liste der AD FS-Anspruchsbeschreibungen mit der Liste der Anspruchsbeschreibungen, die Sie beim Vorbereiten der AD FS-Migration in eine Datei exportiert haben. Fügen Sie alle benutzerdefinierten Anspruchbeschreibungen hinzu, die in der Datei, aber nicht in der Standardliste in AD FS enthalten sind. Der Claim-Bezeichner in der Verwaltungskonsole ist %%amp;quot;ClaimType%%amp;quot; in der Datei zugeordnet.  
  
5. Installieren und konfigurieren Sie alle gesicherten benutzerdefinierten Attributspeicher. Stellen Sie als Administrator sicher, dass alle Binärdateien für benutzerdefinierte Attributspeicher auf .NET Framework 4.0 oder höher aktualisiert werden, bevor die AD FS-Konfiguration für den Verweis auf die Speicher aktualisiert wird.  
  
6. Konfigurieren Sie Diensteigenschaften, die den Parametern der Legacydatei %%amp;quot;web.config%%amp;quot; zugeordnet sind.  
  
   -   Wenn **UseRelayStateForIdpInitiatedSignOn** wurde hinzugefügt, um die **"Web.config"** Datei in Ihrer AD FS 2.0 oder AD FS in Windows Server 2012-Farm müssen Sie die folgenden Diensteigenschaften in Ihrer AD FS in konfigurieren Windows Server 2012 R2-Farm:  
  
       -   AD FS in Windows Server 2012 R2 umfasst eine **%systemroot%\ADFS\Microsoft.IdentityServer.Servicehost.exe.config** Datei. Erstellen Sie ein Element mit derselben Syntax wie die **"Web.config"** "File"-Element: `<useRelayStateForIdpInitiatedSignOn enabled="true" />`. Nehmen Sie dieses Element als Teil des **< microsoft.identityserver.web >** Teil der **Microsoft.IdentityServer.Servicehost.exe.config** Datei.  
  
   -   Wenn **< PersistIdentityProviderInformation aktiviert = "" true "&#124;" false "" LifetimeInDays = "90" EnablewhrPersistence = "" true "&#124;false" /\>**  wurde hinzugefügt, um die **"Web.config"** Datei in Ihrer AD FS 2.0 oder AD FS unter Windows Server 2012-Farm müssen Sie die folgenden Diensteigenschaften in Ihrer AD FS in Windows Server 2012 R2-Farm konfigurieren:  
  
       1.  In AD FS in Windows Server 2012 R2 den folgenden Windows PowerShell-Befehl ausführen: `Set-AdfsWebConfig –HRDCookieEnabled –HRDCookieLifetime`.  
  
   -   Wenn **< SingleSignOn aktiviert = "" true "&#124;" false "" /\>**  wurde hinzugefügt, um die **"Web.config"** -Datei in Ihrer AD FS 2.0 oder AD FS unter Windows Server 2012-Farm, müssen Sie keine zusätzlichen Dienst festlegen Eigenschaften in Ihrer AD FS in Windows Server 2012 R2-Farm. Einmaliges Anmelden ist standardmäßig in AD FS unter Windows Server 2012 R2-Farm aktiviert.  
  
   -   Wenn LocalAuthenticationTypes-Einstellungen hinzugefügt wurden die **"Web.config"** Datei in Ihrer AD FS 2.0 oder AD FS in Windows Server 2012-Farm müssen Sie die folgenden Diensteigenschaften in Ihrer AD FS in Windows Server 2012 R2-Farm konfigurieren:  
  
       -   Integriert, Formulare, TlsClient, Liste in entsprechenden AD FS unter Windows Server 2012 R2 verfügt über globale authentifizierungsrichtlinieneinstellungen, um beide Typen Verbund-Dienst und Proxy-Authentifizierung zu unterstützen. Diese Einstellungen können im AD FS-Verwaltungs-Snap-In unter **Authentifizierungsrichtlinien**konfiguriert werden.  
  
   Nach dem Importieren der ursprünglichen Konfigurationsdaten können Sie die AD FS-Anmeldeseiten nach Bedarf anpassen. Weitere Informationen finden Sie unter [Customizing the AD FS Sign-in Pages](../operations/AD-FS-Customization-in-Windows-Server-2016.md).  
  
## <a name="next-steps"></a>Nächste Schritte
 [Migrieren der Rollendienste für Active Directory Federation Services für Windows Server 2012 R2](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [Vorbereiten der Migration des AD FS-Verbundservers](prepare-migrate-ad-fs-server-r2.md)   
 [Migrieren des AD FS-Verbundserverproxys](migrate-fed-server-proxy-r2.md)   
 [Überprüfen der AD FS-Migrations zu Windows Server 2012 R2](verify-ad-fs-migration.md)