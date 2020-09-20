---
ms.assetid: 35de490f-c506-4b73-840c-b239b72decc2
title: Konfigurieren des gerätebasierten bedingten lokalen Zugriffs
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/11/2017
ms.topic: article
ms.openlocfilehash: 2306c5ad57b7714c10076a5bb11f6cae5bb7f92d
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766883"
---
# <a name="configure-on-premises-conditional-access-using-registered-devices"></a>Konfigurieren des lokalen bedingten Zugriffs mithilfe registrierter Geräte


Das folgende Dokument führt Sie durch die Installation und Konfiguration des lokalen bedingten Zugriffs mit registrierten Geräten.

![Bedingter Zugriff](media/Using-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)

## <a name="infrastructure-pre-requisites"></a>Voraussetzungen für die Infrastruktur
Die folgenden erforderlichen Komponenten sind erforderlich, bevor Sie mit dem lokalen bedingten Zugriff beginnen können.

|Anforderung|BESCHREIBUNG
|-----|-----
|Ein Azure AD-Abonnement mit Azure AD Premium | [Eine kostenlose Testversion ist in Ordnung](https://azure.microsoft.com/trial/get-started-active-directory/) , um das Zurückschreiben von Geräten für den lokalen bedingten Zugriff zu aktivieren.
|Intune-Abonnement|nur erforderlich für die MDM-Integration für Geräte Kompatibilitäts Szenarien:[eine kostenlose Testversion ist in Ordnung](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0) .
|Azure AD Connect|QFE vom November 2015 oder höher.  Holen Sie sich [hier](https://www.microsoft.com/download/details.aspx?id=47594)die neueste Version.
|Windows Server 2016|Build 10586 oder neuer für AD FS
|Windows Server 2016-Active Directory Schema|Die Schema Ebene 85 oder höher ist erforderlich.
|Windows Server 2016-Domänen Controller|Dies ist nur für die Bereitstellung von Hello for Business-Vertrauens Stellungen erforderlich.  Weitere Informationen finden Sie [hier](/windows/security/identity-protection/hello-for-business/hello-identity-verification).
|Windows 10-Client|Build 10586 oder höher, der mit der obigen Domäne verknüpft ist, ist nur für Windows 10-Domänen Beitritt und Microsoft Passport for Work Szenarios erforderlich.
|Azure AD Benutzerkonto mit zugewiesener Azure AD Premium-Lizenz|Zum Registrieren des Geräts



## <a name="upgrade-your-active-directory-schema"></a>Aktualisieren Ihres Active Directory Schemas
Um den lokalen bedingten Zugriff mit registrierten Geräten zu verwenden, müssen Sie zuerst Ihr AD-Schema aktualisieren.  Die folgenden Bedingungen müssen erfüllt sein:
    - Das Schema muss die Version 85 oder höher aufweisen.
    - Dies ist nur für die Gesamtstruktur erforderlich, der AD FS hinzugefügt wurde.

> [!NOTE]
> Wenn Sie Azure AD Connect vor dem Upgrade auf die Schema Version (Stufe 85 oder höher) in Windows Server 2016 installiert haben, müssen Sie die Azure AD Connect Installation erneut ausführen und das lokale AD-Schema aktualisieren, um sicherzustellen, dass die Synchronisierungs Regel für MSDS-keykredentiallink konfiguriert ist.

### <a name="verify-your-schema-level"></a>Überprüfen der Schema Ebene
Gehen Sie folgendermaßen vor, um die Schema Ebene zu überprüfen:

1.  Sie können ADSIEdit oder LDP verwenden und eine Verbindung mit dem Schema namens Kontext herstellen.
2.  Klicken Sie mit ADSIEdit mit der rechten Maustaste auf "CN = Schema, CN = Configuration, DC = <domain> , DC =", <com> und wählen Sie Eigenschaften aus.  Die Domäne und die com-Teile mit den Gesamtstruktur Informationen.
3.  Suchen Sie im Attribut-Editor nach dem objectVersion-Attribut, und geben Sie Ihnen Ihre Version.

![ADSI-Editor](media/Configure-Device-Based-Conditional-Access-on-Premises/adsiedit.png)

Sie können auch das folgende PowerShell-Cmdlet verwenden (ersetzen Sie das-Objekt durch ihre Schema-namens Kontextinformationen):

``` powershell
Get-ADObject "cn=schema,cn=configuration,dc=domain,dc=local" -Property objectVersion

```

![PowerShell](media/Configure-Device-Based-Conditional-Access-on-Premises/pshell1.png)

Weitere Informationen zum Upgrade von finden [Sie unter Aktualisieren von Domänen Controllern auf Windows Server 2016](../../ad-ds/deploy/upgrade-domain-controllers.md).

## <a name="enable-azure-ad-device-registration"></a>Aktivieren von Azure AD Device Registration
Zum Konfigurieren dieses Szenarios müssen Sie die Geräte Registrierungsfunktion in Azure AD konfigurieren.

Befolgen Sie hierzu die Schritte unter Einrichten von [Azure AD beitreten in Ihrer Organisation](/azure/active-directory/devices/device-management-azure-portal) .

## <a name="setup-ad-fs"></a>Setup-AD FS
1. Erstellen Sie eine [neue AD FS 2016-Farm](../deployment/deploying-a-federation-server-farm.md).
2.  Oder [Migrieren](../deployment/upgrading-to-ad-fs-in-windows-server.md) einer Farm zu AD FS 2016 von AD FS 2012 R2
4. Stellen Sie [Azure AD Connect](../deployment/upgrading-to-ad-fs-in-windows-server.md) mithilfe des benutzerdefinierten Pfads bereit, um AD FS mit Azure AD zu verbinden.

## <a name="configure-device-write-back-and-device-authentication"></a>Konfigurieren von Geräte Rückschreiben und Geräte Authentifizierung
> [!NOTE]
> Wenn Sie Azure AD Connect mit Express-Einstellungen ausgeführt haben, wurden die richtigen AD-Objekte für Sie erstellt.  In den meisten AD FS Szenarien wurde Azure AD Connect jedoch mit benutzerdefinierten Einstellungen ausgeführt, um AD FS zu konfigurieren, sodass die folgenden Schritte erforderlich sind.

### <a name="create-ad-objects-for-ad-fs-device-authentication"></a>Erstellen von AD-Objekten für die AD FS Geräte Authentifizierung
Wenn Ihre AD FS-Farm noch nicht für die Geräte Authentifizierung konfiguriert ist (Dies wird in der AD FS Management Console unter Dienst-> Geräteregistrierung angezeigt), führen Sie die folgenden Schritte aus, um die richtigen AD DS Objekte und die Konfiguration zu erstellen.

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device1.png)

>Hinweis: für die unten aufgeführten Befehle sind Active Directory Verwaltungs Tools erforderlich. wenn der Verbund Server nicht auch ein Domänen Controller ist, installieren Sie zunächst die Tools mithilfe von Schritt 1.  Andernfalls können Sie Schritt 1 überspringen.

1.  Führen Sie den Assistenten zum **Hinzufügen von Rollen & Features** aus, und wählen Sie Features **Remoteserver-Verwaltungstools**  ->  **Rollen Verwaltungs Tools**  ->  **AD DS und AD LDS Tools** -> wählen Sie sowohl das **Active Directory-Modul für Windows PowerShell** als auch die **AD DS Tools**aus.

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device2.png)

