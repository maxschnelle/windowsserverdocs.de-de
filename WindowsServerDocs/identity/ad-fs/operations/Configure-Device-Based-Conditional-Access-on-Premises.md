---
ms.assetid: 35de490f-c506-4b73-840c-b239b72decc2
title: Konfigurieren des gerätebasierten bedingten lokalen Zugriffs
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/11/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: bcb6c415aae33b9742d7a7080ec169ca947098b9
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445000"
---
# <a name="configure-on-premises-conditional-access-using-registered-devices"></a>Konfigurieren auf den lokalen bedingten Zugriffs mithilfe der registrierten Geräte


Das folgende Dokument führt Sie durch das Installieren und Konfigurieren des lokalen bedingten Zugriffs mit registrierten Geräten.

![Für den bedingten Zugriff](media/Using-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  

## <a name="infrastructure-pre-requisites"></a>Infrastruktur-Voraussetzungen
Die folgenden erforderlichen sind erforderlich, bevor Sie mit dem bedingten Zugriff auf lokale beginnen können. 

|Anforderung|Beschreibung
|-----|-----
|Ein Azure AD-Abonnement mit Azure AD Premium | Gerät Schreibvorgang zurück zum bedingten Zugriff für lokale - aktivieren [eine kostenlose Testversion ist in Ordnung](https://azure.microsoft.com/trial/get-started-active-directory/)  
|Intune-Abonnement|nur erforderlich, für die Integration der Verwaltung mobiler Geräte für Geräte die Einhaltung von Vorschriften -[eine kostenlose Testversion ist in Ordnung](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0)
|Azure AD Connect|November 2015 QFE oder höher.  Abrufen der neuesten Version [hier](https://www.microsoft.com/en-us/download/details.aspx?id=47594).  
|Windows Server 2016|Build 10586 oder höher für AD FS  
|Windows Server 2016 Active Directory-schema|Schemaebene 85 oder höher ist erforderlich.
|Windows Server 2016-Domänencontroller|Dies ist nur für Hello For Business-Key-Trust-Bereitstellungen erforderlich.  Weitere Informationen finden Sie unter [hier](https://aka.ms/whfbdocs).  
|Windows 10-client|Build 10586 oder neueren, mit der oben genannten Domäne verknüpften erforderlich für Windows 10-Domäne beitreten und Microsoft Passport Arbeit nur für Szenarios  
|Azure AD-Benutzerkonto mit Azure AD Premium-Lizenz zugewiesen|Für die Registrierung des Geräts  


 
## <a name="upgrade-your-active-directory-schema"></a>Aktualisieren Sie Ihre Active Directory-Schema
Um den lokalen bedingten Zugriffs mit registrierten Geräten verwenden, müssen Sie zunächst Ihre Active Directory-Schema aktualisieren.  Die folgenden Bedingungen müssen erfüllt sein:
    - Das Schema sollte Version 85 oder höher sein.
    - Dies ist nur erforderlich, für die Gesamtstruktur, die mit AD FS verbunden ist

> [!NOTE]
> Wenn Sie Azure AD Connect vor dem Upgrade auf die Schemaversion (Level 85 oder höher) in Windows Server 2016 installiert haben, müssen Sie benötigen, führen Sie die Azure AD Connect-Installation erneut aus, und aktualisieren Sie das lokale Active Directory-Schema, um sicherzustellen, dass die Synchronisierungsregel für MsDS-KeyCredentialLink konfiguriert ist.

### <a name="verify-your-schema-level"></a>Überprüfen Sie Ihre Schemaebene
Um Ihre Schemaebene zu überprüfen, führen Sie folgende Schritte aus:

1.  Sie können verwenden Sie ADSIEdit oder "Ldp" und der Schema-Namenskontext verbinden.  
2.  Verwenden ADSIEdit, mit der rechten Maustaste auf "CN = Schema, CN = Configuration, DC =<domain>, DC =<com> , und wählen Sie Eigenschaften.  Relpace-Domäne und die COM-Teile mit Ihren Gesamtstrukturinformationen.
3.  Unter der Attribut-Editor, suchen Sie das Attribut ObjectVersion und teilt es Ihnen, Ihre Version.  

![ADSI-Editor](media/Configure-Device-Based-Conditional-Access-on-Premises/adsiedit.png)  

Sie können auch das folgende PowerShell-Cmdlet (ersetzen Sie das Objekt mit Ihrem Schema, das Benennen von Kontextinformationen) verwenden:

``` powershell
Get-ADObject "cn=schema,cn=configuration,dc=domain,dc=local" -Property objectVersion
    
```

![PowerShell](media/Configure-Device-Based-Conditional-Access-on-Premises/pshell1.png) 

Weitere Informationen zum Upgrade finden Sie unter [Aktualisieren von Domänencontrollern auf Windows Server 2016](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2016.md). 

## <a name="enable-azure-ad-device-registration"></a>Aktivieren von Azure AD-Geräteregistrierung  
Um dieses Szenario zu konfigurieren, müssen Sie die Gerätefunktion für die Registrierung in Azure AD konfigurieren.  

Zu diesem Zweck die Schritte unter [Einrichten von Azure AD Join in Ihrer Organisation](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-setup/)  

## <a name="setup-ad-fs"></a>Einrichten von AD FS  
1. Erstellen Sie die einem [neue AD FS 2016-Farm](https://technet.microsoft.com/library/dn486775.aspx).   
2.  Oder [migrieren](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md) einer Farm mit AD FS 2016 von AD FS 2012 R2  
4. Bereitstellen von [Azure AD Connect](https://azure.microsoft.com/documentation/articles/active-directory-aadconnectfed-whatis/) mit, dass der Pfad der benutzerdefinierten AD FS mit Azure AD verbinden.  

## <a name="configure-device-write-back-and-device-authentication"></a>Konfigurieren von Gerät schreiben zurück und Geräteauthentifizierung  
> [!NOTE]
> Wenn Sie Azure AD Connect mit Expresseinstellungen ausgeführt haben, haben die richtigen AD-Objekte für Sie erstellt wurde.  Jedoch in den meisten Szenarien für AD FS, Azure AD Connect ausgeführt wurde mit benutzerdefinierten Einstellungen zum Konfigurieren von AD FS, sodass die unten aufgeführten Schritte sind erforderlich.  

### <a name="create-ad-objects-for-ad-fs-device-authentication"></a>Erstellen von AD-Objekten für die AD FS-Gerätauthentifizierung  
Sollte die AD FS-Farm noch nicht für die Geräteauthentifizierung konfiguriert sein (was Sie in der AD FS-Verwaltungskonsole unter Dienste > Geräteregistrierung prüfen können), erstellen Sie die richtigen AD DS-Objekte und Konfigurationen mithilfe der folgenden Schritte.  

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device1.png)

>Hinweis: Die folgenden Befehle erfordern Active Directory-Verwaltungstools. Ist Ihr Verbundserver nicht auch ein Domänencontroller, müssen Sie zunächst die Tools installieren, wie unten in Schritt 1 angegeben.  Andernfalls können Sie Schritt 1 überspringen.  

1.  Führen Sie den Assistenten **Hinzufügen von Rollen und Features** aus, und wählen Sie **Remoteserver-Verwaltungstools** -> **Rollenverwaltungstools** -> **AD DS und AD LDS-Tools** -> Wählen Sie sowohl **Active Directory-Modul für Windows PowerShell** als auch **AD DS-Tools**.

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device2.png)
  
2. Stellen Sie sicher auf dem primären AD FS-Server Sie sind angemeldet als AD DS-Benutzer mit Berechtigungen für Enterprise Administrator (EA), und öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten Powershell.  Führen Sie dann die folgenden PowerShell-Befehle aus:  
    
   `Import-module activedirectory`  
   `PS C:\> Initialize-ADDeviceRegistration -ServiceAccountName "<your service account>" ` 
3. Drücken im Popupfenster "Ja" aus.

>Hinweis: Wenn Ihr AD FS-Dienst ein GMSA-Konto verwenden kann, geben Sie den Kontonamen im Format „Domäne\Kontoname$” ein.

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device3.png)  

Die obigen PSH-Befehle erstellen folgende Objekte:  


- RegisteredDevices-Container in der AD-Domänenpartition  
- Device Registration Service-Container und Objekte unter Konfiguration --> Dienste--> Geräteregistrierungskonfiguration  
- Device Registration Service Container DKM-Container und Objekte unter Konfiguration --> Dienste--> Geräteregistrierungskonfiguration  

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device4.png)  

4. Anschließend wird eine Meldung über den erfolgreichen Abschluss angezeigt.

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device5.png) 

###        <a name="create-service-connection-point-scp-in-ad"></a>Erstellen der Dienstverbindungspunkt (SCP) in AD  
Wenn Sie den Windows 10-Domänenbeitritt (mit automatischer Registrierung bei Azure AD) wie hier beschrieben verwenden möchten, führen Sie die folgenden Befehle zum Erstellen eines Dienstverbindungspunkts in AD DS aus:  
1.  Öffnen Sie Windows PowerShell, und führen Sie Folgendes aus:
    
    `PS C:>Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1" ` 

>Hinweis: bei Bedarf kopieren Sie die AdSyncPrep.psm1-Datei von Ihrem Azure AD Connect-Server.  Sie finden diese Datei unter Programme\Microsoft Azure Active Directory Connect\AdPrep.

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device6.png)   

