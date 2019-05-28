---
ms.assetid: c5eb3fa0-550c-4a2f-a0bc-698b690c4199
title: Planen des gerätebasierten bedingten lokalen Zugriffs
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ffd7131f7f3772ab47b62c9755008fe3b1c4b274
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192067"
---
# <a name="plan-device-based-conditional-access-on-premises"></a>Planen des gerätebasierten bedingten lokalen Zugriffs


Dieses Dokument beschreibt die Richtlinien für bedingten Zugriff, die basierend auf Geräten in einem hybridszenario, bei dem die lokalen Verzeichnisse in Azure AD mit Azure AD Connect verbunden sind.     

## <a name="ad-fs-and-hybrid-conditional-access"></a>AD FS und hybride für bedingten Zugriff  

AD FS verfügt, die auf lokale-Komponente der Richtlinien für bedingten Zugriff in einem hybridszenario.  Beim Registrieren von Geräten mit Azure AD für den bedingten Zugriff auf Cloud-Ressourcen das Gerät Azure AD Connect wieder geschrieben, dass die Funktion zur Verfügung Registrierungsinformationen Gerät lokal für die AD FS-Richtlinien zu nutzen und zu erzwingen.  Auf diese Weise haben Sie einen einheitlichen Ansatz für den Zugriff auf Richtlinien für die Zugriffssteuerung sowohl auf lokale und cloudbasierte Ressourcen.  

