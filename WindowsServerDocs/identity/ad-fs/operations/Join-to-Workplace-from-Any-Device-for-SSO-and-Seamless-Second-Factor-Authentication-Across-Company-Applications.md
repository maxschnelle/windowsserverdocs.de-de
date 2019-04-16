---
ms.assetid: e22d84a5-113d-4bec-b484-036ed29f0c28
title: Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 12/05/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4926eb32a0bbffb092ec02ca2508fe97d52d1466
ms.sourcegitcommit: 46439194e5deb0fa5f338b428f95dd6b5b799337
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="join-to-workplace-from-any-device-for-sso-and-seamless-second-factor-authentication-across-company-applications"></a>Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen

>Gilt für: Windows Server 2012 R2

Der rasche Anstieg der Anzahl von endverbrauchergeräten und Informationszugriffs ändert die Art und Weise, dass Personen wir Technologie wahrnehmen. Die ständige Verwendung von Informationstechnologie im Laufe des Tages und der einfache Zugriff auf Informationen, ist die herkömmliche Grenzen zwischen Berufs- und Privatleben weichzeichnen. Grenzen werden von dem glauben begleitet, persönliche Technologie ausgewählt und an Benutzer persönlichkeiten, Aktivitäten und benutzerdefinierte-sollte auf den Arbeitsplatz ausgeweitet. Um die wachsende Anforderung von persönlichen verbrauchergeräten an Unternehmensnetzwerk verbunden sein, zu unterstützen, werden wir die folgenden Wertbeiträge eingeführt:

-   Administratoren können steuern, wer Zugriff auf Unternehmensressourcen hat, die auf die Anwendung, Benutzer, Gerät und Standort basieren.

-   Mitarbeiter können Anwendungen und Daten überall auf jedem Gerät zugreifen. Mitarbeiter können einmaliges Anmelden in Browseranwendungen oder unternehmensanwendungen verwenden.

## <a name="key-concepts-introduced-in-the-solution"></a>Wichtige Konzepte, die in der Lösung eingeführte

### <a name="workplace-join"></a>Arbeitsplatzbeitritt
Mithilfe der Arbeitsplatzbeitritt können Information-Worker ihre persönlichen Geräte mit ihrem Unternehmen geltenden Arbeitsplatz Computer Zugriff auf Unternehmensressourcen und Dienste hinzufügen. Wenn Sie Ihr Persönliches Gerät mit dem Arbeitsplatz verbinden, wird zu einem bekannten Gerät und stellt die nahtlose zweistufige Authentifizierung und einmaliges Anmelden für Arbeitsplatzressourcen und Anwendungen. Wenn ein Gerät über den Arbeitsplatzbeitritt hinzugefügt wird, können Attribute des Geräts aus dem Verzeichnis auf Laufwerk bedingten Zugriff zum Autorisieren der Ausstellung von Sicherheitstoken für Anwendungen abgerufen werden. Windows 8.1 und iOS 6.0 +- sowie Android 4.0 +-Geräte können mithilfe der Arbeitsplatzbeitritt hinzugefügt werden.

### <a name="BKMK_DRS"></a>Azure Active Directory Device Registration service
Arbeitsplatzbeitritt wird durch die Azure Active Directory Device Registration Service ermöglicht. Wenn ein Gerät über den Arbeitsplatzbeitritt hinzugefügt wird, wird der Dienst ein Geräteobjekt in Azure Active Directory bereitstellt und legt dann eine Taste auf dem lokalen Gerät, mit dem die geräteidentität darstellt. Diese geräteidentität kann dann mit Zugriffssteuerungsregeln für Anwendungen verwendet werden, die in der Cloud und lokal gehostet werden.

Weitere Informationen zum Aktivieren von Azure Active Directory Device Registration Service, finden Sie unter [Azure Active Directory Device Registration Service Overview](https://msdn.microsoft.com/6a14cb1f-a058-4453-8ede-d9f4a66a7073.aspx).

### <a name="workplace-join-as-a-seamless-second-factor-authentication"></a>Arbeitsplatzbeitritt als nahtlose Faktor-Authentifizierung
Unternehmen können das Risiko verwalten, das die Zugriff auf Informationen und Governance und Compliance fördern beim Erteilen von Consumer-Geräten Zugriff auf Unternehmensressourcen zugeordnet ist. Arbeitsplatzbeitritt auf Geräte bietet Administratoren die folgenden Funktionen:

-   Identifiziert bekannte Geräte mit Geräteauthentifizierung. Diese Informationen können Administratoren um bedingten Zugriff und Steuerung des Zugriffs auf Ressourcen zu steuern.

-   Bietet eine nahtlosere anmeldeerfahrung für Benutzer von vertrauenswürdigen Geräten auf Unternehmensressourcen zugreifen.

### <a name="single-sign-on"></a>Einmaliges Anmelden
Einmaliges Anmelden (SSO) im Kontext dieses Szenarios ist die Funktionalität, die die Anzahl der Kennwörter eingegeben werden müssen, die der Benutzer zum Zugriff auf Unternehmensressourcen von bekannten Geräten einzugeben, reduziert. Diese Funktion bedeutet, dass Benutzer nur einmal während der Lebensdauer von SSO, den Zugriff auf unternehmensanwendungen und Ressourcen von diesem Gerät aufgefordert werden. Wenn ein Gerät den Arbeitsplatzbeitritt verwendet, erhält der Benutzer, die für die Verwendung des Geräts registriert ist ein beständiges einmaliges Anmelden, werden standardmäßig für sieben Tage. Dieser Benutzer hat eine nahtlose Anmeldung in der gleichen Sitzung oder in neuen Sitzungen.

## <a name="solution-overview"></a>Übersicht über die Lösung
Im Rahmen dieser Lösung erfahren Sie, wie Sie auf einem unterstützten Gerät verwenden Arbeitsplatzbeitritt und einmaliges Anmelden bei einer Unternehmensressource.

> [!NOTE]
> Zur Unterstützung von Windows 8.1, iOS 6.0 +- sowie Android 4.0 +-Geräte müssen Sie Azure Active Directory-Geräteregistrierung zusammen mit Device Zurückschreiben konfigurieren, finden Sie unter [schrittweisen Anleitung für die lokale bedingten Zugriff mithilfe von Azure Active Directory Device Registration Service](https://msdn.microsoft.com/library/azure/dn788908.aspx)

Diese Lösung erfordert führt Sie durch die folgenden Schritte der exemplarischen Vorgehensweise:

1.  [Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem Windows-Gerät](../../ad-fs/operations/Walkthrough--Workplace-Join-with-a-Windows-Device.md)

2.  [Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem iOS-Gerät](../../ad-fs/operations/Walkthrough--Workplace-Join-with-an-iOS-Device.md)

3.  [Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem Android-Gerät](../../ad-fs/operations/walkthrough--workplace-join-to-an-android-device.md)

## <a name="see-also"></a>Siehe auch
[Konfigurieren eines Verbundservers mit Device Registration Service](../deployment/configure-a-federation-server-with-device-registration-service.md)



