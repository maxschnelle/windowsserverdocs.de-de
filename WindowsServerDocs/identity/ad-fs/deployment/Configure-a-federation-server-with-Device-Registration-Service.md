---
ms.assetid: fdd1c1fd-55aa-4eb8-ae84-53f811de042c
title: Konfigurieren eines Verbundservers mit Device Registration Service
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 511a039afd47cf7570fffdcaf17842e0eccc5683
ms.sourcegitcommit: 9278435cbfa8dbeb30d0557ed0d27832b154edd2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="configure-a-federation-server-with-device-registration-service"></a>Konfigurieren eines Verbundservers mit Device Registration Service

>Gilt für: Windows Server 2012 R2

Sie können Device Registration Service \(DRS\) auf dem Verbundserver aktivieren, schließen Sie die Verfahren in [Schritt4: Konfigurieren eines Verbundservers](https://technet.microsoft.com/library/dn303424.aspx). Die Device Registration Service bietet einen Onboarding-Mechanismus für die nahtlose zweistufige Authentifizierung, permanente einzelne Standardparameter auf \(SSO\) und bedingten Zugriff für Kunden, die Zugriff auf Unternehmensressourcen erfordern. Weitere Informationen zu DRS finden Sie unter [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung über Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)  
  
## <a name="prepare-your-active-directory-forest-to-support-devices"></a>Vorbereiten von Active Directory-Gesamtstruktur Geräte zu unterstützen  
  
> [!NOTE]  
> Dies ist ein einmaligen Vorgang, den Sie ausführen müssen, zum Vorbereiten von Active Directory-Gesamtstruktur Geräte zu unterstützen. Sie müssen mit Enterprise-Administratorberechtigungen angemeldet sein, und die Active Directory-Gesamtstruktur muss das Windows Server2012 R2-Schema zum Durchführen dieses Verfahrens haben.  
>   
> Darüber hinaus DRS muss mindestens ein globaler Katalogserver in der Gesamtstruktur-Stammdomäne sein. Der globale Katalogserver ist erforderlich, um Initialize\ ADDeviceRegistration ausführen und bei der AD FS-Authentifizierung. AD FS Initialisiert eine Taste Arbeitsspeicher-Darstellung des Objekts DRS-Konfiguration in jede Authentifizierungsanforderung, und wenn das Objekt DRS-Konfiguration auf einem Domänencontroller in der aktuellen Domäne gefunden werden kann, versucht der Anforderungs gegen die GC, auf denen die DRS-Objekte während der Initialize\ ADDeviceRegistration bereitgestellt wurden.  
  
#### <a name="to-prepare-the-active-directory-forest"></a>Vorbereiten von Active Directory-Gesamtstruktur  
  
1.  Öffnen Sie auf dem Verbundserver eine Windows PowerShell-Befehlsfenster, und geben:  
  
    ```  
    Initialize-ADDeviceRegistration  
    ```  
  
2.  Wenn ServiceAccountName dazu aufgefordert werden, geben Sie den Namen des Dienstkontos ein, die Sie als Dienstkonto für AD FS ausgewählt.  Wenn sie ein gMSA-Konto ist, geben Sie das Konto in der **Domain\\accountname$** Format. Verwenden Sie für ein Domänenkonto, das Format **Domain\\accountname**.  
  
## <a name="enable-device-registration-service-on-a-federation-server-farm-node"></a>Aktivieren von Device Registration Service auf einem Federation Serverfarm Knoten  
  
> [!NOTE]  
> Sie müssen mit Domänenadministrator-Berechtigungen zum Durchführen dieses Verfahrens angemeldet sein.  
  
#### <a name="to-enable-device-registration-service"></a>So aktivieren Sie Device Registration Service  
  
1.  Öffnen Sie auf dem Verbundserver eine Windows PowerShell-Befehlsfenster, und geben:  
  
    ```  
    Enable-AdfsDeviceRegistration  
    ```  
  
2.  Wiederholen Sie diesen Schrittauf jedem Verbundserverproxy-Farmknoten in der AD FS-Farm.  
  
## <a name="enable-seamless-second-factor-authentication"></a>Aktivieren, die eine nahtlose zweistufige Authentifizierung  
Nahtlose zweistufige Authentifizierung ist eine Verbesserung in AD FS, die ein höheres Maß an Zugriffsschutz auf Unternehmensressourcen und Anwendungen von externen Geräten, die versuchen bietet, darauf zuzugreifen. Bei ein persönliches Gerät dem Arbeitsplatz verbunden sind, wird eine "bekannten" Gerät und Administratoren können mithilfe dieser Informationen um bedingten Zugriff und erhalten Sie Zugriff auf Ressourcen zu steuern.  
  
#### <a name="to-enable-seamless-second-factor-authentication-persistent-single-sign-on-sso-and-conditional-access-for-workplace-joined-devices"></a>So aktivieren Sie die nahtlose zweistufige Authentifizierung, permanente einzelne Standardparameter auf \(SSO\) und bedingten Zugriff für Geräte mit dem Arbeitsplatz verbunden sind  
  
1.  Wechseln Sie in der AD FS-Verwaltungskonsole zu Authentifizierungsrichtlinien. Wählen Sie globale primäre Authentifizierung bearbeiten. Wählen Sie das Kontrollkästchen neben Geräteauthentifizierung aktivieren, und klicken Sie dann auf OK.  
  
## <a name="update-the-web-application-proxy-configuration"></a>Aktualisieren Sie die Web Application Proxy-Konfiguration  
  
> [!IMPORTANT]  
> Sie müssen nicht den Geräteregistrierungsdienst in the Web Application Proxy veröffentlichen.  Der Device Registration Service werden über das Web Application Proxy verfügbar, sobald er auf einem Verbundserver aktiviert ist.  Sie müssen zum Abschließen dieses Verfahren, um die Web Application Proxy-Konfiguration zu aktualisieren, wenn sie vor dem Aktivieren des Geräteregistrierungsdiensts bereitgestellt wurde.  
  
#### <a name="to-update-the-web-application-proxy-configuration"></a>Aktualisieren Sie die Konfiguration von Web Application Proxy  
  
1.  Öffnen Sie auf Ihrem Server Web Application Proxy eine Windows PowerShell-Befehlsfenster, und geben  
  
    ```  
    Update-WebApplicationProxyDeviceRegistration  
    ```  
  
2.  Wenn Sie zur Eingabe von Anmeldeinformationen aufgefordert werden, geben Sie die Anmeldeinformationen eines Kontos, das über Administratorrechte auf Ihren Verbundserver verfügt.  
  
## <a name="see-also"></a>Siehe auch 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server2012 R2 ADFS-Bereitstellungshandbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

