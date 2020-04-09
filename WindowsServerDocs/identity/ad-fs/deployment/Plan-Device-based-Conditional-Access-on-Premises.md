---
ms.assetid: c5eb3fa0-550c-4a2f-a0bc-698b690c4199
title: Planen des gerätebasierten bedingten lokalen Zugriffs
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d22897111588393efc148e6f24affeb243ee9e88
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855333"
---
# <a name="plan-device-based-conditional-access-on-premises"></a>Planen des gerätebasierten bedingten lokalen Zugriffs


In diesem Dokument werden Richtlinien für den bedingten Zugriff basierend auf Geräten in einem Hybrid Szenario beschrieben, in dem die lokalen Verzeichnisse mithilfe Azure AD Connect mit Azure AD verbunden sind.     

## <a name="ad-fs-and-hybrid-conditional-access"></a>AD FS und Hybrid bedingter Zugriff  

AD FS bietet die lokale Komponente der Richtlinien für bedingten Zugriff in einem Hybridszenario.  Wenn Sie Geräte mit Azure AD für den bedingten Zugriff auf cloudressourcen registrieren, werden die Geräte Registrierungsinformationen von der Funktion zum Zurückschreiben von Azure AD Connect Geräten lokal zur Verfügung gestellt, damit AD FS Richtlinien genutzt und erzwungen werden können.  Auf diese Weise haben Sie einen konsistenten Ansatz für die Zugriffs Steuerungs Richtlinien sowohl für lokale als auch für cloudressourcen.  

