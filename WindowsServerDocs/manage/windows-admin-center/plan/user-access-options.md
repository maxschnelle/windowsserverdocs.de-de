---
title: Benutzerzugriffsoptionen mit Windows Admin Center
description: Benutzerzugriffsoptionen und Identitätsanbieter mit Windows Admin Center (Projekt Honolulu)
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 184eca56dc14e91220a7fb7eb196c48706562ff7
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766713"
---
# <a name="user-access-options-with-windows-admin-center"></a>Benutzerzugriffsoptionen mit Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Bei Bereitstellung auf Windows Server bietet Windows Admin Center einen zentralen Verwaltungspunkt für die Serverumgebung. Durch die Steuerung des Zugriffs auf Windows Admin Center kann die Sicherheit der Verwaltungsumgebung verbessert werden.

## <a name="gateway-access-roles"></a>Gatewayzugriffsrollen

Windows Admin Center definiert zwei Rollen für den Zugriff auf den Gatewaydienst: Gatewaybenutzer und Gatewayadministratoren.

> [!NOTE]
> Der Zugriff auf das Gateway impliziert nicht den Zugriff auf die Zielserver, die durch das Gateway sichtbar sind. Um einen Zielserver zu verwalten, muss ein Benutzer eine Verbindung mit Anmeldeinformationen herstellen, die auf dem Zielserver über Administratorrechte verfügen.

**Gatewaybenutzer** können eine Verbindung mit dem Windows Admin Center-Gateway herstellen, um Servern über dieses Gateway zu verwalten, aber sie können weder die Zugriffsberechtigungen noch den Authentifizierungsmechanismus ändern, der zum Authentifizieren des Gateways verwendet wird.

**Gatewayadministratoren** können konfigurieren, wer Zugriff erhält und wie sich Benutzer beim Gateway authentifizieren.

>[!NOTE]
> Wenn in Windows Admin Center keine Zugriffsgruppen definiert sind, spiegeln die Rollen den Windows-Kontozugriff auf den Gatewayserver wider.

[Konfiguriere den Gatewaybenutzer- und -administratorzugriff in Windows Admin Center.](../configure/user-access-control.md)

## <a name="identity-provider-options"></a>Optionen für Identitätsanbieter

