---
title: Access-Optionen für Benutzer mit Windows Admin Center
description: User Access-Optionen und Identitätsanbieter mit Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 9adea736d6e7ae181bdfe50289564083146f5b30
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825891"
---
# <a name="user-access-options-with-windows-admin-center"></a>Access-Optionen für Benutzer mit Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Wenn unter Windows Server bereitgestellt wird, bietet Windows Admin Center einen zentralen Verwaltungspunkt für die serverumgebung. Durch die Steuerung des Zugriffs auf Windows Admin Center aus, können Sie die Sicherheit Ihrer Landschaft Management verbessern.

## <a name="gateway-access-roles"></a>Gateway-Zugriffsrollen

Windows Admin Center definiert zwei Rollen für den Zugriff auf den Gateway-Dienst: datenverwaltungsgateway-Benutzer und Administrator des Gateways bereitgestellt.

> [!NOTE]
> Zugriff auf das Gateway impliziert keinen Zugriff auf den Zielservern sichtbar vom Gateway. Um einen Zielserver verwalten zu können, muss ein Benutzer mit Anmeldeinformationen verbinden, das über Administratorrechte auf dem Zielserver verfügen.

**Datenverwaltungsgateway-Benutzer** können mit dem Gateway-Dienst von Windows Admin Center zur Verwaltung von Servern über dieses Gateway verbinden, aber nicht über Zugriffsberechtigungen noch der Authentifizierungsmechanismus verwendet das Gateway zu authentifizieren.

**Gatewayadministratoren** können konfigurieren, wer Zugriff auch erhält, wie Benutzer mit dem Gateway authentifiziert werden.

>[!NOTE]
> Wenn keine Access-Gruppen, die in Windows Admin Center definiert sind, werden die Rollen der Windows-Kontozugriff auf den Gatewayserver angewendet. 

[Konfigurieren Sie Benutzer und Administratoren den Zugriff auf in Windows Admin Center ein.](../configure/user-access-control.md)

## <a name="identity-provider-options"></a>Identitätsoptionen für Anbieter

