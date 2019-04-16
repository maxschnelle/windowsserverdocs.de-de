---
ms.assetid: c5eb3fa0-550c-4a2f-a0bc-698b690c4199
title: "Planen der Geräte-basierter Bedingter Zugriff auf lokale"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6303bba92ce4f4f99ae8e5095060b06885e427d6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="plan-device-based-conditional-access-on-premises"></a>Planen der Geräte-basierter Bedingter Zugriff auf lokale

>Gilt für: Windows Server 2016

Dieses Dokument beschreibt die Richtlinien für bedingten Zugriff basierend auf Geräten in einem hybridszenario, in dem die lokale Verzeichnisse mit Azure AD mithilfe von Azure AD Connect verbunden sind.     

## <a name="ad-fs-and-hybrid-conditional-access"></a>AD FS und hybride bedingten Zugriff  

AD FS bietet, die auf lokalen-Komponente von Richtlinien für bedingten Zugriff in einem hybridszenario.  Wenn Sie Geräte mit Azure AD für bedingten Zugriff auf Cloudressourcen registrieren, das Azure AD Connect-Gerät schreiben wieder macht Geräteinformationen Registrierung verfügbar lokal für AD FS-Richtlinien nutzen, und erzwingen.  Auf diese Weise können Sie einen konsistenten Ansatz für den Zugriff auf Richtlinien für sowohl in lokalen und Cloud-Ressourcen.  