2. Bereitstellen der Azure AD-Anmeldedaten eines globalen Administrators  

    `PS C:>$aadAdminCred = Get-Credential`

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device7.png) 

3. Führen Sie folgenden PowerShell-Befehl aus: 

   `PS C:>Initialize-ADSyncDomainJoinedComputerSync -AdConnectorAccount [AD connector account name] -AzureADCredentials $aadAdminCred ` 

[AD connector account name] steht für den Namen des Kontos, das Sie in Azure AD Connect beim Hinzufügen der lokales AD DS-Verzeichnisses konfiguriert haben.
  
Die oben aufgeführten Befehle erstellen das Objekt serviceConnectionpoint in AD DS und ermöglichen es damit den Windows 10-Clients, die ihnen zugeordnete Azure AD-Domäne zu finden.  

### <a name="prepare-ad-for-device-write-back"></a>Vorbereiten von AD für Geräterückschreibung   
Führen Sie folgende Schritte aus, um sicherzustellen, dass sich AD DS-Objekte und Container im richtigen Zustand für die Geräterückschreibung aus Azure AD befinden.

1.  Öffnen Sie Windows PowerShell, und führen Sie Folgendes aus:  

    `PS C:>Initialize-ADSyncDeviceWriteBack -DomainName <AD DS domain name> -AdConnectorAccount [AD connector account name] ` 

