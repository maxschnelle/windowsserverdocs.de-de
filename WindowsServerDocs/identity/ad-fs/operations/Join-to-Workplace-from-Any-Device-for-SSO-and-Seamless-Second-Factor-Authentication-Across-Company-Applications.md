---
ms.assetid: e22d84a5-113d-4bec-b484-036ed29f0c28
title: Arbeitsplatzbeitritt von einem beliebigen Gerät für SSO und die nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 12/05/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 05a8b8bb5685c31ece29ed8eb38d37a424e478b8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357936"
---
# <a name="join-to-workplace-from-any-device-for-sso-and-seamless-second-factor-authentication-across-company-applications"></a>Arbeitsplatzbeitritt von einem beliebigen Gerät für SSO und die nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen



Der rasche Anstieg der Anzahl von Verbrauchergeräten und des universellen Informationszugriffs ändert die Art und Weise, in der wir Technologie wahrnehmen. Die ständige Verwendung von Informationstechnologie im Laufe des Tages und der einfache Zugriff auf Informationen lassen die herkömmlichen Grenzen zwischen Berufs- und Privatleben verschwimmen. Diese Verschiebungs Grenzen werden von einem Glauben begleitet, dass persönliche Technologie ausgewählt und an die Benutzer-, Aktivitäten und Zeitpläne angepasst werden muss. Um die wachsende Anforderung einer Anbindung von persönlichen Verbrauchergeräten an Unternehmensnetzwerke zu erfüllen, werden die zwei folgenden Wertbeiträge eingeführt:

-   Administratoren können steuern, wer Zugriff auf Unternehmensressourcen hat, die auf Anwendungen, Benutzer, Geräte und Standorte basieren.

-   Mitarbeiter können überall mit jedem Gerät auf Anwendungen und Daten zugreifen. Mitarbeiter können das einmalige Anmelden in Browseranwendungen oder Unternehmensanwendungen verwenden.

## <a name="key-concepts-introduced-in-the-solution"></a>Wichtige in der Lösung eingeführte Konzepte

### <a name="workplace-join"></a>Arbeitsplatzbeitritt
Mit der Verwendung des Arbeitsplatzbeitritts können Information-Worker ihre persönlichen Geräte zu den Arbeitsplatzcomputern ihres Unternehmens hinzufügen, um auf Unternehmensressourcen und -dienste zuzugreifen. Wenn Sie Ihr persönliches Gerät mit dem Arbeitsplatz verbinden, wird es zu einem bekannten Gerät und stellt die nahtlose zweistufige Authentifizierung und ein einmaliges Anmelden für Arbeitsplatzressourcen und -anwendungen bereit. Wenn ein Gerät über den Arbeitsplatzbeitritt hinzugefügt wird, können Attribute des Geräts vom Verzeichnis abgerufen werden, um einen bedingten Zugriff für den Zweck der autorisierenden Ausstellung von Sicherheitstoken für Anwendungen zu fördern. Durch Arbeitsplatzbeitritt können Windows 8.1-, iOS 6.0+- sowie Android 4.0+-Geräte zusammengeführt werden.

### <a name="BKMK_DRS"></a>Azure Active Directory Device Registration-Dienst
Arbeitsplatzbeitritt wird durch den Azure Active Directory-Geräteregistrierungsdienst ermöglicht. Wenn ein Gerät über den Arbeitsplatzbeitritt hinzugefügt wird, stellt der Dienst ein Geräteobjekt in Azure Active Directory bereit und legt einen Schlüssel auf dem lokalen Gerät fest, der die Geräteidentität darstellt. Diese Geräteidentität kann dann mit Zugriffssteuerungsregeln für Anwendungen verwendet werden, die in der Cloud und lokal gehostet werden.

Weitere Informationen finden Sie unter [Einführung in die Geräteverwaltung in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction).

### <a name="workplace-join-as-a-seamless-second-factor-authentication"></a>Arbeitsplatzbeitritt als nahtlose zweistufige Authentifizierung
Unternehmen können das mit dem Informationszugriff verbundene Risiko verwalten und Governance und Compliance fördern, gleichzeitig aber Verbrauchergeräten Zugriff auf Unternehmensressourcen gewähren. Der Arbeitsplatzbeitritt auf Geräte bietet Administratoren die folgenden Funktionen:

-   Identifiziert bekannte Geräte mit Geräteauthentifizierung. Administratoren können diese Informationen verwenden, um einen bedingten Zugriff zu fördern und den Zugriff auf Ressourcen zu steuern.

-   Bietet eine nahtlosere Anmeldeerfahrung für Benutzer, um von vertrauenswürdigen Geräten auf Unternehmensressourcen zuzugreifen.

### <a name="single-sign-on"></a>Einmaliges Anmelden
Im Zusammenhang mit diesem Szenario ist das einmalige Anmelden (Single Sign-On, SSO) die Funktion, mit der die Anzahl von Kennworteingabeaufforderungen reduziert wird, bei denen der Benutzer ein Kennwort eingeben muss, um von bekannten Geräten auf Unternehmensressourcen zuzugreifen. Diese Funktion bedeutet, dass Benutzer während der SSO-Lebensdauer nur einmal aufgefordert werden, um von diesem Gerät auf Anwendungen und Ressourcen des Unternehmens zuzugreifen. Wenn ein Gerät den Arbeitsplatzbeitritt verwendet, erhält der Benutzer, der für die Verwendung des Geräts registriert ist, standardmäßig für sieben ein beständiges einmaliges Anmelden. Dieser Benutzer hat eine nahtlose Anmeldeerfahrung in derselben oder in neuen Sitzungen.

## <a name="solution-overview"></a>Lösungsübersicht
Als Teil dieser Lösung erfahren Sie, wie Sie den Arbeitsplatzbeitritt auf einem unterstützten Gerät verwenden und einmaliges Anmelden bei einer Unternehmensressource nutzen.

> [!NOTE]
> Zur Unterstützung von Windows 8.1-, iOS 6.0+- und Android 4.0+-Geräten MUSS die Azure Active Directory-Geräteregistrierung zusammen mit dem Zurückschreiben von Geräteobjekten konfiguriert werden, wie unter folgendem Link beschrieben: [Step-by-Step Guide for On-premises Conditional Access using Azure Active Directory Device Registration Service](https://msdn.microsoft.com/library/azure/dn788908.aspx)

In den folgenden Lösungshandbüchern finden Sie die einzelnen Schritte für die exemplarische Vorgehensweise:

1.  [Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem Windows-Gerät](../../ad-fs/operations/Walkthrough--Workplace-Join-with-a-Windows-Device.md)

2.  [Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem iOS-Gerät](../../ad-fs/operations/Walkthrough--Workplace-Join-with-an-iOS-Device.md)

3.  [Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem Android-Gerät](../../ad-fs/operations/walkthrough--workplace-join-to-an-android-device.md)

## <a name="see-also"></a>Siehe auch
[Konfigurieren eines Verbund Servers mit dem Geräte Registrierungsdienst](../deployment/configure-a-federation-server-with-device-registration-service.md)



