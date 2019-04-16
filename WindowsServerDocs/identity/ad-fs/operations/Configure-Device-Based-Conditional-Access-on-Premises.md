---
ms.assetid: 35de490f-c506-4b73-840c-b239b72decc2
title: "Konfigurieren Sie die Geräte-basierter Bedingter Zugriff auf lokale"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/11/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 47afd0c6963bd8b8b4dde82650cf807c1954b40b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="configure-on-premises-conditional-access-using-registered-devices"></a>Konfigurieren On-Premises Conditional Access using registrierte Geräte

>Gilt für: Windows Server 2016, Windows Server2012 R2  

Das folgende Dokument führt Sie durch die Installation und Konfiguration von bedingten Zugriff Onlineclients mit registrierten Geräten.

![Bedingter Zugriff](media/Using-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  

## <a name="infrastructure-pre-requisites"></a>Infrastruktur-Voraussetzungen
Die folgende pro-aufgeführt, die erforderlich sind erforderlich, bevor Sie mit der bedingten Zugriff Onlineclients beginnen können. 

|Anforderung|Beschreibung
|-----|-----
|Ein Azure AD-Abonnement mit Azure AD Premium | So aktivieren Sie Schreib-Gerät erneut auf lokalen bedingten Zugriff - [eine kostenlose Testversion ist in Ordnung](https://azure.microsoft.com/en-us/trial/get-started-active-directory/)  
|Intune-Abonnement|nur erforderlich, für die MDM-Integration für Szenarien für Geräte-Compliance -[eine kostenlose Testversion ist in Ordnung](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0)
|Azure AD Connect|November 2015 QFE oder höher.  Herunterladen der neuesten Version [hier](https://www.microsoft.com/en-us/download/details.aspx?id=47594).  
|Windows Server 2016|Build 10586 oder höher für AD FS  
|Windows Server 2016 Active Directory-schema|Auf der Schemaebene 85 oder höher ist erforderlich.
|Windows Server 2016-Domänencontroller|Dies ist nur für Hello für Business Key-Trust-Bereitstellungen erforderlich.  Weitere Informationen finden Sie unter [hier](https://aka.ms/whfbdocs).  
|Windows 10-client|Build 10586 oder höher, der oben genannten Domäne zugeordnet ist erforderlich für Windows 10-Domänenbeitritt und Microsoft Passport Arbeit nur für Szenarios  
|Azure AD-Benutzerkonto mit Azure AD Premium-Lizenz zugewiesen|Für die Registrierung des Geräts  


 
## <a name="upgrade-your-active-directory-schema"></a>Aktualisieren von Active Directory-Schema
Bedingter Zugriff Onlineclients mit registrierten Geräte verwenden möchten, müssen Sie zunächst das Active Directory-Schema aktualisieren.  Die folgenden Bedingungen müssen erfüllt sein:
    - Das Schema sollte 85 oder höher sein.
    - Dies ist nur erforderlich, damit die Gesamtstruktur, die AD FS angehört

> [!NOTE]
> Wenn Sie Azure AD Connect vor dem Upgrade auf die Schemaversion (Level85 oder höher) in Windows Server2016 installiert, Sie müssen die Azure AD Connect-Installation erneut ausführen und Aktualisieren der lokalen Active Directory-Schema, um die Synchronisierungsregel sicherzustellen, dass für MsDS-KeyCredentialLink konfiguriert ist.

### <a name="verify-your-schema-level"></a>Überprüfen Sie Ihre Schemaebene
Führen Sie folgende Schritteaus, um Ihre Schemaebene zu überprüfen:

1.  Sie können mithilfe von ADSIEdit oder LDP und Verbinden mit im Schemanamenskontext.  
2.  Verwenden ADSIEdit, mit der rechten Maustaste auf "CN = Schema, CN = Configuration, DC =<domain>, DC =<com>, und klicken Sie auf Eigenschaften.  Relpace Domäne und die COM-Bereiche mit den Informationen für die Gesamtstruktur.
3.  Unter dem Attribut-Editor Suchen Sie das Attribut ObjectVersion und informiert Sie, Ihre Version.  

![ADSI-Bearbeitung](media/Configure-Device-Based-Conditional-Access-on-Premises/adsiedit.png)  

Sie können auch das folgende PowerShell-Cmdlet (ersetzen Sie das Objekt mit Ihr Schema Kontext Namensinformationen) verwenden:

``` powershell
Get-ADObject "cn=schema,cn=configuration,dc=domain,dc=local" -Property objectVersion
    
```

![PowerShell](media/Configure-Device-Based-Conditional-Access-on-Premises/pshell1.png) 

Weitere Informationen zur Aktualisierung finden Sie unter [Aktualisieren von Domänencontrollern auf Windows Server2016](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2016.md). 

## <a name="enable-azure-ad-device-registration"></a>Aktivieren der Azure AD-Geräteregistrierung  
Um dieses Szenario zu konfigurieren, müssen Sie die Registrierung Gerätefunktion in Azure AD konfigurieren.  

Führen Sie dazu die Schritte unter [Einrichten von Azure AD Join in Ihrer Organisation](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-setup/)  

## <a name="setup-ad-fs"></a>AD FS-Setup  
1. Erstellen Sie die ein [neuen AD FS 2016 Farm](https://technet.microsoft.com/library/dn486775.aspx).   
2.  Oder [migrieren](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md) einer Farm mit AD FS 2016 von AD FS 2012 R2  
4. Bereitstellen von [Azure AD Connect](https://azure.microsoft.com/documentation/articles/active-directory-aadconnectfed-whatis/) über den benutzerdefinierten Pfad zur AD FS mit Azure AD verbinden.  

## <a name="configure-device-write-back-and-device-authentication"></a>Konfigurieren von Gerät Zurückschreiben und Geräteauthentifizierung  
> [!NOTE]
> Wenn Sie Azure AD Connect mithilfe von Express-Einstellungen ausgeführt haben, haben die richtigen Active Directory-Objekte für Sie erstellt wurde.  Jedoch in den meisten Szenarien für AD FS, Azure AD Connect Ausführungszeit mit benutzerdefinierten Einstellungen zum Konfigurieren von AD FS, sodass die unten beschriebenen Schritte sind erforderlich.  

### <a name="create-ad-objects-for-ad-fs-device-authentication"></a>Erstellen von AD-Objekte für die Authentifizierung von AD FS-Gerät  
Wenn die AD FS-Farm für die Authentifizierung des Geräts nicht bereits konfiguriert ist (Sie können Siehe hierzu finden Sie in der AD FS-Verwaltungskonsole unter Windows-Verwaltungsinstrumentationsdienst Geräteregistrierung ->), gehen Sie folgendermaßen vor, um die richtigen AD DS-Objekte und Konfigurationen zu erstellen.  

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device1.png)

>Hinweis: Die folgenden Befehle müssen Sie Active Directory-Verwaltungstools, also wenn Ihrem Verbundserver nicht auch ein Domänencontroller ist, zunächst installieren Sie die Tools mithilfe von Schritt 1.  Andernfalls können Sie Schritt 1 überspringen.  

1.  Ausführen der **Hinzufügen von Rollen und Features** Assistenten, und wählen Sie ein Feature **Remoteserver-Verwaltungstools** -> **Rollenverwaltungstools** -> **AD DS und AD LDS-Tools** -> wählen beide die **Active Directory-Modul für Windows PowerShell** und die **AD DS-Tools**.

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device2.png)
  
2.  Vergewissern Sie sich auf Ihre primären AD FS-Server als AD DS-Benutzer mit Berechtigungen für Enterprise-Administrator (EA) angemeldet sind, und öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten Powershell.  Führen Sie dann die folgenden PowerShell-Befehle aus:  
    
    `Import-module activedirectory`  
    `PS C:\> Initialize-ADDeviceRegistration -ServiceAccountName "<your service account>" ` 
3.  Drücken auf das Popup-Fenster "Ja".

>Hinweis: Wenn Ihre AD FS-Dienst konfiguriert ist, um ein GMSA-Konto verwenden, geben Sie den Kontonamen im Format "Schreibweise Domäne\Benutzername an$"

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device3.png)  

Die oben genannten PSH erstellt die folgenden Objekte:  


- RegisteredDevices Container der Partition der AD-Domäne  
- Device Registration Service Container und unter Konfiguration--> Dienste--> Geräteregistrierungskonfiguration  
- Device Registration Service DKM Container und unter Konfiguration--> Dienste--> Geräteregistrierungskonfiguration  

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device4.png)  

4.  Sobald dies erfolgt ist, sehen Sie eine Meldung des erfolgreichen Abschluss.

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device5.png) 

###        <a name="create-service-connection-point-scp-in-ad"></a>Erstellen der Dienstverbindungspunkt (SCP) in Active Directory  
Wenn Windows 10 den Domänenbeitritt (mit dem die automatische Registrierung bei Azure AD) wie hier beschrieben verwendet werden soll, führen Sie die folgenden Befehle zum Erstellen eines Dienstverbindungspunkts in AD DS  
1.  Öffnen Sie Windows PowerShell, und führen Sie Folgendes aus:
    
    `PS C:>Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1" ` 

>Hinweis: Falls erforderlich, kopieren Sie die Datei AdSyncPrep.psm1 von Ihrem Azure AD Connect-Server.  Diese Datei befindet sich im Programm c:\Programme\Microsoft Azure Active Directory Connect\AdPrep

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device6.png)   

