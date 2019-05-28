---
ms.assetid: fdd1c1fd-55aa-4eb8-ae84-53f811de042c
title: Konfigurieren eines Verbundservers mit dem Geräteregistrierungsdienst
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f1367f03ea8a9ba96bfe4bae1c324deff92576f0
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192260"
---
# <a name="configure-a-federation-server-with-device-registration-service"></a>Konfigurieren eines Verbundservers mit dem Geräteregistrierungsdienst

Sie können Device Registration Service \(DRS\) auf dem Verbundserver, die nach der Durchführung der Verfahren in [Schritt 4: Konfigurieren eines Verbundservers](https://technet.microsoft.com/library/dn303424.aspx). Der Device Registration Service bietet einen Onboarding-Mechanismus für die nahtlose-Factor Authentication, persistente einmaliges Anmelden\-auf \(SSO\), und den bedingten Zugriff für Kunden, die Zugriff auf die Unternehmensressourcen benötigen. Ressourcen zu. Weitere Informationen zu DRS finden Sie unter [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose Second Factor Authentication Across Company Applications](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)  
  
## <a name="prepare-your-active-directory-forest-to-support-devices"></a>Vorbereiten der Active Directory-Gesamtstruktur zur Unterstützung von Geräten  
  
> [!NOTE]  
> Dies ist eine\-Zeit Vorgang, die Sie ausführen müssen, um Active Directory-Gesamtstrukturen zur Unterstützung von Geräten vorzubereiten. Sie müssen mit Enterprise-Administratorberechtigungen angemeldet sein, und Active Directory-Gesamtstruktur muss das Windows Server 2012 R2-Schema zum Durchführen dieses Verfahrens haben.  
>   
> Darüber hinaus DRS erfordert, dass Sie mindestens ein globaler Katalogserver in der Stammdomäne der Gesamtstruktur verfügen. Der globale Katalogserver ist erforderlich, um die Initialisierung ausführen\-ADDeviceRegistration und während der AD FS-Authentifizierung. AD FS Initialisiert ein in\-Objekt-Memory-Darstellung der DRS-Konfiguration auf allen authentifizierungsanforderungen angegeben und wenn die DRS-Config-Objekt auf einem Domänencontroller in der aktuellen Domäne gefunden werden kann, wird die Anforderung versucht, vor der Garbage Collector auf dem die DRS-Objekte wurden Bei der Initialisierung bereitgestellt\-ADDeviceRegistration.  
  
#### <a name="to-prepare-the-active-directory-forest"></a>Vorbereiten von Active Directory-Gesamtstruktur  
  
1.  Öffnen Sie auf Ihrem Verbundserver ein Windows PowerShell-Befehlsfenster, und geben ein:  
  
    ```  
    Initialize-ADDeviceRegistration  
    ```  
  
2.  Wenn Sie zur ServiceAccountName aufgefordert werden, geben Sie den Namen des Dienstkontos, die Sie als Dienstkonto für AD FS ausgewählt.  Wenn es sich um ein gMSA-Konto handelt, geben Sie das Konto in der **Domäne\\Kontoname$** Format. Verwenden Sie für ein Domänenkonto, das Format **Domäne\\Accountname**.  
  
## <a name="enable-device-registration-service-on-a-federation-server-farm-node"></a>Aktivieren des Geräteregistrierungsdiensts auf einem Federation Serverfarm Knoten  
  
> [!NOTE]  
> Sie müssen mit Domänenadministrator-Berechtigungen zum Durchführen dieses Verfahrens angemeldet sein.  
  
#### <a name="to-enable-device-registration-service"></a>Um Device Registration Service zu aktivieren.  
  
1.  Öffnen Sie auf Ihrem Verbundserver ein Windows PowerShell-Befehlsfenster, und geben ein:  
  
    ```  
    Enable-AdfsDeviceRegistration  
    ```  
  
2.  Wiederholen Sie diesen Schritt für jede Verbund-farmknoten in AD FS-Farm aus...  
  
## <a name="enable-seamless-second-factor-authentication"></a>Aktivieren, die nahtlose zweistufige Authentifizierung  
Nahtlose zweistufige Authentifizierung ist eine Erweiterung im AD FS, die ein höheres Maß an Schutz von Zugriffs auf Unternehmensressourcen und Anwendungen von externen Geräten bereitstellt, die sie zugreifen möchten. Wenn Sie ein Persönliches Gerät dem Arbeitsplatz verknüpft ist, wird er einem "bekannten" Gerät aus, und Administratoren können diese Informationen verwenden, um für den bedingten Zugriff und Steuern des Zugriffs auf Ressourcen.  
  
#### <a name="to-enable-seamless-second-factor-authentication-persistent-single-sign-on-sso-and-conditional-access-for-workplace-joined-devices"></a>Nahtlose zweite aktivieren-Factor Authentication, persistente einmaligen Anmeldung\-auf \(SSO\) und den bedingten Zugriff für Geräte dem Arbeitsplatz beigetretene  
  
1.  Navigieren Sie in der AD FS-Verwaltungskonsole zu Authentifizierungsrichtlinien. Wählen Sie globale primäre Authentifizierung bearbeiten. Wählen Sie das Kontrollkästchen neben der Geräteauthentifizierung aktivieren, und klicken Sie dann auf OK.  
  
## <a name="update-the-web-application-proxy-configuration"></a>Aktualisieren Sie die Web Application Proxy-Konfiguration  
  
> [!IMPORTANT]  
> Sie müssen nicht den Geräteregistrierungsdienst in der Web Application Proxy zu veröffentlichen.  Beim Device Registration Service wird über den Webanwendungsproxy verfügbar sein, sobald er auf einem Verbundserver aktiviert ist.  Sie müssen dieses Verfahren, um die Web Application Proxy-Konfiguration zu aktualisieren, wenn sie vor dem Aktivieren des Geräteregistrierungsdiensts bereitgestellt wurde.  
  
#### <a name="to-update-the-web-application-proxy-configuration"></a>Die Webproxykonfiguration für die Anwendung aktualisieren  
  
1.  Öffnen Sie auf dem Webanwendungsproxy-Server eine Windows PowerShell-Befehlsfenster, und geben  
  
    ```  
    Update-WebApplicationProxyDeviceRegistration  
    ```  
  
2.  Wenn Sie zur Eingabe von Anmeldeinformationen aufgefordert werden, geben Sie die Anmeldeinformationen eines Kontos, das über Administratorrechte auf Ihren Verbundserver verfügt.  
  
## <a name="see-also"></a>Siehe auch 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS-Bereitstellung geführt.](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

