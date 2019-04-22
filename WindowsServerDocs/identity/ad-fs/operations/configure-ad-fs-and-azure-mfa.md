---
ms.assetid: 24c4b9bb-928a-4118-acf1-5eb06c6b08e5
title: Konfigurieren von AD FS 2016 und Azure MFA
description: ''
ms.author: billmath
author: billmath
manager: mtillman
ms.date: 01/28/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ae7809089a69ac0ff48168db0aa2e9d61c35257a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814091"
---
# <a name="configure-azure-mfa-as-authentication-provider-with-ad-fs"></a>Konfigurieren Sie Azure MFA als Authentifizierungsanbieter mit AD FS

>Gilt für: WindowsServer 2016, WindowsServer 2019

Wenn Ihre Organisation einen Verbund mit Azure AD ist, können Sie Azure Multi-Factor Authentication, sichere AD FS-Ressourcen, sowohl lokal und in der Cloud verwenden. Azure MFA können Sie zur Vermeidung von Kennwörtern und bieten eine sicherere Methode zur Authentifizierung.  Ab Windows Server 2016 können Sie jetzt Azure MFA zur primären Authentifizierung konfigurieren oder verwenden Sie diese als als zusätzlicher Authentifizierungsanbieter. 
  
Anders als mit AD FS unter Windows Server 2012 R2 AD FS 2016 Azure MFA-Adapter kann direkt in Azure AD integriert und einen lokalen Azure MFA Server ist nicht erforderlich.   Der Azure MFA-Adapter ist in Windows Server 2016 integriert, und besteht keine Notwendigkeit für die weitere Installation.


## <a name="registering-users-for-azure-mfa-with-ad-fs"></a>Registrieren von Benutzern für Azure MFA mit AD FS

AD FS unterstützt keine Inline &#34;einrichten Proof&#34;, oder der Azure MFA Überprüfung Sicherheitsinformationen, wie z. B. die Telefonnummer oder eine mobile app-Registrierung. Dies bedeutet, dass Benutzer müssen sich vorabauflistung zu erhalten, finden Sie unter [ https://account.activedirectory.windowsazure.com/Proofup.aspx ](https://account.activedirectory.windowsazure.com/Proofup.aspx) vor der Verwendung von Azure MFA AD FS-Anwendungen zu authentifizieren. Wenn ein Benutzer, die in Azure AD versucht, für die Authentifizierung mit Azure MFA in AD FS nicht noch um vorabauflistung hat, erhalten sie einen AD FS-Fehler.  Als AD FS-Administrator können Sie diese Fehlermeldungen erspart, der den Benutzer stattdessen auf der Seite "Proofup" führt anpassen.  Hierzu können Sie erkennen die fehlermeldungs-Zeichenfolge in der AD FS-Seite, und zeigen eine neue Nachricht, die der Benutzer zum Besuch führen onload.js Anpassung mit [ https://aka.ms/mfasetup ](https://aka.ms/mfasetup), und klicken Sie dann erneut versuchen Authentifizierung. Eine ausführliche Anleitung finden Sie auf "Anpassen der AD FS Webseite, die Benutzer für MFA Überprüfungsmethoden registrieren führen" unten in diesem Artikel.