2. Geben Sie Ihre Azure AD-globaler Administrator-Anmeldeinformationen  

    `PS C:>$aadAdminCred = Get-Credential`

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device7.png) 

3.  Führen Sie den folgenden PowerShell-Befehl 

    `PS C:>Initialize-ADSyncDomainJoinedComputerSync -AdConnectorAccount [AD connector account name] -AzureADCredentials $aadAdminCred ` 

Steht für [Active Directory Connector-Kontoname] der Name des Kontos, das Sie in Azure AD Connect, beim Hinzufügen der lokales konfiguriert AD DS-Verzeichnis.
  
Die oben aufgeführten Befehle aktivieren Windows 10-Clients finden Sie den richtigen Azure AD-Domäne zu verknüpfen, indem Sie das Objekt ServiceConnectionpoint in AD DS erstellen.  

### <a name="prepare-ad-for-device-write-back"></a>Vorbereiten von Active Directory für Gerät Zurückschreiben   
Führen Sie folgende Schritte aus, um sicherzustellen, dass AD DS-Objekte und Container in den richtigen Status zum Schreiben des Geräten aus Azure AD.

1.  Öffnen Sie Windows PowerShell, und führen Sie Folgendes aus:  

    `PS C:>Initialize-ADSyncDeviceWriteBack -DomainName <AD DS domain name> -AdConnectorAccount [AD connector account name] ` 

