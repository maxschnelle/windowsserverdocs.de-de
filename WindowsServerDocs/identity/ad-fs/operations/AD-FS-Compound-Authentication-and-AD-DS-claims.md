---
title: "Die Verbundauthentifizierung Authentifizierung und Active Directory-Domänendiensten Ansprüche in Active Directory-Verbunddienste"
description: "Nachfolgend wird erläutert, Verbundauthentifizierung und AD DS-Ansprüche in AD FS."
author: billmath
ms.author: billmath
manager: femila
ms.date: 09/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f5f80cbcbdb2deca9b098014627365b8ea819b5f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="compound-authentication-and-ad-ds-claims-in-ad-fs"></a>Verbundauthentifizierung und AD DS-Ansprüche in AD FS
Windows Server2012 wird Kerberos-Authentifizierung durch die Einführung von Verbundauthentifizierung verbessert.  Verbundauthentifizierung kann es sich um eine Anforderung Kerberos Ticket-Granting Warteschlangentransport (TGS) zwei Identitäten enthalten: 

- Die Identität des Benutzers
- Die Identität des Gerät des Benutzers.  

Windows führt Verbundauthentifizierung durch die Erweiterung [Kerberos flexible Authentication Secure Tunneling (FAST) oder Kerberos-hochrüstung](https://technet.microsoft.com/library/hh831747.aspx). 

AD FS 2012 und höheren Versionen können die Nutzung des AD DS-Benutzer bzw. das Gerät Ansprüche ausgestellt, die in ein Kerberos-Authentifizierungsticket befinden. In früheren Versionen von AD FS Ansprüche die Ansprüchen Modul konnte von Kerberos nur Benutzer und Gruppe Sicherheits-IDs (SIDs) gelesen, aber konnte nicht lesen ein Kerberos-Ticket enthaltenen Informationen.

Sie können umfassendere Steuerung des Zugriffs für verbundanwendungen mithilfe von Active Directory-Domänendienste (AD DS)-Benutzer- und Geräteansprüche zusammen mit Active Directory-Verbunddienste (AD FS) ausgegeben.

## <a name="requirements"></a>Anforderungen
1.  Die Computer, die Zugriff auf verbundanwendungen, authentifiziert werden muss mithilfe von AD FS **integrierte Windows-Authentifizierung**. 
    - Integrierte Windows-Authentifizierung ist nur verfügbar, bei der Verbindung mit dem Back-End-AD FS-Server.
    - Computer müssen die Back-End-AD FS-Server für des Verbunddiensts zu erreichen sein.
    - AD FS-Server müssen die integrierte Windows-Authentifizierung als eine primäre Authentifizierungsmethode in die Intraneteinstellungen anbieten.

2.  Die Richtlinie **Kerberos-Clientunterstützung für Ansprüche Verbundauthentifizierung und Kerberos Armoring** muss auf allen Computern, die Zugriff auf verbundanwendungen, die durch Verbundauthentifizierung geschützt sind, angewendet werden. Dies gilt bei einem einzelnen Gesamtstruktur oder plattformübergreifende Szenarien Gesamtstrukturen.

3.  Die Domäne mit der AD FS-Server müssen die **KDC-Unterstützung für Ansprüche die Verbundauthentifizierung und Kerberos-hochrüstung** Richtlinieneinstellung auf Domänencontrollern angewendet.

## <a name="steps-for-configuring-ad-fs-in-windows-server-2012-r2"></a>Schrittezum Konfigurieren von AD FS unter Windows Server2012 R2
Verwenden Sie die folgenden Schrittezum Konfigurieren der Verbundauthentifizierung und Ansprüche 

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>Schritt1: Aktivieren von KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos-hochrüstung auf die Standarddomänencontroller-Richtlinie
1.  Wählen Sie im Server-Manager-Tools **Gruppenrichtlinienverwaltung**.
2.  Navigieren Sie nach unten, um die **Standarddomänencontroller-Richtlinie**mit der rechten Maustaste auf, und wählen Sie **bearbeiten**.
![Die Gruppenrichtlinien-Verwaltungskonsole](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc1.png)
3.  Auf der **Gruppenrichtlinienverwaltungs-Editor**unter **Computerkonfiguration**, erweitern Sie **Richtlinien**, erweitern Sie **Administrative Vorlagen**, erweitern Sie **System**, und wählen Sie **KDC**.
4.  Doppelklicken Sie im rechten Bereich auf **KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring**.
![Die Gruppenrichtlinien-Verwaltungskonsole](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc2.png)
5.  Legen Sie im Fenster neue KDC-Unterstützung für Ansprüche **aktiviert**.
6.  Aktivieren Sie unter **unterstützte** aus dem Dropdownmenü und klicken Sie dann auf **übernehmen** und **OK**.
![Die Gruppenrichtlinien-Verwaltungskonsole](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc3.png)

### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>Schritt2: Aktivieren der Kerberos-Clientunterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring auf Computern, die Zugriff auf verbundanwendungen

1.  Auf einer Gruppenrichtlinie angewendet werden, auf den Computern, die Zugriff auf verbundanwendungen, in dem **Gruppenrichtlinienverwaltungs-Editor**unter **Computerkonfiguration**, erweitern Sie **Richtlinien**, erweitern Sie **Administrative Vorlagen**, erweitern Sie **System**, und wählen Sie **Kerberos**.
2.  Doppelklicken Sie im rechten Bereich des Gruppenrichtlinienverwaltungs-Editor-Fensters auf **Kerberos-Clientunterstützung für Ansprüche, Verbundauthentifizierung und Kerberos-hochrüstung.**
3.  Legen Sie im Fenster neue Kerberos-Clientunterstützung auf **aktiviert**, und klicken Sie auf **übernehmen** und **OK**.
![Die Gruppenrichtlinien-Verwaltungskonsole](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc4.png)
4.  Schließen Sie den Gruppenrichtlinienverwaltungs-Editor.

### <a name="step-3-ensure-the-ad-fs-servers-have-been-updated"></a>Schritt3: Stellen Sie sicher, dass die AD FS-Server aktualisiert wurden.
Sie müssen sicherstellen, dass die folgenden Updates auf die AD FS-Server installiert sind.

|Update|Beschreibung|
|----- | ----- |
|[KB2919355](https://www.microsoft.com/download/details.aspx?id=42335)|Kumulatives Sicherheitsupdate (einschließlich KB2919355, KB2932046, KB2934018, KB2937592, KB2938439)|
|[KB2959977](https://www.microsoft.com/download/details.aspx?id=42530)|Update für Server2012 R2|
|[Hotfix 3052122](https://support.microsoft.com/help/3052122/update-adds-support-for-compound-id-claims-in-ad-fs-tokens-in-windows)|Dieses Update bietet Unterstützung für zusammengesetzte ID Ansprüche in Active Directory-Verbunddienste.|

### <a name="step-4-configure-the-primary-authentication-provider"></a>Schritt4: Konfigurieren des primären Authentifizierungsanbieters

1. Legen Sie den primären Authentifizierungsanbieter auf **Windows-Authentifizierung** für AD FS-Intraneteinstellungen.
2. In AD FS-Verwaltung unter **Authentifizierungsrichtlinien**Option **primäre Authentifizierung** unter **globale Einstellungen** klicken Sie auf **bearbeiten**.
3. Auf **globale Authentifizierungsrichtlinie bearbeiten** unter **Intranet** wählen **Windows-Authentifizierung**.
4. Klicken Sie auf **gelten** und **Ok**.

![Die Gruppenrichtlinien-Verwaltungskonsole](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc5.png)

5. Mithilfe von PowerShell können Sie die **Set-AdfsGlobalAuthenticationPolicy** Cmdlet.

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>Basieren in einer WID Farm, die PowerShell-Befehl auf dem primären AD FS-Server ausgeführt werden muss.
>In einer Farm SQL-basierte kann der PowerShell-Befehl auf einem AD FS-Server ausgeführt werden, die Mitglied der Farm ist.

### <a name="step-5--add-the-claim-description-to-ad-fs"></a>Schritt5: Hinzufügen der anspruchsbeschreibung zu AD FS
1.  Fügen Sie die folgende Beschreibung der Anspruch der Farm hinzu. Diese Anspruchsbeschreibung ist nicht in AD FS 2012 R2 standardmäßig vorhanden und muss manuell hinzugefügt werden.
2.  In AD FS-Verwaltung unter **Service**, mit der rechten Maustaste **Beschreibung der Forderung**, und wählen Sie **Beschreibung der Forderung hinzufügen**
3.  Geben Sie die folgenden Informationen in der anspruchsbeschreibung
    - Anzeigename: "Windows Device Group" 
    - Anspruchsbeschreibung: 'https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup' "
4. Setzen Sie ein Häkchen in beide Felder ein.
5. Klicken Sie auf **OK**.

![Beschreibung der Forderung](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc6.png)

6. Mithilfe von PowerShell können Sie die **hinzufügen AdfsClaimDescription** Cmdlet.
``` powershell
Add-AdfsClaimDescription -Name 'Windows device group' -ClaimType 'https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup' `
-ShortName 'windowsdevicegroup' -IsAccepted $true -IsOffered $true -IsRequired $false -Notes 'The windows group SID of the device' 
```


>[!NOTE]
>Basieren in einer WID Farm, die PowerShell-Befehl auf dem primären AD FS-Server ausgeführt werden muss.
>In einer Farm SQL-basierte kann der PowerShell-Befehl auf einem AD FS-Server ausgeführt werden, die Mitglied der Farm ist.

### <a name="step-6--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>Schritt6: Aktivieren der Verbundauthentifizierung Bit des MsDS-SupportedEncryptionTypes-Attributs

1.  Enable-Verbundauthentifizierung bit für das MsDS-SupportedEncryptionTypes-Attribut für das Konto, das Sie zum Ausführen der AD FS-Dienst mit bestimmt die **Set-ADServiceAccount** PowerShell-Cmdlet.  

>[!NOTE]
>Wenn Sie das Dienstkonto ändern, müssen Sie manuell die Verbundauthentifizierung aktivieren, durch Ausführen der **Set-ADUser – CompoundIdentitySupported: $true** Windows PowerShell-Cmdlets.

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true 
```
2.  Starten Sie den AD FS-Dienst neu.

>[!NOTE]
>Sobald auf true festgelegt ist, Installation von dasselbe gMSA auf dem neuen Server (2012R2/2016) fehlschlägt, mit dem folgenden Fehler: 'CompoundIdentitySupported' festgelegt ist **Install-ADServiceAccount: Dienstkonto kann nicht installiert werden. Fehlermeldung: "der bereitgestellte Kontext Ziel entsprach nicht."**.
>
>**Lösung**: CompoundIdentitySupported vorübergehend auf $false festgelegt. Dieser Schrittbewirkt, dass AD FS zum Ausstellen von Ansprüchen WindowsDeviceGroup zu beenden. Set-ADServiceAccount-Identity 'AD FS-Dienstkonto' – CompoundIdentitySupported: $false gMSA auf dem neuen Server installieren und aktivieren Sie dann wieder auf $True CompoundIdentitySupported.
CompoundIdentitySupported deaktivieren und dann erneutes braucht nicht AD FS-Dienst neu gestartet werden.

### <a name="step-7-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>Schritt7: Update der AD FS-Anspruchsanbieter-Vertrauensstellung für Active Directory

1. Aktualisieren Sie die AD FS Anspruchsanbieter-Vertrauensstellung für Active Directory um folgende Anspruchsregel von 'Pass-Through-' für 'WindowsDeviceGroup' Anspruch.
2.  In **AD FS-Verwaltungs**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen** und im rechten Bereich mit der rechten Maustaste auf **Active Directory**, und wählen Sie **Anspruchsregeln bearbeiten**.
3.  Auf der **Anspruchsregeln bearbeiten für Active Directory** klicken Sie auf **Regel hinzufügen**.
4.  Auf der **Transform Claim Regel Assistenten zum Hinzufügen von** wählen **weiterleiten oder Filtern eines eingehenden Anspruchs**, und klicken Sie auf **Weiter**.
5.  Fügen Sie einen Anzeigenamen ein und wählen Sie **Windows Gerätegruppe** aus der **eingehender Anspruchstyp** Dropdownliste.
6.  Klicken Sie auf **Fertig stellen**.  Klicken Sie auf **gelten** und **Ok**. 
![Beschreibung der Forderung](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc7.png)

### <a name="step-8-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>Schritt8: Fügen Sie auf die vertrauende Seite von, in denen die Ansprüche 'WindowsDeviceGroup' erwartet werden, eine ähnliche Anspruchsregel 'Pass-Through-' oder "Transformieren".
2.  In **AD FS-Verwaltungs**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten** und im rechten Bereich mit der rechten Maustaste auf die RP und wählen Sie **Anspruchsregeln bearbeiten**.
3.  Auf der **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen**.
4.  Auf der **Transform Claim Regel Assistenten zum Hinzufügen von** wählen **weiterleiten oder Filtern eines eingehenden Anspruchs**, und klicken Sie auf **Weiter**.
5.  Fügen Sie einen Anzeigenamen ein und wählen Sie **Windows Gerätegruppe** aus der **eingehender Anspruchstyp** Dropdownliste.
6.  Klicken Sie auf **Fertig stellen**.  Klicken Sie auf **gelten** und **Ok**.
![Beschreibung der Forderung](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc8.png)


##<a name="steps-for-configuring-ad-fs-in-windows-server-2016"></a>Schrittezum Konfigurieren von AD FS in Windows Server2016
Im folgenden werden die Schrittezum Konfigurieren der Verbundauthentifizierung von AD FS für Windows Server 2016 beschrieben.

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>Schritt1: Aktivieren von KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos-hochrüstung auf die Standarddomänencontroller-Richtlinie
1.  Wählen Sie im Server-Manager-Tools **Gruppenrichtlinienverwaltung**.
2.  Navigieren Sie nach unten, um die **Standarddomänencontroller-Richtlinie**mit der rechten Maustaste auf, und wählen Sie **bearbeiten**.
3.  Auf der **Gruppenrichtlinienverwaltungs-Editor**unter **Computerkonfiguration**, erweitern Sie **Richtlinien**, erweitern Sie **Administrative Vorlagen**, erweitern Sie **System**, und wählen Sie **KDC**.
4.  Doppelklicken Sie im rechten Bereich auf **KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring**.
5.  Legen Sie im Fenster neue KDC-Unterstützung für Ansprüche **aktiviert**.
6.  Aktivieren Sie unter **unterstützte** aus dem Dropdownmenü und klicken Sie dann auf **übernehmen** und **OK**.


### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>Schritt2: Aktivieren der Kerberos-Clientunterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring auf Computern, die Zugriff auf verbundanwendungen

1.  Auf einer Gruppenrichtlinie angewendet werden, auf den Computern, die Zugriff auf verbundanwendungen, in dem **Gruppenrichtlinienverwaltungs-Editor**unter **Computerkonfiguration**, erweitern Sie **Richtlinien**, erweitern Sie **Administrative Vorlagen**, erweitern Sie **System**, und wählen Sie **Kerberos**.
2.  Doppelklicken Sie im rechten Bereich des Gruppenrichtlinienverwaltungs-Editor-Fensters auf **Kerberos-Clientunterstützung für Ansprüche, Verbundauthentifizierung und Kerberos-hochrüstung.**
3.  Legen Sie im Fenster neue Kerberos-Clientunterstützung auf **aktiviert**, und klicken Sie auf **übernehmen** und **OK**.
4.  Schließen Sie den Gruppenrichtlinienverwaltungs-Editor.

### <a name="step-3-configure-the-primary-authentication-provider"></a>Schritt3: Konfigurieren des primären Authentifizierungsanbieters

1. Legen Sie den primären Authentifizierungsanbieter auf **Windows-Authentifizierung** für AD FS-Intraneteinstellungen.
2. In AD FS-Verwaltung unter **Authentifizierungsrichtlinien**Option **primäre Authentifizierung** unter **globale Einstellungen** klicken Sie auf **bearbeiten**.
3. Auf **globale Authentifizierungsrichtlinie bearbeiten** unter **Intranet** wählen **Windows-Authentifizierung**.
4. Klicken Sie auf **gelten** und **Ok**.
5. Mithilfe von PowerShell können Sie die **Set-AdfsGlobalAuthenticationPolicy** Cmdlet.

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>Basieren in einer WID Farm, die PowerShell-Befehl auf dem primären AD FS-Server ausgeführt werden muss.
>In einer Farm SQL-basierte kann der PowerShell-Befehl auf einem AD FS-Server ausgeführt werden, die Mitglied der Farm ist.

### <a name="step-4--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>Schritt4: Aktivieren der Verbundauthentifizierung Bit des MsDS-SupportedEncryptionTypes-Attributs

1.  Enable-Verbundauthentifizierung bit für das MsDS-SupportedEncryptionTypes-Attribut für das Konto, das Sie zum Ausführen der AD FS-Dienst mit bestimmt die **Set-ADServiceAccount** PowerShell-Cmdlet.  

>[!NOTE]
>Wenn Sie das Dienstkonto ändern, müssen Sie manuell die Verbundauthentifizierung aktivieren, durch Ausführen der **Set-ADUser – CompoundIdentitySupported: $true** Windows PowerShell-Cmdlets.

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true 
```
2.  Starten Sie den AD FS-Dienst neu.

>[!NOTE]
>Sobald auf true festgelegt ist, Installation von dasselbe gMSA auf dem neuen Server (2012R2/2016) fehlschlägt, mit dem folgenden Fehler: 'CompoundIdentitySupported' festgelegt ist **Install-ADServiceAccount: Dienstkonto kann nicht installiert werden. Fehlermeldung: "der bereitgestellte Kontext Ziel entsprach nicht."**.
>
>**Lösung**: CompoundIdentitySupported vorübergehend auf $false festgelegt. Dieser Schrittbewirkt, dass AD FS zum Ausstellen von Ansprüchen WindowsDeviceGroup zu beenden. Set-ADServiceAccount-Identity 'AD FS-Dienstkonto' – CompoundIdentitySupported: $false gMSA auf dem neuen Server installieren und aktivieren Sie dann wieder auf $True CompoundIdentitySupported.
CompoundIdentitySupported deaktivieren und dann erneutes braucht nicht AD FS-Dienst neu gestartet werden.

### <a name="step-5-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>Schritt5: Aktualisieren der AD FS-Anspruchsanbieter-Vertrauensstellung für Active Directory

1. Aktualisieren Sie die AD FS Anspruchsanbieter-Vertrauensstellung für Active Directory um folgende Anspruchsregel von 'Pass-Through-' für 'WindowsDeviceGroup' Anspruch.
2.  In **AD FS-Verwaltungs**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen** und im rechten Bereich mit der rechten Maustaste auf **Active Directory**, und wählen Sie **Anspruchsregeln bearbeiten**.
3.  Auf der **Anspruchsregeln bearbeiten für Active Directory** klicken Sie auf **Regel hinzufügen**.
4.  Auf der **Transform Claim Regel Assistenten zum Hinzufügen von** wählen **weiterleiten oder Filtern eines eingehenden Anspruchs**, und klicken Sie auf **Weiter**.
5.  Fügen Sie einen Anzeigenamen ein und wählen Sie **Windows Gerätegruppe** aus der **eingehender Anspruchstyp** Dropdownliste.
6.  Klicken Sie auf **Fertig stellen**.  Klicken Sie auf **gelten** und **Ok**. 


### <a name="step-6-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>Schritt6: Fügen Sie auf die vertrauende Seite von, in denen die Ansprüche 'WindowsDeviceGroup' erwartet werden, eine ähnliche Anspruchsregel 'Pass-Through-' oder "Transformieren".
2.  In **AD FS-Verwaltungs**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten** und im rechten Bereich mit der rechten Maustaste auf die RP und wählen Sie **Anspruchsregeln bearbeiten**.
3.  Auf der **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen**.
4.  Auf der **Transform Claim Regel Assistenten zum Hinzufügen von** wählen **weiterleiten oder Filtern eines eingehenden Anspruchs**, und klicken Sie auf **Weiter**.
5.  Fügen Sie einen Anzeigenamen ein und wählen Sie **Windows Gerätegruppe** aus der **eingehender Anspruchstyp** Dropdownliste.
6.  Klicken Sie auf **Fertig stellen**.  Klicken Sie auf **gelten** und **Ok**.

## <a name="validation"></a>Überprüfung
Überprüfen die Version von 'WindowsDeviceGroup' Ansprüche, erstellen Sie einen Test-Ansprüche unterstützende Anwendung, die mit .net 4.6. Mit WIF-SDK 4.0.
Konfigurieren Sie die Anwendung als einer vertrauenden in AD FS, und aktualisieren Sie ihn mit Anspruchsregel gemäß der Angabe in der oben beschriebenen Schritte.
Bei der Authentifizierung an die Anwendung, die integrierte Windows-Authentifizierung-Anbieter des AD FS verwenden, werden die folgenden Ansprüche umgewandelt.
![Überprüfung](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc9.png)

Die Ansprüche für den Computer/Gerät können jetzt für umfangreichere zugriffssteuerungen genutzt werden.

Beispielsweise die folgenden **AdditionalAuthenticationRules** weist AD FS MFA aufgerufen, wenn – authentifiziert Benutzer nicht Mitglied der Sicherheitsgruppe ist "-1-5-21-2134745077-1211275016-3050530490-1117" und der Computer (steht für der Benutzer ist. Authentifizieren von) ist kein Mitglied der Sicherheitsgruppe "S-1-5-21-2134745077-1211275016-3050530490-1115 (WindowsDeviceGroup)"

Jedoch, wenn eine der oben genannten Bedingungen erfüllt sind, führen Sie keine rufen Sie MFA auf.

```
'NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1115"])
&& NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1117"])
=> issue(Type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", Value = "https://schemas.microsoft.com/claims/multipleauthn");'
```