![Bedingter Zugriff](media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  

### <a name="types-of-registered-devices"></a>Arten von registrierten Geräten  
Es gibt drei Arten von registrierten Geräten, die in Azure AD als Geräteobjekte dargestellt und für bedingten Zugriff mit AD FS auch lokal verwendet werden kann.  

| |Hinzufügen von Arbeit oder Schule Konto  |Beitritt zu Azure AD  |Windows 10 Domian beitreten    
| --- | --- |--- | --- |
|Beschreibung    |  Benutzer hinzufügen ihrer Arbeit oder schulkonto BYOD Gerät interaktiv.  **Hinweis:** hinzufügen Geschäfts- oder Schulkonto ist der Ersatz für den Arbeitsplatzbeitritt in Windows 8/8.1       | Benutzer werden ihre Windows 10-Gerät arbeiten mit Azure AD beitreten.|Windows 10-Geräten werden automatisch bei Azure AD registrieren.|           
|Wie Benutzer auf dem Gerät anmelden     |  Keine Anmeldung bei Windows als Dienstkonto Geschäfts- oder schulkonto.  Melden Sie sich mit einem Microsoft-Konto.       |   Melden Sie sich bei Windows als Dienstkonto (Arbeits- oder Schulcomputer), die das Gerät registriert.      |     Melden Sie sich mit AD-Konto.|      
|Verwaltung von Geräten    |      MDM-Richtlinien (mit zusätzlichen Intune-Registrierung)   | MDM-Richtlinien (mit zusätzlichen Intune-Registrierung)        |   Gruppenrichtlinien, System Center Configuration Manager (SCCM) |
|Azure AD Trust-Typ|Mit dem Arbeitsplatz verbundene|Azure AD eingebunden sind|Domäne angehört  |     
|Speicherort der W10-Einstellungen    | Einstellungen > Konten > Ihr Konto > Hinzufügen eines Geschäfts- oder schulkontos-Kontos        | Einstellungen > System > zu > Azure AD beitreten       |   Einstellungen > System > zu > einer Domäne beitreten |       
|Auch für IOS- und Android-Geräten verfügbar?   |    Ja     |       Nein  |   Nein   |   

  

Weitere Informationen zu den verschiedenen Möglichkeiten zum Registrieren von Geräten Siehe auch:  
* [Mithilfe von Windows 10-Geräten an Ihrem Arbeitsplatz](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-windows10-devices/)  
* [Einrichten von Windows 10-Geräten für die Arbeit](https://jairocadena.com/2016/01/18/setting-up-windows-10-devices-for-work-domain-join-azure-ad-join-and-add-work-or-school-account/)  
[Verknüpfen von Windows 10 Mobile mit Azure Active Directory](https://technet.microsoft.com/itpro/windows/manage/join-windows-10-mobile-to-azure-active-directory)  

### <a name="how-windows-10-user-and-device-sign-on-is-different-from-previous-versions"></a>Wie Windows 10-Benutzer und Gerät anmelden unterscheidet sich von früheren Versionen  
Für Windows10 und AD FS 2016 einige neue der Geräteregistrierung und -Authentifizierung Aspekte sollten Sie kennen (insbesondere, wenn Sie sehr Geräteregistrierung und "arbeitsplatzbeitritt" in früheren Versionen kennen).  

Zuerst in Windows 10 und AD FS unter Windows Server 2016, geräteregistrierung und -Authentifizierung nicht mehr basiert ausschließlich auf ein X509 Benutzerzertifikat.  Es ist ein neues und stabilere-Protokoll, die eine höhere Sicherheit und eine nahtlose Benutzeroberfläche bietet.  Die wichtigsten Unterschiede sind, für Windows 10-Domäne und Azure AD Join, ergibt sich eine X509 Computerzertifikat und neue Anmeldeinformationen eine PRT aufgerufen.  Alle Informationen zu [hier](https://jairocadena.com/2016/01/18/how-domain-join-is-different-in-windows-10-with-azure-ad/) und [hier](https://jairocadena.com/2016/02/01/azure-ad-join-what-happens-behind-the-scenes/).  

Zweitens Windows 10 und AD FS 2016 unterstützt die Benutzerauthentifizierung, die mithilfe von Microsoft Passport for Work, um Sie zu lesen können [hier](https://jairocadena.com/2016/03/09/azure-ad-and-microsoft-passport-for-work-in-windows-10/) und [hier](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-passport-deployment/).  

AD FS 2016 bietet nahtlose und Benutzer SSO basierend auf den Druck und Passport-Anmeldeinformationen.  Verwenden die Schritte in diesem Dokument, können Sie diese Funktionen zu aktivieren und sie funktionieren.  

### <a name="device-access-control-policies"></a>Gerät Zugriffsrichtlinien  
Geräte können z. B. in einfachen Zugriffssteuerungsregeln für AD FS verwendet werden:  

- Zugriff nur von einem registrierten Gerät zulassen   
- Multi-Factor Authentication erforderlich, wenn ein Gerät nicht registriert ist  

Diese Regeln können dann mit anderen Faktoren wie den Speicherort im Netzwerk zugreifen und Multi-Factor Authentication, erstellen ansprechende bedingte Zugriffsrichtlinien z. B. kombiniert werden:  


- erfordern Sie Multi-Factor Authentication für nicht registrierte Geräte, die außerhalb des Unternehmensnetzwerks, mit Ausnahme der Mitglieder einer bestimmten Gruppe oder Gruppen zugreifen  

Diese Richtlinien können mit AD FS 2016, speziell für ein bestimmtes Gerät Vertrauensebene sowie erfordern konfiguriert werden: entweder **authentifiziert**, **verwaltet**, oder **kompatibel**.  

Weitere Informationen zum Konfigurieren von AD FS Zugriff auf Richtlinien, finden Sie unter [Zugriffssteuerungsrichtlinien in AD FS](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md).  

#### <a name="authenticated-devices"></a>Authentifizierte Geräte  
Authentifizierte Geräte sind registrierte Geräte, die nicht in MDM (Intune und 3rd Party MDMs für Windows 10, Intune nur für iOS und Android) registriert sind.   

Authentifizierte Geräte enthalten die **IsManaged** AD FS mit Wert Anspruch **FALSE**. (Während der Geräte, die überhaupt nicht registriert werden diesem Anspruch fehlen werden.) Authentifizierte Geräte (und alle registrierten Geräte) müssen die IsKnown AD FS mit Wert Anspruch **TRUE**.  

#### <a name="managed-devices"></a>Verwaltete Geräte:   

Verwaltete Geräte sind registrierte Geräte, die mit MDM angemeldet werden  

Verwaltete Geräte müssen die IsManaged AD FS mit Wert Anspruch **TRUE**.  

#### <a name="devices-compliant-with-mdm-or-group-policies"></a>(Mit MDM oder Gruppenrichtlinien) kompatible Geräte  
Kompatible Geräte sind registrierte Geräte, die nicht nur mit MDM jedoch mit der MDM-Richtlinien kompatibel registriert sind. (Kompatibilitätsinformationen mit MDM stammt und in Azure AD geschrieben.)  

Kompatible Geräte müssen die **IsCompliant** AD FS mit Wert Anspruch **TRUE**.    

Vollständige Liste der AD FS 2016 Geräte- und Ansprüche des bedingten Zugriffs, finden Sie unter [Verweis](#reference).  


## <a name="reference"></a>Referenz zu  
#### <a name="complete-list-of-new-ad-fs-2016-and-device-claims"></a>Vollständige Liste der neuen AD FS 2016 und Geräteansprüche  

* https://schemas.microsoft.com/ws/2014/01/identity/claims/anchorclaimtype  
* http://Schemas.xmlsoap.org/ws/2005/05/Identity/Claims/implicitupn  
* https://schemas.microsoft.com/2014/03/psso  
* https://schemas.microsoft.com/2015/09/prt  
* http://Schemas.xmlsoap.org/ws/2005/05/Identity/Claims/UPN  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid  
* http://Schemas.xmlsoap.org/ws/2005/05/Identity/Claims/Name  
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
* https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-Client-user-Agent  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path  
* https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/Client-request-id  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/relyingpartytrustid  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-Client-ip  
* https://schemas.microsoft.com/2014/09/requestcontext/claims/userip  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod  
