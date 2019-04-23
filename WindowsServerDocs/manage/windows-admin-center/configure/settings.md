---
title: Einstellungen
description: Informationen Sie zu Einstellungen in Windows Admin Center (Projekt Honolulu). Benutzereinstellungen können Benutzer ihre Sprache/Region und andere Einstellungen zu ändern. Gateway-Einstellungen können Administratoren, die das Gateway zu konfigurieren.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 1e1231500733f70ddfcbd4f8a847047b73f24a00
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882381"
---
# <a name="settings"></a>Einstellungen

> Gilt für: Windows Admin Center

Einstellungen für Windows Admin Center bestehen aus Benutzer-Ebene und Gateway Einstellungen. Eine Änderung an einer Benutzerebene Einstellung betrifft nur das aktuelle Profil des Benutzers, eine Änderung an einer Gatewayebene Einstellung alle Benutzer auf diesem Windows Admin Center-Gateway.

## <a name="user-settings"></a>Benutzereinstellungen

Auf Benutzerebene Einstellungen bestehen aus den folgenden Abschnitten:

- Konto
- Sprache/Region
- Vorschläge

In der **Konto** Registerkarte Benutzer können die Anmeldeinformationen, die sie der zur Authentifizierung verwendet haben, um Windows Admin Center überprüfen. Wenn Azure AD als Identitätsanbieter konfiguriert ist, kann der Benutzer aus ihrem Azure AD-Konto auf dieser Registerkarte anmelden.

In der **Sprache/Region** Registerkarte, die Benutzer können eine Ändern der Sprache und Region-Formate, die von Windows Admin Center angezeigt.

In der **Vorschläge** Registerkarte Benutzer können Vorschläge für die Azure-Dienste und neue Features ein-oder ausblenden.

### <a name="dark-theme"></a>Dunkles Design

> Gilt für: Windows Admin Center – Vorschau

In Windows Admin Center Preview können Sie einen zusätzlichen Entsperren **Personalisierung** Abschnitt enthält die Möglichkeit, die in einem dunklen Design der Benutzeroberfläche zu wechseln. So aktivieren Sie die **Personalisierung** Geben Sie im Abschnitt ```msft.sme.shell.personalization``` als Experiment Schlüssel.

>[!IMPORTANT]
> Design "dunkel" noch In Bearbeitung ist, führen Sie zu diesem Zeitpunkt nicht Melden von Fehlern.

## <a name="gateway-settings"></a>Gateway-Einstellungen

Einstellungen auf Ebene von Gateway bestehen aus den folgenden Abschnitten:

- Extensions
- Access
- Azure

Nur die gatewayadministratoren können zum Anzeigen und ändern diese Einstellungen zur Verfügung. Änderungen an diesen Einstellungen ändern Sie die Konfiguration des Gateways und betrifft alle Benutzer des Gateways Windows Admin Center.

In der **Erweiterungen** Registerkarte Administratoren installieren, deinstallieren oder Aktualisieren von Gateways Erweiterungen können. [Erfahren Sie mehr über Erweiterungen.](using-extensions.md)

Die **Zugriff** auf der Registerkarte können Administratoren konfigurieren, die das Gateway Windows Admin Center als auch der Identitätsanbieter zur Authentifizierung von Benutzern zugreifen können. [Weitere Informationen zum Steuern des Zugriffs auf das Gateway.](user-access-control.md)

Von der **Azure** Registerkarte Administratoren können registrieren das Gateway in Azure zu ermöglichen [Azure-Integrationsfeatures kennen](azure-integration.md) in Windows Admin Center.