2. Stellen Sie sicher, dass Sie auf dem primären Server AD FS als AD DS Benutzer mit Enterprise admin-Berechtigungen (EA) angemeldet sind, und öffnen Sie eine PowerShell-Eingabeaufforderung mit erhöhten Rechten.  Führen Sie anschließend die folgenden PowerShell-Befehle aus:

   `Import-module activedirectory`
   `PS C:\> Initialize-ADDeviceRegistration -ServiceAccountName "<your service account>" `
3. Öffnen Sie im Popup Fenster ja.

>Hinweis: Wenn Ihr AD FS Dienst für die Verwendung eines GMSA-Kontos konfiguriert ist, geben Sie den Kontonamen im Format "Domäne \ Accountname $" ein.

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device3.png)

Mit dem obigen PSH werden die folgenden Objekte erstellt:


- Registereddevices-Container unter der AD-Domänen Partition
- Geräte Registrierungsdienst-Container und-Objekt unter Konfiguration--> Services--> Geräte Registrierungs Konfiguration
- Geräte Registrierungsdienst-DKM-Container und-Objekt unter Konfiguration--> Services--> Geräte Registrierungs Konfiguration

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device4.png)

4. Nachdem dies geschehen ist, wird eine erfolgreiche Abschluss Meldung angezeigt.

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device5.png)