Gateway-Administratoren können eine der folgenden:

 - [Active Directory/Lokale Computergruppen](../configure/user-access-control.md#active-directory-or-local-machine-groups)
 - [Azure Active Directory als Identitätsanbieter für Windows Admin Center](../configure/user-access-control.md#azure-active-directory)


### <a name="smartcard-authentication"></a>Smartcard-Authentifizierung

Wenn Sie Active Directory oder lokale Benutzergruppen als Identitätsanbieter verwenden, können Sie Smartcard-Authentifizierung erzwingen, indem Sie Benutzer, die auf Windows Admin Center, um zusätzliche Smartcard-basierte Sicherheitsgruppen angehören zugreifen. [Smartcard-Authentifizierung in Windows Admin Center zu konfigurieren.](../configure/user-access-control.md#active-directory-or-local-machine-groups)

### <a name="conditional-access-and-multi-factor-authentication"></a>Für den bedingten Zugriff und Multi-Factor authentication

Durch das Anfordern von Azure AD-Authentifizierung für das Gateway, können Sie zusätzliche Sicherheitsfunktionen wie bedingten Zugriff und Multi-Factor Authentication von Azure AD bereitgestellten nutzen. [Erfahren Sie mehr über das Konfigurieren des bedingten Zugriffs in Azure Active Directory.](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## <a name="role-based-access-control"></a>Rollenbasierte Zugriffsteuerung

Standardmäßig müssen Benutzer die vollständige lokale Administratorrechte auf den Computern, die sie verwalten, Windows Admin Center verwenden möchten.
Dies können sie eine Remoteverbindung mit dem Computer herstellen und stellt sicher, dass sie ausreichende Berechtigungen zum Anzeigen und Ändern von Systemeinstellungen.
Allerdings können einige Benutzer nicht uneingeschränkten Zugriff auf den Computer zum Ausführen ihrer Aufgaben benötigen.
Sie können **Role-based Access Control,** in Windows Admin Center, um solche Benutzer mit eingeschränktem Zugriff auf den Computer aus, anstatt Sie vollständige lokale Administratoren bereitzustellen.

Rollenbasierte Zugriffssteuerung in Windows Admin Center funktioniert durch Konfigurieren von jedem verwalteten Server mit einem PowerShell [Just Enough Administration](https://aka.ms/jeadocs) Endpunkt.
Dieser Endpunkt definiert die Rollen, einschließlich welche Aspekte des Systems jede Rolle zulässig ist, verwalten und welche Benutzer die Rolle zugewiesen sind.
Wenn ein Benutzer mit dem eingeschränkten Endpunkt herstellt, wird ein temporäre lokale Administratorkonto erstellt, um das System in ihrem Auftrag zu verwalten.
Dadurch wird sichergestellt, dass auch Tools, die nicht ihre eigenen Delegierungsmodell besitzen immer noch mit Windows Admin Center verwaltet werden können.
Das temporäre Konto wird automatisch entfernt, wenn der Benutzer den Computer über Windows Admin Center verwalten.

Wenn ein Benutzer auf einem Computer mit der rollenbasierten Zugriffssteuerung herstellt, überprüft Windows Admin Center zuerst, ob sie ein lokaler Administrator sind.
Wenn sie sich befinden, erhalten sie die vollständige Windows Admin Center-Erfahrung ohne Einschränkungen.
Andernfalls überprüft Windows Admin Center, ob der Benutzer eine der vordefinierten Rollen angehört.
Ein Benutzer gilt als haben *nur mit beschränktem Zugriff* , wenn sie zu einer Rolle gehört Windows Admin Center sind jedoch keinem vollständigen Administratorkonto.
Abschließend, wenn der Benutzer weder Administrator noch Mitglied einer Rolle ist, werden ihnen der Zugriff zur Verwaltung des Computers verweigert werden.

Rollenbasierte Zugriffssteuerung steht für den Server-Manager und Failovercluster-Lösungen zur Verfügung.

### <a name="available-roles"></a>Verfügbare Rollen

Windows Admin Center unterstützt die folgenden Rollen für den Endbenutzer:

Rollenname | Beabsichtigte Nutzung
----------|-------------
Administratoren | Ermöglicht Benutzern, die meisten Features in Windows Admin Center zu verwenden, ohne sie Zugriff auf Remote Desktop oder über PowerShell erteilen. Diese Rolle eignet sich für "sprungbrettserver" Szenarien Sie die Management-Einstiegspunkte auf einem Computer zu beschränken möchten.
Leser | Ermöglicht das Anzeigen von Informationen und Einstellungen auf dem Server, jedoch keine Änderungen vornehmen.
Hyper-V-Administratoren | Ermöglicht Benutzern, um Hyper-V-Computer und Switches zu ändern, aber andere Features, mit schreibgeschützten Zugriff beschränkt.

Die folgenden integrierten Erweiterungen haben Funktionalität reduziert, wenn ein Benutzer mit eingeschränktem Zugriff herstellt:

- Dateien (keine Datei hochladen oder herunterladen)
- PowerShell (nicht verfügbar)
- Remotedesktop (nicht verfügbar)
- Funktion "Speicherreplikat" (nicht verfügbar)

Zu diesem Zeitpunkt können nicht Sie benutzerdefinierte Rollen für Ihre Organisation erstellen, aber Sie können auswählen, welche Benutzer Zugriff auf jede Rolle gewährt werden.

### <a name="preparing-for-role-based-access-control"></a>Vorbereiten für die rollenbasierte Zugriffssteuerung

Um die temporären lokalen Konten zu nutzen, muss jeder Zielcomputer konfiguriert werden, zur Unterstützung der rollenbasierten Zugriffssteuerung in Windows Admin Center.
Der Konfigurationsprozess umfasst das Installieren von PowerShell-Skripts und einen Just Enough Administration-Endpunkt auf dem Computer mithilfe von Desired State Configuration.

Wenn Sie nur auf wenige Computern verfügen, können Sie die Konfiguration einfach einzeln auf jedem Computer, die im Windows Admin Center über die rollenbasierte Access Control-Seite anwenden.
Wenn Sie die rollenbasierte Zugriffssteuerung auf einem einzelnen Computer einrichten, werden lokale Sicherheitsgruppen zum Steuern des Zugriffs für die einzelnen Rollen erstellt.
Sie können den Zugriff auf Benutzer oder andere Sicherheitsgruppen gewähren, indem Sie sie als Mitglieder der Rolle Sicherheitsgruppen hinzufügen.

Für eine unternehmensweite-Bereitstellung auf mehreren Computern können Sie Herunterladen des Konfigurationsskripts über das Gateway und verteilen Sie sie an Ihre Computer mit einer Desired State Configuration Pull-Server, Azure Automation oder Ihre bevorzugte Management-Tools.
