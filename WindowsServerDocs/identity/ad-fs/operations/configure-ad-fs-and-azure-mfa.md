---
ms.assetid: 24c4b9bb-928a-4118-acf1-5eb06c6b08e5
title: Konfigurieren von AD FS 2016 und Azure MFA
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 11/01/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: be8e88ae36f344f1265fb76e66c19e0ac8aeb533
ms.sourcegitcommit: ffdfbb76c7f775e20d089d3f662d4f9a7d642f1e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2018
---
# <a name="configure-ad-fs-2016-and-azure-mfa"></a>Konfigurieren von AD FS 2016 und Azure MFA

>Gilt für: Windows Server 2016

Wenn Ihre Organisation mit Azure AD verbunden ist, können Sie Azure Multi-Factor Authentication auf sichere AD FS-Ressourcen, sowohl lokal und in der Cloud verwenden. Azure MFA können Sie Kennwörter und sicherere Authentifizierung ermöglichen.  Ab Windows Server2016 können Sie jetzt Azure MFA für die primäre Authentifizierung konfigurieren. 
  
Im Gegensatz zu mit AD FS unter Windows Server2012 R2, die AD FS 2016 Azure MFA-Adapter direkte Integration mit Azure AD und einer auf lokalen Azure MFA-Server ist nicht erforderlich.   Die Azure MFA-Adapter ist in Windows Server2016 integriert und besteht keine Notwendigkeit für zusätzliche Installation.

## <a name="registering-users-for-azure-mfa-with-ad-fs-2016"></a>Registrieren von Benutzern für Azure MFA mit AD FS 2016
AD FS unterstützt keine Inline "Nachweis von" oder Erfassung von Azure MFA Überprüfung Sicherheitsinformationen wie z.B. Telefonnummer oder mobile Anwendung. Dies bedeutet, dass Benutzer von geprüft abrufen müssen, Berichtdetails https://account.activedirectory.windowsazure.com/Proofup.aspx vor der Verwendung von Azure MFA zur Authentifizierung der AD FS-Anwendungen. Wenn ein Benutzer, die in Azure AD-Versuche zur Authentifizierung beim Azure MFA zur AD FS nicht noch oben geprüft wurde, erhalten sie einen AD FS-Fehler.  Als AD FS-Administrator können Sie diese Fehler-Erfahrung, um den Benutzer stattdessen an der Proofup-Seite führt anpassen.  Sie können dazu onload.js Anpassung Zeichenfolge der Fehlermeldung in der AD FS-Seite zu erkennen und zeigen eine neue Nachricht, die Benutzer besuchen https://aka.ms/mfasetup führt dann Authentifizierung erneut versuchen. Ausführliche Anweisungen finden Sie auf der "Anpassen der AD FS Benutzer zum Registrieren des MFA-Überprüfungsmethoden geführt" unten in diesem Artikel.

