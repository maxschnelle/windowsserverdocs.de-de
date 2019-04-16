---
ms.assetid: ddfbbda3-30ca-4537-af12-667efc6f63ff
title: "Konfigurieren Sie zusätzlicher Authentifizierungsmethoden für AD FS"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 65baa6f94e1efa1fa337eab477b18f947cf0bb2d
ms.sourcegitcommit: 36d7b1dfd7da8e9f303d007a628e76149de000f2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
---
# <a name="configure-additional-authentication-methods-for-ad-fs"></a>Konfigurieren Sie zusätzlicher Authentifizierungsmethoden für AD FS

>Gilt für: Windows Server 2016, Windows Server2012 R2

Um Multi-Factor Authentication (MFA) zu aktivieren, müssen Sie mindestens eine zusätzliche Authentifizierungsmethode auswählen. In der Standardeinstellung können in Active Directory-Verbunddienste (AD FS) in Windows Server2012 R2 Sie Zertifikatauthentifizierung (anders ausgedrückt, Smartcard-basierte Authentifizierung) als zusätzliche Authentifizierungsmethode auswählen.

> [!NOTE]
> Wenn Sie zertifikatbasierte Authentifizierung auswählen, stellen Sie sicher, dass die Smartcard-Zertifikate sicher bereitgestellt wurden und Pin-Anforderungen.

Wussten Sie, dass Microsoft Azure bietet eine ähnliche Funktionalität in der Cloud? Erfahren Sie mehr über [Microsoft Azure-identitätslösungen ](http://aka.ms/m2w274).<br /><br />Erstellen einer hybrididentitätslösung in Microsoft Azure:<br /> - [Enthält Informationen Sie zu Azure Multi-Factor Authentication.](http://aka.ms/ey6o9r)<br /> - [Verwalten von Identitäten für Gesamtstruktur-hybridumgebungen mit Cloud-Authentifizierung.](http://aka.ms/g1jat8)<br /> - [Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen.](http://aka.ms/kt1bbm)|

## <a name="microsoft-and-third-party-additional-authentication-methods"></a>Zusätzliche Authentifizierungsmethoden von Microsoft und Drittanbietern
Sie können auch konfigurieren und Aktivieren von Microsoft und Drittanbieter-Authentifizierungsmethoden in AD FS unter Windows Server2012 R2. Nach der Installation und mit AD FS registriert sind, können Sie als Teil der globalen oder pro-nutzen-Partei Authentifizierungsrichtlinie MFA erzwingen.

Unten ist eine alphabetische Liste von Microsoft und Drittanbietern MFA-Angebote für AD FS unter Windows Server2012 R2 derzeit verfügbar.

||||
|-|-|-|
|**Anbieter**|**Angebot**|**Weitere Informationen zu verknüpfen**|
|Gemalto|Gemalto Identitäts- & Sicherheitsdienste|[http://www.gemalto.com/identity](http://www.gemalto.com/identity)|
|InWebo Technologien|InWebo Enterprise Authentication-Dienst|[InWebo Enterprise Authentication](http://www.inwebo.com)|
|Melden Sie sich Personen|Melden Sie sich Personen MFA-API-Connector für AD FS 2012 R2 (öffentliche Betaversion)|[https://www.loginpeople.com](https://www.loginpeople.com)|
|Microsoft Corporation|Microsoft Azure MFA|[Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](https://technet.microsoft.com/library/dn280946.aspx) (siehe Schritt3)|
|RSA, der Security Division von EMC|RSA SecurID Authentication Agent für Microsoft Active Directory-Verbunddienste|[RSA SecurID Authentication Agent für Microsoft Active Directory-Verbunddienste](http://www.emc.com/security/rsa-securid/rsa-authentication-agents/microsoft-ad-fs.htm)|
|SafeNet, Inc.|SafeNet Authentifizierung (SAS)-Dienst-Agent für AD FS|[SafeNet Authentifizierungsdienst: AD FS-Agent-Konfiguration Anleitung](http://www.safenet-inc.com/resources/integration-guide/data-protection/Safenet_Authentication_Service/SafeNet_Authentication_Service__AD_FS_Agent_Configuration_Guide/?langtype=1033)|
|Swisscom|Mobile-ID-Authentifizierungsdienst und Signaturdienste|[Mobile-ID-Authentifizierungsdienst](http://swisscom.ch/mid)|
|Symantec|Symantec-Überprüfung und ID-Schutzdienst (VIP)|[Symantec-Überprüfung und ID-Schutzdienst (VIP)](http://www.symantec.com/vip-authentication-service)|

## <a name="custom-authentication-method-for-ad-fs-in-windows-server-2012-r2"></a>Benutzerdefinierte Authentifizierungsmethode für AD FS unter Windows Server2012 R2
Wir bieten nun Anweisungen zum Erstellen Ihrer eigenen benutzerdefinierten Authentifizierungsmethode für AD FS unter Windows Server2012 R2. Weitere Informationen finden Sie unter [Erstellen einer benutzerdefinierten Authentifizierungsmethode für AD FS unter Windows Server2012 R2](https://go.microsoft.com/fwlink/?LinkID=511980).

## <a name="see-also"></a>Siehe auch
[Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)