###        <a name="create-service-connection-point-scp-in-ad"></a>Erstellen eines Dienst Verbindungs Punkts (Service Connection Point, SCP) in AD
Wenn Sie beabsichtigen, den Windows 10-Domänen Beitritt (mit automatischer Registrierung bei Azure AD) wie hier beschrieben zu verwenden, führen Sie die folgenden Befehle aus, um einen Dienst Verbindungspunkt in zu erstellen AD DS
1.  Öffnen Sie Windows PowerShell, und führen Sie Folgendes aus:

    `PS C:>Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1" `

>Hinweis: Kopieren Sie ggf. die Datei "adsyncprep. psm1" vom Azure AD Connect Server.  Diese Datei befindet sich im Verzeichnis "Programme\Microsoft Azure Active Directory connect\adprep".

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device6.png)

2. Geben Sie Ihre Azure AD globalen Administrator Anmelde Informationen an.

    `PS C:>$aadAdminCred = Get-Credential`

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device7.png)

3. Führen Sie den folgenden PowerShell-Befehl aus:

   `PS C:>Initialize-ADSyncDomainJoinedComputerSync -AdConnectorAccount [AD connector account name] -AzureADCredentials $aadAdminCred `

Dabei ist der [AD Connector Account Name] der Name des Kontos, das Sie in Azure AD Connect beim Hinzufügen Ihres lokalen AD DS Verzeichnisses konfiguriert haben.

Mit den obigen Befehlen können Windows 10-Clients die richtige Azure AD Domäne zum beitreten suchen, indem Sie das serviceConnectionPoint-Objekt in AD DS erstellen.

### <a name="prepare-ad-for-device-write-back"></a>Vorbereiten von AD für das Zurückschreiben von Geräten
Führen Sie die folgenden Schritte aus, um sicherzustellen, dass sich AD DS Objekte und Container im richtigen Zustand für das Zurückschreiben von Geräten aus Azure AD befinden.

1.  Öffnen Sie Windows PowerShell, und führen Sie Folgendes aus:

    `PS C:>Initialize-ADSyncDeviceWriteBack -DomainName <AD DS domain name> -AdConnectorAccount [AD connector account name] `

Dabei ist [AD Connector Account Name] der Name des Kontos, das Sie in Azure AD Connect beim Hinzufügen Ihres lokalen AD DS Verzeichnisses im Format Domäne \ Accountname konfiguriert haben.

Mit dem obigen Befehl werden die folgenden Objekte für das Zurückschreiben von Geräten in AD DS erstellt, sofern Sie noch nicht vorhanden sind, und der Zugriff auf den angegebenen AD Connector-Kontonamen wird ermöglicht.

- Registereddevices-Container in der AD-Domänen Partition
- Geräte Registrierungsdienst-Container und-Objekt unter Konfiguration--> Services--> Geräte Registrierungs Konfiguration

### <a name="enable-device-write-back-in-azure-ad-connect"></a>Aktivieren des Geräte Rückschreibens in Azure AD Connect
Wenn Sie dies noch nicht getan haben, aktivieren Sie das Zurückschreiben von Geräten in Azure AD Connect, indem Sie den Assistenten ein zweites Mal ausführen und **"Synchronisierungs Optionen anpassen"** auswählen, das Kontrollkästchen für das Zurückschreiben von Geräten aktivieren und die Gesamtstruktur auswählen, in der Sie die obigen Cmdlets ausgeführt haben.