Steht für [Active Directory Connector-Kontoname] der Name des Kontos, das Sie in Azure AD Connect, beim Hinzufügen der lokales konfiguriert AD DS-Verzeichnis im Format der Schreibweise Domäne\Benutzername an  

Der obige Befehl erstellt die folgenden Objekte zum Schreiben von Gerät wieder in AD DS, wenn sie nicht bereits vorhanden sind, und ermöglicht den Zugriff auf den angegebenen Kontonamen für AD-connector  

- RegisteredDevices Container in der Partition der AD-Domäne  
- Device Registration Service Container und unter Konfiguration--> Dienste--> Geräteregistrierungskonfiguration  

### <a name="enable-device-write-back-in-azure-ad-connect"></a>Gerät schreiben aktivieren wieder in Azure AD Connect  
Wenn Sie nicht vor ausgeführt haben, aktivieren Sie Gerät schreiben in Azure AD Connect durch Ausführen des Assistenten ein zweites Mal aus, und wählen Sie **"Synchronisierungsoptionen anpassen"**, des Kontrollkästchens zum Gerät schreiben zurück, und Auswählen der Gesamtstruktur, in dem Sie die oben genannten Cmdlets ausgeführt haben,  

### <a name="configure-device-authentication-in-ad-fs"></a>Konfigurieren der Geräteauthentifizierung in AD FS  
Konfigurieren Sie AD FS-Richtlinie mit einer mit erhöhten Rechten PowerShell-Befehlsfenster durch den folgenden Befehl ausführen  