![bedingter Zugriff](media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  

### <a name="types-of-registered-devices"></a>Typen registrierter Geräte  
Es gibt drei Arten registrierter Geräte, die alle in Azure AD als Geräte Objekte dargestellt und auch für den bedingten Zugriff mit AD FS lokal verwendet werden können.  

| |Geschäfts-oder Schul Konto hinzufügen  |Azure AD-Beitritt  |Windows 10-Domänen Beitritt    
| --- | --- |--- | --- |
|Beschreibung    |  Benutzer fügen ihr Geschäfts-, Schul-oder unikonto dem BYOD-Gerät interaktiv hinzu.  **Hinweis:** Das Hinzufügen eines Geschäfts-, Schul-oder unikontos ist der Ersatz für Workplace Join in Windows 8/8.1       | Benutzer fügen ihr Windows 10-Arbeitsgerät in Azure AD ein.|In die Domäne eingebundener Windows 10-Geräte werden automatisch bei Azure AD registriert|           
|Anmelden von Benutzern beim Gerät     |  Keine Anmeldung bei Windows als Geschäfts-, Schul-oder unikonto.  Melden Sie sich mit einem Microsoft-Konto an.       |   Melden Sie sich bei Windows als (Geschäfts-, Schul-oder unikonto) an, das das Gerät registriert hat      |     Anmelden mit AD-Konto|      
|Verwalten von Geräten    |      MDM-Richtlinien (mit zusätzlicher InTune-Registrierung)   | MDM-Richtlinien (mit zusätzlicher InTune-Registrierung)        |   Gruppenrichtlinie Configuration Manager |
|Azure AD vertrauensungstyp|Arbeitsplatz Beitritt|Azure AD verknüpft|Mit Domäne verknüpft  |     
|Speicherort für die Einstellungen    | Einstellungen > Konten > Ihrem Konto > Hinzufügen eines Geschäfts-, Schul-oder unikontos        | Einstellungen > System > Informationen zum > Join Azure AD       |   Einstellungen > System > über > beitreten zu einer Domäne |       
|Auch für IOS-und Android-Geräte verfügbar?   |    Ja     |       Nein  |   Nein   |   

  

Weitere Informationen zu den verschiedenen Methoden zum Registrieren von Geräten finden Sie unter:  
* [Verwenden von Windows 10-Geräten an Ihrem Arbeitsplatz](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-windows10-devices/)  
* [Einrichten von Windows 10-Geräten für die Arbeit](https://jairocadena.com/2016/01/18/setting-up-windows-10-devices-for-work-domain-join-azure-ad-join-and-add-work-or-school-account/)  
[Verknüpfen von Windows 10 Mobile mit Azure Active Directory](https://technet.microsoft.com/itpro/windows/manage/join-windows-10-mobile-to-azure-active-directory)  

### <a name="how-windows-10-user-and-device-sign-on-is-different-from-previous-versions"></a>Unterschiede zwischen der Windows 10-Benutzer-und-Geräte Anmeldung und früheren Versionen  
Für Windows 10 und AD FS 2016 gibt es einige neue Aspekte der Geräteregistrierung und-Authentifizierung, die Sie kennen sollten (insbesondere, wenn Sie in früheren Versionen mit der Geräteregistrierung und dem Arbeitsplatz Beitritt vertraut sind).  

Erstens: in Windows 10 und AD FS in Windows Server 2016 basieren die Geräteregistrierung und-Authentifizierung nicht mehr ausschließlich auf einem X509-Benutzerzertifikat.  Es gibt ein neues und stabileres Protokoll, das eine bessere Sicherheit und eine nahtlose Benutzer Leistung bietet.  Der Hauptunterschied besteht darin, dass für Windows 10-Domänen Beitritt und-Azure AD Join ein X509-Computer Zertifikat und neue Anmelde Informationen als PRT bezeichnet werden.  [Hier](https://jairocadena.com/2016/01/18/how-domain-join-is-different-in-windows-10-with-azure-ad/) finden Sie Informationen [dazu.](https://jairocadena.com/2016/02/01/azure-ad-join-what-happens-behind-the-scenes/)  

Zweitens unterstützen Windows 10 und AD FS 2016 die Benutzerauthentifizierung mithilfe Microsoft Passport for Work, die Sie [hier](https://jairocadena.com/2016/03/09/azure-ad-and-microsoft-passport-for-work-in-windows-10/) und [hier](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)lesen können.  

AD FS 2016 bietet nahtlose Geräte-und Benutzer-SSO basierend auf den PRT-und Passport-Anmelde Informationen.  Mithilfe der in diesem Dokument beschriebenen Schritte können Sie diese Funktionen aktivieren und sehen, wie Sie funktionieren.  

### <a name="device-access-control-policies"></a>Geräte Access Control Richtlinien  
Geräte können in einfachen AD FS Zugriffs Steuerungs Regeln verwendet werden, wie z. b.:  

- Zugriff nur von einem registrierten Gerät zulassen   
- Multi-Factor Authentication erforderlich, wenn ein Gerät nicht registriert ist  

Diese Regeln können dann mit anderen Faktoren wie dem Netzwerk Zugriffs Standort und Multi-Factor Authentication kombiniert werden. so können Sie umfassende Richtlinien für den bedingten Zugriff erstellen, z.b.:  


- erfordert mehrstufige Authentifizierung für nicht registrierte Geräte, die von außerhalb des Unternehmensnetzwerks zugreifen, außer für Mitglieder einer bestimmten Gruppe oder Gruppen  

Mit AD FS 2016 können diese Richtlinien so konfiguriert werden, dass auch eine bestimmte Geräte Vertrauensstellungs Ebene erforderlich ist: **authentifiziert**, **verwaltet**oder **kompatibel**.  

Weitere Informationen zum Konfigurieren AD FS Zugriffs Steuerungs Richtlinien finden Sie unter [Zugriffs Steuerungs Richtlinien in AD FS](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md).  

#### <a name="authenticated-devices"></a>Authentifizierte Geräte  
Bei authentifizierten Geräten handelt es sich um registrierte Geräte, die nicht bei MDM registriert sind (InTune-und Drittanbieter-mdms für Windows 10, nur InTune für IOS und Android).   

Für authentifizierte Geräte wird der **IsManaged** AD FS-Anspruch mit dem Wert " **false**" verwendet. (Im Gegensatz zu Geräten, die überhaupt nicht registriert sind, wird dieser Anspruch nicht angezeigt.)  Für authentifizierte Geräte (und alle registrierten Geräte) wird der isknown AD FS-Anspruch mit dem Wert " **true**" verwendet.  

#### <a name="managed-devices"></a>Verwaltete Geräte:   

Verwaltete Geräte sind registrierte Geräte, die bei MDM registriert sind.  

Verwaltete Geräte verfügen über den IsManaged AD FS-Anspruch mit dem Wert " **true**".  

#### <a name="devices-compliant-with-mdm-or-group-policies"></a>Geräte kompatibel (mit MDM-oder Gruppenrichtlinien)  
Kompatible Geräte sind registrierte Geräte, die nicht nur bei MDM registriert, sondern mit den MDM-Richtlinien kompatibel sind. (Die Kompatibilitätsinformationen stammen aus der MDM und werden in Azure AD geschrieben.)  

Kompatible Geräte verfügen über den **iscompliance** -AD FS Anspruch mit dem Wert " **true**".    

Eine umfassende Liste mit AD FS 2016-Gerät und bedingten Zugriffs Ansprüchen finden Sie unter [Reference](#reference).  


## <a name="reference"></a>Verweis  
#### <a name="complete-list-of-new-ad-fs-2016-and-device-claims"></a>Umfassende Liste der neuen AD FS 2016-und Geräteansprüche  

* https://schemas.microsoft.com/ws/2014/01/identity/claims/anchorclaimtype  
* http://schemas.xmlsoap.org/ws/2005/05/identity/claims/implicitupn  
* https://schemas.microsoft.com/2014/03/psso  
* https://schemas.microsoft.com/2015/09/prt  
* http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid  
* http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/registrationid  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/displayname  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/identifier  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/ostype  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/osversion  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser  
* https://schemas.microsoft.com/2014/02/devicecontext/claims/isknown  
* https://schemas.microsoft.com/2014/02/deviceusagetime  
* https://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant  
* https://schemas.microsoft.com/2014/09/devicecontext/claims/trusttype  
* https://schemas.microsoft.com/claims/authnmethodsreferences  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path  
* https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/client-request-id  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/relyingpartytrustid  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-ip  
* https://schemas.microsoft.com/2014/09/requestcontext/claims/userip  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod  
