---
title: Zugriffsoptionen für Benutzer mit Windows Admin Center
description: Zugriffsoptionen für Benutzer und Identitätsanbietern mit Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 9adea736d6e7ae181bdfe50289564083146f5b30
ms.sourcegitcommit: 4961576f2891600ef9a760ca7df650d14332e057
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/09/2019
ms.locfileid: "9151995"
---
# Zugriffsoptionen für Benutzer mit Windows Admin Center

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

Wenn unter Windows Server bereitgestellt wird, bietet Windows Admin Center eine zentrale Anlaufstelle für Verwaltung Ihrer Server-Umgebung. Durch die Steuerung des Zugriffs auf Windows Admin Center, können Sie die Sicherheit Ihrer Management-Landschaft verbessern.

## Gateway-Zugriff-Rollen

Windows Admin Center definiert zwei Rollen für den Zugriff auf den Gatewaydienst: Gateway-Benutzer und Gateway-Administratoren.

> [!NOTE]
> Zugriff auf das Gateway bedeutet nicht den Zugriff auf den Zielserver sichtbar vom Gateway. Um einen Zielserver verwalten zu können, muss ein Benutzer mit Anmeldeinformationen verbinden, die über auf dem Zielserver Administratorrechte.

**Gateway-Benutzer** können mit dem Windows Admin Center Gateway-Dienst herstellen können, um die Verwaltung von Servern über dieses Gateway, aber sie nicht ändern, Zugriffsberechtigungen noch den Authentifizierungsmechanismus verwendet, um das Gateway zu authentifizieren.

**Gateway-Administratoren** können konfigurieren, wer Zugriff sowie erhält, wie Benutzer auf das Gateway authentifizieren können.

>[!NOTE]
> Wenn es keine Zugriffsgruppen in Windows Admin Center definiert, werden die Rollen den Windows-Kontozugriff auf den Gatewayserver wider. 

[Konfigurieren Sie Benutzer und Administrator-Gateway-Zugriff in Windows Admin Center.](../configure/user-access-control.md)

## Optionen für Identity provider

