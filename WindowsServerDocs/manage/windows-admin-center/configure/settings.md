---
title: Einstellungen
description: Weitere Informationen zu Einstellungen finden Sie im Windows Admin Center (Project Honolulu). Benutzereinstellungen ermöglichen es Benutzern, Ihre Sprache/Region und andere Einstellungen zu ändern. Mit den Gatewayeinstellungen können Administratoren das Gateway konfigurieren.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 04/12/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: e0fd6618f275058d4e22fe9abb9e484d4752ac9a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407054"
---
# <a name="windows-admin-center-settings"></a>Windows Admin Center-Einstellungen

> Gilt für: Windows Admin Center

Die Einstellungen des Windows Admin Centers bestehen aus Einstellungen auf Benutzer-und Gatewayebene. Eine Änderung an einer Einstellung auf Benutzerebene wirkt sich nur auf das Profil des aktuellen Benutzers aus, während eine Änderung an einer Einstellung auf Gatewayebene alle Benutzer dieses Windows Admin Center-Gateways betrifft.

## <a name="user-settings"></a>Benutzereinstellungen

Die Einstellungen auf Benutzerebene bestehen aus den folgenden Abschnitten:

- Konto
- Personalization
- Sprache/Region
- Vorschläge
- Erweitert

Auf der Registerkarte **Konto** können Benutzer die Anmelde Informationen überprüfen, die Sie für die Authentifizierung beim Windows Admin Center verwendet haben. Wenn Azure AD als Identitäts Anbieter konfiguriert ist, kann sich der Benutzer von seinem Azure AD Konto auf dieser Registerkarte abmelden.

Auf der Registerkarte **Personalisierung** können Benutzer zu einem dunklen UI-Design wechseln.

Auf der Registerkarte **Sprache/Region** können Benutzer die von Windows Admin Center angezeigten sprach-und Regions Formate ändern.

Auf der Registerkarte **Vorschläge** können Benutzer Vorschläge zu Azure-Diensten und neuen Features umschalten.

Die Registerkarte **erweitert** bietet Entwicklern Windows Admin Center-Erweiterungen zusätzliche Funktionen.

## <a name="gateway-settings"></a>Gatewayeinstellungen

Einstellungen auf Gatewayebene bestehen aus den folgenden Abschnitten:

- Extensions
- Zugriff
- Azure
- Freigegebene Verbindungen

Diese Einstellungen können nur von gatewayadministratoren angezeigt und geändert werden. Änderungen an diesen Einstellungen ändern die Konfiguration des Gateways und wirken sich auf alle Benutzer des Windows Admin Center-Gateways aus.

Auf der Registerkarte **Erweiterungen** können Administratoren gatewayerweiterungen installieren, deinstallieren oder aktualisieren. [Erfahren Sie mehr über Erweiterungen.](using-extensions.md)

Auf der Registerkarte " **Zugriff** " können Administratoren konfigurieren, wer auf das Windows Admin Center-Gateway zugreifen kann, sowie den Identitäts Anbieter, der zum Authentifizieren von Benutzern verwendet wird. [Erfahren Sie mehr über das Steuern des Zugriffs auf das Gateway.](user-access-control.md)

Auf der Registerkarte **Azure** können Administratoren das Gateway bei Azure registrieren, um die [Azure-Integrations Features](azure-integration.md) im Windows Admin Center zu aktivieren.

Mithilfe der Registerkarte frei **gegebene Verbindungen** können Administratoren eine einzelne Liste von Verbindungen konfigurieren, die für alle Benutzer des Windows Admin Center-Gateways freigegeben werden. [Erfahren Sie mehr über das einmalige Konfigurieren von Verbindungen für alle Benutzer eines Gateways.](shared-connections.md)