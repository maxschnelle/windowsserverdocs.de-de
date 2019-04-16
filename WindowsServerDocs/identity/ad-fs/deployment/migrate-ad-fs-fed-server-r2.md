---
title: Migrieren des AD FS 2.0-Verbundservers
description: "Enthält Informationen zum Migrieren eines AD FS-Servers zu Windows Server 2012 R2."
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: bef24f79cfa92dfeca1846501f14ebf6d8231f0d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="migrate-the-ad-fs-20-federation-server-to-ad-fs-on-windows-server-2012-r2"></a>Migrieren der AD FS 2.0-Verbundserver zu AD FS unter Windows Server 2012 R2

Informationen zum Migrieren eines AD FS-Verbundservers, das eine AD FS-Farm mit einzelnem Knoten, einer WIF-Farm oder einer SQL Server-Farm zu Windows Server 2012 R2 angehört, müssen Sie die folgenden Aufgaben ausführen:  
  
1.  [Exportieren und Sichern der AD FS-Konfigurationsdaten](migrate-ad-fs-fed-server-r2.md#export-and-backup-the-ad-fs-configuration-data)  
  
2.  [Erstellen einer Windows Server 2012 R2-Verbundserverfarm](migrate-ad-fs-fed-server-r2.md#create-a-windows-server-2012-r2-federation-server-farm)  
  
3.  [Importieren der ursprünglichen Konfigurationsdaten in der Windows Server 2012 R2 AD FS-farm](migrate-ad-fs-fed-server-r2.md#import-the-original-configuration-data-into-the-windows-server-2012-r2-ad-fs-farm)  
  
##  <a name="export-and-backup-the-ad-fs-configuration-data"></a>Exportieren und Sichern der AD FS-Konfigurationsdaten  
 Führen Sie die folgenden Verfahren, um die AD FS-Konfigurationseinstellungen zu exportieren:  
  
###  <a name="to-export-service-settings"></a>So exportieren Sie diensteinstellungen  
  
1.  Stellen Sie sicher, dass Sie Zugriff auf die folgenden Zertifikate und ihre privaten Schlüssel in eine PFX-Datei verfügen:  
  
    -   Das SSL-Zertifikat, das von der Verbundserverfarm verwendet wird, die Sie migrieren möchten.  
  
    -   Das dienstkommunikationszertifikat (falls es sich vom SSL-Zertifikat unterscheidet), die von zu migrierenden Verbundserverfarm verwendet wird  
  
    -   Alle von Drittanbietern Tokensignaturzertifikate oder Token tokenverschlüsselungs-/tokenentschlüsselungszertifikate Zertifikate, die von der Verbundserverfarm verwendet werden, die Sie migrieren möchten.  
  
Um das SSL-Zertifikat zu suchen, öffnen Sie die Internetinformationsdienste (Internet Information Services, IIS)-Verwaltungskonsole, wählen **Default Web Site** klicken Sie im linken Bereich auf **Bindungen...** in der **Aktion** Bereich, suchen und wählen Sie die Https-Bindung, klicken Sie auf **bearbeiten**, und klicken Sie dann auf **Ansicht**.  
  
Sie müssen das SSL-Zertifikat verwendet, indem Sie den Verbunddienst und seinen privaten Schlüssel in eine PFX-Datei exportieren. Weitere Informationen finden Sie unter [Exportieren des Bereichs der privaten Schlüssel eines Serverauthentifizierungszertifikats](export-the-private-key-portion-of-a-server-authentication-certificate.md).  
  
> [!NOTE]
>  Wenn Sie den Geräteregistrierungsdienst im Rahmen der Ausführung von AD FS unter Windows Server2012 R2 bereitstellen möchten, müssen Sie ein neues SSL-Zertifikat abrufen. Weitere Informationen finden Sie unter [Registrieren eines SSL-Zertifikats für AD FS](enroll-an-ssl-certificate-for-ad-fs.md) und [Konfigurieren eines Verbundservers mit Device Registration Service](configure-a-federation-server-with-device-registration-service.md).  
  
Zum Anzeigen der Tokensignatur-, tokenentschlüsselungs- und dienstkommunikationszertifikate, die verwendet werden, führen Sie den folgenden Windows PowerShell-Befehl zum Erstellen einer Liste aller Zertifikate in einer Datei verwendet:  
  
``` powershell
Get-ADFSCertificate | Out-File “.\certificates.txt”  
 ```  
  
2.  Exportieren Sie AD FS-verbunddiensteigenschaften wie etwa den verbunddienstnamen, Anzeigename des Verbunddiensts und den Bezeichner des Verbunddiensts in eine Datei.  
  
Um die verbunddiensteigenschaften zu exportieren, öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl aus: 

``` powershell
Get-ADFSProperties | Out-File “.\properties.txt”`.  
``` 

Die Ausgabedatei enthält die folgenden wichtigen Konfigurationswerte:  
 
|**Den Namen der verbunddiensteigenschaft von Get-ADFSProperties gemeldet**|**Den Namen der verbunddiensteigenschaft in AD FS-Verwaltungskonsole**|
|-----|-----|  
|HostName|Verbunddienstname|  
|Bezeichner|Bezeichner des Verbunddiensts|  
|"DisplayName"|Anzeigename des Verbunddiensts|  
  
3.  Sichern der Anwendungskonfigurationsdatei. Neben anderen Einstellungen enthält diese Datei die Verbindungszeichenfolge der Richtliniendatenbank.  
  
Sie müssen manuell kopieren, zum Sichern der Anwendungskonfigurationsdatei der `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` Datei an einem sicheren Speicherort auf einem Sicherungsserver.  
  
> [!NOTE]
>  Notieren Sie sich die Datenbankverbindungszeichenfolge in dieser Datei befindet sich direkt hinter "Policystore Connectionstring =". Wenn die Verbindungszeichenfolge eine SQL Server-Datenbank angegeben ist, wird der Wert beim Wiederherstellen der ursprünglichen AD FS-Konfigurations auf dem Verbundserver benötigt.  
>   
>  Im folgenden finden Sie ein Beispiel für eine WID-Verbindungszeichenfolge: `“Data Source=\\.\pipe\mssql$microsoft##ssee\sql\query;Initial Catalog=AdfsConfiguration;Integrated Security=True"`. Im folgenden finden Sie ein Beispiel für eine SQL Server-Verbindungszeichenfolge: `"Data Source=databasehostname;Integrated Security=True"`.  
  
4.  Notieren Sie die Identität des AD FS-Verbunddienstkontos und das Kennwort für dieses Konto.  
  
Der Identitätswert befindet, überprüfen Sie die **Anmelden als** Spalte **AD FS 2.0-Windows-Dienst** in der **Dienste** Konsole und zeichnen Sie diesen Wert manuell.  
  
> [!NOTE]
>  Für einen eigenständigen Verbunddienst wird das integrierte Konto Netzwerkdienst verwendet.  In diesem Fall müssen Sie nicht über ein Kennwort verfügen.  
  
5.  Exportieren Sie die Liste der aktivierten AD FS-Endpunkte in eine Datei.  
  
Zu diesem Zweck öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl aus: 

``` powershell
Get-ADFSEndpoint | Out-File “.\endpoints.txt”`.  
``` 

6.  Exportieren Sie alle benutzerdefinierten anspruchbeschreibungen in eine Datei.  
  
Zu diesem Zweck öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl aus: 

``` powershell
Get-ADFSClaimDescription | Out-File “.\claimtypes.txt”`.  
 ```

7.  Wenn Sie benutzerdefinierte Einstellungen wie z. B. UseRelayStateForIdpInitiatedSignOn in der Datei "Web.config" konfiguriert haben, stellen Sie sicher sichern Sie die Datei "Web.config" Referenz. Kopieren Sie die Datei aus dem Verzeichnis, das den virtuellen Pfad zugeordnet ist **"/ Adfs/ls"** in IIS. Es wird standardmäßig der **%systemdrive%\inetpub\adfs\ls** Verzeichnis.  
  
###  <a name="to-export-claims-provider-trusts-and-relying-party-trusts"></a>So exportieren Sie Anspruchsanbieter-Vertrauensstellungen und Vertrauensstellungen der vertrauenden Seite  
  
1.  So exportieren Sie AD FS Anspruchsanbieter-Vertrauensstellungen und Vertrauensstellungen der vertrauenden Seite Vertrauensstellungen, Sie müssen melden Sie sich als Administrator (jedoch nicht als Domänenadministrator) bei Ihrem Verbundserver Server, und führen Sie die folgenden Windows PowerShell-Skript befindet sich im die **Media/Server_support/Adfs** der Windows Server 2012 R2-Installations-CD im Ordner: `export-federationconfiguration.ps1`.  
  
> [!IMPORTANT]
>  Das Exportskript enthält die folgenden Parameter:  
>   
>  -   Export-FederationConfiguration.ps1-Path < String\ > [-ComputerName < String\ >] [-Credential < Pscredential\ >] [-Force] [-CertificatePassword < Securestring\ >]  
> -   Export-FederationConfiguration.ps1-Path < String\ > [-ComputerName < String\ >] [-Credential < Pscredential\ >] [-Force] [-CertificatePassword < Securestring\ >] [-RelyingPartyTrustIdentifier < String [] >] [-ClaimsProviderTrustIdentifier < String [] >]  
> -   Export-FederationConfiguration.ps1-Path < String\ > [-ComputerName < String\ >] [-Credential < Pscredential\ >] [-Force] [-CertificatePassword < Securestring\ >] [-RelyingPartyTrustName < String [] >] [-ClaimsProviderTrustName < String [] >]  
>   
>  **-RelyingPartyTrustIdentifier < String [] >** – die Vertrauensstellungen der vertrauenden Seite, deren Bezeichner im Zeichenfolgenarray angegeben sind, Vertrauensstellungen Cmdlet werden nur exportiert. Standardmäßig werden keine Vertrauensstellungen der vertrauenden Seite exportiert. Wenn weder, ClaimsProviderTrustIdentifier, RelyingPartyTrustName und ClaimsProviderTrustName angegeben ist, das Skript exportiert alle Vertrauensstellungen der vertrauenden und Anspruchsanbieter-Vertrauensstellungen.  
>   
>  **-ClaimsProviderTrustIdentifier < String [] >** -das-Cmdlet exportiert nur die Anspruchsanbieter-Vertrauensstellungen, deren Bezeichner im Zeichenfolgenarray angegeben sind. Standardmäßig werden keine Anspruchsanbieter-Vertrauensstellungen exportiert.  
>   
>  **-RelyingPartyTrustName < String [] >** – die Vertrauensstellungen der vertrauenden Seite, deren Namen im Zeichenfolgenarray angegeben sind, Vertrauensstellungen Cmdlet werden nur exportiert. Standardmäßig werden keine Vertrauensstellungen der vertrauenden Seite exportiert.  
>   
>  **-ClaimsProviderTrustName < String [] >** -das-Cmdlet exportiert nur die Anspruchsanbieter-Vertrauensstellungen, deren Namen im Zeichenfolgenarray angegeben sind. Standardmäßig werden keine Anspruchsanbieter-Vertrauensstellungen exportiert.  
>   
>  **-Path < String\ >** – der Pfad zu einem Ordner, der die exportierten Dateien enthalten soll.  
>   
>  **-ComputerName < String\ >** – gibt den Hostnamen des STS-Server. Der Standardwert ist der lokale Computer. Wenn Sie AD FS 2.0 oder AD FS unter Windows Server 2012 zu AD FS unter Windows Server 2012 R2 migrieren, ist dies der Hostname des AD FS-legacyservers.  
>   
>  **-Credential < PSCredential\ >** – gibt ein Benutzerkonto an, die über die Berechtigung zum Ausführen dieser Aktion verfügt. Der Standardwert ist der aktuelle Benutzer.  
>   
>  **-Force** – gibt an, dass keine Bestätigung des Benutzers.  
>   
>  **-CertificatePassword < SecureString\ >** – gibt ein Kennwort für das AD FS-Zertifikaten, privaten Schlüssel exportieren. Nicht angegeben ist, wird das Skript ein Kennwort angefordert, wenn ein AD FS-Zertifikat mit privatem Schlüssel exportiert werden muss.  
>   
>  **Eingaben**: keine  
>   
>  **Ausgaben**: String - dieses Cmdlet gibt den Ordnerpfad exportieren. Sie können das zurückgegebene Objekt, das Import-FederationConfiguration übergeben.  
  
###  <a name="to-back-up-custom-attribute-stores"></a>So sichern Sie benutzerdefinierte Attributspeicher  
  
1.  Alle benutzerdefinierten Attributspeicher, die Sie in der neuen AD FS-Farm in Windows Server 2012 R2 beibehalten möchten, müssen manuell exportiert werden.  
  
> [!NOTE]
>  In Windows Server 2012 R2 AD FS benutzerdefinierte Attributspeicher erforderlich, die auf .NET Framework 4.0 oder höher basieren. Folgen Sie den Anweisungen im [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653) installieren und Einrichten von .net Framework 4.5.  
  
Finden Sie Informationen zu benutzerdefinierten attributspeichern von AD FS verwendeten, indem Sie den folgenden Windows PowerShell-Befehl ausführen: 

``` powershell
Get-ADFSAttributeStore
```  

Die Schritte zum Aktualisieren oder Migrieren von attributspeichern variieren.  
  
2.  Alle DLL-Dateien der benutzerdefinierten Attributspeicher, die Sie in der neuen AD FS-Farm in Windows Server 2012 R2 beibehalten möchten, müssen auch manuell exportiert werden. Die Schritte zum Aktualisieren oder Migrieren von DLL-Dateien benutzerdefinierter Attributspeicher variieren.  
  
##  <a name="create-a-windows-server-2012-r2-federation-server-farm"></a>Erstellen einer Windows Server 2012 R2-Verbundserverfarm  
  
1.  Installieren Sie das Betriebssystem Windows Server 2012 R2 auf einem Computer, den Sie als Verbundserver fungieren, und klicken Sie dann die AD FS-Serverrolle hinzufügen möchten. Weitere Informationen finden Sie unter [Installieren des AD FS-Rollendiensts](install-the-ad-fs-role-service.md). Konfigurieren Sie dann den neuen Verbunddienst entweder über die Active Directory Konfigurations-Assistenten Verbunddienste oder über Windows PowerShell. Weitere Informationen finden Sie unter "Konfigurieren des ersten Verbundservers in einer neuen Verbundserverfarm" in [Konfigurieren eines Verbundservers](configure-a-federation-server.md).  

Beim Ausführen dieses Schritts, müssen Sie diese Schritte befolgen:  
  
-   Sie müssen Domänenadministrator-Berechtigungen verfügen, um den Verbunddienst zu konfigurieren.  
  
-   Sie müssen denselben verbunddienstnamen (Farmnamen) verwenden, wie in der AD FS 2.0 oder AD FS unter Windows Server 2012 verwendet wurde. Wenn Sie nicht denselben verbunddienstnamen verwenden, funktionieren die gesicherten Zertifikate nicht im Windows Server 2012 R2-Verbunddienst, die Sie konfigurieren möchten.  
  
-   Geben Sie, ob es sich um eine WID- oder SQL Server-Verbundserverfarm handelt. Wenn es sich um einen SQL-Farm handelt, geben Sie den SQL Server-Datenbank-Speicherort und den Instanznamen.  
  
-   Geben Sie eine Pfx-Datei mit dem SSL-Serverauthentifizierungszertifikat, das Sie bei der Vorbereitung für den Prozess der AD FS-Migration gesichert haben.  
  
-   Sie müssen dieselbe dienstkontoidentität angeben, die in AD FS 2.0 oder AD FS unter Windows Server 2012-Farm verwendet wurde.  
  
2.  Nachdem der erste Knoten konfiguriert wurde, können Sie der neuen Farm weitere Knoten hinzufügen. Weitere Informationen finden Sie unter "Hinzufügen ein Verbundservers zu einer vorhandenen Verbundserverfarm" in [Konfigurieren eines Verbundservers](configure-a-federation-server.md).  
  
##  <a name="import-the-original-configuration-data-into-the-windows-server-2012-r2-ad-fs-farm"></a>Importieren der ursprünglichen Konfigurationsdaten in der Windows Server 2012 R2 AD FS-farm  
 Nun, dass Sie eine AD FS-Verbundserverfarm, die in Windows Server 2012 R2 ausgeführt haben, können Sie die ursprünglichen AD FS-Konfigurationsdaten in die Datei importieren.  
  
1.  Importieren und konfigurieren weitere benutzerdefinierte AD FS-Zertifikate, u. a. extern registrierte Tokensignaturzertifikate und Entschlüsselung/tokenverschlüsselung Zertifikate und das dienstkommunikationszertifikat, wenn er sich vom SSL-Zertifikat unterscheidet.  
  
Wählen Sie in der AD FS-Verwaltungskonsole **Zertifikate**. Überprüfen Sie die Dienst-Kommunikation, Token tokenverschlüsselungs-/tokenentschlüsselungs- und Tokensignaturzertifikate Zertifikate mit den Werten, die Sie beim Vorbereiten der Migration in der Datei "certificates.txt" exportiert haben.  
  
Wenn Sie die tokenverschlüsselungs- oder Tokensignaturzertifikate Zertifikate von der standardmäßigen selbstsignierten Zertifikaten in externe Zertifikate ändern möchten, müssen Sie zuerst das automatische Rollover-Feature deaktivieren, das standardmäßig aktiviert ist. Zu diesem Zweck können Sie den folgenden Windows PowerShell-Befehl verwenden:  
  
``` powershell 
Set-ADFSProperties –AutoCertificateRollover $false  
```  
  
2.  Konfigurieren Sie alle benutzerdefinierten AD FS-diensteinstellungen, z. B. AutoCertificateRollover oder SSO-Lebensdauer, die mit dem Set-AdfsProperties-Cmdlet.  
  
3.  AD FS Vertrauensstellungen vertrauenden Seite und Anspruchsanbieter-Vertrauensstellungen importieren möchten, Sie müssen angemeldet sein als Administrator (jedoch nicht als Domänenadministrator) bei Ihrem Verbundserver Server, und führen Sie die folgenden Windows PowerShell-Skript befindet sich im Ordner \support\adfs der Windows Server 2012 R2-Installations-CD:  
  
``` powershell 
import-federationconfiguration.ps1  
```  
  
> [!IMPORTANT]
>  Das Importskript enthält die folgenden Parameter:  
>   
>  -  Import-FederationConfiguration.ps1-Path < String\ > [-ComputerName < String\ >] [-Credential < Pscredential\ >] [-Force] [-LogPath < String\ >] [-CertificatePassword < Securestring\ >]  
> -   Import-FederationConfiguration.ps1-Path < String\ > [-ComputerName < String\ >] [-Credential < Pscredential\ >] [-Force] [-LogPath < String\ >] [-CertificatePassword < Securestring\ >] [-RelyingPartyTrustIdentifier < String [] >] [-ClaimsProviderTrustIdentifier < String [] >  
> -   Import-FederationConfiguration.ps1-Path < String\ > [-ComputerName < String\ >] [-Credential < Pscredential\ >] [-Force] [-LogPath < String\ >] [-CertificatePassword < Securestring\ >] [-RelyingPartyTrustName < String [] >] [-ClaimsProviderTrustName < String [] >]  
>   
>  **-RelyingPartyTrustIdentifier < String [] >** – die Vertrauensstellungen der vertrauenden Seite, deren Bezeichner im Zeichenfolgenarray angegeben sind, Vertrauensstellungen Cmdlet werden nur importiert. Standardmäßig werden keine Vertrauensstellungen der vertrauenden Seite importiert. Wenn weder, ClaimsProviderTrustIdentifier, RelyingPartyTrustName und ClaimsProviderTrustName angegeben ist, wird das Skript importiert alle Vertrauensstellungen der vertrauenden und Anspruchsanbieter-Vertrauensstellungen.  
>   
>  **-ClaimsProviderTrustIdentifier < String [] >** -das-Cmdlet importiert nur die Anspruchsanbieter-Vertrauensstellungen, deren Bezeichner im Zeichenfolgenarray angegeben sind. Standardmäßig werden keine Anspruchsanbieter-Vertrauensstellungen importiert.  
>   
>  **-RelyingPartyTrustName < String [] >** – die Vertrauensstellungen der vertrauenden Seite, deren Namen im Zeichenfolgenarray angegeben sind, Vertrauensstellungen Cmdlet werden nur importiert. Standardmäßig werden keine Vertrauensstellungen der vertrauenden Seite importiert.  
>   
>  **-ClaimsProviderTrustName < String [] >** -das-Cmdlet importiert nur die Anspruchsanbieter-Vertrauensstellungen, deren Namen im Zeichenfolgenarray angegeben sind. Standardmäßig werden keine Anspruchsanbieter-Vertrauensstellungen importiert.  
>   
>  **-Path < String\ >** – der Pfad zu einem Ordner, die zu importierenden Konfigurationsdateien enthält.  
>   
>  **-LogPath < String\ >** – der Pfad zu einem Ordner, die die Log-Importdatei enthalten soll. In diesem Ordner wird eine Protokolldatei mit dem Namen %% amp;quot;Import.log%%amp;quot; erstellt.  
>   
>  **-ComputerName < String\ >** -Gibt Hostnamen des STS-Servers. Der Standardwert ist der lokale Computer. Wenn Sie AD FS 2.0 oder AD FS unter Windows Server 2012 zu AD FS unter Windows Server 2012 R2 migrieren, sollte dieser Parameter der Hostname des AD FS-legacyservers festgelegt werden.  
>   
>  **-Credential < PSCredential\ >**– gibt ein Benutzerkonto an, die über die Berechtigung zum Ausführen dieser Aktion verfügt. Der Standardwert ist der aktuelle Benutzer.  
>   
>  **-Force** – gibt an, dass keine Bestätigung des Benutzers.  
>   
>  **-CertificatePassword < SecureString\ >** – gibt ein Kennwort zum Importieren von AD FS-Zertifikaten, privaten Schlüssel. Nicht angegeben ist, wird das Skript ein Kennwort angefordert, wenn ein AD FS-Zertifikat mit privatem Schlüssel importiert werden muss.  
>   
>  **Eingaben:** String - dieser Befehl verwendet den importordnerpfad als Eingabe. Sie können Export-FederationConfiguration für diesen Befehl übergeben.  
>   
>  **Ausgaben:** keine.  
  
Nachgestellten Leerzeichen in der WSFedEndpoint-Eigenschaft einer Vertrauensstellung der vertrauenden Seite können Fehler im Importskript verursachen. In diesem Fall, entfernen Sie die Leerzeichen manuell aus der Datei vor dem import. Diese Einträge sind beispielsweise Fehler verursachen:  
  
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
>  Wenn Sie auf die Active Directory-Anspruchsanbieter-Vertrauensstellung im Quellsystem benutzerdefinierte Anspruchsregeln (also nicht die AD FS-Standardregeln) haben, werden diese nicht von den Skripts migriert. Dies ist, da Windows Server 2012 R2 neue Standardwerte enthält. Benutzerdefinierten Regeln müssen zusammengeführt werden, indem sie die Active Directory-Anspruchsanbieter-Vertrauensstellung in der neuen Windows Server 2012 R2-Farm manuell hinzufügen.  
  
4.  Konfigurieren Sie alle benutzerdefinierten AD FS-endpunkteinstellungen. Wählen Sie in der AD FS-Verwaltungskonsole **Endpunkte**. Überprüfen Sie die aktivierten AD FS-Endpunkte anhand der Liste der aktivierten AD FS-Endpunkte, die Sie beim Vorbereiten der AD FS-Migration in eine Datei exportiert haben.  
  
     \ – Und –  
  
     Konfigurieren Sie alle benutzerdefinierten anspruchbeschreibungen. Wählen Sie in der AD FS-Verwaltungskonsole **Anspruchsbeschreibungen**. Überprüfen Sie die Liste der AD FS-anspruchsbeschreibungen mit der Liste der anspruchsbeschreibungen, die Sie beim Vorbereiten der AD FS-Migration in eine Datei exportiert haben. Fügen Sie alle benutzerdefinierten anspruchbeschreibungen in der Datei enthalten, aber nicht in der Standardliste in AD FS enthalten. Beachten Sie, dass Anspruchs-ID in der Verwaltungskonsole der ClaimType in der Datei zugeordnet ist.  
  
5.  Installieren und konfigurieren Sie alle gesicherten benutzerdefinierten Attributspeicher. Als Administrator stellen Sie sicher, dass alle benutzerdefinierten Attributs Store Binärdateien Upgrade auf .NET Framework 4.0 oder höher aktualisiert werden, bevor die AD FS-Konfiguration auf sie verweisen.  
  
6.  Konfigurieren Sie Diensteigenschaften, die die ältere web.config-Datei-Parameter zugeordnet.  
  
    -   Wenn **UseRelayStateForIdpInitiatedSignOn** wurde hinzugefügt, um die **"Web.config"** Datei in Ihrer AD FS 2.0 oder AD FS unter Windows Server 2012-Farm, Sie müssen die folgenden Diensteigenschaften in Ihrer AD FS in Windows Server 2012 R2-Farm konfigurieren:  
  
        -   AD FS unter Windows Server 2012 R2 umfasst eine **%systemroot%\ADFS\Microsoft.IdentityServer.Servicehost.exe.config** Datei. Erstellen Sie ein Element mit derselben Syntax wie die **"Web.config"** Dateielement: `<useRelayStateForIdpInitiatedSignOn enabled="true" />`. Nehmen Sie dieses Element als Teil der **< microsoft.identityserver.web >** Teil der **Microsoft.IdentityServer.Servicehost.exe.config** Datei.  
  
    -   Wenn **< PersistIdentityProviderInformation aktiviert = "" true "& #124; False" LifetimeInDays = "90" EnablewhrPersistence = "" true "& #124; False" / \ >** wurde hinzugefügt, um die **"Web.config"** Datei in Ihrer AD FS 2.0 oder AD FS unter Windows Server 2012-Farm, müssen Sie die folgenden Diensteigenschaften in Ihrer AD FS in Windows Server 2012 R2-Farm konfigurieren:  
  
        1.  In AD FS unter Windows Server 2012 R2, führen Sie den folgenden Windows PowerShell-Befehl: `Set-AdfsWebConfig –HRDCookieEnabled –HRDCookieLifetime`.  
  
    -   Wenn **< für einmaliges Anmelden aktiviert = "" true "& #124; False" / \ >** wurde hinzugefügt, um die **"Web.config"** Datei in Ihrer AD FS 2.0 oder AD FS unter Windows Server 2012-Farm, Sie brauchen keine zusätzlichen Diensteigenschaften in Ihrer AD FS in Windows Server 2012 R2-Farm festgelegt. Einmaliges Anmelden ist in AD FS unter Windows Server 2012 R2-Farm standardmäßig aktiviert.  
  
    -   Wenn LocalAuthenticationTypes-Einstellungen hinzugefügt wurden die **"Web.config"** Datei in Ihrer AD FS 2.0 oder AD FS unter Windows Server 2012-Farm, Sie müssen die folgenden Diensteigenschaften in Ihrer AD FS in Windows Server 2012 R2-Farm konfigurieren:  
  
        -   Integriert, Formulare, TlsClient, Liste in entsprechenden AD FS unter Windows Server 2012 R2 verfügt über globale authentifizierungsrichtlinieneinstellungen sowohl auch die Proxyauthentifizierung die verbunddienstauthentifizierung unterstützen. Diese Einstellungen können konfiguriert werden, in AD FS-Verwaltungs-Snap-in unter der **Authentifizierungsrichtlinien**.  
  
 Nachdem Sie die ursprünglichen Konfigurationsdaten importieren, können Sie die AD FS-Anmeldeseiten nach Bedarf anpassen. Weitere Informationen finden Sie unter [Customizing the AD FS Sign-in Pages](../operations/AD-FS-Customization-in-Windows-Server-2016.md).  
  
## <a name="next-steps"></a>Nächste Schritte
 [Migrieren der Rollendienste für Active Directory Federation Services zu Windows Server 2012 R2](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [Vorbereiten der Migration des AD FS-Verbundservers](prepare-migrate-ad-fs-server-r2.md)   
 [Migrieren des AD FS-Verbundserverproxys](migrate-fed-server-proxy-r2.md)   
 [Überprüfen der AD FS-Migrations zu Windows Server 2012 R2](verify-ad-fs-migration.md)