Gateway-Administratoren können eine der folgenden wählen:

 - [Active Directory/Lokale Computergruppen](../configure/user-access-control.md#active-directory-or-local-machine-groups)
 - [Azure Active Directory als Identitätsanbieter für Windows Admin Center](../configure/user-access-control.md#azure-active-directory)


### Smartcard-Authentifizierung

Wenn Sie Active Directory oder lokale Gruppen als Identitätsanbieter verwenden, können Sie die Smartcard-Authentifizierung erzwingen, durch die Verwendung von Benutzern Zugriff auf Windows Admin Center, um ein Mitglied des zusätzliche Smartcard-basierte Sicherheitsgruppen sein. [Konfigurieren der Smartcard-Authentifizierung in Windows Admin Center.](../configure/user-access-control.md#active-directory-or-local-machine-groups)

### Bedingter Zugriff und Multi-Factor authentication

Durch die Verwendung von Azure AD-Authentifizierung für das Gateway, können Sie zusätzliche Sicherheitsfeatures wie bedingten Zugriff und Multi-Factor Authentication von Azure AD bereitgestellt nutzen. [Weitere Informationen zum Konfigurieren des bedingten Zugriffs mit Azure Active Directory.](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## Rollenbasierte Zugriffssteuerung

Benutzer müssen in der Standardeinstellung vollständige lokale Administratorrechte auf dem Computer, auf denen, die Sie mithilfe von Windows Admin Center verwalten möchten.
Dies ermöglicht es ihnen, für die Remoteverbindung mit dem Computer und stellt sicher, dass sie über ausreichende Berechtigungen zum Anzeigen und Ändern von Systemeinstellungen.
Allerdings benötigen einige Benutzer möglicherweise keine uneingeschränkten Zugriff auf den Computer für ihre Aufgaben.
Sie können **rollenbasierte Zugriffssteuerung** in Windows Admin Center verwenden, um diese Benutzer mit eingeschränkten Zugriff auf den Computer anstelle von machen Sie vollständige lokale Administratoren bereitzustellen.

Rollenbasierte Zugriffssteuerung in Windows Admin Center funktioniert, indem Sie jeden verwalteten Server mit einem PowerShell [Just Enough Administration](https://aka.ms/jeadocs) -Endpunkt konfigurieren.
Diesen Endpunkt definiert die Rollen, z. B. welche Aspekte des Systems jede Rolle zulässig ist, verwalten und welche Benutzer zur Rolle zugewiesen sind.
Wenn ein Benutzer mit der eingeschränkten Endpunkt verbunden ist, wird ein temporäres Administratorkonto für lokale Verwaltung des Systems im Auftrag erstellt.
Dadurch wird sichergestellt, dass auch Tools, die nicht ihre eigenen Modell verfügen weiterhin mit Windows Admin Center verwaltet werden können.
Das temporäre Konto wird automatisch entfernt, wenn der Benutzer nicht mehr den Computer über Windows Admin Center verwalten.

Wenn ein Benutzer mit einem Computer mit der rollenbasierten Zugriffssteuerung verbunden ist, wird Windows Admin Center zuerst prüfen, ob sie ein lokaler Administrator sind.
Wenn dies der Fall, erhalten sie die vollständige Windows Admin Center-Erfahrung mit keine Einschränkungen.
Andernfalls wird Windows Admin Center überprüft, ob der Benutzer auf eine der vordefinierten Rollen gehört.
Ein Benutzer wird als *eingeschränkten Zugriff* haben, wenn sie zu einer Windows Admin Center-Rolle gehören sind jedoch kein Administrator bezeichnet.
Schließlich, wenn der Benutzer ein Administrator weder ein Mitglied einer Rolle ist, werden sie Zugriff auf den Computer verwalten abgelehnt.

Rollenbasierte Zugriffssteuerung ist für die Server-Manager und Failover Cluster-Lösungen verfügbar.

### Verfügbare Rollen

Windows Admin Center unterstützt die folgenden Endbenutzer-Funktionen:

Name der Rolle | Beabsichtigte Nutzung
----------|-------------
Administratoren | Ermöglicht Benutzern, die meisten Funktionen in Windows Admin Center verwenden, ohne Zugriff auf Remotedesktop oder PowerShell. Mit dieser Rolle eignet sich für "springen Server" Fälle, in denen Sie die Management-Einstiegspunkte auf einem Computer zu beschränken.
Leser | Ermöglicht Benutzern das Anzeigen von Informationen und Einstellungen auf dem Server, jedoch nicht ändern.
Hyper-V-Administratoren | Ermöglicht es Benutzern, Hyper-V-Computern und Switches zu ändern, aber andere Features schreibgeschützten Zugriff beschränkt.

Die folgenden integrierten Erweiterungen haben Funktionalität reduziert, wenn ein Benutzer mit eingeschränkten Zugriff anschließt:

- Dateien (keine Datei hochladen oder herunterladen)
- PowerShell (nicht verfügbar)
- Remotedesktop (nicht verfügbar)
- Das Speicherreplikatfeature (nicht verfügbar)

Zu diesem Zeitpunkt können nicht Sie benutzerdefinierte Rollen für Ihre Organisation erstellen, aber Sie können auswählen, welche Benutzer Zugriff auf jede Rolle gewährt werden.

### Vorbereiten für die rollenbasierte Zugriffssteuerung

Um die temporären lokalen Konten nutzen zu können, muss jeder Zielcomputer konfiguriert werden, um rollenbasierte Zugriffssteuerung in Windows Admin Center zu unterstützen.
Der Konfigurationsprozess umfasst die Installation von PowerShell-Skripts und einen Endpunkt Just Enough Administration auf dem Computer mit Desired State Configuration.

Wenn Sie nur wenige Computer verfügen, können Sie die Konfiguration problemlos einzeln für jeden Computer, auf der Seite "-Steuerelement rollenbasierter Zugriff" im Windows Admin Center mit anwenden.
Wenn Sie rollenbasierte Zugriffssteuerung auf einem einzelnen Computer einrichten, werden lokale Sicherheitsgruppen zum Steuern des Zugriffs auf jede Rolle erstellt.
Sie können Benutzern oder anderen Sicherheitsgruppen Zugriff gewähren, indem Sie sie als Mitglieder der Rolle Sicherheitsgruppen hinzufügen.

Für eine unternehmensweite-Bereitstellung auf mehreren Computern können Sie das Skript vom Gateway herunterladen und verteilen Sie sie an Ihren Computern mit einem Desired State Configuration Pull-Server, Azure-Automatisierung oder Ihre bevorzugte Management-Tools.
