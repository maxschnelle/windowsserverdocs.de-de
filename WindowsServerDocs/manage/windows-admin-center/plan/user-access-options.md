---
title: Benutzer Zugriffs Optionen mit Windows Admin Center
description: Benutzer Zugriffs Optionen und Identitäts Anbieter mit Windows Admin Center (Project Honolulu)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 084cdae0bf8ca0eb3aff1f4679d30978b860efef
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356918"
---
# <a name="user-access-options-with-windows-admin-center"></a>Benutzer Zugriffs Optionen mit Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Wenn das Windows Admin Center auf Windows Server bereitgestellt wird, stellt es einen zentralen Verwaltungspunkt für Ihre Server Umgebung bereit. Indem Sie den Zugriff auf das Windows Admin Center steuern, können Sie die Sicherheit ihrer Verwaltungs Landschaft verbessern.

## <a name="gateway-access-roles"></a>Gateway-Zugriffs Rollen

Windows Admin Center definiert zwei Rollen für den Zugriff auf den Gatewaydienst: gatewaybenutzer und Gateway-Administratoren.

> [!NOTE]
> Der Zugriff auf das Gateway impliziert nicht den Zugriff auf die Zielserver, die für das Gateway sichtbar sind. Um einen Zielserver zu verwalten, muss ein Benutzer eine Verbindung mit Anmelde Informationen herstellen, die auf dem Zielserver über Administratorrechte verfügen.

**Gatewaybenutzer** können eine Verbindung mit dem Windows Admin Center-Gatewaydienst herstellen, um Server über dieses Gateway zu verwalten. Sie können jedoch weder die Zugriffsberechtigungen noch den Authentifizierungsmechanismus ändern, der für die Authentifizierung beim Gateway verwendet wird.

**Gatewayadministratoren** können konfigurieren, wer Zugriff erhält und wie sich Benutzer beim Gateway authentifizieren.

>[!NOTE]
> Wenn keine Zugriffs Gruppen im Windows Admin Center definiert sind, werden die Rollen dem Windows-Konto Zugriff auf den Gatewayserver widerspiegeln. 

[Konfigurieren Sie den gatewaybenutzer-und Administrator Zugriff im Windows Admin Center.](../configure/user-access-control.md)

## <a name="identity-provider-options"></a>Optionen des Identitäts Anbieters