[AD connector account name] steht für den Namen des Kontos, das Sie in Azure AD Connect beim Hinzufügen der lokales AD DS-Verzeichnisses im Format Domäne\Kontoname konfiguriert haben.  

Der obige Befehl erstellt die folgenden Objekte zum Geräterückschreiben in AD DS, sofern sie nicht bereits vorhanden sind, und ermöglicht den Zugriff auf den angegebenen Kontonamen für den AD-Connector:  

- RegisteredDevices-Container in der AD-Domänenpartition  
- Device Registration Service-Container und Objekte unter Konfiguration --> Dienste--> Geräteregistrierungskonfiguration  

### <a name="enable-device-write-back-in-azure-ad-connect"></a>Aktivieren der Geräterückschreibung in Azure AD Connect  
Aktivieren Sie die Geräterückschreibung in Azure AD Connect (sofern sie nicht bereits aktiviert ist), indem Sie den Assistenten ein zweites Mal ausführen und **Synchronisierungsoptionen anpassen** wählen. Dann aktivieren Sie das Kontrollkästchen für die Geräterückschreibung und wählen die Gesamtstruktur, in der Sie die oben genannten Cmdlets ausgeführt haben.  

### <a name="configure-device-authentication-in-ad-fs"></a>Konfigurieren der Geräteauthentifizierung in AD FS  
Konfigurieren Sie eine AD FS-Richtlinie in einem PowerShell-Befehlsfenster mit erweiterten Rechten durch folgenden Befehl:  

