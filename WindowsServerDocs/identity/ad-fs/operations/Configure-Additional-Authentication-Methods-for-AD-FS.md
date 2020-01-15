---
ms.assetid: ddfbbda3-30ca-4537-af12-667efc6f63ff
title: Configure Additional Authentication Methods for AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/26/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 89a1f745e1e928a5e5bd79adb94e41fd9da399d9
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75948545"
---
# <a name="configure-additional-authentication-methods-for-ad-fs"></a>Configure Additional Authentication Methods for AD FS

Um die mehrstufige Authentifizierung (Multi-Factor Authentication, MFA) zu aktivieren, müssen Sie mindestens eine zusätzliche Authentifizierungsmethode auswählen. Standardmäßig können Sie in Active Directory-Verbunddienste (AD FS) (AD FS) in Windows Server 2012 R2 eine Zertifikat Authentifizierung (anders ausgedrückt: smartcardbasierte Authentifizierung) als zusätzliche Authentifizierungsmethode auswählen.

> [!NOTE]
> Stellen Sie bei Auswahl der Zertifikatauthentifizierung sicher, dass die Smartcard-Zertifikate auf sichere Weise bereitgestellt wurden und PIN-Anforderungen dafür festgelegt wurden.

Wussten Sie, dass Microsoft Azure bietet eine ähnliche Funktionalität in die Cloud? Erfahren Sie mehr zu [Microsoft Azure-Identitätslösungen](https://aka.ms/m2w274).<br /><br />Erstellen einer Hybrididentitätslösung in Microsoft Azure:<br /> - [erfahren Sie mehr über Azure Multi-Factor Authentication.](https://aka.ms/ey6o9r)<br /> - [Verwalten von Identitäten für Hybrid Umgebungen mit einer einzelnen Gesamtstruktur mithilfe der cloudauthentifizierung.](https://aka.ms/g1jat8)<br /> - [Verwaltung von Risiken mit zusätzlichen Multi-Factor Authentication für sensible Anwendungen.](https://aka.ms/kt1bbm)

## <a name="microsoft-and-third-party-additional-authentication-methods"></a>Zusätzliche Authentifizierungsmethoden von Microsoft und Drittanbietern
Sie können auch Authentifizierungsmethoden von Microsoft und Drittanbietern in AD FS in Windows Server 2012 R2 konfigurieren und aktivieren. Nach der Installation und Registrierung bei AD FS können Sie MFA als Teil der globalen oder pro Authentifizierungs Richtlinie für die vertrauende Seite erzwingen.

Nachstehend finden Sie eine alphabetische Liste der MFA-Angebote von Microsoft und Drittanbietern, die derzeit für AD FS in Windows Server 2012 R2 zur Verfügung stehen.

|Anbieter|Angebot|Link mit weiteren Informationen|
|-|-|-| 
|apersona|apersona Adaptive Multi-Factor Authentication für Microsoft ADFS SSO|[apersona ASM-ADFS-Adapter](https://www.apersona.com/adfs)|
|Duo Security|Duo-MFA-Adapter für AD FS|[Duo-Authentifizierung für AD FS](https://duo.com/docs/adfs)|
|Futurae|"Futurae Authentication Suite" für AD FS|[Sichere futurae-Authentifizierung](https://futurae.com)|
|Gemalto|Gemalto Identitäts- & Sicherheitsdienste|[http://www.gemalto.com/identity](http://www.gemalto.com/identity)|
|inWebo Technologies|inWebo Enterprise Authentication-Dienst|[inwebo Enterprise-Authentifizierung](http://www.inwebo.com)|
|Login People|Login People MFA-API-Connector für AD FS 2012 R2 (öffentliche Betaversion)|[https://www.loginpeople.com](https://www.loginpeople.com)|
|Microsoft Corp.|Microsoft Azure MFA|[Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher mehrstufiger Authentifizierung für sensible Anwendungen](https://technet.microsoft.com/library/dn280946.aspx) (siehe Schritt 3)|
Mide | Mide Ye-Authentifizierungs Anbieter für ADFS | [Die zweistufige Authentifizierung mit Microsoft Active Directory Verbunddienst](https://www.mideye.com/support/administrators/documentation/integration/microsoft-adfs/)|
|Okta | Okta MFA für Active Directory-Verbunddienste (AD FS) | [Okta MFA für Active Directory-Verbunddienste (AD FS) (ADFS)](https://help.okta.com/en/prod/Content/Topics/integrations/adfs-okta-int.htm)|
|One Identity| Starte 2FA-AD FS|[Starte 2FA-AD FS Adapter](https://www.oneidentity.com/products/starling-two-factor-authentication/)|
|One Identity| Defender-AD FS|[Defender AD FS-Adapter](https://www.oneidentity.com/products/defender/)|
|Ping Identity|Pgid-MFA-Adapter für AD FS|[Pgid-MFA-Adapter für AD FS](https://documentation.pingidentity.com/pingid/pingidAdminGuide/index.shtml#pid_c_PingIDforADFSSSO.html)|
|RSA, The Security Division of EMC|RSA SecurID Authentication Agent for Microsoft Active Directory Federation Services|[RSA SecurID Authentication Agent für Microsoft Active Directory-Verbunddienste (AD FS)](http://www.emc.com/security/rsa-securid/rsa-authentication-agents/microsoft-ad-fs.htm)|
|SafeNet, Inc.|SafeNet Authentication Service (SAS) Agent for AD FS|[SafeNet-Authentifizierungsdienst: Konfigurations Handbuch für AD FS-Agent](http://www.safenet-inc.com/resources/integration-guide/data-protection/Safenet_Authentication_Service/SafeNet_Authentication_Service__AD_FS_Agent_Configuration_Guide/?langtype=1033)|
|Securemfa|Securemfa OTP-Anbieter| [AD FS-Anbieter für Multi-Factor Authentication](https://www.securemfa.com/)|
|Swisscom|Mobile ID Authentication Service and Signature Services|[Dienst für die Mobile ID-Authentifizierung](http://swisscom.ch/mid)|
|Symantec|Symantec Validation and ID Protection Service (VIP)|[Symantec-Validierung und ID-Schutzdienst (VIP)](http://www.symantec.com/vip-authentication-service)|
|Trusona|Unverzichtbar (passuneless MFA) und Executive (unverzichtbar + Identitätsnachweis)| [Trusona Multi-Factor Authentication](https://www.trusona.com/solution-overview/)|


## <a name="custom-authentication-method-for-ad-fs-in-windows-server-2012-r2"></a>Benutzerdefinierte Authentifizierungsmethode für AD FS in Windows Server 2012 R2
Wir stellen jetzt Informationen zum Erstellen einer eigenen, benutzerdefinierten Authentifizierungsmethode für AD FS in Windows Server 2012 R2 bereit. Weitere Informationen finden Sie unter [Erstellen einer benutzerdefinierten Authentifizierungsmethode für AD FS in Windows Server 2012 R2](https://go.microsoft.com/fwlink/?LinkID=511980).

## <a name="see-also"></a>Siehe auch
[Verwalten von Risiken mit zusätzlicher mehrstufiger Authentifizierung für sensible Anwendungen](Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)


