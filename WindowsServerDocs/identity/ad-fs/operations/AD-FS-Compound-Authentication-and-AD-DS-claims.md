---
title: Verbund Authentifizierung und Active Directory Domain Services Ansprüche in Active Directory-Verbunddienste (AD FS)
description: Im folgenden Dokument werden die Verbund Authentifizierung und die AD DS Ansprüche in AD FS erläutert.
author: billmath
ms.author: billmath
manager: femila
ms.date: 09/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b67177c8bf0ce9869aa51c3012d57f3208ac02f5
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866286"
---
# <a name="compound-authentication-and-ad-ds-claims-in-ad-fs"></a>Zusammengesetzte Authentifizierung und AD DS-Ansprüchen in AD FS
Windows Server 2012 verbessert die Kerberos-Authentifizierung durch die Einführung der Verbund Authentifizierung.  Die Verbund Authentifizierung ermöglicht es, dass eine Kerberos-TGS-Anforderung (Ticket Gewährung Service) zwei Identitäten umfasst: 

- die Identität des Benutzers.
- die Identität des Geräts des Benutzers.  

Windows erreicht die Verbund Authentifizierung durch Erweiterung der [flexiblen Kerberos-Authentifizierung Secure Tunneling (fast) oder Kerberos armoring](https://technet.microsoft.com/library/hh831747.aspx). 

AD FS 2012 und höhere Versionen können AD DS ausgegebene Benutzer-oder Geräteansprüche in einem Kerberos-Authentifizierungs Ticket genutzt werden. In früheren Versionen von AD FS konnte die Anspruchs-Engine nur Benutzer-und Gruppen Sicherheits-IDs (SIDs) aus Kerberos lesen, konnte jedoch keine in einem Kerberos-Ticket enthaltenen Anspruchs Informationen lesen.

Sie können eine umfassendere Zugriffs Steuerung für Verbund Anwendungen mithilfe Active Directory Domain Services (AD DS) ausgestelltes Benutzer-und Geräteansprüche mit Active Directory-Verbunddienste (AD FS) (AD FS) aktivieren.

## <a name="requirements"></a>Anforderungen
1.  Die Computer, die auf Verbund Anwendungen zugreifen, müssen sich bei AD FS mithilfe der **integrierten Windows-Authentifizierung**authentifizieren. 
    - Die integrierte Windows-Authentifizierung ist nur verfügbar, wenn eine Verbindung mit den Back-End-AD FS Servern
    - Computer müssen die Back-End-AD FS Server für Verbunddienst Namen erreichen können.
    - AD FS Server müssen die integrierte Windows-Authentifizierung als primäre Authentifizierungsmethode in den Intraneteinstellungen anbieten.

2.  Die Richtlinie **Kerberos-Client Unterstützung für Anspruchs Verbund Authentifizierung und Kerberos armoring** muss auf alle Computer angewendet werden, die auf Verbund Anwendungen zugreifen, die durch Verbund Authentifizierung geschützt sind. Dies gilt für einzelne Gesamtstruktur-oder Gesamtstruktur übergreifende Szenarien.

3.  Die Domänen, auf denen sich die AD FS Server befinden, müssen über die **KDC-Unterstützung für die Anspruchs Verbund Authentifizierung und die Kerberos armoring-** Richtlinien Einstellung verfügen

## <a name="steps-for-configuring-ad-fs-in-windows-server-2012-r2"></a>Schritte zum Konfigurieren von AD FS in Windows Server 2012 R2
Verwenden Sie die folgenden Schritte zum Konfigurieren der Verbund Authentifizierung und der Ansprüche. 

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>Schritt 1:  Aktivieren der KDC-Unterstützung für Ansprüche, Verbund Authentifizierung und Kerberos armoring in der Standard Domänen Controller-Richtlinie
1.  Wählen Sie in Server-Manager Tools, **Gruppenrichtlinie Verwaltung**aus.
2.  Navigieren Sie zur **Standard Domänen Controller Richtlinie**, klicken Sie mit der rechten Maustaste, und wählen Sie **Bearbeiten**aus.
![Gruppenrichtlinie Verwaltung](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc1.png)
3.  Erweitern Sie auf der **Gruppenrichtlinienverwaltungs-Editor**unter **Computer Konfiguration**nacheinander **Richtlinien**, **Administrative Vorlagen**, **System**und **KDC**.
4.  Doppelklicken Sie im rechten Bereich auf **KDC-Unterstützung für Ansprüche, Verbund Authentifizierung und Kerberos armoring**.
![Gruppenrichtlinie Verwaltung](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc2.png)
5.  Legen Sie im Dialogfeld neu die Option KDC-Unterstützung für Ansprüche auf **aktiviert**fest.
6.  Wählen Sie unter Optionen die Option **unterstützt** im Dropdown Menü aus, **und klicken Sie** dann auf übernehmen und **OK**.
![Gruppenrichtlinie Verwaltung](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc3.png)

### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>Schritt 2: Aktivieren der Kerberos-Client Unterstützung für Ansprüche, Verbund Authentifizierung und Kerberos armoring auf Computern, die auf Verbund Anwendungen zugreifen

1.  Auf einer Gruppenrichtlinie die auf die Computer angewendet werden, die auf Verbund Anwendungen zugreifen, klicken Sie im **Gruppenrichtlinienverwaltungs-Editor**unter **Computer Konfiguration**auf **Richtlinien**, erweitern Sie **Administrative Vorlagen**und dann **System.** , und wählen Sie **Kerberos**aus.
2.  Doppelklicken Sie im rechten Fensterbereich des Fensters Gruppenrichtlinienverwaltungs-Editor auf **Kerberos-Client Unterstützung für Ansprüche, Verbund Authentifizierung und Kerberos armoring.**
3.  Legen Sie im Dialogfeld neu die Kerberos-Client Unterstützung auf **aktiviert** fest, und klicken Sie **dann** auf übernehmen und **OK**.
![Gruppenrichtlinie Verwaltung](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc4.png)
4.  Schließen Sie den Gruppenrichtlinienverwaltungs-Editor.

### <a name="step-3-ensure-the-ad-fs-servers-have-been-updated"></a>Schritt 3: Stellen Sie sicher, dass die AD FS Server aktualisiert wurden.
Sie müssen sicherstellen, dass die folgenden Updates auf dem AD FS-Server installiert sind.

|Update|Beschreibung|
|----- | ----- |
|[KB2919355](https://www.microsoft.com/download/details.aspx?id=42335)|Kumulatives Sicherheitsupdate (umfasst KB2919355, KB2932046, KB2934018, KB2937592, KB2938439)|
|[KB2959977](https://www.microsoft.com/download/details.aspx?id=42530)|Update für Server 2012 R2|
|[Hotfix 3052122](https://support.microsoft.com/help/3052122/update-adds-support-for-compound-id-claims-in-ad-fs-tokens-in-windows)|Dieses Update fügt Unterstützung für Verbund-ID-Ansprüche in Active Directory-Verbunddienste (AD FS) hinzu.|

### <a name="step-4-configure-the-primary-authentication-provider"></a>Schritt 4: Konfigurieren des primären Authentifizierungs Anbieters

1. Legen Sie den primären Authentifizierungs Anbieter für AD FS Intraneteinstellungen auf **Windows-Authentifizierung** fest.
2. Wählen Sie in AD FS Verwaltung unter **Authentifizierungs Richtlinien**die Option **primäre Authentifizierung** aus, und klicken Sie unter **globale Einstellungen** auf **Bearbeiten**.
3. Wählen Sie unter **Globale Authentifizierungs Richtlinie bearbeiten** unter **Intranet** die Option **Windows-Authentifizierung**aus.
4. Klicken **Sie** auf übernehmen und **OK**.

![Gruppenrichtlinienverwaltung](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc5.png)

5. Mithilfe von PowerShell können Sie das Cmdlet **Set-adfsglobalauthenticationpolicy** verwenden.

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>In einer wid-basierten Farm muss der PowerShell-Befehl auf dem primären AD FS Server ausgeführt werden.
>In einer SQL-basierten Farm kann der PowerShell-Befehl auf jedem AD FS Server ausgeführt werden, der Mitglied der Farm ist.

### <a name="step-5--add-the-claim-description-to-ad-fs"></a>Schritt 5:  Fügen Sie die Anspruchs Beschreibung AD FS
1. Fügen Sie der Farm die folgende Anspruchs Beschreibung hinzu. Diese Anspruchs Beschreibung ist in ADFS 2012 R2 standardmäßig nicht vorhanden und muss manuell hinzugefügt werden.
2. Klicken Sie in AD FS Verwaltung unter **Dienst**mit der rechten Maustaste auf **Anspruchs Beschreibung** , und wählen Sie **Anspruchs Beschreibung hinzufügen** aus.
3. Geben Sie in der Anspruchs Beschreibung die folgenden Informationen ein:
   - Anzeigename: "Windows-Gerätegruppe" 
   - Anspruchs Beschreibung: '<https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup>' '
4. Aktivieren Sie beide Kontrollkästchen.
5. Klicken Sie auf **OK**.

![Anspruchs Beschreibung](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc6.png)

6. Mithilfe von PowerShell können Sie das Cmdlet **Add-ADF sclaimdescription** verwenden.
   ``` powershell
   Add-AdfsClaimDescription -Name 'Windows device group' -ClaimType 'https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup' `
   -ShortName 'windowsdevicegroup' -IsAccepted $true -IsOffered $true -IsRequired $false -Notes 'The windows group SID of the device' 
   ```


>[!NOTE]
>In einer wid-basierten Farm muss der PowerShell-Befehl auf dem primären AD FS Server ausgeführt werden.
>In einer SQL-basierten Farm kann der PowerShell-Befehl auf jedem AD FS Server ausgeführt werden, der Mitglied der Farm ist.

### <a name="step-6--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>Schritt 6:  Aktivieren Sie das Verbund Authentifizierungs Bit für das msDS-supportedencryptiontypes-Attribut.

1.  Aktivieren Sie das Verbund Authentifizierungs Bit für das msDS-supportedencryptiontypes-Attribut im Konto, das Sie zum Ausführen des AD FS Dienstanbieter mit dem PowerShell-Cmdlet " **Set-ADServiceAccount** " angegeben haben.  

>[!NOTE]
>Wenn Sie das Dienst Konto ändern, müssen Sie die Verbund Authentifizierung manuell aktivieren, indem Sie die Windows PowerShell-Cmdlets " **Set-ADUser-compoundidentitysupported: $true** " ausführen.

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true 
```
2. Starten Sie den ADFS-Dienst neu.

>[!NOTE]
>Wenn "compoundidentitysupported" auf "true" festgelegt ist, schlägt die Installation desselben GMSA auf den neuen Servern (2012r2/2016) mit folgendem **Fehler fehl – Install-ADServiceAccount: Das Dienst Konto kann nicht installiert werden. Fehlermeldung: "Der angegebene Kontext entsprach nicht dem Ziel."** .
>
>**Lösung**: Temporäres Festlegen von compoundidentitysupported auf $false. Dieser Schritt bewirkt, dass ADFS das Ausstellen von windowsdevicegroup-Ansprüchen beendet. Set-ADServiceAccount-Identity "ADFS-Dienst Konto"-compoundidentitysupported: $false das GMSA auf dem neuen Server installieren und compoundidentitysupported wieder auf $true aktivieren.
Wenn Sie compoundidentitysupported deaktivieren und dann erneut aktivieren, muss der ADFS-Dienst nicht neu gestartet werden.

### <a name="step-7-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>Schritt 7: Aktualisieren Sie die AD FS Anspruchs Anbieter-Vertrauensstellung für Active Directory

1. Aktualisieren Sie die AD FS Anspruchs Anbieter-Vertrauensstellung für Active Directory, um die folgende "Pass-Through"-Anspruchs Regel für den Anspruch "windowsdevicegroup" einzuschließen.
2.  Klicken Sie in **AD FS Verwaltung**auf **Anspruchs Anbieter** -Vertrauens Stellungen, und klicken Sie im rechten Bereich auf **Active Directory** , und wählen Sie **Anspruchs Regeln bearbeiten**aus.
3.  Klicken Sie unter **Anspruchs Regeln für Active Directory bearbeiten** auf **Regel hinzufügen**.
4.  Wählen Sie im **Assistenten zum Hinzufügen von Transformations Anspruchs Regeln** die **Option weiterleiten oder eingehenden Anspruch Filtern** aus, und klicken Sie auf **weiter**
5.  Fügen Sie einen anzeigen Amen hinzu, und wählen Sie **Windows-Gerätegruppe** aus der Dropdown-Datei **eingehender Anspruchstyp** aus.
6.  Klicken Sie auf **Fertig stellen**.  Klicken **Sie** auf übernehmen und **OK**. 
![Anspruchs Beschreibung](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc7.png)

### <a name="step-8-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>Schritt 8: Fügen Sie auf der vertrauenden Seite, in der die "windowsdevicegroup"-Ansprüche erwartet werden, eine ähnliche "Pass-Through"-oder "Transform"-Anspruchs Regel hinzu.
2. Klicken Sie in **AD FS Verwaltung**auf Vertrauens Stellungen der vertrauenden **Seite** , und klicken Sie im rechten Bereich mit der rechten Maustaste auf Ihre RP, und wählen Sie **Anspruchs Regeln bearbeiten**aus.
3. Klicken Sie in den Ausstellungs **Transformationsregeln** auf **Regel hinzufügen**.
4. Wählen Sie im **Assistenten zum Hinzufügen von Transformations Anspruchs Regeln** die **Option weiterleiten oder eingehenden Anspruch Filtern** aus, und klicken Sie auf **weiter**
5. Fügen Sie einen anzeigen Amen hinzu, und wählen Sie **Windows-Gerätegruppe** aus der Dropdown-Datei **eingehender Anspruchstyp** aus.
6. Klicken Sie auf **Fertig stellen**.  Klicken **Sie** auf übernehmen und **OK**.
   ![Anspruchs Beschreibung](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc8.png)


## <a name="steps-for-configuring-ad-fs-in-windows-server-2016"></a>Schritte zum Konfigurieren von AD FS in Windows Server 2016
Im folgenden werden die Schritte zum Konfigurieren der Verbund Authentifizierung auf AD FS für Windows Server 2016 ausführlich erläutert.

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>Schritt 1:  Aktivieren der KDC-Unterstützung für Ansprüche, Verbund Authentifizierung und Kerberos armoring in der Standard Domänen Controller-Richtlinie
1.  Wählen Sie in Server-Manager Tools, **Gruppenrichtlinie Verwaltung**aus.
2.  Navigieren Sie zur **Standard Domänen Controller Richtlinie**, klicken Sie mit der rechten Maustaste, und wählen Sie **Bearbeiten**aus.
3.  Erweitern Sie auf der **Gruppenrichtlinienverwaltungs-Editor**unter **Computer Konfiguration**nacheinander **Richtlinien**, **Administrative Vorlagen**, **System**und **KDC**.
4.  Doppelklicken Sie im rechten Bereich auf **KDC-Unterstützung für Ansprüche, Verbund Authentifizierung und Kerberos armoring**.
5.  Legen Sie im Dialogfeld neu die Option KDC-Unterstützung für Ansprüche auf **aktiviert**fest.
6.  Wählen Sie unter Optionen die Option **unterstützt** im Dropdown Menü aus, **und klicken Sie** dann auf übernehmen und **OK**.


### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>Schritt 2: Aktivieren der Kerberos-Client Unterstützung für Ansprüche, Verbund Authentifizierung und Kerberos armoring auf Computern, die auf Verbund Anwendungen zugreifen

1.  Auf einer Gruppenrichtlinie die auf die Computer angewendet werden, die auf Verbund Anwendungen zugreifen, klicken Sie im **Gruppenrichtlinienverwaltungs-Editor**unter **Computer Konfiguration**auf **Richtlinien**, erweitern Sie **Administrative Vorlagen**und dann **System.** , und wählen Sie **Kerberos**aus.
2.  Doppelklicken Sie im rechten Fensterbereich des Fensters Gruppenrichtlinienverwaltungs-Editor auf **Kerberos-Client Unterstützung für Ansprüche, Verbund Authentifizierung und Kerberos armoring.**
3.  Legen Sie im Dialogfeld neu die Kerberos-Client Unterstützung auf **aktiviert** fest, und klicken Sie **dann** auf übernehmen und **OK**.
4.  Schließen Sie den Gruppenrichtlinienverwaltungs-Editor.

### <a name="step-3-configure-the-primary-authentication-provider"></a>Schritt 3: Konfigurieren des primären Authentifizierungs Anbieters

1. Legen Sie den primären Authentifizierungs Anbieter für AD FS Intraneteinstellungen auf **Windows-Authentifizierung** fest.
2. Wählen Sie in AD FS Verwaltung unter **Authentifizierungs Richtlinien**die Option **primäre Authentifizierung** aus, und klicken Sie unter **globale Einstellungen** auf **Bearbeiten**.
3. Wählen Sie unter **Globale Authentifizierungs Richtlinie bearbeiten** unter **Intranet** die Option **Windows-Authentifizierung**aus.
4. Klicken **Sie** auf übernehmen und **OK**.
5. Mithilfe von PowerShell können Sie das Cmdlet **Set-adfsglobalauthenticationpolicy** verwenden.

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>In einer wid-basierten Farm muss der PowerShell-Befehl auf dem primären AD FS Server ausgeführt werden.
>In einer SQL-basierten Farm kann der PowerShell-Befehl auf jedem AD FS Server ausgeführt werden, der Mitglied der Farm ist.

### <a name="step-4--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>Schritt 4:  Aktivieren Sie das Verbund Authentifizierungs Bit für das msDS-supportedencryptiontypes-Attribut.

1.  Aktivieren Sie das Verbund Authentifizierungs Bit für das msDS-supportedencryptiontypes-Attribut im Konto, das Sie zum Ausführen des AD FS Dienstanbieter mit dem PowerShell-Cmdlet " **Set-ADServiceAccount** " angegeben haben.  

>[!NOTE]
>Wenn Sie das Dienst Konto ändern, müssen Sie die Verbund Authentifizierung manuell aktivieren, indem Sie die Windows PowerShell-Cmdlets " **Set-ADUser-compoundidentitysupported: $true** " ausführen.

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true 
```
2. Starten Sie den ADFS-Dienst neu.

>[!NOTE]
>Wenn "compoundidentitysupported" auf "true" festgelegt ist, schlägt die Installation desselben GMSA auf den neuen Servern (2012r2/2016) mit folgendem **Fehler fehl – Install-ADServiceAccount: Das Dienst Konto kann nicht installiert werden. Fehlermeldung: "Der angegebene Kontext entsprach nicht dem Ziel."** .
>
>**Lösung**: Temporäres Festlegen von compoundidentitysupported auf $false. Dieser Schritt bewirkt, dass ADFS das Ausstellen von windowsdevicegroup-Ansprüchen beendet. Set-ADServiceAccount-Identity "ADFS-Dienst Konto"-compoundidentitysupported: $false das GMSA auf dem neuen Server installieren und compoundidentitysupported wieder auf $true aktivieren.
Wenn Sie compoundidentitysupported deaktivieren und dann erneut aktivieren, muss der ADFS-Dienst nicht neu gestartet werden.

### <a name="step-5-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>Schritt 5: Aktualisieren Sie die AD FS Anspruchs Anbieter-Vertrauensstellung für Active Directory

1. Aktualisieren Sie die AD FS Anspruchs Anbieter-Vertrauensstellung für Active Directory, um die folgende "Pass-Through"-Anspruchs Regel für den Anspruch "windowsdevicegroup" einzuschließen.
2.  Klicken Sie in **AD FS Verwaltung**auf **Anspruchs Anbieter** -Vertrauens Stellungen, und klicken Sie im rechten Bereich auf **Active Directory** , und wählen Sie **Anspruchs Regeln bearbeiten**aus.
3.  Klicken Sie unter **Anspruchs Regeln für Active Directory bearbeiten** auf **Regel hinzufügen**.
4.  Wählen Sie im **Assistenten zum Hinzufügen von Transformations Anspruchs Regeln** die **Option weiterleiten oder eingehenden Anspruch Filtern** aus, und klicken Sie auf **weiter**
5.  Fügen Sie einen anzeigen Amen hinzu, und wählen Sie **Windows-Gerätegruppe** aus der Dropdown-Datei **eingehender Anspruchstyp** aus.
6.  Klicken Sie auf **Fertig stellen**.  Klicken **Sie** auf übernehmen und **OK**. 


### <a name="step-6-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>Schritt 6: Fügen Sie auf der vertrauenden Seite, in der die "windowsdevicegroup"-Ansprüche erwartet werden, eine ähnliche "Pass-Through"-oder "Transform"-Anspruchs Regel hinzu.
2. Klicken Sie in **AD FS Verwaltung**auf Vertrauens Stellungen der vertrauenden **Seite** , und klicken Sie im rechten Bereich mit der rechten Maustaste auf Ihre RP, und wählen Sie **Anspruchs Regeln bearbeiten**aus.
3. Klicken Sie in den Ausstellungs **Transformationsregeln** auf **Regel hinzufügen**.
4. Wählen Sie im **Assistenten zum Hinzufügen von Transformations Anspruchs Regeln** die **Option weiterleiten oder eingehenden Anspruch Filtern** aus, und klicken Sie auf **weiter**
5. Fügen Sie einen anzeigen Amen hinzu, und wählen Sie **Windows-Gerätegruppe** aus der Dropdown-Datei **eingehender Anspruchstyp** aus.
6. Klicken Sie auf **Fertig stellen**.  Klicken **Sie** auf übernehmen und **OK**.

## <a name="validation"></a>Validierung
Erstellen Sie zum Überprüfen der Veröffentlichung von "windowsdevicegroup"-Ansprüchen mithilfe von .NET 4,6 eine Anwendung zum Testen von Ansprüchen. Mit WIF SDK 4,0.
Konfigurieren Sie die Anwendung als vertrauende Seite in AD FS, und aktualisieren Sie Sie mit der Anspruchs Regel, wie in den obigen Schritten angegeben.
Bei der Authentifizierung bei der Anwendung mit dem integrierten Windows-Authentifizierungs Anbieter von ADFS werden die folgenden Ansprüche eingefügt.
![Validierungs](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc9.png)

Die Ansprüche für den Computer/das Gerät können jetzt für umfassendere Zugriffs Steuerungen genutzt werden.

Beispielsweise weist die folgenden **additionalauthenticationrules** AD FS an, MFA aufzurufen, wenn – der authentifizier Ende Benutzer nicht Mitglied der Sicherheitsgruppe "-1-5-21-2134745077-1211275016-3050530490-1117" und des Computers ist (wobei der Benutzer ist Die Authentifizierung von) ist nicht Mitglied der Sicherheitsgruppe "S-1-5-21-2134745077-1211275016-3050530490-1115 (windowsdevicegroup)".

Wenn jedoch eine der oben genannten Bedingungen erfüllt ist, sollten Sie MFA nicht aufrufen.

```
'NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1115"])
&& NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1117"])
=> issue(Type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", Value = "https://schemas.microsoft.com/claims/multipleauthn");'
```