`PS C:>Set-AdfsGlobalAuthenticationPolicy -DeviceAuthenticationEnabled $true -DeviceAuthenticationMethod All` 

### <a name="check-your-configuration"></a>Überprüfen der Konfiguration  
Als Referenz sind in der nachstehenden umfassenden Liste AD DS-Geräte, Container und Berechtigungen aufgeführt, die zur Authentifizierung und Geräterückschreibung erforderlich sind.
 


- Objekt vom Typ ms-DS-DeviceContainer für CN=RegisteredDevices,DC=&lt;domain&gt;        
    - Lesezugriff auf das AD FS-Dienstkonto   
    - Lese- und Schreibzugriff auf das Synchronisierung-AD-Konnektorkonto von Azure AD Connect</br></br>

- Container CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=&lt;domain&gt;  
- Container Device Registration Service DKM unter dem obigen Container

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device8.png) 
 


- Objekt vom Typ serviceConnectionpoint für CN =&lt;guid&gt;, CN = Device Registration

- Configuration,CN=Services,CN=Configuration,DC=&lt;domain&gt;  
  - Lese- und Schreibzugriff auf den angegebenen AD-Konnektorkontonamen für das neue Objekt</br></br> 


- object of type msDS-DeviceRegistrationServiceContainer at CN=Device Registration Services,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=&ltdomain>  


- Objekt vom Typ msDS-DeviceRegistrationService im obigen Container  