Gatewayadministratoren können eine der folgenden Optionen auswählen:

 - [Active Directory/lokale Computergruppen](../configure/user-access-control.md#active-directory-or-local-machine-groups)
 - [Azure Active Directory als Identitätsanbieter für Windows Admin Center](../configure/user-access-control.md#azure-active-directory)


### <a name="smartcard-authentication"></a>Smartcard-Authentifizierung

Wenn Active Directory oder lokale Computergruppen als Identitätsanbieter verwendet werden, kann die Smartcard-Authentifizierung erzwungen werden, indem Benutzer, die auf Windows Admin Center zugreifen, Mitglied zusätzlicher Smartcard-basierter Sicherheitsgruppen sein müssen. [Konfiguriere die Smartcard-Authentifizierung in Windows Admin Center.](../configure/user-access-control.md#active-directory-or-local-machine-groups)

### <a name="conditional-access-and-multi-factor-authentication"></a>Bedingter Zugriff und mehrstufige Authentifizierung

Durch die Anforderung der Azure AD-Authentifizierung für das Gateway kannst du zusätzliche Sicherheitsfeatures wie den bedingten Zugriff und die mehrstufige Authentifizierung nutzen, die von Azure AD bereitgestellt werden. [Weitere Informationen zum Konfigurieren des bedingten Zugriffs mit Azure Active Directory](/azure/active-directory/active-directory-conditional-access-azure-portal-get-started).

## <a name="role-based-access-control"></a>Rollenbasierte Zugriffsteuerung

Standardmäßig benötigen Benutzer auf den Computern, die sie mit dem Windows Admin Center verwalten möchten, uneingeschränkte lokale Administratorrechte.
Dadurch können sie sich remote mit dem Computer verbinden und sicherstellen, dass sie über ausreichende Berechtigungen zum Anzeigen und Ändern von Systemeinstellungen verfügen.
Einige Benutzer benötigen jedoch möglicherweise keinen uneingeschränkten Zugriff auf das Gerät, um ihre Aufgaben auszuführen.
Du kannst die **rollenbasierte Zugriffssteuerung** (Role-Based Access Control, RBAC) in Windows Admin Center verwenden, um diesen Benutzern eingeschränkten Zugriff auf den Computer zu gewähren, anstatt sie zu vollständigen lokalen Administratoren zu machen.

Die rollenbasierte Zugriffssteuerung in Windows Admin Center funktioniert, indem jeder verwaltete Server mit einem PowerShell [Just Enough Administration](/powershell/scripting/learn/remoting/jea/overview)-Endpunkt konfiguriert wird.
Dieser Endpunkt definiert die Rollen, einschließlich der Aspekte des Systems, die jede Rolle verwalten darf und welche Benutzer der Rolle zugeordnet werden.
Wenn sich ein Benutzer mit dem eingeschränkten Endpunkt verbindet, wird ein temporäres lokales Administratorkonto erstellt, um das System in seinem Auftrag zu verwalten.
Dadurch wird sichergestellt, dass auch Tools, die über kein eigenes Delegierungsmodell verfügen, weiterhin mit Windows Admin Center verwaltet werden können.
Das temporäre Konto wird automatisch entfernt, wenn der Benutzer die Verwaltung des Computers über Windows Admin Center beendet.

Wenn ein Benutzer eine Verbindung mit einem Computer herstellt, der mit rollenbasierter Zugriffssteuerung konfiguriert ist, prüft Windows Admin Center zunächst, ob es sich um einen lokalen Administrator handelt.
Wenn dies der Fall ist, erhalten sie die volle Windows Admin Center-Erfahrung ohne Einschränkungen.
Andernfalls prüft Windows Admin Center, ob der Benutzer zu einer der vordefinierten Rollen gehört.
Ein Benutzer soll *begrenzten Zugriff* erhalten, wenn er zu einer Windows Admin Center-Rolle gehört, aber kein vollständiger Administrator ist.
Wenn der Benutzer weder Administrator noch Mitglied einer Rolle ist, wird ihm schließlich der Zugriff zur Verwaltung des Computers verweigert.

Die rollenbasierte Zugriffssteuerung ist für die Server-Manager- und Failoverclusterlösungen verfügbar.

### <a name="available-roles"></a>Verfügbare Rollen

Windows Admin Center unterstützt die folgenden Endbenutzerrollen:

Rollenname | Beabsichtigte Nutzung
----------|-------------
Administratoren | Ermöglicht Benutzern die Verwendung der meisten Features in Windows Admin Center, ohne dass sie Zugriff auf Remotedesktop oder PowerShell erhalten. Diese Rolle eignet sich gut für „Sprungbrettserver“-Szenarien, bei denen die Einstiegspunkte für die Verwaltung auf einem Computer begrenzt werden sollen.
Leser | Ermöglicht es Benutzern, Informationen und Einstellungen auf dem Server anzuzeigen, aber keine Änderungen vorzunehmen.
Hyper-V-Administratoren | Ermöglicht es Benutzern, Änderungen an virtuellen Hyper-V-Computern und -Switches vorzunehmen, schränkt aber andere Features auf den schreibgeschützten Zugriff ein.

Die folgenden integrierten Erweiterungen weisen eine reduzierte Funktionalität auf, wenn ein Benutzer mit eingeschränktem Zugriff eine Verbindung herstellt:

- Dateien (kein Dateiupload oder Dateidownload)
- PowerShell (nicht verfügbar)
- Remotedesktop (nicht verfügbar)
- Speicherreplikat (nicht verfügbar)

Zur Zeit kannst du keine benutzerdefinierten Rollen für deine Organisation erstellen, aber du kannst auswählen, welche Benutzer Zugriff auf die einzelnen Rollen erhalten.

### <a name="preparing-for-role-based-access-control"></a>Vorbereiten auf die rollenbasierte Zugriffssteuerung

Um die temporären lokalen Konten zu nutzen, muss jeder Zielcomputer so konfiguriert werden, dass er die rollenbasierte Zugriffssteuerung in Windows Admin Center unterstützt.
Der Konfigurationsprozess umfasst die Installation von PowerShell-Skripts und eines Just Enough Administration-Endpunkts auf dem Computer unter Verwendung der Desired State Configuration.

Wenn du nur über einige wenige Computer verfügst, kannst du die Konfiguration mithilfe der rollenbasierten Zugriffssteuerungsseite in Windows Admin Center problemlos individuell auf jeden Computer anwenden.
Wenn du eine rollenbasierte Zugriffssteuerung auf einem einzelnen Computer einrichtest, werden lokale Sicherheitsgruppen erstellt, um den Zugriff auf die einzelnen Rollen zu kontrollieren.
Du kannst Benutzern oder anderen Sicherheitsgruppen Zugriff gewähren, indem du sie als Mitglieder der Rolle „Sicherheitsgruppen“ hinzufügst.

Für eine unternehmensweite Bereitstellung auf mehreren Computern kannst du das Konfigurationsskript vom Gateway herunterladen und mit einem Pullserver für die Desired State Configuration, mit Azure Automation oder deinem bevorzugten Verwaltungstools auf deine Computer verteilen.