![Für den bedingten Zugriff](media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  

### <a name="types-of-registered-devices"></a>Arten von registrierten Geräten  
Es gibt drei Arten von registrierten Geräte, die als Geräteobjekte in Azure AD dargestellt werden, und für den bedingten Zugriff mit AD FS auch lokal verwendet werden können.  

| |Arbeit hinzufügen Schul- oder Unikonto  |Azure AD-Beitritt  |Windows 10 Domian Join    
| --- | --- |--- | --- |
|Beschreibung    |  Benutzer fügen ihre Arbeit Schul- oder unikonto auf ihre BYOD-Geräte interaktiv.  **Hinweis**: Hinzufügen von Geschäfts-, Schul- oder Unikonto ist der Ersatz für den Arbeitsplatzbeitritt in Windows 8/8.1       | Benutzer einbinden ihre Windows 10-Gerät für Arbeit in Azure AD.|Windows 10-Domäne eingebundene Geräte werden automatisch in Azure AD registriert.|           
|Wie Benutzer auf dem Gerät anmelden     |  Keine Anmeldung bei Windows als Geschäfts-, Schul- oder UNI-Konto.  Melden Sie sich mit einem Microsoft-Konto.       |   Melden Sie sich Windows als Konto (Geschäfts-, Schul- oder unikonto), das das Gerät registriert.      |     Melden Sie sich mit der AD-Konto.|      
|Verwaltung von Geräten    |      MDM-Verwaltungsrichtlinien (mit zusätzlichen Intune-Registrierung)   | MDM-Verwaltungsrichtlinien (mit zusätzlichen Intune-Registrierung)        |   Gruppenrichtlinien, System Center Configuration Manager (SCCM) |
|Azure AD-Vertrauensstellung-Typ|Workplace Join|Azure AD eingebunden|Domäne beigetreten  |     
|W10 einstellungsspeicherort    | Einstellungen > Konten > Ihr Konto > Hinzufügen eines Geschäfts-, Schul- oder unikontos-Kontos        | Einstellungen > System > über > Azure AD beitreten       |   Einstellungen > System > über > einer Domäne beitreten |       
|Auch verfügbar für iOS und Android-Geräte?   |    Ja     |       Nein  |   Nein   |   

  

Weitere Informationen zu den verschiedenen Möglichkeiten zum Registrieren von Geräten Siehe auch:  
* [Verwenden von Windows 10-Geräten an Ihrem Arbeitsplatz](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-windows10-devices/)  
* [Einrichten von Windows 10-Geräte für die Arbeit](https://jairocadena.com/2016/01/18/setting-up-windows-10-devices-for-work-domain-join-azure-ad-join-and-add-work-or-school-account/)  
[Windows 10 Mobile zu Azure Active Directory Join](https://technet.microsoft.com/itpro/windows/manage/join-windows-10-mobile-to-azure-active-directory)  

### <a name="how-windows-10-user-and-device-sign-on-is-different-from-previous-versions"></a>Wie Windows 10-Benutzer und Gerät anmelden unterscheidet sich von früheren Versionen  
Für Windows 10 und AD FS 2016 einige neue Aspekte der geräteregistrierung und -Authentifizierung stehen sollten Sie über wissen (insbesondere, wenn Sie mit der geräteregistrierung und "Workplace join" in früheren Versionen vertraut sind).  

Zuerst in Windows 10 und AD FS unter Windows Server 2016, geräteregistrierung und -Authentifizierung nicht mehr basiert ausschließlich auf eine X509 Benutzerzertifikat.  Es ist ein neues und robuster-Protokoll, das eine bessere Sicherheit und eine nahtlose benutzererfahrung bietet.  Der Hauptunterschied besteht, dass für Windows 10-Domäne beitreten und Azure AD Join eine X509 ist Computerzertifikat und die neuen Anmeldeinformationen bezeichnet ein PRT.  Sie erhalten alle Informationen über [hier](https://jairocadena.com/2016/01/18/how-domain-join-is-different-in-windows-10-with-azure-ad/) und [hier](https://jairocadena.com/2016/02/01/azure-ad-join-what-happens-behind-the-scenes/).  

Zweitens: Windows 10 und AD FS 2016 unterstützt Benutzerauthentifizierung, die mithilfe von Microsoft Passport für die Arbeit, die Sie sich vertraut machen können [hier](https://jairocadena.com/2016/03/09/azure-ad-and-microsoft-passport-for-work-in-windows-10/) und [hier](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/).  

AD FS 2016 bietet nahtlose Geräte- und SSO auf der Grundlage sowohl PRT-Passport-Anmeldeinformationen.  Verwenden die Schritte in diesem Dokument an, können Sie diese Funktionen zu aktivieren und arbeiten.  

### <a name="device-access-control-policies"></a>Device Access Control-Richtlinien  
Geräte können z. B. in einfachen Zugriffssteuerungsregeln für AD FS verwendet werden:  

- Zugriff nur von einem registrierten Gerät zulassen   
- Multi-Factor Authentication erforderlich, wenn ein Gerät nicht registriert ist  

Diese Regeln können dann mit anderen Faktoren wie z. B. die Netzwerkadresse für den Zugriff und Multi-Factor Authentication, Erstellung bedingter Zugriffsrichtlinien wie z. B. umfangreiche kombiniert werden:  


- erfordern von Multi-Factor Authentication für nicht registrierte Geräte, die Zugriff auf von außerhalb des Unternehmensnetzwerks, außer für Mitglieder einer bestimmten Gruppe oder Gruppen  

Diese Richtlinien können mit AD FS 2016 speziell für ein bestimmtes Gerät Vertrauensebene sowie erforderlich konfiguriert werden: entweder **authentifiziert**, **verwaltet**, oder **kompatibel**.  

Weitere Informationen zum Konfigurieren von AD FS Zugriff auf Richtlinien für die Zugriffssteuerung, finden Sie unter [Zugriffssteuerungsrichtlinien in AD FS](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md).  

#### <a name="authenticated-devices"></a>Authentifizierte Geräte  
Authentifizierte Geräte werden registrierte Geräte, die in der Verwaltung mobiler Geräte (Intune und 3rd Party MDMs für Windows 10, Intune, nur für iOS und Android) nicht registriert werden.   

Authentifizierte Geräte haben den **IsManaged** AD FS-Anspruch mit dem Wert **"false"** . (Während auf Geräten, die überhaupt nicht registriert werden dieser Anspruch verfügen werden.)  Authentifizierte Geräte (und alle registrierten Geräte) müssen die IsKnown AD FS-Anspruch mit dem Wert **"true"** .  

#### <a name="managed-devices"></a>Verwaltete Geräte:   

Verwaltete Geräte werden registrierte Geräte, die mit MDM registriert sind  

Verwaltete Geräte haben den IsManaged AD FS-Anspruch mit dem Wert **"true"** .  

#### <a name="devices-compliant-with-mdm-or-group-policies"></a>Geräte sind konform (mit MDM- oder Gruppenrichtlinien)  
Konforme Geräte werden registrierte Geräte, die jedoch kompatibel mit den MDM-Richtlinien nicht nur bei MDM registriert sind. (Informationen zur Compliance stammt, mit der Verwaltung mobiler Geräte und mit Azure AD geschrieben.)  

Kompatible Geräte müssen die **IsCompliant** AD FS-Anspruch mit dem Wert **"true"** .    

Vollständige Liste der AD FS 2016 und für den bedingten Zugriff Ansprüche Geräts, finden Sie unter [Verweis](#reference).  


## <a name="reference"></a>Referenz  
#### <a name="complete-list-of-new-ad-fs-2016-and-device-claims"></a>Vollständige Liste der neuen AD FS 2016 und Geräteansprüche  

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
