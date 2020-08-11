---
title: Settings
description: Weitere Informationen zu Einstellungen im Windows Admin Center (Projekt Honolulu). Mit den Benutzereinstellungen können Benutzer ihre Sprache/Region und andere Einstellungen ändern. Mit den Gatewayeinstellungen können Administratoren das Gateway konfigurieren.
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 04/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: ff06a19d85858b8332412a51c029c9aeeba2af50
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997442"
---
# <a name="windows-admin-center-settings"></a>Windows Admin Center – Einstellungen

> Gilt für: Windows Admin Center

Die Einstellungen im Windows Admin Centers umfassen Einstellungen auf Benutzer- und Gatewayebene. Eine Änderung einer Einstellung auf Benutzerebene wirkt sich nur auf das Profil des aktuellen Benutzers aus, während eine Änderung an einer Einstellung auf Gatewayebene alle Benutzer dieses Windows Admin Center-Gateways betrifft.

## <a name="user-settings"></a>Benutzereinstellungen

Die Einstellungen auf Benutzerebene umfassen die folgenden Abschnitte:

- Konto
- Personalization
- Sprache/Region
- Vorschläge
- Erweitert

Auf der Registerkarte **Konto** können Benutzer die Anmeldeinformationen überprüfen, die sie für die Authentifizierung beim Windows Admin Center verwendet haben. Wenn Azure AD als Identitätsanbieter konfiguriert ist, kann sich der Benutzer auf dieser Registerkarte von seinem Azure AD-Konto abmelden.

Auf der Registerkarte **Personalisierung** können Benutzer zu einem dunklen Benutzeroberflächendesign wechseln.

Auf der Registerkarte **Sprache/Region** können Benutzer die im Windows Admin Center angezeigten Sprach- und Regionsformate ändern.

Auf der Registerkarte **Vorschläge** können Benutzer Vorschläge zu Azure-Diensten und neuen Features umschalten.

Die Registerkarte **Erweitert** stellt Entwicklern von Erweiterungen für das Windows Admin Center zusätzliche Funktionen zur Verfügung.

## <a name="gateway-settings"></a>Gatewayeinstellungen

Die Einstellungen auf Gatewayebene umfassen die folgenden Abschnitte:

- Extensions
- Access
- Azure
- Gemeinsam genutzte Verbindungen

Diese Einstellungen können nur von Gatewayadministratoren angezeigt und geändert werden. Änderungen an diesen Einstellungen ändern die Konfiguration des Gateways und wirken sich auf alle Benutzer des Windows Admin Center-Gateways aus.

Auf der Registerkarte **Erweiterungen** können Administratoren Gatewayerweiterungen installieren, deinstallieren oder aktualisieren. [Weitere Informationen zu Erweiterungen.](using-extensions.md)

Auf der Registerkarte **Zugriff** können Administratoren konfigurieren, wer auf das Windows Admin Center-Gateway zugreifen kann und welcher Identitätsanbieter zum Authentifizieren von Benutzern verwendet wird. [Erfahren Sie mehr über das Steuern des Zugriffs auf das Gateway.](user-access-control.md)

Auf der Registerkarte **Azure** können Administratoren das Gateway bei Azure registrieren, um [Azure-Integrationsfeatures](../azure/azure-integration.md) im Windows Admin Center zu aktivieren.

Mithilfe der Registerkarte **Gemeinsam genutzte Verbindungen** können Administratoren eine Liste von Verbindungen konfigurieren, die für alle Benutzer des Windows Admin Center-Gateways freigegeben werden. [Erfahren Sie mehr über das einmalige Konfigurieren von Verbindungen für alle Benutzer eines Gateways.](shared-connections.md)