---
ms.assetid: 24c4b9bb-928a-4118-acf1-5eb06c6b08e5
title: Konfigurieren von AD FS 2016 und Azure MFA
description: ''
ms.author: billmath
author: billmath
manager: mtillman
ms.date: 01/28/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d00092ee2cd4e6cc74d48e08ad5c316c2b309ab4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357867"
---
# <a name="configure-azure-mfa-as-authentication-provider-with-ad-fs"></a>Konfigurieren von Azure MFA als Authentifizierungs Anbieter mit AD FS

Wenn Ihr Unternehmen einen Verbund mit Azure AD hat, können Sie Azure Multi-Factor Authentication verwenden, um AD FS Ressourcen sowohl lokal als auch in der Cloud zu sichern. Azure MFA ermöglicht Ihnen die Vermeidung von Kenn Wörtern und bietet eine sicherere Möglichkeit zum authentifizieren.  Ab Windows Server 2016 können Sie Azure MFA für die primäre Authentifizierung konfigurieren oder als zusätzlichen Authentifizierungs Anbieter verwenden. 
  
Anders als bei AD FS in Windows Server 2012 R2 ist der Azure MFA-Adapter AD FS 2016 direkt in Azure AD integriert und erfordert keinen lokalen Azure MFA-Server.   Der Azure MFA-Adapter ist in Windows Server 2016 integriert, und es ist keine weitere Installation erforderlich.


## <a name="registering-users-for-azure-mfa-with-ad-fs"></a>Registrieren von Benutzern für Azure MFA mit AD FS

AD FS unterstützt keine Inline &#34;-Sicherung&#34;oder Registrierung von Informationen zur Azure MFA-Sicherheitsüberprüfung, wie z. b. Telefonnummer oder Mobile App. Dies bedeutet, dass Benutzer [https://account.activedirectory.windowsazure.com/Proofup.aspx](https://account.activedirectory.windowsazure.com/Proofup.aspx) vor der Verwendung von Azure MFA zum Authentifizieren bei AD FS-Anwendungen eine gesicherte Prüfung erhalten müssen. Wenn ein Benutzer, der sich noch nicht in Azure AD gesichert hat, versucht, sich bei Azure MFA bei AD FS zu authentifizieren, wird ein AD FS Fehler ausgegeben.  Als AD FS-Administrator können Sie diese Fehlerdarstellung so anpassen, dass Sie den Benutzer stattdessen zur Seite "" proofup "führt.  Verwenden Sie hierzu die OnLoad. js-Anpassung, um die Fehlermeldungs Zeichenfolge auf der Seite "AD FS" zu erkennen und eine neue Meldung [https://aka.ms/mfasetup](https://aka.ms/mfasetup)anzuzeigen, die die Benutzer zum Besuch führt, und wiederholen Sie dann die Authentifizierung. Eine ausführliche Anleitung finden Sie im Abschnitt "Anpassen der AD FS Webseite, um Benutzer zur Registrierung von MFA-Überprüfungsmethoden weiter unten in diesem Artikel zu unterstützen.

