---
title: Zusammengesetzte Authentifizierung und Active Directory-Domänendiensten Ansprüche in Active Directory Federation Services
description: Das folgende Dokument wird erläutert, Verbundauthentifizierung und AD DS-Ansprüche in AD FS.
author: billmath
ms.author: billmath
manager: femila
ms.date: 09/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 270fb6efd63e6355c410ee45d09e6fd16b14222b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867991"
---
# <a name="compound-authentication-and-ad-ds-claims-in-ad-fs"></a>Zusammengesetzte Authentifizierung und AD DS-Ansprüchen in AD FS
Windows Server 2012 erweitert die Kerberos-Authentifizierung durch die Einführung von Verbundauthentifizierung.  Verbundauthentifizierung kann es sich um ein Kerberos Ticket-Granting Service (TGS) Anforderung zwei Identitäten gehören: 

- die Identität des Benutzers
- die Identität des Gerät des Benutzers.  

Windows führt der Verbundauthentifizierung durch die Erweiterung [Kerberos Flexible Authentication Secure Tunneling (FAST) oder Kerberos-hochrüstung](https://technet.microsoft.com/library/hh831747.aspx). 

AD FS 2012 und höheren Versionen können die Nutzung von AD DS-Benutzer oder Gerät Ansprüche ausgestellt, die in einer Kerberos-Authentifizierungsticket befinden. In früheren Versionen von AD FS die Ansprüche-Engine konnte von Kerberos nur Benutzer und Gruppe Sicherheits-IDs (SIDs) gelesen, aber konnte nicht gelesen werden alle Informationen zu Ansprüchen in ein Kerberos-Ticket enthalten sind.

Sie können umfangreichere Steuerung des Zugriffs auf verbundanwendungen mithilfe von Active Directory Domain Services (AD DS) aktivieren – Benutzer- und Geräteansprüche zusammen mit Active Directory-Verbunddienste (AD FS) ausgegeben.

## <a name="requirements"></a>Anforderungen
1.  Die Computer, die Zugriff auf verbundanwendungen, authentifiziert werden muss AD FS verwenden **integrierte Windows-Authentifizierung**. 
    - Integrierte Windows-Authentifizierung ist nur verfügbar, bei der die AD FS-Server im Back-End-Verbindung.
    - Computer müssen die Back-End-AD FS-Server für den Verbunddienstnamen erreichen sein.
    - AD FS-Server muss die integrierte Windows-Authentifizierung als eine primäre Authentifizierungsmethode in den zugehörigen Intranet-Einstellungen anbieten.

2.  Die Richtlinie **Kerberos-Clientunterstützung für Ansprüche Verbundauthentifizierung und Kerberos armoring** muss auf allen Computern, die Zugriff auf verbundanwendungen, die durch die Verbundauthentifizierung geschützten angewendet werden. Dies ist bei einem einzelnen Gesamtstruktur oder Gesamtstruktur-Szenarien anwendbar.

3.  Die Domäne, speichern die AD FS-Server müssen die **Kerberos-Clientunterstützung für Ansprüche und Kerberos armoring zusammengesetzte** richtlinieneinstellung, die auf die Domänencontroller angewendet.

## <a name="steps-for-configuring-ad-fs-in-windows-server-2012-r2"></a>Schritte zum Konfigurieren von AD FS in Windows Server 2012 R2
Verwenden Sie die folgenden Schritte aus, für die Konfiguration der Verbundauthentifizierung und Ansprüche 

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>Schritt 1:  Aktivieren der Kerberos-Clientunterstützung für Ansprüche, Verbundauthentifizierung und Kerberos-hochrüstung auf die Standard-Domänencontrollerrichtlinie
1.  Wählen Sie im Server-Manager-Tools, **Gruppenrichtlinienverwaltung**.
2.  Navigieren Sie nach unten, um die **Standarddomänencontroller-Richtlinie**mit der rechten Maustaste auf, und wählen Sie **bearbeiten**.
![Die Gruppenrichtlinien-Verwaltungskonsole](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc1.png)
3.  Auf der **Gruppenrichtlinienverwaltungs-Editor**unter **Computerkonfiguration**, erweitern Sie **Richtlinien**, erweitern Sie **Administrative Vorlagen** , erweitern Sie **System**, und wählen Sie **KDC**.
4.  Doppelklicken Sie im rechten Bereich auf **KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos-hochrüstung**.
![Die Gruppenrichtlinien-Verwaltungskonsole](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc2.png)
5.  Legen Sie im neuen Dialogfeld Fenster, Kerberos-Clientunterstützung für Ansprüche, **aktiviert**.
6.  Wählen Sie unter Optionen **unterstützte** aus der Dropdown-Menü, und klicken Sie dann auf **übernehmen** und **OK**.
![Die Gruppenrichtlinien-Verwaltungskonsole](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc3.png)

### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>Schritt 2: Aktivieren der Kerberos-Clientunterstützung für Ansprüche, Verbundauthentifizierung und Kerberos armoring auf Computern, die Zugriff auf verbundanwendungen

1.  Auf einer Gruppenrichtlinie angewendet werden, auf den Computern, die Zugriff auf verbundanwendungen, in der **Gruppenrichtlinienverwaltungs-Editor**unter **Computerkonfiguration**, erweitern Sie **Richtlinien**, erweitern Sie **Administrative Vorlagen**, erweitern Sie **System**, und wählen Sie **Kerberos**.
2.  Doppelklicken Sie im rechten Bereich des Gruppenrichtlinienverwaltungs-Editor-Fensters auf **Kerberos-Clientunterstützung für Ansprüche, Verbundauthentifizierung und Kerberos-hochrüstung.**
3.  Legen Sie im Fenster Neues Kerberos-Clientunterstützung auf **aktiviert** , und klicken Sie auf **übernehmen** und **OK**.
![Die Gruppenrichtlinien-Verwaltungskonsole](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc4.png)
4.  Schließen Sie den Gruppenrichtlinienverwaltungs-Editor.

### <a name="step-3-ensure-the-ad-fs-servers-have-been-updated"></a>Schritt 3: Stellen Sie sicher, dass die AD FS-Server aktualisiert wurden.
Sie müssen sicherstellen, dass die folgenden Updates auf Ihren AD FS-Servern installiert sind.

|Update/Aktualisieren|Beschreibung|
|----- | ----- |
|[KB2919355](https://www.microsoft.com/download/details.aspx?id=42335)|Kumulatives Sicherheitsupdate (einschließlich KB2919355, KB2932046, KB2934018, KB2937592, KB2938439)|
|[KB2959977](https://www.microsoft.com/download/details.aspx?id=42530)|Updates für Server 2012 R2|
|[Hotfix 3052122](https://support.microsoft.com/help/3052122/update-adds-support-for-compound-id-claims-in-ad-fs-tokens-in-windows)|Dieses Update bietet Unterstützung für zusammengesetzte ID-Ansprüche in Active Directory-Verbunddienste.|

### <a name="step-4-configure-the-primary-authentication-provider"></a>Schritt 4: Konfigurieren Sie den Anbieter für die primäre Authentifizierung

1. Legen Sie den primären Authentifizierungsanbieter auf **Windows-Authentifizierung** für AD FS-Intraneteinstellungen.
2. In AD FS-Verwaltung unter **Authentifizierungsrichtlinien**Option **primäre Authentifizierung** und wählen Sie unter **globale Einstellungen** klicken Sie auf **bearbeiten**.
3. Auf **globale Authentifizierungsrichtlinie bearbeiten** unter **Intranet** wählen **Windows-Authentifizierung**.
4. Klicken Sie auf **anwenden** und **Ok**.

![Gruppenrichtlinienverwaltung](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc5.png)

5. Mithilfe von PowerShell Sie können die **Set-AdfsGlobalAuthenticationPolicy** Cmdlet.

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>Basiert die eine WID-Farm, die PowerShell-Befehl auf dem primären AD FS-Server ausgeführt werden muss.
>In einer SQL-basierte-Farm kann der PowerShell-Befehl auf jedem AD FS-Server ausgeführt werden, die ein Mitglied der Farm ist.

### <a name="step-5--add-the-claim-description-to-ad-fs"></a>Schritt 5:  Fügen Sie die anspruchsbeschreibung für AD FS
1.  Fügen Sie die folgenden Anspruchsbeschreibung zur Farm hinzu. Diese Anspruchsbeschreibung ist nicht standardmäßig im AD FS 2012 R2 vorhanden und muss manuell hinzugefügt werden.
2.  In AD FS-Verwaltung unter **Service**, mit der rechten Maustaste **Beschreibung der Forderung** , und wählen Sie **Beschreibung der Forderung hinzufügen**
3.  Geben Sie die folgende Informationen in der anspruchsbeschreibung
    - Anzeigename: "Windows-Gerät-Group" 
    - Anspruchsbeschreibung: "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup" "
4. Setzen Sie ein Häkchen in beide Felder ein.
5. Klicken Sie auf **OK**.

![Anspruchsbeschreibung](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc6.png)

6. Mithilfe von PowerShell Sie können die **hinzufügen-AdfsClaimDescription** Cmdlet.
``` powershell
Add-AdfsClaimDescription -Name 'Windows device group' -ClaimType 'https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup' `
-ShortName 'windowsdevicegroup' -IsAccepted $true -IsOffered $true -IsRequired $false -Notes 'The windows group SID of the device' 
```


>[!NOTE]
>Basiert die eine WID-Farm, die PowerShell-Befehl auf dem primären AD FS-Server ausgeführt werden muss.
>In einer SQL-basierte-Farm kann der PowerShell-Befehl auf jedem AD FS-Server ausgeführt werden, die ein Mitglied der Farm ist.

### <a name="step-6--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>Schritt 6:  Aktivieren Sie die Verbundauthentifizierung Bit des MsDS-SupportedEncryptionTypes-Attributs

1.  Enable-Verbundauthentifizierung bit des MsDS-SupportedEncryptionTypes-Attributs für das Konto, die Sie festgelegt haben, führen Sie den AD FS-Dienst mithilfe der **Set-ADServiceAccount** PowerShell-Cmdlet.  

>[!NOTE]
>Wenn Sie das Dienstkonto ändern, müssen Sie manuell die Verbundauthentifizierung aktivieren, indem Sie Ausführung der **Set-ADUser - CompoundIdentitySupported: $true** Windows PowerShell-Cmdlets.

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true 
```
2.  Starten Sie den AD FS-Dienst neu.

>[!NOTE]
>Nach dem Festlegen auf "true" Installation von dasselbe gMSA auf neuen Servern (2012 R2/2016) nicht mit etwa folgendem Wortlaut: "CompoundIdentitySupported" **Install-ADServiceAccount: Dienstkonto kann nicht installiert werden. Fehlermeldung: "Des bereitgestellten Kontexts entsprach nicht das Ziel."** .
>
>**Lösung**: CompoundIdentitySupported werden vorübergehend auf $false festgelegt. Dieser Schritt bewirkt, dass AD FS, um Ausstellen von Ansprüchen von WindowsDeviceGroup zu beenden. Set-ADServiceAccount-Identity "AD FS-Dienstkonto" - CompoundIdentitySupported: $false das gruppenverwaltete Dienstkonto auf dem neuen Server installieren und aktivieren Sie dann wieder auf $True CompoundIdentitySupported.
CompoundIdentitySupported deaktivieren, und klicken Sie dann ein erneutes Aktivieren, ist AD FS-Dienst neu gestartet werden, nicht erforderlich.

### <a name="step-7-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>Schritt 7: Update der AD FS-Anspruchsanbieter-Vertrauensstellung für Active Directory

1. Aktualisieren Sie die AD FS Anspruchsanbieter-Vertrauensstellung für Active Directory die folgende Anspruchsregel von 'Pass-Through-' für "WindowsDeviceGroup"-Anspruch enthält.
2.  In **AD FS-Verwaltung**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen** und im rechten Bereich mit der rechten Maustaste auf **Active Directory** , und wählen Sie **Edit Claim Rules**.
3.  Auf der **Anspruchsregeln für Active Directory** klicken Sie auf **Regel hinzufügen**.
4.  Auf der **transformieren Anspruch Assistenten zum Hinzufügen von** wählen **Pass-Through oder Filtern eines eingehenden Anspruchs** , und klicken Sie auf **Weiter**.
5.  Fügen Sie einen Anzeigenamen ein, und wählen **Windows Gerätegruppe** aus der **eingehender Anspruchstyp** Dropdownliste aus.
6.  Klicken Sie auf **Fertig stellen**.  Klicken Sie auf **anwenden** und **Ok**. 
![Anspruchsbeschreibung](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc7.png)

### <a name="step-8-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>Schritt 8: Fügen Sie auf die abhängige Seite, in dem die Ansprüche 'WindowsDeviceGroup' erwartet werden, ähnlich wie "Pass-Through-" oder "Transformieren" Anspruchsregel hinzu.
2.  In **AD FS-Verwaltung**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten** und im rechten Bereich mit der rechten Maustaste auf Ihre RP, und wählen **Edit Claim Rules**.
3.  Auf der **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen**.
4.  Auf der **transformieren Anspruch Assistenten zum Hinzufügen von** wählen **Pass-Through oder Filtern eines eingehenden Anspruchs** , und klicken Sie auf **Weiter**.
5.  Fügen Sie einen Anzeigenamen ein, und wählen **Windows Gerätegruppe** aus der **eingehender Anspruchstyp** Dropdownliste aus.
6.  Klicken Sie auf **Fertig stellen**.  Klicken Sie auf **anwenden** und **Ok**.
![Anspruchsbeschreibung](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc8.png)


##<a name="steps-for-configuring-ad-fs-in-windows-server-2016"></a>Schritte zum Konfigurieren von AD FS in Windows Server 2016
Im folgenden werden die Schritte zum Konfigurieren von Verbundauthentifizierung in AD FS für WindowsServer 2016 beschrieben.

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>Schritt 1:  Aktivieren der Kerberos-Clientunterstützung für Ansprüche, Verbundauthentifizierung und Kerberos-hochrüstung auf die Standard-Domänencontrollerrichtlinie
1.  Wählen Sie im Server-Manager-Tools, **Gruppenrichtlinienverwaltung**.
2.  Navigieren Sie nach unten, um die **Standarddomänencontroller-Richtlinie**mit der rechten Maustaste auf, und wählen Sie **bearbeiten**.
3.  Auf der **Gruppenrichtlinienverwaltungs-Editor**unter **Computerkonfiguration**, erweitern Sie **Richtlinien**, erweitern Sie **Administrative Vorlagen** , erweitern Sie **System**, und wählen Sie **KDC**.
4.  Doppelklicken Sie im rechten Bereich auf **KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos-hochrüstung**.
5.  Legen Sie im neuen Dialogfeld Fenster, Kerberos-Clientunterstützung für Ansprüche, **aktiviert**.
6.  Wählen Sie unter Optionen **unterstützte** aus der Dropdown-Menü, und klicken Sie dann auf **übernehmen** und **OK**.


### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>Schritt 2: Aktivieren der Kerberos-Clientunterstützung für Ansprüche, Verbundauthentifizierung und Kerberos armoring auf Computern, die Zugriff auf verbundanwendungen

1.  Auf einer Gruppenrichtlinie angewendet werden, auf den Computern, die Zugriff auf verbundanwendungen, in der **Gruppenrichtlinienverwaltungs-Editor**unter **Computerkonfiguration**, erweitern Sie **Richtlinien**, erweitern Sie **Administrative Vorlagen**, erweitern Sie **System**, und wählen Sie **Kerberos**.
2.  Doppelklicken Sie im rechten Bereich des Gruppenrichtlinienverwaltungs-Editor-Fensters auf **Kerberos-Clientunterstützung für Ansprüche, Verbundauthentifizierung und Kerberos-hochrüstung.**
3.  Legen Sie im Fenster Neues Kerberos-Clientunterstützung auf **aktiviert** , und klicken Sie auf **übernehmen** und **OK**.
4.  Schließen Sie den Gruppenrichtlinienverwaltungs-Editor.

### <a name="step-3-configure-the-primary-authentication-provider"></a>Schritt 3: Konfigurieren Sie den Anbieter für die primäre Authentifizierung

1. Legen Sie den primären Authentifizierungsanbieter auf **Windows-Authentifizierung** für AD FS-Intraneteinstellungen.
2. In AD FS-Verwaltung unter **Authentifizierungsrichtlinien**Option **primäre Authentifizierung** und wählen Sie unter **globale Einstellungen** klicken Sie auf **bearbeiten**.
3. Auf **globale Authentifizierungsrichtlinie bearbeiten** unter **Intranet** wählen **Windows-Authentifizierung**.
4. Klicken Sie auf **anwenden** und **Ok**.
5. Mithilfe von PowerShell Sie können die **Set-AdfsGlobalAuthenticationPolicy** Cmdlet.

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>Basiert die eine WID-Farm, die PowerShell-Befehl auf dem primären AD FS-Server ausgeführt werden muss.
>In einer SQL-basierte-Farm kann der PowerShell-Befehl auf jedem AD FS-Server ausgeführt werden, die ein Mitglied der Farm ist.

### <a name="step-4--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>Schritt 4:  Aktivieren Sie die Verbundauthentifizierung Bit des MsDS-SupportedEncryptionTypes-Attributs

1.  Enable-Verbundauthentifizierung bit des MsDS-SupportedEncryptionTypes-Attributs für das Konto, die Sie festgelegt haben, führen Sie den AD FS-Dienst mithilfe der **Set-ADServiceAccount** PowerShell-Cmdlet.  

>[!NOTE]
>Wenn Sie das Dienstkonto ändern, müssen Sie manuell die Verbundauthentifizierung aktivieren, indem Sie Ausführung der **Set-ADUser - CompoundIdentitySupported: $true** Windows PowerShell-Cmdlets.

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true 
```
2.  Starten Sie den AD FS-Dienst neu.

>[!NOTE]
>Nach dem Festlegen auf "true" Installation von dasselbe gMSA auf neuen Servern (2012 R2/2016) nicht mit etwa folgendem Wortlaut: "CompoundIdentitySupported" **Install-ADServiceAccount: Dienstkonto kann nicht installiert werden. Fehlermeldung: "Des bereitgestellten Kontexts entsprach nicht das Ziel."** .
>
>**Lösung**: CompoundIdentitySupported werden vorübergehend auf $false festgelegt. Dieser Schritt bewirkt, dass AD FS, um Ausstellen von Ansprüchen von WindowsDeviceGroup zu beenden. Set-ADServiceAccount-Identity "AD FS-Dienstkonto" - CompoundIdentitySupported: $false das gruppenverwaltete Dienstkonto auf dem neuen Server installieren und aktivieren Sie dann wieder auf $True CompoundIdentitySupported.
CompoundIdentitySupported deaktivieren, und klicken Sie dann ein erneutes Aktivieren, ist AD FS-Dienst neu gestartet werden, nicht erforderlich.

### <a name="step-5-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>Schritt 5: Update der AD FS-Anspruchsanbieter-Vertrauensstellung für Active Directory

1. Aktualisieren Sie die AD FS Anspruchsanbieter-Vertrauensstellung für Active Directory die folgende Anspruchsregel von 'Pass-Through-' für "WindowsDeviceGroup"-Anspruch enthält.
2.  In **AD FS-Verwaltung**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen** und im rechten Bereich mit der rechten Maustaste auf **Active Directory** , und wählen Sie **Edit Claim Rules**.
3.  Auf der **Anspruchsregeln für Active Directory** klicken Sie auf **Regel hinzufügen**.
4.  Auf der **transformieren Anspruch Assistenten zum Hinzufügen von** wählen **Pass-Through oder Filtern eines eingehenden Anspruchs** , und klicken Sie auf **Weiter**.
5.  Fügen Sie einen Anzeigenamen ein, und wählen **Windows Gerätegruppe** aus der **eingehender Anspruchstyp** Dropdownliste aus.
6.  Klicken Sie auf **Fertig stellen**.  Klicken Sie auf **anwenden** und **Ok**. 


### <a name="step-6-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>Schritt 6: Fügen Sie auf die abhängige Seite, in dem die Ansprüche 'WindowsDeviceGroup' erwartet werden, ähnlich wie "Pass-Through-" oder "Transformieren" Anspruchsregel hinzu.
2.  In **AD FS-Verwaltung**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten** und im rechten Bereich mit der rechten Maustaste auf Ihre RP, und wählen **Edit Claim Rules**.
3.  Auf der **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen**.
4.  Auf der **transformieren Anspruch Assistenten zum Hinzufügen von** wählen **Pass-Through oder Filtern eines eingehenden Anspruchs** , und klicken Sie auf **Weiter**.
5.  Fügen Sie einen Anzeigenamen ein, und wählen **Windows Gerätegruppe** aus der **eingehender Anspruchstyp** Dropdownliste aus.
6.  Klicken Sie auf **Fertig stellen**.  Klicken Sie auf **anwenden** und **Ok**.

## <a name="validation"></a>Überprüfung
Die Version von "WindowsDeviceGroup" Ansprüche zu überprüfen, erstellen Sie einen Test-Ansprüche unterstützende Anwendung, die mithilfe von .net 4.6. Mit WIF SDK 4.0.
Konfigurieren Sie die Anwendung als eine vertrauende Seite in AD FS, und aktualisieren Sie es mit Anspruchsregel, wie im oben genannten Schritte angegeben.
Wenn in der Anwendung mithilfe der integrierten Windows-Authentifizierung-Anbieter von ADFS authentifiziert, sind die folgenden Ansprüche umgewandelt.
![Validation](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc9.png)

Die Ansprüche für den Computer/Gerät können nun für umfassendere Zugriffssteuerung genutzt werden.

Beispielsweise die folgenden **AdditionalAuthenticationRules** weist AD FS für die MFA aufrufen, ist – die authentifiziert Benutzer nicht Mitglied der Sicherheitsgruppe "-1-5-21-2134745077-1211275016-3050530490-1117" und dem Computer (, wo ist der Benutzer ist, Authentifizieren von) ist nicht Mitglied der Sicherheitsgruppe "S-1-5-21-2134745077-1211275016-3050530490-1115 (WindowsDeviceGroup)"

Allerdings, wenn eine der oben genannten Bedingungen erfüllt sind, rufen Sie nicht MFA auf.

```
'NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1115"])
&& NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1117"])
=> issue(Type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", Value = "https://schemas.microsoft.com/claims/multipleauthn");'
```