>[!NOTE]
> Zuvor mussten Benutzer zur Authentifizierung mit MFA für die Registrierung (unter [ https://account.activedirectory.windowsazure.com/Proofup.aspx ](https://account.activedirectory.windowsazure.com/Proofup.aspx), z. B. über die Verknüpfung [ https://aka.ms/mfasetup ](https://aka.ms/mfasetup)).  Nun kann ein AD FS-Benutzer, die noch nicht Überprüfungsinformationen für MFA registriert hat Azure AD zugreifen&#34;s Seite "Proofup" über die Verknüpfung [ https://aka.ms/mfasetup ](https://aka.ms/mfasetup) nur mit der primären Authentifizierung (z. B. die integrierte Windows-Authentifizierung oder Benutzername und Kennwort über die AD FS Webseiten).  Wenn der Benutzer keine Überprüfungsmethoden konfiguriert hat, führt Azure AD Inline-Registrierung in der der Benutzer die Nachricht sieht &#34;Ihr Administrator verlangt, dass Sie dieses Konto für eine zusätzliche sicherheitsüberprüfung einrichten&#34;, und der Benutzer kann dann Wählen Sie diese Option &#34;jetzt einrichten&#34;.
> Benutzer, die bereits mindestens eine Überprüfungsmethode für MFA konfiguriert haben werden weiterhin aufgefordert, die MFA geben beim Besuch der Seite "Proofup".

## <a name="recommended-deployment-topologies"></a>Empfohlene Bereitstellungstopologien

### <a name="azure-mfa-as-primary-authentication"></a>Azure MFA als primäre Authentifizierung

Es gibt ein paar gute Gründe für die Verwendung von Azure MFA als primäre Authentifizierung mit AD FS:

 - Um Kennwörter für die Anmeldung in Azure AD, Office 365 und andere AD FS-apps zu vermeiden.
 - Um ein Kennwort schützen basierenden Anmeldung durch ein weiterer Faktor, z. B. Prüfcode, bevor Sie das Kennwort anfordern

Wenn Sie Azure MFA als primäre Authentifizierungsmethode in AD FS zu verwenden, um diese Vorteile zu erzielen. möchten Sie wahrscheinlich auch die Möglichkeit, einschließlich der Azure AD für den bedingten Zugriff zu &#34;"true" MFA&#34; auffordern zur Angabe weiterer Faktoren in AD FS.

Sie können dies jetzt tun, durch Konfigurieren der Azure AD-Domäne-Einstellung Sie MFA lokal (Einstellung &#34;SupportsMfa&#34; auf $True).  In dieser Konfiguration wird AD FS kann werden dazu aufgefordert werden von Azure AD eine zusätzliche Authentifizierung durchführen oder &#34;"true" MFA&#34; für bedingte Szenarios, die dies erfordern.  

Wie oben beschrieben, sollte jeder AD FS-Benutzer, die noch nicht (konfigurierten MFA-Überprüfungsinformationen) registriert hat über eine benutzerdefinierte AD FS-Fehlerseite aufgefordert werden, zu besuchende [ https://aka.ms/mfasetup ](https://aka.ms/mfasetup) so konfigurieren Sie die Informationen zur Überprüfung, klicken Sie dann Wiederholen Sie den AD FS-Anmeldung.  
Da Azure MFA als primäre einen Faktor, gilt nach der Erstkonfiguration Benutzer einen weiteren Faktor, verwalten oder aktualisieren die Informationen zur Überprüfung in Azure Active Directory oder auf andere Ressourcen zugreifen, die MFA erfordern angeben müssen.

>[!NOTE]
> Mit AD FS-2019 müssen Sie nehmen eine Änderung an den ankeranspruchstyp für die Active Directory-Anspruchsanbieter-Vertrauensstellung, und ändern dies aus der Windowsaccountname zu UPN. Führen Sie die unten stehenden Powershell-Cmdlet. Dies hat keine Auswirkungen auf die interne Funktionsweise von AD FS-Farm. Sie werden feststellen, dass einige Benutzer zur Eingabe von Anmeldeinformationen reprompted werden können, nachdem diese Änderung vorgenommen wird. Nach der Anmeldung erneut sehen Endbenutzer keinen Unterschied. 

```powershell
Set-AdfsClaimsProviderTrust -AnchorClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" -TargetName "Active Directory"
```

### <a name="azure-mfa-as-additional-authentication-to-office-365"></a>Azure MFA als zusätzliche Authentifizierung für Office 365

Wenn Sie haben wurde wie eine zusätzliche Authentifizierungsmethode in AD FS für die Office 365 oder andere vertrauenden Seiten, die beste Option zum Konfigurieren von Azure AD zum MFA, zusammengesetzte in der primären Authentifizierung in AD FS und MFA lokal ausgeführt wird zuvor Azure MFA tr Iggered von Azure AD. Jetzt können Sie Azure MFA als zusätzliche Authentifizierung in AD FS verwenden, wenn die Einstellung für die SupportsMfa auf $True festgelegt ist.  

Wie oben beschrieben, sollte jeder AD FS-Benutzer, die noch nicht (konfigurierten MFA-Überprüfungsinformationen) registriert hat über eine benutzerdefinierte AD FS-Fehlerseite aufgefordert werden, zu besuchende [ https://aka.ms/mfasetup ](https://aka.ms/mfasetup) so konfigurieren Sie die Informationen zur Überprüfung, klicken Sie dann Wiederholen Sie den AD FS-Anmeldung.  

## <a name="pre-requisites"></a>Voraussetzungen

Die folgenden Voraussetzungen sind erforderlich, wenn Sie Azure MFA für die Authentifizierung mit AD FS verwenden:  
  
- Ein [Azure-Abonnement mit Azure Active Directory](https://azure.microsoft.com/pricing/free-trial/).  
- [Azure Multi-Factor Authentication](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/)  
- Web-app-Proxy kann Communticate mit den folgenden über die Ports 80 und 443

    - https://adnotifications.windowsazure.com
    - https://login.microsoftonline.com


> [!NOTE]
> Azure AD und Azure MFA in Azure AD Premium und Enterprise Mobility Suite (EMS) enthalten sind.  Wenn Sie davon haben, benötigen Sie nicht einzelne Abonnements.
- Ein Windows Server 2016 AD FS in lokalen Umgebung.  
   - Der Server muss über die Ports 80 und 443 mit den folgenden URLs kommunizieren können.
      - https://adnotifications.windowsazure.com
      - https://login.microsoftonline.com
- Wird von Ihrer lokalen Umgebung [Verbund mit Azure AD.](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#configuring-federation-with-ad-fs)  
- [Windows Azure Active Directory-Modul für Windows PowerShell](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0).  
- Berechtigungen als globaler Administrator für Ihre Instanz von Azure AD mit Azure AD PowerShell konfigurieren.  
- Anmeldeinformationen des Unternehmensadministrators für Azure MFA AD FS-Farm zu konfigurieren.  
  
## <a name="configure-the-ad-fs-servers"></a>Konfigurieren Sie die AD FS-Server

Um die Konfiguration für Azure MFA für AD FS abgeschlossen haben, müssen Sie so konfigurieren Sie jeden AD FS-Server anhand der beschriebenen Schritte aus. 

>[!NOTE]
>Stellen Sie sicher, dass diese Schritte ausgeführt werden, auf **alle** AD FS-Server in der Farm. Wenn Sie mehrere AD FS-Server in der Farm verfügen, können Sie die erforderliche Konfiguration Remote mithilfe von Azure AD Powershell durchführen.  

### <a name="step-1-generate-a-certificate-for-azure-mfa-on-each-ad-fs-server-using-the-new-adfsazuremfatenantcertificate-cmdlet"></a>Schritt 1: Generieren eines Zertifikats für Azure MFA auf einzelnen AD FS-Server unter Verwendung der `New-AdfsAzureMfaTenantCertificate` Cmdlet

Zunächst müssen Sie lediglich ist das Generieren eines Zertifikats für Azure MFA verwenden.  Dies kann erfolgen mithilfe von PowerShell.  Generierte Zertifikat im Zertifikatspeicher lokalen Computer befinden, und mit einem Antragstellernamen an, die die "tenantid" für Azure AD-Verzeichnis enthält markiert ist.

![AD FS und MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA3.png)  

Beachten Sie, dass die "tenantid" den Namen Ihres Verzeichnisses in Azure AD fungiert.  Verwenden Sie das folgende PowerShell-Cmdlet, um das neue Zertifikat zu generieren.  
    `$certbase64 = New-AdfsAzureMfaTenantCertificate -TenantID <tenantID>`  

![AD FS und MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA1.PNG)  
  
### <a name="step-2-add-the-new-credentials-to-the-azure-multi-factor-auth-client-service-principal"></a>Schritt 2: Fügen Sie die neuen Anmeldeinformationen auf dem Azure Multi-Factor Authentication-Client Dienstprinzipal hinzu

Um die AD FS-Server für die Kommunikation mit dem Azure Multi-Factor Authentication-Client zu ermöglichen, müssen Sie die Anmeldeinformationen für den Dienstprinzipal für den Azure Multi-Factor Authentication-Client hinzufügen. Die Zertifikate generiert, mit der `New-AdfsAzureMFaTenantCertificate` Cmdlet dient als diese Anmeldeinformationen. Führen Sie die folgenden Schritte mithilfe von PowerShell die neuen Anmeldeinformationen auf dem Azure Multi-Factor Authentication-Client Dienstprinzipal hinzufügen.  

> [!NOTE]
> Zum Durchführen dieses Schrittes müssen Sie mit einer Instanz von Azure AD mit PowerShell mithilfe der Connect-MsolService herstellen.  Diese Schritte setzen voraus, dass Sie bereits eine Verbindung über PowerShell hergestellt haben.  Weitere Informationen finden Sie unter [Connect-MsolService.](https://msdn.microsoft.com/library/dn194123.aspx)  

**Legen Sie das Zertifikat wie die neuen Anmeldeinformationen für den Azure Multi-Factor Authentication-Client**  

`New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type asymmetric -Usage verify -Value $certBase64`

> [!IMPORTANT]
> Dieser Befehl muss auf allen AD FS-Servern in der Farm ausgeführt werden.  Azure AD MFA schlägt fehl, auf Servern, die nicht das Zertifikat an, wie die neuen Anmeldeinformationen für den Azure Multi-Factor Authentication-Client festgelegt haben.

> [!NOTE]  
> 981f26a1-7f43-403b-a875-f8b09b8cd720 ist die GUID für den Azure Multi-Factor Authentication-Client.  
  
## <a name="configure-the-ad-fs-farm"></a>Konfigurieren der AD FS-Farm  
  
Nachdem Sie den vorherigen Abschnitt auf jedem AD FS-Server abgeschlossen haben, müssen Sie zum Ausführen der `Set-AdfsAzureMfaTenant` Cmdlet.  
  
Dieses Cmdlet muss nur einmal für eine AD FS-Farm ausgeführt werden.  Verwenden Sie PowerShell, um diesen Schritt abzuschließen.
  
> [!NOTE]  
> Sie müssen diese Änderungen werden erst ausgeführt, starten Sie den AD FS-Dienst auf jedem Server in der Farm neu.  
  
    Set-AdfsAzureMfaTenant -TenantId <tenant ID> -ClientId 981f26a1-7f43-403b-a875-f8b09b8cd720  

![AD FS und MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA5.png)  
  
Anschließend sehen Sie sich, dass es sich bei Azure MFA als eine primäre Authentifizierungsmethode für Intranet- und extranet Verwendung verfügbar ist.    
  
![AD FS und MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA6.png)  

## <a name="renew-and-manage-ad-fs-azure-mfa-certificates"></a>Erneuern und Verwalten von AD FS Azure MFA-Zertifikate

Die folgende Anleitung führt Sie durch die Azure MFA-Zertifikate auf Ihren AD FS-Servern zu verwalten.
Beim Konfigurieren von AD FS mit Azure MFA, werden standardmäßig über das New-AdfsAzureMfaTenantCertificate-PowerShell-Cmdlet generierten Zertifikate ungültig für 2 Jahre.  Um zu bestimmen, wie nahe an Ablauf Ihrer Zertifikate sind, und klicken Sie dann zum Erneuern und neue Zertifikate installieren, gehen Sie folgendermaßen vor.

### <a name="assess-ad-fs-azure-mfa-certificate-expiration-date"></a>Bewerten der AD FS, Azure MFA Ablaufdatum des Zertifikats

Auf jedem AD FS-Server, auf dem lokalen Computer My-Zertifikatspeicher, wird ein selbstsigniertes Zertifikat mit &#34;OU = Microsoft AD FS, Azure MFA&#34; in der Aussteller und Antragsteller.  Dies ist das Azure MFA-Zertifikat.  Überprüfen Sie die Gültigkeitsdauer des Zertifikats auf jedem AD FS-Server, um zu bestimmen, das Ablaufdatum.  

### <a name="create-new-ad-fs-azure-mfa-certificate-on-each-ad-fs-server"></a>Erstellen von neuen AD FS Azure MFA-Zertifikat auf jedem AD FS-server

Wenn die Gültigkeitsdauer der Zertifikate mit das Ende nähert, starten Sie durch Generieren eines neuen Azure MFA-Zertifikats auf jedem AD FS-Server die Verlängerung durchführen. Generieren Sie in einem Powershell-Befehlsfenster ein neues Zertifikat auf jedem AD FS-Server mit dem folgenden Cmdlet:

```
PS C:\> $newcert = New-AdfsAzureMfaTenantCertificate -TenantId <tenant id such as contoso.onmicrosoft.com> -Renew $true
```

Als Ergebnis dieses Cmdlet wird ein neues Zertifikat, das über 2 Tage im Voraus zu zwei Tage + 2 Jahre gültig ist, generiert werden.  AD FS und Azure MFA-Vorgänge werden durch dieses Cmdlet aus, oder das neue Zertifikat nicht betroffen. (Hinweis: die Verzögerung von 2 Tagen ist beabsichtigt und stellt die Zeit für die Ausführung der nachstehenden Schritte zum Konfigurieren des neuen Zertifikats im Mandanten vor Beginn der AD FS für Azure MFA verwenden.)

### <a name="configure-each-new-ad-fs-azure-mfa-certificate-in-the-azure-ad-tenant"></a>Konfigurieren Sie jedes neues AD FS, Azure MFA-Zertifikat in Azure AD-Mandanten

Aktualisieren Sie die Azure AD-Mandanten-Einstellungen wie folgt mithilfe des Azure AD PowerShell-Moduls für jedes neue Zertifikat (auf jedem AD FS-Server) (Hinweis: Sie müssen zuerst eine Verbindung herstellen mit Connect-MsolService zum Ausführen der folgenden Befehle auf den Mandanten).

```
PS C:/> New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type Asymmetric -Usage Verify -Value $newcert
```

$certbase64 ist das neue Zertifikat.  Die base64-codierte Zertifikat kann abgerufen werden, indem Sie das Zertifikat (ohne den privaten Schlüssel) exportieren, wie einer DER-codiert-Datei und öffnen in Notepad.exe, und klicken Sie dann kopieren/einfügen, um die PSH-Sitzung und der Variablen $certbase64

### <a name="verify-that-the-new-certificates-will-be-used-for-azure-mfa"></a>Stellen Sie sicher, dass die neuen Zertifikate für Azure MFA verwendet wird

Sobald die neuen Zertifikate gültig sind, wird AD FS HEB sie auf und nutzen jedes entsprechenden Zertifikat für Azure MFA in wenigen Stunden pro Tag.  Sobald dies erfolgt, wird Sie auf jedem Server ein Ereignis im Ereignisprotokoll AD FS-Administrator mit den folgenden Informationen angezeigt: Protokollname:      Quelle für AD FS/Administrator:        AD FS-Datum:          2/27/2018 7:33:31 PM-Ereignis-ID:      547 Aufgabenkategorie: Keine Ebene:         Schlüsselwörter der Informationen:      AD FS-Benutzer:          DOMAIN\adfssvc-Computer:      ADFS.domain.contoso.com-Beschreibung: Die Mandanten-Zertifikat für Azure MFA wurde erneuert.  

TenantId: contoso.onmicrosoft.com.
Fingerabdruck des alten: 7CC103D60967318A11D8C51C289EF85214D9FC63.
Alte Ablaufdatum: 9/15/2019 9:43:17 UHR.
Neuen Fingerabdruck: 8110D7415744C9D4D5A4A6309499F7B48B5F3CCF.
Neues Ablaufdatum: 2/27/2020 2:16:07 UHR.

## <a name="customize-the-ad-fs-web-page-to-guide-users-to-register-mfa-verification-methods"></a>Anpassen der AD FS-Webseite zum Benutzerhandbuch um Überprüfungsmethoden für MFA zu registrieren.

Verwenden Sie die folgenden Beispiele zum Anpassen von Ihren AD FS-Webseiten für Benutzer, die noch nicht um vorabauflistung haben (konfiguriert Informationen zur MFA).

### <a name="find-the-error"></a>Suchen Sie den Fehler

Es gibt zuerst eine Reihe verschiedener Fehlermeldungen, die AD FS in der dem Benutzer fehlen die Informationen zur Überprüfung in die Groß-/Kleinschreibung zurückgibt.
Wenn Sie Azure MFA als primäre Authentifizierung verwenden, wird dem nicht proofed Benutzer eine AD FS-Fehlerseite, enthält die folgenden Meldungen angezeigt:
```
    <div id="errorArea">
        <div id="openingMessage" class="groupMargin bigText">
            An error occurred
        </div>
        <div id="errorMessage" class="groupMargin">
            Authentication attempt failed. Select a different sign in option or close the web browser and sign in again. Contact your administrator for more information.
        </div>
```
Wenn Azure AD als zusätzliche Authentifizierung versucht wird, wird der Benutzer nicht proofed eine AD FS-Fehlerseite, enthält die folgenden Meldungen angezeigt:
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

### <a name="catch-the-error-and-update-the-page-text"></a>Fangen Sie den Fehler, und aktualisieren Sie die Seitentext

Um den Fehler abfangen und zeigt dem Benutzer benutzerdefinierten Prozessleitfaden fügen Sie einfach den JavaScript-Code an das Ende der onload.js-Datei, die Teil des Webdesigns für AD FS ist.  Dadurch können Sie die folgenden Schritte ausführen:
 - Suchen Sie nach der Identifizierung Fehler Zeichenfolge(n)
 - Geben Sie benutzerdefinierte Web-Inhalte.  

(Anleitungen im Allgemeinen zum Anpassen der onload.js-Datei finden Sie im Artikel [Advanced Customization of AD FS-Sign-in-Webseiten](advanced-customization-of-ad-fs-sign-in-pages.md).)

Hier ist ein einfaches Beispiel, Sie erweitern möchten:

1. Öffnen Sie Windows PowerShell auf dem primären AD FS-Server aus, und erstellen Sie ein neues AD FS-Web-Design mithilfe des folgenden Befehls:
    
    ``` PowerShell
        New-AdfsWebTheme –Name ProofUp –SourceName default
    ``` 
2. Als Nächstes exportieren Sie standardmäßig AD FS-Web-Design:

    ``` PowerShell
       Export-AdfsWebTheme –Name default –DirectoryPath c:\Theme
    ```
3. Öffnen Sie die C:\Theme\script\onload.js-Datei in einem Text-editor
4. Fügen Sie den folgenden Code am Ende der Datei onload.js
    
    ``` JavaScript
    //Custom Code
    //Customize MFA exception
    //Begin

    var domain_hint = "<YOUR_DOMAIN_NAME_HERE>";
    var mfaSecondFactorErr = "The selected authentication method is not available for";
    var mfaProofupMessage = "You will be automatically redirected in 5 seconds to set up your account for additional security verification. Once you have completed the setup, please return to the application you are attempting to access.<br><br>If you are not redirected automatically, please click <a href='{0}'>here</a>."
    var authArea = document.getElementById("authArea");
    if (authArea) {
        var errorMessage = document.getElementById("errorMessage");
        if (errorMessage.innerHTML.indexOf(mfaSecondFactorErr) >= 0) {

        //Hide the error message
            var openingMessage = document.getElementById("openingMessage");
            if (openingMessage) {
                openingMessage.style.display = 'none'
            }
            var errorDetailsLink = document.getElementById("errorDetailsLink");
            if (errorDetailsLink) {
                errorDetailsLink.style.display = 'none'
            }

            //Provide a message and redirect to Azure AD MFA Registration Url
            var mfaRegisterUrl = "https://account.activedirectory.windowsazure.com/proofup.aspx?proofup=1&whr=" + domain_hint;
            errorMessage.innerHTML = "<br>" + mfaProofupMessage.replace("{0}", mfaRegisterUrl);
            window.setTimeout(function () { window.location.href = mfaRegisterUrl; }, 5000);
        }
    }

    //End Customize MFA Exception
    //End Custom Code
    ```
    > [!IMPORTANT]
    > Sie müssen "< YOUR_DOMAIN_NAME_HERE >"; ändern. um Ihren Domänennamen zu verwenden. Beispiel: `var domain_hint = "contoso.com";`
    
5. Speichern Sie die Datei onload.js
6. Importieren Sie die onload.js-Datei in Ihr benutzerdefiniertes Design, indem Sie die folgenden Windows PowerShell-Befehl eingeben:
    
    ``` PowerShell
    Set-AdfsWebTheme -TargetName ProofUp -AdditionalFileResource @{Uri=’/adfs/portal/script/onload.js’;path="c:\theme\script\onload.js"}
    ```
7. Wenden Sie schließlich des benutzerdefinierten Webdesigns für AD FS, indem Sie die folgenden Windows PowerShell-Befehl eingeben:
    
    ``` PowerShell
    Set-AdfsWebConfig -ActiveThemeName
    ```

## <a name="next-steps"></a>Nächste Schritte

[Verwalten von TLS/SSL-Protokollen und Verschlüsselungssammlungen, die von AD FS und Azure MFA verwendet](manage-ssl-protocols-in-ad-fs.md)