### <a name="configure-device-authentication-in-ad-fs"></a>Konfigurieren der Geräte Authentifizierung in AD FS
Konfigurieren Sie mithilfe eines PowerShell-Befehls Fensters mit erhöhten Rechten AD FS Richtlinie, indem Sie den folgenden Befehl ausführen:

`PS C:>Set-AdfsGlobalAuthenticationPolicy -DeviceAuthenticationEnabled $true -DeviceAuthenticationMethod All`

### <a name="check-your-configuration"></a>Überprüfen Ihrer Konfiguration
Im folgenden finden Sie eine umfassende Liste der AD DS Geräte, Container und Berechtigungen, die für das Zurückschreiben von Geräten und die Authentifizierung erforderlich sind.



- Objekt vom Typ ms-DS-devicecontainer bei CN = registereddevices, DC = &lt; Domäne&gt;
    - Lesezugriff auf das AD FS-Dienst Konto
    - Lese-/Schreibzugriff auf das AD-Connector-Konto für Azure AD Connect Sync</br></br>

- Container CN = Geräte Registrierungs Konfiguration, CN = Services, CN = Configuration, DC = &lt; Domäne&gt;
- Container Device Registration Service DKM unter dem obigen Container

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device8.png)



- Objekt vom Typ serviceConnectionPoint bei CN = &lt; GUID &gt; , CN = Geräteregistrierung

- Konfiguration, CN = Services, CN = Configuration, DC = &lt; Domäne&gt;
  - Lese-/Schreibzugriff auf den angegebenen AD Connector-Kontonamen für das neue Objekt</br></br>


- Objekttyp MSDS-deviceregistrationservicecontainer at CN = Device Registration Services, CN = Device Registration Configuration, CN = Services, CN = Configuration, DC =&ltdomain>


- Objekt vom Typ "msDS-deviceregistrationservice" im obigen Container

### <a name="see-it-work"></a>Siehe it work
Wenn Sie die neuen Ansprüche und Richtlinien auswerten möchten, registrieren Sie zunächst ein Gerät.  Beispielsweise können Sie mit der App "Einstellungen" unter "System->" einen Windows 10-Computer verknüpfen Azure AD oder den Windows 10-Domänen Beitritt mithilfe der automatischen Geräteregistrierung einrichten, indem Sie die folgenden [zusätzlichen Schritte ausführen](/azure/active-directory/devices/hybrid-azuread-join-plan).  Informationen zum beitreten zu Windows 10 Mobile-Geräten finden Sie in [diesem Dokument.](/windows/client-management/join-windows-10-mobile-to-azure-active-directory)

Melden Sie sich für die einfachste Auswertung bei AD FS mithilfe einer Testanwendung an, in der eine Liste mit Ansprüchen angezeigt wird. Sie können neue Ansprüche wie IsManaged, iscompliance und TrustType sehen.  Wenn Sie Microsoft Passport for Work aktivieren, wird auch der PRT-Anspruch angezeigt.


## <a name="configure-additional-scenarios"></a>Konfigurieren zusätzlicher Szenarien
### <a name="automatic-registration-for-windows-10-domain-joined-computers"></a>Automatische Registrierung für in eine Domäne eingebundener Windows 10
Um die automatische Geräteregistrierung für in eine Domäne eingebundener Windows 10-Computer zu aktivieren, führen Sie die Schritte 1 und 2 [hier](/azure/active-directory/devices/hybrid-azuread-join-plan)
Dies hilft Ihnen dabei, Folgendes zu erreichen:

1. Stellen Sie sicher, dass Ihr Dienst Verbindungspunkt in AD DS vorhanden ist und über die entsprechenden Berechtigungen verfügt (wir haben dieses Objekt oben erstellt, aber die doppelte Prüfung wird nicht beeinträchtigt).
2. Sicherstellen, dass AD FS richtig konfiguriert ist
3. Stellen Sie sicher, dass im AD FS System die richtigen Endpunkte aktiviert und die Anspruchs Regeln konfiguriert sind.
4. Konfigurieren der für die automatische Geräteregistrierung von in die Domäne eingebundener Computer erforderlichen Gruppenrichtlinien Einstellungen