`PS C:>Set-AdfsGlobalAuthenticationPolicy -DeviceAuthenticationEnabled $true -DeviceAuthenticationMethod All` 

### <a name="check-your-configuration"></a>Überprüfen Sie die Konfiguration  
Für den Verweis wird im folgenden eine umfassende Liste von Geräten, Container und Berechtigungen für die Authentifizierung und Gerät Zurückschreiben zum Arbeiten in AD DS
 


- Objekt vom Typ ms-DS-DeviceContainer unter CN = RegisteredDevices, DC =&lt;Domäne&gt;        
    - Lesezugriff auf die AD FS-Dienstkonto   
    - Lese-und Schreibzugriff auf die Azure AD Connect Synchronisierung AD-Connector-Konto</br></br>

- Container CN = Device Registration Configuration, CN = Services, CN = Configuration, DC =&lt;Domäne&gt;  
- Container Device Registration Service DKM unter dem oben genannten container

![Geräteregistrierung](media/Configure-Device-Based-Conditional-Access-on-Premises/device8.png) 
 


- Objekt vom Typ ServiceConnectionpoint unter CN =&lt;Guid&gt;, CN = Device Registration

- Configuration, CN = Services, CN = Configuration, DC =&lt;Domäne&gt;  
 - Lese-und Schreibzugriff für den angegebenen Active Directory Connector-Kontonamen für das neue Objekt</br></br> 


- Objekt vom Typ MsDS-DeviceRegistrationServiceContainer unter CN Gerät Registrierung Services, CN = = Device Registration Configuration, CN = Services, CN = Configuration, DC = & Ltdomain >  


- Objekt vom Typ MsDS-DeviceRegistrationService in den oben genannten container  