Gatewayadministratoren können eine der folgenden Optionen auswählen:

 - [Active Directory/lokale Computer Gruppen](../configure/user-access-control.md#active-directory-or-local-machine-groups)
 - [Azure Active Directory als Identitäts Anbieter für Windows Admin Center](../configure/user-access-control.md#azure-active-directory)


### <a name="smartcard-authentication"></a>Smartcardauthentifizierung

Wenn Sie Active Directory oder lokale Computer Gruppen als Identitäts Anbieter verwenden, können Sie die Smartcard-Authentifizierung erzwingen, indem Sie Benutzern, die auf das Windows Admin Center zugreifen, als Mitglied von zusätzlichen smartcardbasierten Sicherheitsgruppen aufgefordert werden. [Konfigurieren Sie die Smartcard-Authentifizierung im Windows Admin Center.](../configure/user-access-control.md#active-directory-or-local-machine-groups)

### <a name="conditional-access-and-multi-factor-authentication"></a>Bedingter Zugriff und Multi-Factor Authentication

Wenn Sie Azure AD Authentifizierung für das Gateway benötigen, können Sie zusätzliche Sicherheitsfeatures wie den bedingten Zugriff und die mehrstufige Authentifizierung nutzen, die von Azure AD bereitgestellt werden. [Weitere Informationen zum Konfigurieren des bedingten Zugriffs mit Azure Active Directory.](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## <a name="role-based-access-control"></a>Rollenbasierte Zugriffsteuerung

Standardmäßig benötigen Benutzer vollständige lokale Administratorrechte auf den Computern, die Sie mithilfe des Windows Admin Centers verwalten möchten.
Dies ermöglicht es Ihnen, eine Remote Verbindung mit dem Computer herzustellen und sicherzustellen, dass Sie über ausreichende Berechtigungen zum Anzeigen und Ändern von Systemeinstellungen verfügen.
Allerdings benötigen einige Benutzer möglicherweise keinen uneingeschränkten Zugriff auf den Computer, um Ihre Aufgaben auszuführen.
Sie können die **rollenbasierte Zugriffs Steuerung** im Windows Admin Center verwenden, um solchen Benutzern eingeschränkten Zugriff auf den Computer zu gewähren, anstatt sie vollständig als lokale Administratoren zu erstellen.

Die rollenbasierte Zugriffs Steuerung im Windows Admin Center konfiguriert jeden verwalteten Server mit einem PowerShell-Endpunkt, der [gerade genug Verwaltungs](https://aka.ms/jeadocs) Endpunkt ist.
Dieser Endpunkt definiert die Rollen, einschließlich der Aspekte des Systems, die die einzelnen Rollen verwalten dürfen und welche Benutzer der Rolle zugewiesen sind.
Wenn ein Benutzer eine Verbindung mit dem eingeschränkten Endpunkt herstellt, wird ein temporäres lokales Administrator Konto erstellt, um das System in seinem Namen zu verwalten.
Dadurch wird sichergestellt, dass auch Tools, die nicht über ein eigenes Delegierten Modell verfügen, weiterhin mit dem Windows Admin Center verwaltet werden können.
Das temporäre Konto wird automatisch entfernt, wenn der Benutzer die Verwaltung des Computers über das Windows Admin Center beendet.

Wenn ein Benutzer eine Verbindung mit einem Computer herstellt, der mit der rollenbasierten Zugriffs Steuerung konfiguriert ist, prüft das Windows Admin Center zunächst, ob es sich um einen lokalen Administrator handelt.
Wenn dies der Fall ist, erhalten Sie eine vollständige Windows Admin Center-Benutzerversion ohne Einschränkungen.
Andernfalls prüft das Windows Admin Center, ob der Benutzer zu einer der vordefinierten Rollen gehört.
Ein Benutzer hat einen *eingeschränkten Zugriff* , wenn er zu einer Windows Admin Center-Rolle gehört, aber kein vollständiger Administrator ist.
Wenn der Benutzer weder ein Administrator noch ein Mitglied einer Rolle ist, wird ihm der Zugriff zum Verwalten des Computers verweigert.

Die rollenbasierte Zugriffs Steuerung ist für die Server-Manager-und Failoverclusterlösungen verfügbar.

### <a name="available-roles"></a>Verfügbare Rollen

Das Windows Admin Center unterstützt die folgenden Endbenutzer Rollen:

Rollenname | Beabsichtigte Nutzung
----------|-------------
Administratoren | Ermöglicht Benutzern die Verwendung der meisten Features im Windows Admin Center, ohne dass Ihnen Zugriff auf Remotedesktop oder PowerShell gewährt wird. Diese Rolle eignet sich für "Jump Server"-Szenarien, in denen Sie die Verwaltungs Einstiegspunkte auf einem Computer begrenzen möchten.
Leser | Ermöglicht es Benutzern, Informationen und Einstellungen auf dem Server anzuzeigen, aber keine Änderungen vorzunehmen.
Hyper-V-Administratoren | Ermöglicht Benutzern das vornehmen von Änderungen an virtuellen Hyper-V-Computern und-Switches, schränkt jedoch andere Funktionen auf den schreibgeschützten Zugriff ein.

Die folgenden integrierten Erweiterungen verfügen über eingeschränkte Funktionen, wenn ein Benutzer eine Verbindung mit eingeschränktem Zugriff herstellt:

- Dateien (kein Hochladen oder Herunterladen von Dateien)
- PowerShell (nicht verfügbar)
- Remotedesktop (nicht verfügbar)
- Speicher Replikat (nicht verfügbar)

Zu diesem Zeitpunkt können Sie keine benutzerdefinierten Rollen für Ihre Organisation erstellen, aber Sie können auswählen, welchen Benutzern der Zugriff auf die einzelnen Rollen gewährt wird.

### <a name="preparing-for-role-based-access-control"></a>Vorbereiten der rollenbasierten Zugriffs Steuerung

Um die temporären lokalen Konten zu nutzen, muss jeder Zielcomputer so konfiguriert werden, dass die rollenbasierte Zugriffs Steuerung im Windows Admin Center unterstützt wird.
Der Konfigurationsprozess umfasst die Installation von PowerShell-Skripts und einen gerade ausreichenden Verwaltungs Endpunkt auf dem Computer mithilfe der Konfiguration des gewünschten Zustands.

Wenn Sie nur über wenige Computer verfügen, können Sie die Konfiguration problemlos auf jeden Computer anwenden, indem Sie die rollenbasierte Zugriffs Steuerungs Seite im Windows Admin Center verwenden.
Wenn Sie die rollenbasierte Zugriffs Steuerung auf einem einzelnen Computer einrichten, werden lokale Sicherheitsgruppen erstellt, um den Zugriff auf die einzelnen Rollen zu steuern.
Sie können Benutzern oder anderen Sicherheitsgruppen Zugriff gewähren, indem Sie Sie als Mitglieder der Rollen Sicherheitsgruppen hinzufügen.

Für eine unternehmensweite Bereitstellung auf mehreren Computern können Sie das Konfigurationsskript vom Gateway herunterladen und mithilfe eines pullservers, Azure Automation oder Ihrer bevorzugten Verwaltungs Tools auf Ihre Computer verteilen.