### <a name="see-it-work"></a>Sehen Sie die Funktionsweise  
Um die neue Ansprüche und Richtlinien auszuwerten, müssen Sie zuerst registrieren Sie ein Gerät.  Z. B. können Sie Azure AD Join zu ein Windows 10-Computer mithilfe der Einstellungen-app unter System ->, oder Sie können Windows 10-Domänenbeitritt einrichten, bei der automatischen geräteregistrierung die zusätzlichen Schritte [hier](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/).  Informationen zum Verknüpfen von Windows 10 mobile Geräte finden Sie im Dokument [hier](https://technet.microsoft.com/itpro/windows/manage/join-windows-10-mobile-to-azure-active-directory).  

Für die Evaluierung der einfachste melden Sie sich bei AD FS mit einer testanwendung, die eine Liste von Ansprüchen angezeigt wird. Sie werden damit neue Ansprüche wie z.B. IsManaged IsCompliant und Trusttype sichtbar.  Wenn Sie für die Arbeit Microsoft Passport aktivieren, sehen Sie auch den Anspruch Prt.  
 

## <a name="configure-additional-scenarios"></a>Konfigurieren Sie zusätzliche Szenarien  
### <a name="automatic-registration-for-windows-10-domain-joined-computers"></a>Automatische Registrierung für Windows 10 Domäne eingebundenen Computern  
Aktivieren der automatischen geräteregistrierung für Windows 10-Domäne eingebundenen Computer, führen Sie die Schritte 1 und 2 [hier](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/).   
Dies hilft Ihnen Folgendes:  

1. Sicherzustellen, dass Ihr Dienstverbindungspunkt im AD DS vorhanden ist und über die richtigen Berechtigungen verfügt (wir diese oben stehendes Objekt erstellt, aber es ist nicht Schaden überprüfen).  
2. Stellen Sie sicher, dass AD FS ordnungsgemäß konfiguriert ist  
3. Stellen Sie sicher, dass Ihre AD FS-System die korrekten Endpunkte aktiviert ist und von Anspruchsregeln konfiguriert   
4. Konfigurieren Sie die gruppenrichtlinieneinstellungen für die automatische geräteregistrierung von in Domänen eingebundene Computer erforderlich sind   

### <a name="microsoft-passport-for-work"></a>Microsoft Passport for Work   
Weitere Informationen zum Aktivieren von Windows 10 in Microsoft Passport for Work, finden Sie unter [Microsoft Passport for Work in Ihrer Organisation aktivieren.](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)  

### <a name="automatic-mdm-enrollment"></a>Automatische MDM-Registrierung   
Führen Sie die Schritte, um automatische MDM-Registrierung von registrierten Geräten aktivieren, damit Sie den Anspruch IsCompliant in Ihre Access-Control-Richtlinie verwenden können, [hier.](https://blogs.technet.microsoft.com/ad/2015/08/14/windows-10-azure-ad-and-microsoft-intune-automatic-mdm-enrollment-powered-by-the-cloud/)  

## <a name="troubleshooting"></a>Problembehandlung  
1.  Wenn Sie eine Fehlermeldung erhalten, auf `Initialize-ADDeviceRegistration` meldet, die ein Objekt, das bereits in den falschen Status auf, wie z. B. "die drs-Dienstobjekt wurde ohne aller erforderlichen Attribute gefunden", Sie können Azure AD Connect-Powershell-Befehle bereits zuvor ausgeführt haben und haben Sie eine partielle Konfiguration in AD DS.  Versuchen Sie es manuell unter die Objekte zu löschen **CN = Device Registration Configuration, CN = Services, CN = Configuration, DC =&lt;Domäne&gt;**  und versuchen Sie es erneut.  
2.  Für Windows 10-Domäne eingebundene clients  
    1. Um sicherzustellen, dass die Geräteauthentifizierung funktioniert, melden Sie sich bei des Domäne eingebundenen Clients als ein Testbenutzerkonto. Zum Auslösen der Bereitstellung schnell Sperren Sie und entsperren Sie den Desktop mindestens einmal aus.   
    2. Anweisungen zu prüfen, Stk schlüsselanmeldeinformationen, die auf einen link auf AD DS-Objekt (Synchronisierung weiterhin muss zweimal ausgeführt?)  
3.  Wenn einen Fehler bei versuchen, einen Windows-Computer zu registrieren, die das Gerät wurde bereits registriert, aber Sie haben bereits das Gerät abgemeldet oder können nicht angezeigt wird, müssen Sie ein Fragment der Gerätekonfiguration für die Registrierung in der Registrierung möglicherweise.  Um zu untersuchen, und entfernen, verwenden Sie die folgenden Schritte aus:  
    1. Klicken Sie auf dem Windows-Computer, öffnen Sie "regedit", und navigieren Sie zu **HKLM\Software\Microsoft\Enrollments**   
    2. Unter diesem Schlüssel stehen viele Unterschlüssel im GUID-Format.  Navigieren Sie zu den Unterschlüssel den ~ 17 Werte enthält, und verfügt über "EnrollmentType" von "6" [MDM verknüpft] oder "13" (Azure AD eingebunden)  
    3. Ändern Sie **EnrollmentType** zu **0** 
    4. Wiederholen Sie die Registrierung des Geräts oder der Registrierung  

### <a name="related-articles"></a>Verwandte Artikel  
* [Sichern des Zugriffs auf Office 365 und andere apps, die mit Azure Active Directory verbunden sind](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access/)  
* [Geräterichtlinien für den bedingten Zugriff für Office 365-Dienste](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-device-policies/)  
* [Einrichten des lokalen bedingten Zugriffs, die mithilfe der Azure Active Directory-Geräteregistrierung](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup)  
* [Verbinden von in Domänen eingebundene Geräte mit Azure AD für Windows 10-Funktionen](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)  
