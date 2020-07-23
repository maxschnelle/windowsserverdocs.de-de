---
ms.assetid: fdd1c1fd-55aa-4eb8-ae84-53f811de042c
title: Konfigurieren eines Verbundservers mit dem Geräteregistrierungsdienst
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 7e9634cff6f8bf92dcc556914b72657142f9a25e
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966032"
---
# <a name="configure-a-federation-server-with-device-registration-service"></a>Konfigurieren eines Verbundservers mit dem Geräteregistrierungsdienst

Sie können den Geräte Registrierungsdienst \( DRS \) auf dem Verbund Server aktivieren, nachdem Sie die Verfahren in [Schritt 4: Konfigurieren eines Verbund Servers](/previous-versions/orphan-topics/ws.11/dn303424(v=ws.11))ausgeführt haben. Der Geräte Registrierungsdienst bietet einen Onboarding-Mechanismus für die nahtlose zweistufige Authentifizierung, das permanente einmalige Anmelden ( \- \( SSO) und den \) bedingten Zugriff auf Kunden, die Zugriff auf Unternehmensressourcen benötigen. Weitere Informationen zu DRS finden [Sie unter Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md) .  
  
## <a name="prepare-your-active-directory-forest-to-support-devices"></a>Vorbereiten der Active Directory-Gesamtstruktur für die Unterstützung von Geräten  
  
> [!NOTE]  
> Dies ist ein einmal \- Vorgang, den Sie ausführen müssen, um Ihre Active Directory-Gesamtstruktur auf die Unterstützung von Geräten vorzubereiten. Sie müssen mit der Berechtigung "Unternehmensadministrator" angemeldet sein, und Ihre Active Directory-Gesamtstruktur muss über das Windows Server 2012 R2-Schema verfügen, damit dieses Verfahren abgeschlossen werden kann.  
>   
> Darüber hinaus erfordert DRS, dass Sie mindestens einen globalen Katalogserver in der Stamm Domäne der Gesamtstruktur haben. Der globale Katalogserver ist erforderlich, um die Initialisierung von \- addeviceregistration und während der AD FS Authentifizierung auszuführen. AD FS Initialisiert eine in- \- Memory-Darstellung des DRS-Konfigurations Objekts für jede Authentifizierungsanforderung, und wenn das DRS-Konfigurationsobjekt auf einem Domänen Controller in der aktuellen Domäne nicht gefunden werden kann, wird die Anforderung für die GC versucht, auf der die DRS-Objekte während der Initialisierung der \- addeviceregistration bereitgestellt wurden.  
  
#### <a name="to-prepare-the-active-directory-forest"></a>So bereiten Sie die Active Directory Gesamtstruktur vor  
  
1.  Öffnen Sie auf Ihrem Verbundserver ein Windows PowerShell-Befehlsfenster, und geben Sie dann Folgendes ein:  
  
    ```  
    Initialize-ADDeviceRegistration  
    ```  
  
2.  Wenn Sie aufgefordert werden, den ServiceAccountName einzugeben, geben Sie den Namen des Dienstkontos ein, das Sie als Dienstkonto für AD FS ausgewählt haben.  Wenn es sich um ein GMSA-Konto handelt, geben Sie das Konto im Format ** \\ Accountname $ der Domäne** ein. Verwenden Sie für ein Domänen Konto das Format **Domäne \\ Accountname**.  
  
## <a name="enable-device-registration-service-on-a-federation-server-farm-node"></a>Aktivieren des Geräte Registrierungs Dienstanbieter auf einem Knoten der Verbund Serverfarm  
  
> [!NOTE]  
> Sie müssen mit Domänen Administrator Berechtigungen angemeldet sein, um dieses Verfahren abzuschließen.  
  
#### <a name="to-enable-device-registration-service"></a>So aktivieren Sie den Geräte Registrierungsdienst  
  
1.  Öffnen Sie auf Ihrem Verbundserver ein Windows PowerShell-Befehlsfenster, und geben Sie dann Folgendes ein:  
  
    ```  
    Enable-AdfsDeviceRegistration  
    ```  
  
2.  Wiederholen Sie diesen Schritt für jeden Verbund Farm Knoten in Ihrer AD FS Farm.  
  
## <a name="enable-seamless-second-factor-authentication"></a>Aktivieren der nahtlosen zweistufigen Authentifizierung  
Die nahtlose zweistufige Authentifizierung ist eine Erweiterung in AD FS, die ein zusätzliches Maß an Zugriffsschutz für Unternehmensressourcen und-Anwendungen von externen Geräten bereitstellt, die versuchen, auf diese zuzugreifen. Wenn ein persönliches Gerät mit dem Arbeitsplatz verbunden ist, wird es zu einem bekannten Gerät, und Administratoren können diese Informationen verwenden, um den bedingten Zugriff zu fördern und den Zugriff auf Ressourcen zu steuern.  
  
#### <a name="to-enable-seamless-second-factor-authentication-persistent-single-sign-on-sso-and-conditional-access-for-workplace-joined-devices"></a>So aktivieren Sie die nahtlose zweistufige Authentifizierung, das permanente einmalige Anmelden ( \- \( SSO) und den \) bedingten Zugriff für mit dem Arbeitsplatz verbundene Geräte  
  
1.  Navigieren Sie in der AD FS-Verwaltungskonsole zu Authentifizierungs Richtlinien. Wählen Sie Globale primäre Authentifizierung bearbeiten aus. Aktivieren Sie das Kontrollkästchen neben Geräteauthentifizierung aktivieren, und klicken Sie dann auf OK.  
  
## <a name="update-the-web-application-proxy-configuration"></a>Aktualisieren der webanwendungsproxy-Konfiguration  
  
> [!IMPORTANT]  
> Sie müssen den Geräte Registrierungsdienst nicht auf dem webanwendungsproxy veröffentlichen.  Der Geräte Registrierungsdienst wird über den webanwendungsproxy verfügbar sein, sobald er auf einem Verbund Server aktiviert ist.  Möglicherweise müssen Sie dieses Verfahren ausführen, um die webanwendungsproxy-Konfiguration zu aktualisieren, wenn Sie vor dem Aktivieren des Geräte Registrierungs Diensts bereitgestellt wurde.  
  
#### <a name="to-update-the-web-application-proxy-configuration"></a>So aktualisieren Sie die webanwendungsproxy-Konfiguration  
  
1.  Öffnen Sie auf dem webanwendungsproxy-Server ein Windows PowerShell-Befehlsfenster, und geben Sie  
  
    ```  
    Update-WebApplicationProxyDeviceRegistration  
    ```  
  
2.  Wenn Sie zur Eingabe von Anmelde Informationen aufgefordert werden, geben Sie die Anmelde Informationen eines Kontos ein, das über Administratorrechte für die Verbund Server verfügt  
  
## <a name="see-also"></a>Weitere Informationen 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Bereitstellungshandbuch für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  