### <a name="microsoft-passport-for-work"></a>Microsoft Passport for Work
Informationen zum Aktivieren von Windows 10 mit Microsoft Passport for Work finden [Sie unter Aktivieren von Microsoft Passport for Work in Ihrer Organisation.](/windows/security/identity-protection/hello-for-business/hello-identity-verification)

### <a name="automatic-mdm-enrollment"></a>Automatische MDM-Registrierung
Um die automatische MDM-Registrierung registrierter Geräte so zu aktivieren, dass Sie den iscompliance-Anspruch in ihrer Zugriffs Steuerungs Richtlinie verwenden können, führen Sie die hier beschriebenen Schritte aus [.](/windows/client-management/join-windows-10-mobile-to-azure-active-directory)

## <a name="troubleshooting"></a>Problembehandlung
1.  Wenn Sie eine Fehlermeldung erhalten, `Initialize-ADDeviceRegistration` die sich über ein bereits im falschen Zustand vorhandenes Objekt beschwert (z. b. "das DRS-Dienst Objekt wurde ohne alle erforderlichen Attribute gefunden"), haben Sie möglicherweise zuvor Azure AD Connect PowerShell-Befehle ausgeführt und verfügen über eine partielle Konfiguration in AD DS.  Versuchen Sie, die Objekte unter " **CN = Device Registration Configuration, CN = Services, CN = Configuration, DC &lt; = &gt; Domain** " manuell zu löschen, und versuchen Sie es noch mal.
2.  Für mit der Domäne verbundene Windows 10-Clients
    1. Um zu überprüfen, ob die Geräte Authentifizierung funktioniert, melden Sie sich beim in die Domäne eingebundener Client als Test Benutzerkonto an. Zum schnellen lösen der Bereitstellung Sperren und Entsperren Sie den Desktop mindestens einmal.
    2. Anweisungen zum Überprüfen des Links "generiertes-Schlüssel Anmelde Informationen" auf AD DS Objekt (Synchronisierung muss immer noch zweimal ausgeführt werden?)
3.  Wenn beim Registrieren eines Windows-Computers eine Fehlermeldung angezeigt wird, dass das Gerät bereits registriert war, Sie aber die Registrierung des Geräts nicht bereits aufgehoben haben, ist möglicherweise ein Fragment der Konfiguration der Geräteregistrierung in der Registrierung vorhanden.  Um dies zu untersuchen und zu entfernen, führen Sie die folgenden Schritte aus:
    1. Öffnen Sie auf dem Windows-Computer regedit, und navigieren Sie zu **hklm\software\microsoft\registrierungen** .
    2. Unter diesem Schlüssel werden viele Unterschlüssel im GUID-Formular angezeigt.  Navigieren Sie zu dem Unterschlüssel mit ungefähr 17 Werten, und weisen Sie "registrimenttype" von "6" [MDM-Einbindung] oder "13" (Azure AD verknüpft) auf.
    3. Ändern von **anmelmenttype** in **0**
    4. Geräteregistrierung oder Registrierung erneut versuchen

### <a name="related-articles"></a>Verwandte Artikel
* [Sichern des Zugriffs auf Office 365 und andere mit Azure Active Directory verbundene Apps](/azure/active-directory/conditional-access/overview)
* [Geräterichtlinien für den bedingten Zugriff auf Office 365-Dienste](/azure/active-directory/conditional-access/overview)
* [Einrichten des lokalen bedingten Zugriffs mit Azure Active Directory Device Registration](/azure/active-directory/active-directory-device-registration-on-premises-setup)
* [Benutzererfahrungen beim Verknüpfen von in die Domäne eingebundenen Windows 10-Geräten mit Azure AD](/azure/active-directory/devices/hybrid-azuread-join-plan)