>[!NOTE]
> Bisher mussten Benutzer mit der MFA für die Registrierung (besuchen https://account.activedirectory.windowsazure.com/Proofup.aspx, z.B. über die Verknüpfung aka.ms/mfasetup) authentifizieren.  Jetzt kann ein AD FS-Benutzer, die Informationen zur MFA Überprüfung noch nicht registriert ist Azure AD zugreifen Proofup-Seite über die Verknüpfung aka.ms/mfasetup mit dem nur das primäre Authentifizierung (z.B. die integrierte Windows-Authentifizierung oder Benutzernamen und Kennwort über die AD FS Seiten Web) .  Wenn der Benutzer keine Überprüfungsmethoden konfiguriert hat, Azure AD führt Inline-Registrierung, in denen der Benutzer die Meldung sieht "der Administrator hat erforderlich, dass Sie dieses Konto für zusätzliche Sicherheitsüberprüfung einrichten", und der Benutzer kann dann wählen Sie "jetzt einrichten".
> Benutzer, die bereits über mindestens eine MFA-Überprüfungsmethode konfiguriert werden weiterhin MFA bereitstellen, wenn die Proofup-Seite besuchen aufgefordert.

### <a name="recommended-deployment-topologies"></a>Empfohlenen Bereitstellungstopologien

#### <a name="azure-mfa-as-primary-authentication"></a>Azure MFA als primäre Authentifizierung
Es gibt ein paar gute Gründe für die Verwendung von Azure MFA als primäre Authentifizierung mit AD FS:
 - Vermeiden Sie Kennwörter für die Anmeldung bei Azure AD, Office365 und andere AD FS-Apps
 - Um den Kennwortschutz basierend Anmeldung durch Anfordern einer zusätzlichen Authentifizierungsstufe z.B. Bestätigungscode, bevor Sie das Kennwort

Wenn Sie Azure MFA als primäre Authentifizierungsmethode in AD FS verwenden, um folgende Vorteile zu erzielen möchten Sie wahrscheinlich auch die Möglichkeit zur Verwendung von Azure AD bedingten behalten möchten einschließlich "true MFA" auffordert für weitere Faktoren in AD FS.

Sie können nun dazu durch Konfigurieren der Einstellung des Azure AD-Domäne der mehrstufigen Authentifizierung auf lokalen (Einstellung "SupportsMfa" auf $True) zu tun.  In dieser Konfiguration können AD FS von Azure AD aufgefordert, zusätzliche Authentifizierung oder "true MFA" für Szenarien der bedingten ausführen, die dies erfordern.  

Wie oben beschrieben, jeder AD FS-Benutzer, die noch nicht registrierte (konfigurierten MFA Überprüfungsinformationen) über eine benutzerdefinierte Fehlerseite von AD FS zum aka.ms/mfasetup zum Konfigurieren von Informationen zur Überprüfung, finden aufgefordert werden soll dann erneut versuchen AD FS-Anmeldung.  
Da Azure MFA als primären einzigen Faktor, betrachtet wird, nach der Erstkonfiguration Benutzer eine zusätzliche Authentifizierungsstufe zu verwalten oder aktualisieren ihre Informationen zur Überprüfung in Azure AD oder auf andere Ressourcen zugreifen, die MFA erfordern angeben müssen.


#### <a name="azure-mfa-as-additional-authentication-to-office-365"></a>Azure MFA als zusätzliche Authentifizierung mit Office365
Wenn Sie wollte wurde wie eine zusätzliche Authentifizierungsmethode in AD FS für Office365 oder anderen vertrauenden Seiten, die beste Option zum Konfigurieren von Azure AD so MFA, die Verbundauthentifizierung in der primären Authentifizierung, lokal in AD FS und MFA ausgeführt wird zuvor Azure MFA tr Iggered von Azure AD. Jetzt können Sie Azure MFA als zusätzliche Authentifizierung in AD FS verwenden, wenn die Einstellung für die SupportsMfa auf $True festgelegt ist.  

Wie oben beschrieben, jeder AD FS-Benutzer, die noch nicht registrierte (konfigurierten MFA Überprüfungsinformationen) über eine benutzerdefinierte Fehlerseite von AD FS zum aka.ms/mfasetup zum Konfigurieren von Informationen zur Überprüfung, finden aufgefordert werden soll dann erneut versuchen AD FS-Anmeldung.  


## <a name="pre-requisites"></a>Voraussetzungen  
Die folgenden erforderlichen Komponenten sind erforderlich, wenn mithilfe von Azure MFA für die Authentifizierung mit AD FS:  
  
- Ein [Azure-Abonnement mit Azure Active Directory](https://azure.microsoft.com/pricing/free-trial/).  
- [Azure Multi-Factor Authentication](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/)  

>[!NOTE]   
> Azure AD und Azure MFA in Azure AD Premium und Enterprise Mobility Suite (EMS) enthalten sind.  Wenn Sie eine der folgenden haben benötigen Sie nicht einzelne Abonnements.   
- Eine Windows Server2016 AD FS lokalen Umgebung.  
- Wird von Ihrer lokalen Umgebung [Verbund mit Azure AD.](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#configuring-federation-with-ad-fs)  
- [Windows Azure Active Directory-Modul für WindowsPowerShell](https://go.microsoft.com/fwlink/p/?linkid=236297).  
- Berechtigungen als globaler Administrator für die Instanz von Azure AD mit Azure AD-PowerShell konfigurieren.  
- Enterprise-Anmeldeinformationen für Azure MFA die AD FS-Farm zu konfigurieren.  
  
  
## <a name="configure-the-ad-fs-servers"></a>Konfigurieren Sie die AD FS-Server  
Um die Konfiguration für Azure MFA für AD FS abzuschließen, müssen Sie jeden AD FS-Server mithilfe der Schrittekonfigurieren. 

>[!NOTE]
>Stellen Sie sicher, dass für diese Schritteausgeführt werden **alle** AD FS-Server in der Farm. Wenn Sie haben mehrere AD FS-Server in der Farm verfügen, können Sie die erforderlichen Konfigurationsschritte Remote mit Azure AD-PowerShell ausführen.  
  
  
  
### <a name="step-1-generate-a-certificate-for-azure-mfa-on-each-ad-fs-server-using-the-new-adfsazuremfatenantcertificate-cmdlet"></a>Schritt1: Erstellen Sie ein Zertifikat auf jedem Server mit AD FS für Azure MFA die `New-AdfsAzureMfaTenantCertificate`Cmdlet.   
Zunächst müssen Sie ist für Azure MFA verwendet ein Zertifikat generieren.  Dies kann mithilfe von PowerShell.  Das Zertifikat generiert, finden Sie im Zertifikatspeicher lokalen Computer, und mit einem Antragstellernamen an, die die TenantID für Azure AD-Verzeichnis enthält markiert ist.    
  
![AD FS und MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA3.png)  
  
Beachten Sie, dass TenantID den Namen des Verzeichnisses in Azure AD.  Verwenden Sie das folgende PowerShell-Cmdlet, um das neue Zertifikat zu generieren.  
    `$certbase64 = New-AdfsAzureMfaTenantCertificate -TenantID <tenantID>`  
      
![AD FS und MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA1.PNG)  
  
### <a name="step-2-add-the-new-credentials-to-azure-multi-factor-auth-client-spn"></a>Schritt2: Hinzufügen der neuen Anmeldeinformationen für Azure Multi-Factor Authentication Client Dienstprinzipalnamen   
Um die AD FS-Server für die Kommunikation mit dem Azure Multi-Factor Authentication-Client zu aktivieren, müssen Sie die Anmeldeinformationen für den Dienstprinzipalnamen für den Azure Multi-Factor Authentication-Client hinzufügen. Die Zertifikate mit der `New-AdfsAzureMFaTenantCertificate`Cmdlet dient als diese Anmeldeinformationen. Führen Sie folgende Schrittemithilfe von PowerShell den Azure Multi-Factor Authentication-Client-SPN die neuen Anmeldeinformationen hinzu.  

>[!NOTE]   
>Um diesen Schrittabgeschlossen haben, müssen Sie zur Verbindung mit Ihrer Instanz von Azure AD mit PowerShell Connect-MsolService verwenden.  Diese Schrittesetzen voraus, dass Sie bereits über PowerShell verbunden sind.  Weitere Informationen finden Sie unter [Connect-MsolService.](https://msdn.microsoft.com/library/dn194123.aspx)  
     
  
2. **Legen Sie das Zertifikat als Anmeldeinformationen für den Azure Multi-Factor Authentication-Client**  
    
    `New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type asymmetric -Usage verify -Value $certBase64 `

>[!IMPORTANT]
>  Dieser Befehl muss auf allen von der AD FS-Server in der Farm ausgeführt werden.  Azure AD-MFA tritt ein Fehler auf dem Server, auf denen nicht das Zertifikat als Anmeldeinformationen für den Azure Multi-Factor Authentication-Client festgelegt haben. 

>[!NOTE]  
> 981f26a1-7f43-403b-a875-f8b09b8cd720 ist die GUID für Azure Multi-Factor Authentication-Client.  
  
## <a name="configure-the-ad-fs-farm"></a>Konfigurieren der AD FS-Farm  
  
Nachdem Sie im vorherigen Abschnittauf jedem AD FS-Server abgeschlossen haben, müssen zum Ausführen der `Set-AdfsAzureMfaTenant`Cmdlet.  
  
Dieses Cmdlet muss nur einmal für eine AD FS-Farm ausgeführt werden.  Verwenden Sie PowerShell, um diesen Schrittabgeschlossen haben.    
  
>[!NOTE]  
>Sie müssen den AD FS-Dienst auf jedem Server in der Farm neu starten, bevor diese Änderung wirksam.  
  
    Set-AdfsAzureMfaTenant -TenantId <tenant ID> -ClientId 981f26a1-7f43-403b-a875-f8b09b8cd720  
      
![AD FS und MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA5.png)  
  
Danach sehen Sie sich, dass die Azure MFA als eine primäre Authentifizierungsmethode für Intranet- und Extranetanwendungen verfügbar ist.    
  
![AD FS und MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA6.png)  

## <a name="renew-and-manage-ad-fs-azure-mfa-certificates"></a>Erneuern und Verwalten von AD FS Azure MFA-Zertifikate
Die folgende Anleitung führt Sie durch die Azure MFA-Zertifikate auf Ihre AD FS-Server verwalten.
Standardmäßig beim Konfigurieren von AD FS mit Azure MFA, sind die Zertifikate, die über das New-AdfsAzureMfaTenantCertificate PowerShell-Cmdlet generiert gültig für 2Jahre.  Um wie schließen, um zu ermitteln Ablaufzeit Ihre Zertifikate sind, und klicken Sie dann zu erneuern, und installieren neue Zertifikate, die mithilfe des folgenden Verfahrens.

### <a name="assess-ad-fs-azure-mfa-certificate-expiration-date"></a>Bewerten der AD FS Azure MFA Zertifikat – Ablaufdatum
Auf jedem AD FS-Server, auf dem lokalen Computer Shop, es werden ein selbstsigniertes Zertifikat mit "OU = Microsoft AD FS Azure MFA" in der Aussteller und Antragsteller.  Hierbei handelt es sich um den Azure MFA-Zertifikat.  Überprüfen Sie die Gültigkeitsdauer des Zertifikats auf jedem AD FS-Server zu ermitteln, das Ablaufdatum.  

### <a name="create-new-ad-fs-azure-mfa-certificate-on-each-ad-fs-server"></a>Erstellen Sie neue AD FS Azure MFA-Zertifikat auf jedem AD FS-Server
Wenn die Gültigkeitsdauer der Zertifikate Ende nähert, starten Sie den Erneuerungsprozess generiert ein neues Azure MFA-Zertifikat auf jedem AD FS-Server. Generieren Sie in einem PowerShell-Befehlsfenster ein neues Zertifikat auf jedem AD FS-Server mit dem folgenden Cmdlet:

```
PS C:\> $newcert = New-AdfsAzureMfaTenantCertificate -TenantId <tenant id such as contoso.onmicrosoft.com> -Renew $true
```

Aufgrund dieses Cmdlet wird ein neues Zertifikat, das aus zwei Tage in der Zukunft zu 2Tage + 2Jahre gültig ist, generiert werden.  AD FS und Azure MFA-Vorgänge werden von diesem Cmdlet oder das neue Zertifikat nicht beeinflusst. (Hinweis: die Verzögerung von 2Tagen ist beabsichtigt und Zeit, führen Sie die folgenden Schrittezum Konfigurieren des neuen Zertifikats im Mandanten, bevor AD FS gestartet wird, dessen Verwendung für Azure MFA bietet.)


### <a name="configure-each-new-ad-fs-azure-mfa-certificate-in-the-azure-ad-tenant"></a>Konfigurieren Sie jedes neue AD FS Azure MFA-Zertifikat in Azure AD-Mandanten
Verwenden das Azure AD-PowerShell-Modul für jedes neue Zertifikat (auf jedem AD FS-Server), Ihre Azure AD-Mandanten-Einstellungen wie folgt aktualisieren (Hinweis: Sie müssen zunächst eine Verbindung mit Mandanten mit Connect-MsolService zum Ausführen der folgenden Befehle).

```
PS C:/> New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type Asymmetric -Usage Verify -Value $certbase64
```
    Where $certbase64 is the new certificate.  The base64 encoded certificate can be obtained by exporting the certificate (without the private key) as a DER encoded file and opening in Notepad.exe, then copy/pasting to the PSH session and assigning to the variable $certbase64

### <a name="verify-that-the-new-certificates-will-be-used-for-azure-mfa"></a>Stellen Sie sicher, dass neue Zertifikate für Azure MFA verwendet werden soll
Einmal neue Zertifikate gültig, AD FS wird abzuholen und verwenden jedes entsprechenden Zertifikat für Azure MFA innerhalb weniger Stunden einen Tag.  Sobald dies erfolgt ist, auf jedem Server wird daraufhin ein Ereignis im Ereignisprotokoll AD FS-Administrator mit den folgenden Informationen protokolliert: Protokollname: AD FS/Administrator Quelle: AD FS Datum: 2/27/2018 7:33:31 Uhr Ereignis-ID: 547 Aufgabenkategorie: None Ebene: Informationen Schlüsselwörter : AD FS-Benutzer: DOMAIN\adfssvc Computer: ADFS.Domain.contoso.com Beschreibung: der Mandanten-Zertifikat für Azure MFA wurde erneuert wurde.  

TenantId: contoso.onmicrosoft.com. Alten Fingerabdruck: 7CC103D60967318A11D8C51C289EF85214D9FC63. Alte Ablaufdatum: 9/15/2019 21:43:17: 00 Uhr. Neue Fingerabdruck: 8110D7415744C9D4D5A4A6309499F7B48B5F3CCF. Neue Ablaufdatum: 2/27/2020 2:16:07 AM.

## <a name="customize-the-ad-fs-web-page-to-guide-users-to-register-mfa-verification-methods"></a>Anpassen der AD FS-Webseite zum zum Registrieren von Überprüfungsmethoden MFA-Benutzerhandbuch

Verwenden Sie die folgenden Beispielen angepasst werden, Ihre AD FS-Webseiten für Benutzer, die Sie noch nicht geprüft haben (konfiguriert Überprüfungsinformationen MFA).

### <a name="find-the-error"></a>Suchen Sie den Fehler
Zunächst stehen eine Reihe von Fehlermeldungen, die AD FS im Fall zurückgeben kann, in denen dem Benutzer Informationen zur Überprüfung fehlen.
Bei Verwendung von Azure MFA als primäre Authentifizierung wird der Benutzer nicht proofed eine AD FS-Fehlerseite, enthält die folgenden Meldungen angezeigt:
```
    <div id="errorArea"> 
        <div id="openingMessage" class="groupMargin bigText">
            An error occurred 
        </div> 
        <div id="errorMessage" class="groupMargin">
            Authentication attempt failed. Select a different sign in option or close the web browser and sign in again. Contact your administrator for more information. 
        </div>
```
Bei Azure AD als zusätzliche Authentifizierung versucht wird, wird der Benutzer nicht proofed eine AD FS-Fehlerseite, enthält die folgenden Meldungen angezeigt:
```
<div id='mfaGreetingDescription' class='groupMargin'>For security reasons, we require additional information to verify your account (mahesh@jenfield.net)</div>
    <div id="errorArea"> 
        <div id="openingMessage" class="groupMargin bigText">
            An error occurred 
        </div> 
        <div id="errorMessage" class="groupMargin">
            The selected authentication method is not available for &#39;username@contoso.com&#39;. Choose another authentication method or contact your system administrator for details. 
        </div>
```

### <a name="catch-the-error-and-update-the-page-text"></a>Abgefangen Sie den Fehler und aktualisieren Sie den Text
Den Fehler abgefangen und zeigt dem Benutzer benutzerdefinierte Richtlinien ist eine Frage des Anfügen von Javascript an das Ende der onload.js-Datei, die Teil der AD FS ist Web-Design, um (1) suchen identifizierende Fehlerzeichenfolgen und (2) benutzerdefinierte Web-Inhalte.  (Im Allgemeinen zum Anpassen der Datei onload.js Anleitung finden Sie im Artikel [hier](https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/operations/advanced-customization-of-ad-fs-sign-in-pages).)