>[!NOTE]
> Bisher mussten sich Benutzer für die Registrierung bei MFA authentifizieren ( [https://account.activedirectory.windowsazure.com/Proofup.aspx](https://account.activedirectory.windowsazure.com/Proofup.aspx)z. b. über die Verknüpfung [https://aka.ms/mfasetup](https://aka.ms/mfasetup)).  Nun kann ein AD FS Benutzer, der noch keine MFA-Überprüfungs Informationen registriert hat,&#34;über die Verknüpfung [https://aka.ms/mfasetup](https://aka.ms/mfasetup) auf Azure AD s "proofup-Seite zugreifen, indem er nur die primäre Authentifizierung verwendet (z.b. die integrierte Windows-Authentifizierung oder Benutzername und Kennwort über die AD FS-Webseiten).  Wenn für den Benutzer keine Überprüfungsmethoden konfiguriert sind, wird Azure AD eine Inline Registrierung durchführen, bei der der &#34;Benutzer die von Ihrem Administrator benötigte Meldung erhält, dass Sie dieses Konto für&#34;eine zusätzliche Sicherheitsüberprüfung einrichten, und der Benutzer kann dann Wählen Sie &#34;diese Option aus,&#34;um Sie jetzt einzurichten.
> Benutzer, die bereits über mindestens eine konfigurierte MFA-Überprüfungs Methode verfügen, werden beim Besuchen der Seite "proofup weiterhin aufgefordert, MFA anzugeben.

## <a name="recommended-deployment-topologies"></a>Empfohlene Bereitstellungstopologien

### <a name="azure-mfa-as-primary-authentication"></a>Azure MFA als primäre Authentifizierung

Es gibt einige hervorragend Gründe, Azure MFA als primäre Authentifizierung mit AD FS zu verwenden:

 - So vermeiden Sie Kenn Wörter für die Anmeldung bei Azure AD, Office 365 und anderen AD FS-apps
 - So schützen Sie die Kenn Wort basierte Anmeldung mithilfe eines zusätzlichen Faktors, z. b. Überprüfungs Code vor dem Kennwort

Wenn Sie Azure MFA als primäre Authentifizierungsmethode in AD FS verwenden möchten, um diese Vorteile zu erzielen, möchten Sie wahrscheinlich auch die Möglichkeit behalten, Azure AD bedingten Zugriff einschließlich &#34;echter MFA&#34; zu verwenden, indem Sie zusätzliche Faktoren in AD FS anfordern.

Zu diesem Zweck können Sie die Azure AD Domänen Einstellung für die lokale MFA-Konfiguration konfigurieren ( &#34;supportsmfa&#34; auf $true festlegen).  In dieser Konfiguration können AD FS von Azure AD aufgefordert werden, eine zusätzliche Authentifizierung oder &#34;eine echte MFA&#34; für bedingte Zugriffs Szenarien durchzuführen, die dies erfordern.  

Wie oben beschrieben, sollte jeder AD FS Benutzer, der noch nicht registriert ist (MFA-Überprüfungs Informationen konfiguriert), über eine angepasste AD FS Fehlerseite [https://aka.ms/mfasetup](https://aka.ms/mfasetup) aufgefordert werden, zum Überprüfen der Überprüfungs Informationen aufgefordert zu werden. Anschließend wird AD FS Anmeldung erneut versucht.  
Da Azure MFA als primär Faktor angesehen wird, müssen die Benutzer nach der Erstkonfiguration einen zusätzlichen Faktor zum Verwalten oder Aktualisieren Ihrer Überprüfungs Informationen in Azure AD oder zum Zugriff auf andere Ressourcen, für die MFA erforderlich ist, bereitstellen.

>[!NOTE]
> Mit ADFS 2019 müssen Sie eine Änderung am Anker Anspruchstyp für die Active Directory Anspruchs Anbieter-Vertrauensstellung vornehmen und diese von "windowsaccountname" in "UPN" ändern. Führen Sie das unten angegebene PowerShell-Cmdlet aus. Dies hat keine Auswirkung auf die interne Funktionsweise der AD FS Farm. Möglicherweise werden Sie feststellen, dass einige Benutzer erneut zur Eingabe von Anmelde Informationen aufgefordert werden, sobald diese Änderung vorgenommen wird. Nachdem die Anmeldung wieder erfolgt ist, sehen Endbenutzer keinen Unterschied. 

```powershell
Set-AdfsClaimsProviderTrust -AnchorClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" -TargetName "Active Directory"
```

### <a name="azure-mfa-as-additional-authentication-to-office-365"></a>Azure MFA als zusätzliche Authentifizierung für Office 365

Wenn Sie in der Vergangenheit Azure MFA als zusätzliche Authentifizierungsmethode in AD FS für Office 365 oder andere vertrauende Seiten verwenden wollten, war es am besten, Azure AD für eine Verbund-MFA zu konfigurieren, bei der die primäre Authentifizierung lokal in AD FS und MFA der TR-Dienst ausgeführt wird. durch Azure AD igelt. Nun können Sie Azure MFA als zusätzliche Authentifizierung in AD FS verwenden, wenn die Einstellung für die Einstellung für die Domäne auf $true festgelegt ist.  

Wie oben beschrieben, sollte jeder AD FS Benutzer, der noch nicht registriert ist (MFA-Überprüfungs Informationen konfiguriert), über eine angepasste AD FS Fehlerseite [https://aka.ms/mfasetup](https://aka.ms/mfasetup) aufgefordert werden, zum Überprüfen der Überprüfungs Informationen aufgefordert zu werden. Anschließend wird AD FS Anmeldung erneut versucht.  

## <a name="pre-requisites"></a>Voraussetzungen

Die folgenden Voraussetzungen sind erforderlich, wenn Sie Azure MFA für die Authentifizierung mit AD FS verwenden:  
  
- Ein [Azure-Abonnement mit Azure Active Directory](https://azure.microsoft.com/pricing/free-trial/).  
- [Azure-Multi-Factor Authentication](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/) 


> [!NOTE]
> Azure AD und Azure MFA sind in Azure AD Premium und in der Enterprise Mobility Suite (EMS) enthalten.  Wenn Sie über eines dieser beiden verfügen, benötigen Sie keine einzelnen Abonnements.

- Eine lokale Umgebung von Windows Server 2016 AD FS.  
   - Der Server muss in der Lage sein, über Port 443 mit den folgenden URLs zu kommunizieren.
      - https://adnotifications.windowsazure.com
      - https://login.microsoftonline.com
- Ihre lokale Umgebung ist im [Verbund mit Azure AD.](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#configuring-federation-with-ad-fs)  
- [Windows Azure Active Directory-Modul für Windows PowerShell](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0).  
- Globale Administrator Berechtigungen für Ihre Instanz von Azure AD, Sie mithilfe Azure AD PowerShell zu konfigurieren.  
- Unternehmens Administrator-Anmelde Informationen zum Konfigurieren der AD FS-Farm für Azure MFA.  
  
## <a name="configure-the-ad-fs-servers"></a>Konfigurieren der AD FS Server

Um die Konfiguration für Azure MFA für AD FS abzuschließen, müssen Sie alle AD FS Server mithilfe der beschriebenen Schritte konfigurieren. 

>[!NOTE]
>Stellen Sie sicher, dass diese Schritte auf **allen** AD FS Servern in der Farm ausgeführt werden. Wenn Sie über mehrere AD FS Server in der Farm verfügen, können Sie die erforderliche Konfiguration remote mithilfe Azure AD PowerShell ausführen.  

### <a name="step-1-generate-a-certificate-for-azure-mfa-on-each-ad-fs-server-using-the-new-adfsazuremfatenantcertificate-cmdlet"></a>Schritt 1: Generieren eines Zertifikats für Azure MFA auf jedem AD FS Server mithilfe des `New-AdfsAzureMfaTenantCertificate` Cmdlets

Als erstes müssen Sie ein Zertifikat generieren, das von Azure MFA verwendet werden kann.  Dies kann mithilfe von PowerShell erfolgen.  Das generierte Zertifikat befindet sich im Zertifikat Speicher der lokalen Computer und ist mit einem Antragsteller Namen gekennzeichnet, der die Mandanten-ID für Ihr Azure AD Verzeichnis enthält.

![AD FS und MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA3.png)  

Beachten Sie, dass tenantid der Name Ihres Verzeichnisses in Azure AD ist.  Verwenden Sie das folgende PowerShell-Cmdlet, um das neue Zertifikat zu generieren.  
    `$certbase64 = New-AdfsAzureMfaTenantCertificate -TenantID <tenantID>`  

![AD FS und MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA1.PNG)  
  
### <a name="step-2-add-the-new-credentials-to-the-azure-multi-factor-auth-client-service-principal"></a>Schritt 2: Fügen Sie die neuen Anmelde Informationen zum Azure Multi-Factor Authentication-Client Dienst Prinzipal hinzu.

Um für die AD FS-Server die Kommunikation mit dem Azure Multi-Factor Authentication-Client zu ermöglichen, müssen Sie die Anmelde Informationen dem Dienst Prinzipal für den Azure Multi-Factor Authentication-Client hinzufügen. Die Zertifikate, die mit `New-AdfsAzureMFaTenantCertificate` dem Cmdlet generiert werden, dienen als diese Anmelde Informationen. Führen Sie die folgenden Schritte mithilfe von PowerShell aus, um die neuen Anmelde Informationen zum Azure Multi-Factor Authentication-Client Dienst Prinzipal hinzuzufügen.  

> [!NOTE]
> Zum Ausführen dieses Schritts müssen Sie mit PowerShell `Connect-MsolService`eine Verbindung mit Ihrer Instanz von Azure AD herstellen.  Diese Schritte setzen voraus, dass Sie bereits eine Verbindung über PowerShell hergestellt haben.  Weitere Informationen finden [ `Connect-MsolService`Sie unter.](https://msdn.microsoft.com/library/dn194123.aspx)  

**Legen Sie das Zertifikat als die neuen Anmelde Informationen für den Azure Multi-Factor Authentication-Client fest.**  

`New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type asymmetric -Usage verify -Value $certBase64`

> [!IMPORTANT]
> Dieser Befehl muss auf allen AD FS Servern in der Farm ausgeführt werden.  Azure AD MFA schlägt auf Servern fehl, auf denen das Zertifikat nicht als neue Anmelde Informationen für den Azure Multi-Factor Authentication-Client festgelegt ist.

> [!NOTE]  
> 981b1-7B b-A875-b08b09b8cd720 ist die GUID für den Azure Multi-Factor Authentication-Client.  
  
## <a name="configure-the-ad-fs-farm"></a>Konfigurieren der AD FS-Farm  
  
Nachdem Sie den vorherigen Abschnitt auf den einzelnen AD FS Server abgeschlossen haben, müssen Sie das `Set-AdfsAzureMfaTenant` Cmdlet ausführen.  
  
Dieses Cmdlet muss nur einmal für eine AD FS Farm ausgeführt werden.  Verwenden Sie PowerShell, um diesen Schritt abzuschließen.
  
> [!NOTE]  
> Sie müssen den AD FS-Dienst auf jedem Server in der Farm neu starten, damit diese Änderungen wirksam werden.  
  
    Set-AdfsAzureMfaTenant -TenantId <tenant ID> -ClientId 981f26a1-7f43-403b-a875-f8b09b8cd720  

![AD FS und MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA5.png)  
  
Danach sehen Sie, dass Azure MFA als primäre Authentifizierungsmethode für die Intranet-und Extranetverwendung verfügbar ist.    
  
![AD FS und MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA6.png)  

## <a name="renew-and-manage-ad-fs-azure-mfa-certificates"></a>Erneuern und Verwalten von AD FS Azure MFA-Zertifikaten

Die folgende Anleitung führt Sie durch die Verwaltung der Azure MFA-Zertifikate auf Ihren AD FS Servern.
Wenn Sie AD FS mit Azure MFA konfigurieren, sind die Zertifikate, die über das `New-AdfsAzureMfaTenantCertificate` PowerShell-Cmdlet generiert werden, standardmäßig für 2 Jahre gültig.  Gehen Sie folgendermaßen vor, um zu bestimmen, wie kurz die Zertifikate ablaufen, und um neue Zertifikate zu erneuern.

### <a name="assess-ad-fs-azure-mfa-certificate-expiration-date"></a>Bewerten des Ablaufdatums für das Azure MFA-Zertifikat AD FS

Auf jedem AD FS Server auf dem lokalen Computer My Store ist ein selbst signiertes Zertifikat mit &#34;OE = Microsoft AD FS Azure MFA&#34; im Aussteller und Betreff vorhanden.  Dies ist das Azure MFA-Zertifikat.  Überprüfen Sie die Gültigkeitsdauer dieses Zertifikats auf jedem AD FS Server, um das Ablaufdatum zu bestimmen.  

### <a name="create-new-ad-fs-azure-mfa-certificate-on-each-ad-fs-server"></a>Erstellen Sie auf jedem AD FS Server neue AD FS Azure MFA-Zertifikat.

Wenn sich die Gültigkeitsdauer Ihrer Zertifikate nähert, starten Sie den Erneuerungs Vorgang, indem Sie auf jedem AD FS Server ein neues Azure MFA-Zertifikat erstellen. Generieren Sie in einem PowerShell-Befehlsfenster auf jedem AD FS Server ein neues Zertifikat mit dem folgenden Cmdlet:

```
PS C:\> $newcert = New-AdfsAzureMfaTenantCertificate -TenantId <tenant id such as contoso.onmicrosoft.com> -Renew $true
```

Durch dieses Cmdlet wird ein neues Zertifikat generiert, das von 2 Tagen in der Zukunft bis 2 Tage + 2 Jahre gültig ist.  Die AD FS-und Azure MFA-Vorgänge werden von diesem Cmdlet oder dem neuen Zertifikat nicht beeinträchtigt. (Hinweis: die 2-tägige Verzögerung ist beabsichtigt und bietet Zeit zum Ausführen der folgenden Schritte, um das neue Zertifikat im Mandanten zu konfigurieren, bevor AD FS es für Azure MFA verwendet.)

### <a name="configure-each-new-ad-fs-azure-mfa-certificate-in-the-azure-ad-tenant"></a>Konfigurieren Sie jedes neue AD FS Azure MFA-Zertifikat im Azure AD Mandanten.

Wenn Sie das Azure AD PowerShell-Modul verwenden, aktualisieren Sie für jedes neue Zertifikat (auf jedem AD FS Server) ihre Azure AD Mandanten Einstellungen wie folgt (Hinweis: Sie müssen zuerst mithilfe `Connect-MsolService` von eine Verbindung mit dem Mandanten herstellen, um die folgenden Befehle auszuführen).

```
PS C:/> New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type Asymmetric -Usage Verify -Value $newcert
```

`$certbase64`ist das neue Zertifikat.  Das Base64-codierte Zertifikat kann abgerufen werden, indem Sie das Zertifikat (ohne den privaten Schlüssel) als die der-codierten Datei exportieren und in "Notepad. exe" öffnen, dann in die PowerShell-Sitzung `$certbase64`kopieren/einfügen und der Variablen zuweisen.

### <a name="verify-that-the-new-certificates-will-be-used-for-azure-mfa"></a>Überprüfen Sie, ob die neuen Zertifikate für Azure MFA verwendet werden.

Sobald die neuen Zertifikate gültig sind, werden Sie von AD FS in wenigen Stunden bis zu einem Tag abgerufen und mit der Verwendung der einzelnen Zertifikate für Azure MFA begonnen.  Sobald dies geschieht, wird auf jedem Server ein Ereignis mit den folgenden Informationen im AD FS admin-Ereignisprotokoll angezeigt:

```
Log Name:      AD FS/Admin
Source:        AD FS
Date:          2/27/2018 7:33:31 PM
Event ID:      547
Task Category: None
Level:         Information
Keywords:      AD FS
User:          DOMAIN\adfssvc
Computer:      ADFS.domain.contoso.com
Description:
The tenant certificate for Azure MFA has been renewed.  

TenantId: contoso.onmicrosoft.com.
Old thumbprint: 7CC103D60967318A11D8C51C289EF85214D9FC63.
Old expiration date: 9/15/2019 9:43:17 PM.
New thumbprint: 8110D7415744C9D4D5A4A6309499F7B48B5F3CCF.
New expiration date: 2/27/2020 2:16:07 AM.
```

## <a name="customize-the-ad-fs-web-page-to-guide-users-to-register-mfa-verification-methods"></a>Anpassen der AD FS Webseite, um Benutzer zum Registrieren von MFA-Überprüfungsmethoden zu unterstützen

Verwenden Sie die folgenden Beispiele, um Ihre AD FS Webseiten für Benutzer anzupassen, die sich noch nicht gesichert haben (konfigurierte MFA-Überprüfungs Informationen).

### <a name="find-the-error"></a>Fehler suchen

Erstens gibt es eine Reihe von unterschiedlichen Fehlermeldungen AD FS die zurückgibt, wenn dem Benutzer keine Überprüfungs Informationen angezeigt werden.
Wenn Sie Azure MFA als primäre Authentifizierung verwenden, wird dem nicht gesicherten Benutzer eine AD FS Fehlerseite mit den folgenden Meldungen angezeigt:
```
    <div id="errorArea">
        <div id="openingMessage" class="groupMargin bigText">
            An error occurred
        </div>
        <div id="errorMessage" class="groupMargin">
            Authentication attempt failed. Select a different sign in option or close the web browser and sign in again. Contact your administrator for more information.
        </div>
```
Wenn Azure AD, dass eine weitere Authentifizierung versucht wird, wird dem nicht gesicherten Benutzer eine AD FS Fehlerseite mit den folgenden Meldungen angezeigt:
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

### <a name="catch-the-error-and-update-the-page-text"></a>Fangen Sie den Fehler ab, und aktualisieren Sie den Seiten Text

Um den Fehler zu erfassen und den benutzerdefinierten Leitfaden anzuzeigen, fügen Sie einfach das JavaScript an das Ende der Datei "OnLoad. js" an, die Teil des AD FS Webdesigns ist.  Dies ermöglicht Folgendes:
 - Suchen Sie nach der identifizierenden Fehler Zeichenfolge (n).
 - Bereitstellen von benutzerdefiniertem Webinhalt  

> [!NOTE]
> Eine Anleitung zum Anpassen der Datei "OnLoad. js" finden Sie im Artikel [Erweiterte Anpassung der AD FS Anmelde Seiten](advanced-customization-of-ad-fs-sign-in-pages.md).

Hier ist ein einfaches Beispiel, das Sie möglicherweise erweitern möchten:

1. Öffnen Sie Windows PowerShell auf Ihrem primären AD FS Server, und erstellen Sie ein neues AD FS-Webdesign, indem Sie den folgenden Befehl ausführen:
    
    ``` PowerShell
        New-AdfsWebTheme –Name ProofUp –SourceName default
    ``` 
2. Erstellen Sie als nächstes den Ordner, und exportieren Sie den Standard AD FS Webdesign:

    ``` PowerShell
       New-Item -Path 'c:\Theme' -ItemType Directory;Export-AdfsWebTheme –Name default –DirectoryPath c:\Theme
    ```
3. Öffnen Sie die Datei "c:\me\script\onload.js" in einem Text-Editor.
4. Fügen Sie den folgenden Code an das Ende der Datei "OnLoad. js" an.
    
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
        if (errorMessage) {
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
    }

    //End Customize MFA Exception
    //End Custom Code
    ```
    > [!IMPORTANT]
    > Sie müssen "< YOUR_DOMAIN_NAME_HERE >" ändern. , wenn der Domänen Name verwendet werden soll. Beispiel: `var domain_hint = "contoso.com";`
    
5. Speichern Sie die Datei "OnLoad. js".
6. Importieren Sie die Datei "OnLoad. js" in Ihr benutzerdefiniertes Design, indem Sie den folgenden Windows PowerShell-Befehl eingeben:
    
    ``` PowerShell
    Set-AdfsWebTheme -TargetName ProofUp -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';path="c:\theme\script\onload.js"}
    ```
7. Zum Schluss wenden Sie das benutzerdefinierte AD FS Webdesign an, indem Sie den folgenden Windows PowerShell-Befehl eingeben:
    
    ``` PowerShell
    Set-AdfsWebConfig -ActiveThemeName "ProofUp"
    ```

## <a name="next-steps"></a>Nächste Schritte

[Verwalten von TLS/SSL-Protokollen und Verschlüsselungs Sammlungen, die von AD FS und Azure MFA verwendet werden](manage-ssl-protocols-in-ad-fs.md)
