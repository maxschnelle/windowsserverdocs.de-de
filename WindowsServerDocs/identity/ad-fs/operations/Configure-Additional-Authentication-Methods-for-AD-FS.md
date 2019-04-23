---
ms.assetid: ddfbbda3-30ca-4537-af12-667efc6f63ff
title: Konfigurieren zusätzlicher Authentifizierungsmethoden für AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/04/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 73de8908677b3f74651b10c29ef2abe62e484694
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868411"
---
# <a name="configure-additional-authentication-methods-for-ad-fs"></a>Konfigurieren zusätzlicher Authentifizierungsmethoden für AD FS

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Um die mehrstufige Authentifizierung (Multi-Factor Authentication, MFA) zu aktivieren, müssen Sie mindestens eine zusätzliche Authentifizierungsmethode auswählen. In der Standardeinstellung können in Active Directory Federation Services (AD FS) in Windows Server 2012 R2 Sie Zertifikatauthentifizierung (das heißt, Smartcard-basierte Authentifizierung) als zusätzliche Authentifizierungsmethode auswählen.

> [!NOTE]
> Stellen Sie bei Auswahl der Zertifikatauthentifizierung sicher, dass die Smartcard-Zertifikate auf sichere Weise bereitgestellt wurden und PIN-Anforderungen dafür festgelegt wurden.

Wussten Sie, dass Microsoft Azure eine ähnliche Funktionalität in der Cloud bietet? Erfahren Sie mehr zu [Microsoft Azure-Identitätslösungen](http://aka.ms/m2w274).<br /><br />Erstellen einer hybriden Identitätslösung in Microsoft Azure:<br /> - [Informationen Sie zu Azure Multi-Factor Authentication.](http://aka.ms/ey6o9r)<br /> - [Verwalten von Identitäten für einzelstruktur-hybridumgebungen mit Cloud-Authentifizierung.](http://aka.ms/g1jat8)<br /> - [Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen.](http://aka.ms/kt1bbm)

## <a name="microsoft-and-third-party-additional-authentication-methods"></a>Zusätzliche Authentifizierungsmethoden von Microsoft und Drittanbietern
Sie können auch konfigurieren und Aktivieren von Microsoft und Drittanbieter-Authentifizierungsmethoden in AD FS unter Windows Server 2012 R2. Nachdem installiert und registriert mit AD FS, können Sie MFA als Teil der globalen oder pro vertrauenden Authentifizierungsrichtlinie erzwingen.

Nachstehend finden Sie eine alphabetische Liste der MFA-Angebote von Microsoft und Drittanbietern, die derzeit für AD FS in Windows Server 2012 R2 zur Verfügung stehen.

|Anbieter|Angebot|Link mit weiteren Informationen|
|-|-|-| 
|aPersona|aPersona Adaptive Multi-Factor Authentication für Microsoft-ADFS-SSO|[aPersona ASM-AD FS-Adapter](https://www.apersona.com/adfs)|
|Duo-Sicherheit|Duo-MFA-Adapter für AD FS|[Duo-Authentifizierung für AD FS](https://duo.com/docs/adfs)|
|Gemalto|Gemalto Identitäts- & Sicherheitsdienste|[http://www.gemalto.com/identity](http://www.gemalto.com/identity)|
|inWebo Technologies|inWebo Enterprise Authentication-Dienst|[inWebo Enterprise Authentication](http://www.inwebo.com)|
|Login People|Login People MFA-API-Connector für AD FS 2012 R2 (öffentliche Betaversion)|[https://www.loginpeople.com](https://www.loginpeople.com)|
|Microsoft Corp.|Microsoft Azure MFA|[Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher mehrstufiger Authentifizierung für sensible Anwendungen](https://technet.microsoft.com/library/dn280946.aspx) (siehe Schritt 3)|
Mideye | Mideye Authentifizierungsanbieter für AD FS | [Mideye zweistufige Authentifizierung mit Microsoft Active Directory Federation Service](https://www.mideye.com/support/administrators/documentation/integration/microsoft-adfs/)|
|Okta | Okta-MFA für Active Directory-Verbunddienste | [Okta-MFA für Active Directory Federation Services (AD FS)](https://help.okta.com/en/prod/Content/Topics/integrations/adfs-okta-int.htm)|
|Eine Identität| Starling 2FA AD FS|[Starling 2FA AD FS-Adapter](https://www.oneidentity.com/products/starling-two-factor-authentication/)|
|Eine Identität| Defender AD FS|[Defender AD FS-Adapter](https://www.oneidentity.com/products/defender/)|
|Ping Identity|PingID MFA-Adapter für AD FS|[PingID MFA-Adapter für AD FS](https://documentation.pingidentity.com/pingid/pingidAdminGuide/index.shtml#pid_c_PingIDforADFSSSO.html)|
|RSA, The Security Division of EMC|RSA SecurID Authentication Agent for Microsoft Active Directory Federation Services|[RSA SecurID-Authentifizierung-Agent für Microsoft Active Directory-Verbunddienste](http://www.emc.com/security/rsa-securid/rsa-authentication-agents/microsoft-ad-fs.htm)|
|SafeNet, Inc.|SafeNet Authentication Service (SAS) Agent for AD FS|[SafeNet Authentication-Dienst: AD FS Agent Configuration Guide](http://www.safenet-inc.com/resources/integration-guide/data-protection/Safenet_Authentication_Service/SafeNet_Authentication_Service__AD_FS_Agent_Configuration_Guide/?langtype=1033)|
|SecureMFA|SecureMFA OTP Provider| [AD FS, Multi-Factor Authentication-Anbietern](https://www.securemfa.com/)|
|Swisscom|Mobile ID Authentication Service and Signature Services|[Mobile-ID-Authentifizierungsdienst](http://swisscom.ch/mid)|
|Symantec|Symantec Validation and ID Protection Service (VIP)|[Symantec-Überprüfung und ID-Schutzdienst (VIP)](http://www.symantec.com/vip-authentication-service)|
|Trusona|Grundlegende (ohne Kennwort MFA) und Executive (grundlegende + Identität Korrektur)| [Trusona Multi-Factor Authentication](https://www.trusona.com/solution-overview/)|


## <a name="custom-authentication-method-for-ad-fs-in-windows-server-2012-r2"></a>Benutzerdefinierte Authentifizierungsmethode für AD FS in Windows Server 2012 R2
Wir stellen jetzt Informationen zum Erstellen einer eigenen, benutzerdefinierten Authentifizierungsmethode für AD FS in Windows Server 2012 R2 bereit. Weitere Informationen finden Sie unter [Erstellen einer benutzerdefinierten Authentifizierungsmethode für AD FS in Windows Server 2012 R2](https://go.microsoft.com/fwlink/?LinkID=511980).

## <a name="see-also"></a>Siehe auch
[Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)


