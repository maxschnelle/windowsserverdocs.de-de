---
title: Einstellungen
description: Informationen Sie zu Einstellungen in Windows Admin Center (Projekt Honolulu). Benutzer können Benutzer ihre Sprache/Region und anderen Einstellungen zu ändern. Gateway-Einstellungen können der Administrator das Gateway zu konfigurieren.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 04/12/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: d67a2c743900792353141186112cd09dbf780309
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296622"
---
# Windows Admin Center-Einstellungen

> Gilt für: Windows Admin Center

Windows Admin Center-Einstellungen bestehen aus Benutzerebene und Gateway-Ebene-Einstellungen. Eine Änderung an einer Einstellung wirkt sich nur auf den aktuellen Benutzer Profil, während eine Änderung zu einer Gateway-Level-Einstellung wirkt sich alle Benutzer auf dem Windows Admin Center-Gateway auf Benutzerebene.

## Benutzereinstellungen

Benutzerebene Einstellungen bestehen aus den folgenden Abschnitten:

- Account
- Personalisierung
- Sprache/Region
- Vorschläge
- Erweitert

In der Registerkarte " **Konto** " können Benutzer die Anmeldeinformationen überprüfen können, die bei Windows Admin Center zur Authentifizierung verwendet haben. Wenn Azure AD der Identitätsanbieter konfiguriert ist, kann der Benutzer ihr Azure AD-Konto auf dieser Registerkarte anmelden.

In der Registerkarte " **Personalisierung** " können Benutzer zu einem dunklen UI-Design umschalten.

Benutzer können in der Registerkarte " **Sprache/Region** " die Sprache und Region-Formate, die von Windows Admin Center angezeigt ändern.

In der Registerkarte " **Vorschläge** " können Benutzer Vorschläge zu Azure-Dienste und neue Features aktivieren oder deaktivieren.

Die Registerkarte " **Erweitert** " bietet Windows Admin Center-Erweiterung Entwickler zusätzliche Funktionen.

## Gateway-Einstellungen

Gateway-Ebene Einstellungen bestehen aus den folgenden Abschnitten:

- Erweiterungen
- Access
- Azure
- Gemeinsam genutzte Verbindungen

Nur Gateway-Administratoren, anzeigen und diese Einstellungen ändern können. Änderungen an diese Einstellungen ändern Sie die Konfiguration des Gateways und wirken sich auf alle Benutzer des Windows Admin Center-Gateways.

Administratoren können in der Registerkarte " **Extensions** " installieren, deinstallieren oder Aktualisieren von Gateway-Erweiterungen. [Hier erfahren Sie mehr über die Erweiterungen.](using-extensions.md)

Die Registerkarte **Zugriff** kann Administratoren konfigurieren, wer das Windows Admin Center-Gateway sowie der Identitätsanbieter verwendet zum Authentifizieren von Benutzern zugreifen kann. [Weitere Informationen zum Steuern des Zugriffs auf das Gateway.](user-access-control.md)

Auf der Registerkarte **Azure** können Administratoren das Gateway mit Azure zum Aktivieren von [Azure-Integration-Features](azure-integration.md) in Windows Admin Center registrieren.

Verwenden die Registerkarte " **Freigegebenen Verbindungen** ", können Administratoren eine einzelne Liste von Verbindungen mit allen Benutzern von Windows Admin Center-Gateway gemeinsam genutzt werden konfigurieren. [Weitere Informationen zum Konfigurieren von Verbindungen einmal für alle Benutzer eines Gateways.](shared-connections.md)