### <a name="see-it-work"></a>Finden Sie es funktioniert  
Um die neue Ansprüche und Richtlinien zu bewerten, müssen Sie zuerst registrieren Sie ein Gerät.  Beispielsweise können Sie ein Windows 10-Computer mithilfe der Einstellungs-app unter System -> zum Beitritt zu Azure AD oder Sie können Windows 10-Domänenbeitritt mit folgenden zusätzlichen Schritte automatische geräteregistrierung einrichten [hier](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/).  Informationen zum Verknüpfen von Windows 10 mobile Geräte finden Sie im Dokument [hier](https://technet.microsoft.com/itpro/windows/manage/join-windows-10-mobile-to-azure-active-directory).  

Für die am einfachsten Evaluierung melden Sie sich bei AD FS mit einer testanwendung, die eine Liste von Ansprüchen enthält. Kann neue Ansprüche einschließlich IsManaged, IsCompliant und Trusttype angezeigt werden.  Wenn Sie Microsoft Passport für die Arbeit aktivieren, wird auch der Anspruch Prt angezeigt.  
 

## <a name="configure-additional-scenarios"></a>Weitere Szenarien konfigurieren  
### <a name="automatic-registration-for-windows-10-domain-joined-computers"></a>Automatische Registrierung für Windows 10 Domäne verbundene Computer  
So aktivieren Sie automatische geräteregistrierung für Windows 10-Domäne verbundene Computer, führen Sie die Schritte 1 und 2 [hier](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/).   
Dies hilft Ihnen Folgendes zu erreichen:  

1. Stellen Sie sicher, Ihre Dienstverbindungspunkt in AD DS vorhanden ist und die entsprechenden Berechtigungen (wir dieses Objekt darüber erstellt, aber es ist nicht lohnt sich prüfen).  
2. Stellen Sie sicher, dass AD FS ordnungsgemäß konfiguriert ist  
3. Stellen Sie sicher, dass das AD FS System die richtigen Endpunkte aktiviert und konfiguriert Anspruchsregeln   
4. Konfigurieren der gruppenrichtlinieneinstellungen für die automatische geräteregistrierung der Domäne verbundene Computer erforderlich   

### <a name="microsoft-passport-for-work"></a>Microsoft Passport for Work   
Informationen zum Aktivieren von Windows 10 mit Microsoft Passport for Work, finden Sie unter [ermöglichen Microsoft Passport for Work in Ihrer Organisation.](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-passport-deployment/)  

### <a name="automatic-mdm-enrollment"></a>Automatische MDM-Registrierung   
Um automatische MDM-Registrierung der registrierten Geräte aktivieren, damit Sie den Anspruch IsCompliant in Ihrem Zugriffssteuerungsrichtlinie verwenden können, führen Sie die Schritte [hier.](https://blogs.technet.microsoft.com/ad/2015/08/14/windows-10-azure-ad-and-microsoft-intune-automatic-mdm-enrollment-powered-by-the-cloud/)  

## <a name="troubleshooting"></a>Problembehandlung  
1.  Wenn Sie eine Fehlermeldung erhalten, auf `Initialize-ADDeviceRegistration` , die zu einem Objekt, z. B. in den Zustand des falschen vorhandene erwähnten "das Objekt drs-Dienst wurde ohne alle erforderlichen Attribute gefunden", Sie können Azure AD Connect Powershell zuvor Befehle und verfügen über eine teilweise Konfiguration in AD DS ausgeführt haben.  Löschen Sie manuell die Objekte unter **CN = Device Registration Configuration, CN = Services, CN = Configuration, DC =&lt;Domäne&gt; ** und versuchen Sie es erneut.  
2.  Bei Windows 10-Domäne beigetreten clients  
    1. Stellen Sie sicher, dass die Geräteauthentifizierung funktioniert, melden Sie sich an der Domäne hinzugefügt als ein Testbenutzerkonto Client. Zum Auslösen der Bereitstellung schnell, Sperren Sie und entsperren Sie den Desktop mindestens ein Mal.   
    2. Anweisungen, um zu prüfen, ob wichtige Anmeldeinformationen Stk auf AD DS-Objekt verknüpft (wird synchronisiert haben Sie noch zweimal ausgeführt?)  
3.  Wenn Sie eine beim Versuch Fehlermeldung, einen Windows-Computer zu registrieren, die das Gerät bereits registriert wurde, aber Sie können keine oder haben bereits Registrierung des Geräts aufgehoben, müssen Sie ein Fragment des Gerätekonfiguration Registrierung in der Registrierung möglicherweise.  Untersuchen und entfernen, verwenden Sie die folgenden Schritte aus:  
    1. Klicken Sie auf dem Windows-Computer, öffnen Sie "regedit" ein, und navigieren Sie zu **HKLM\Software\Microsoft\Enrollments**   
    2. Unter diesem Schlüssel kann viele Unterschlüssel in den GUID-Form.  Navigieren Sie zu dem Unterschlüssel dessen ~ 17 Werte darin und dessen "EnrollmentType" von "6" [MDM-Mitglied] oder "13" (Azure AD eingebunden sind)  
    3. Ändern Sie **EnrollmentType** auf **0** 
    4. Wiederholen Sie die geräteregistrierung oder der Registrierung  

### <a name="related-articles"></a>Verwandte Artikel  
* [Sichern des Zugriffs auf Office 365 und andere apps verbunden mit Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access/)  
* [Richtlinien für bedingten Zugriff Gerät für Office 365-Dienste](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-device-policies/)  
* [Einrichten von lokalen bedingten Zugriff mithilfe von Azure Active Directory Device Registration](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-device-registration-on-premises-setup)  
* [Verbinden Sie Geräte in einer Domäne mit Azure AD für Windows 10](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-devices-group-policy/)  
