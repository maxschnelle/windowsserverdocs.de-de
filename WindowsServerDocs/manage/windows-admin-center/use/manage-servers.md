---
title: Verwalten von Servern mit Windows Admin Center
description: Verwalten von Servern mit Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 04ade4a14272c7840b5036ca6ad5a3bf3d09bcf9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891151"
---
# <a name="manage-servers-with-windows-admin-center"></a>Verwalten von Servern mit Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center Preview

> [!Tip]
> Neu bei Windows Admin Center?
> [Erfahren Sie mehr über Windows Admin Center](../understand/windows-admin-center.md) oder [jetzt herunterladen](https://aka.ms/windowsadmincenter).

## <a name="managing-windows-server-machines"></a>Verwalten von Windows Server-Computer

Sie können einzelne Server, Windows Server 2012 oder höher auf Windows Admin Center zum Verwalten des Servers mit einem umfassenden Satz von Tools einschließlich ausgeführt Zertifikate, Geräte, Ereignisse, Prozesse, Rollen und Features, Updates, Virtual Machines und weitere hinzufügen.

![Übersichtsseite für Server-Verbindung](../media/manage-servers/server-overview.png)

## <a name="adding-a-server-to-windows-admin-center"></a>Hinzufügen eines Servers in Windows Admin Center

Um einen Server, Windows Admin Center hinzuzufügen:

1. Klicken Sie auf **+ hinzufügen** unter alle Verbindungen.
2. Hinzufügen einer **Serververbindung**.
3. Geben Sie den Namen des Servers und, wenn Sie dazu aufgefordert werden, die zu verwendenden Anmeldeinformationen.
4. Klicken Sie auf **senden** um den Vorgang abzuschließen.

Der Server wird der Liste "Verbindung" auf der Seite "Übersicht" hinzugefügt werden. Klicken Sie auf die sie für die Verbindung mit dem Server.

> [!NOTE]
> Sie können auch hinzufügen [Failovercluster](manage-failover-clusters.md) oder [hyperkonvergenten Cluster](manage-hyper-converged.md) als eine separate Verbindung in Windows Admin Center.

## <a name="tools"></a>Tools

Die folgenden Tools sind verfügbar für Server-Verbindungen:

| Tool | Beschreibung |
| ---- | ----------- |
| [Übersicht](#overview) | Anzeigen von Serverdetails und den Steuerelementzustand für server |
| [Backup](#backup) | Anzeigen und Konfigurieren von Azure Backup |  
| [Zertifikate](#certificates) | Anzeigen und Ändern von Zertifikaten |
| [Container](#containers) | Container anzeigen |
| [Geräte](#devices) | Anzeigen und Ändern von Geräten |
| [Ereignisse](#events) | Anzeigen von Ereignissen |
| [Dateien](#files) | Dateien und Ordner durchsuchen |
| [Firewall](#firewall) | Anzeigen und Ändern von Firewallregeln |
| [Installierte Apps](#installed-apps) | Zeigen Sie an und entfernen Sie die installierten apps |
| [Lokale Benutzer und Gruppen](#local-users-and-groups) | Zeigen Sie an und ändern Sie lokale Benutzer und Gruppen |
| [Network](#network) | Anzeigen und Ändern von Netzwerkgeräten |
| [PowerShell](#powershell) | Interagieren Sie mit dem Server mithilfe von PowerShell |
| [Prozesse](#processes) | Zeigen Sie an und ändern Sie die laufende Prozesse |
| [Registrierung](#registry) | Zeigen Sie an und ändern Sie die Registrierungseinträge |
| [Remotedesktop](#remote-desktop) | Interagieren Sie mit der Server über Remotedesktop |
| [Rollen und Features](#roles-and-features) | Anzeigen und Ändern von Rollen und features |
| [Geplante Aufgaben](#scheduled-tasks) | Zeigen Sie an und bearbeiten Sie geplanter Aufgaben |
| [Dienste](#services) | Anzeigen und Ändern von Diensten |
| [Speicher](#storage) | Anzeigen und Ändern von Speichergeräten |
| [Storage-Migration-Dienst](#storage-migration-service) | Migrieren von Servern und Dateifreigaben in Azure oder Windows Server-2019 |
| [Funktion "Speicherreplikat"](#storage-replica) | Verwenden Sie die Funktion "Speicherreplikat" zum Verwalten von Server-zu-Server-Speicherreplikation |
| [System-Einblicke](#system-insights) | System-Insights erhalten, die Sie Einblicke in die Funktionsweise Ihres Servers erhöhen. |
| [Updates](#updates) | Anzeigen von installierter und nach neuen Updates suchen |
| [Virtuelle Computer](manage-virtual-machines.md) | Anzeigen und Verwalten von virtuellen Computern |
| [Virtuelle Switches](#virtual-switches) | Anzeigen und Verwalten von virtuellen switches |

## <a name="overview"></a>Übersicht

**Übersicht über die** sowie als Vorgänge ausführen und ändern Sie die Einstellungen auf einem Ziel-PC oder Server können Sie den aktuellen Zustand der CPU, Arbeitsspeicher und Leistung des Netzwerks, finden Sie unter.

### <a name="features"></a>Features

Die folgenden Funktionen werden in der Übersicht über die Server-Manager unterstützt:

- Server-Details anzeigen
- Anzeigen der CPU-Aktivität
- Arbeitsspeicher-Aktivität anzeigen
- Anzeigen der Netzwerkaktivität
- Starten Sie Server neu
- Herunterfahren des Servers
- Aktivieren von Datenträger-Metriken auf server
- Bearbeiten Sie die Nachrichtenquellcomputer-ID auf server

[**Anzeigen von Feedback und vorgeschlagenen Features für Server Overview**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BOverview%5D).

## <a name="backup"></a>Sicherung

**Sicherung** können Sie Ihre Windows-Server von Beschädigungen, Angriffen oder Notfällen schützen, durch das Sichern Ihrer Servers direkt in Microsoft Azure.
[Weitere Informationen zu Azure Backup.](https://aka.ms/windows-admin-center-backup)

[Bereitstellen von Feedback für die Sicherung in Windows Admin Center](https://aka.ms/backup-wac-feedback)

### <a name="features"></a>Features

Die folgenden Funktionen werden in der Sicherung unterstützt:

- Zeigen Sie eine Übersicht über den Azure backup-status
- Konfigurieren Sie die Elemente für die Sicherung und Zeitplan
- Starten oder Beenden eines Sicherungsauftrags
- Sicherung des Auftragsverlaufs und des status
- Anzeigen von Wiederherstellungspunkten und Wiederherstellen von Daten
- Sicherungsdaten löschen

## <a name="certificates"></a>Zertifikate

**Zertifikate** ermöglicht Ihnen das Verwalten von Zertifikatspeichern auf einem Computer oder Server.

### <a name="features"></a>Features

Die folgenden Funktionen werden in Zertifikate unterstützt:

- Durchsuchen Sie vorhandene Zertifikate
- Details zum Zertifikat
- Exportieren von Zertifikaten
- Erneuern von Zertifikaten
- Neue Zertifikate anfordern
- Löschen von Zertifikaten

[**Anzeigen von Feedback und vorgeschlagenen Features für Zertifikate**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BCertificates%5D).

## <a name="containers"></a>Container

**Container** können Sie die Container auf einem Windows Server-containerhost anzeigen. Im Fall von einem ausgeführten Windows Server Core-Container können Sie die Ereignisprotokolle anzuzeigen und Zugriff auf die CLI des Containers.

[**Anzeigen von Feedback und vorgeschlagenen Features für Container**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BContainers%5D).

## <a name="devices"></a>Geräte

**Geräte** ermöglicht Ihnen das Verwalten von verbundener Geräten, die auf einem Computer oder Server.

### <a name="features"></a>Features

Die folgenden Funktionen werden in Geräte unterstützt:

- Suchen und Durchsuchen von Geräten
- Anzeigen von Gerätedetails
- Deaktivieren eines Geräts
- Treiber auf einem Gerät aktualisieren

[**Anzeigen von Feedback und vorgeschlagenen Features für Geräte**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDevices%5D).

## <a name="events"></a>Ereignisse

**Ereignisse** können Sie Ereignisprotokolle auf einem Computer oder Server zu verwalten.

### <a name="features"></a>Features

Die folgenden Funktionen werden in Ereignisse unterstützt:

- Suchen und Durchsuchen von Ereignissen
- Anzeigen von Ereignisdetails
- Ereignisse aus dem Protokoll löschen
- Ereignisse aus dem Protokoll exportieren

[**Anzeigen von Feedback und vorgeschlagenen Features für Ereignisse**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BEvents%5D).

## <a name="files"></a>Dateien

**Dateien** ermöglicht Ihnen das Verwalten von Dateien und Ordner auf einem Computer oder Server.

### <a name="features"></a>Features

Die folgenden Funktionen werden in Dateien unterstützt:

- Dateien und Ordner durchsuchen
- Suchen Sie nach einer Datei oder eines Ordners
- Erstellen eines neuen Ordners
- Löschen einer Datei oder Ordner
- Herunterladen einer Datei oder eines Ordners
- Hochladen einer Datei oder Ordner
- Eine Datei oder Ordner umbenennen
- Extrahieren Sie eine Zip-Datei
- Datei oder eines Ordners-Eigenschaften anzeigen
- Verwalten von Ressourcen-Manager [Kontingente](https://docs.microsoft.com/windows-server/storage/fsrm/quota-management)
- Hinzufügen, bearbeiten oder Entfernen von Dateifreigaben
- Ändern von Benutzer- und Gruppenberechtigungen in Dateifreigaben

[**Anzeigen von Feedback und vorgeschlagenen Features für Dateien**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFiles%5D).

## <a name="firewall"></a>Firewall

**Firewall** können Sie Firewall-Einstellungen und Regeln auf einem Computer oder Server zu verwalten.

### <a name="features"></a>Features

Die folgenden Funktionen werden in der Firewall unterstützt:

- Einen Überblick über die Firewall-Einstellungen anzeigen
- Anzeigen von eingehenden Firewallregeln
- Ausgehende Firewallregeln anzeigen
- Firewallregeln für die Suche
- Anzeigen von firewallregeldetails
- Erstellen einer neuen Firewallregel
- Aktivieren oder Deaktivieren einer Firewallregel
- Löschen einer Firewallregel
- Bearbeiten Sie die Eigenschaften einer Firewallregel

[**Anzeigen von Feedback und vorgeschlagenen Features für die Firewall**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFirewall%5D).

## <a name="installed-apps"></a>Installierte Apps

**Installierte Apps** ermöglicht Ihnen das Auflisten und Deinstallieren der Anwendung, die installiert werden.

[**Anzeigen von Feedback und vorgeschlagenen Features für installierte Apps**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BInstalled%20Apps%5D).

## <a name="local-users-and-groups"></a>Lokale Benutzer und Gruppen

**Lokale Benutzer und Gruppen** ermöglicht Ihnen das Verwalten von Sicherheitsgruppen und Benutzern, die lokal auf einem Computer oder Server vorhanden sind.

### <a name="features"></a>Features

Die folgenden Funktionen werden in die lokale Benutzer und Gruppen unterstützt:

- Anzeigen und Suchen von Benutzern und Gruppen
- Erstellen Sie einen neuen Benutzer oder Gruppe
- Verwalten der Gruppenmitgliedschaft eines Benutzers
- Löschen von Benutzern oder Gruppen
- Ändern Sie das Kennwort eines Benutzers
- Bearbeiten Sie die Eigenschaften eines Benutzers oder einer Gruppe

[**Anzeigen von Feedback und vorgeschlagenen Funktionen für lokale Benutzer und Gruppen**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BLocal%20users%20and%20Groups%5D)

## <a name="network"></a>Network

**Netzwerk** ermöglicht Ihnen das Verwalten von Netzwerkgeräten und dazugehörigen Einstellungen auf einem Computer oder Server.

### <a name="features"></a>Features

Die folgenden Funktionen werden im Netzwerk unterstützt:

- Durchsuchen Sie vorhandenen Netzwerkadapter
- Anzeigen von Details eines Netzwerkadapters
- Bearbeiten der Eigenschaften eines Netzwerkadapters
- Erstellen Sie eine [Azure-Netzwerkadapter (Vorschaufeature)](https://blogs.technet.microsoft.com/networking/2018/09/05/azurenetworkadapter/)

[**Anzeigen von Feedback und vorgeschlagenen Features für das Netzwerk**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BNetwork%5D)

## <a name="powershell"></a>PowerShell

**PowerShell** können Sie für die Interaktion mit einem Computer oder Server über eine PowerShell-Sitzung.

### <a name="features"></a>Features

Die folgenden Funktionen werden in PowerShell unterstützt:

- Erstellen Sie eine interaktive PowerShell-Sitzung auf dem server
- PowerShell-Sitzung auf dem Server trennen

[**Anzeigen von Feedback und vorgeschlagenen Features für PowerShell**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BPowerShell%5D)

## <a name="processes"></a>Prozesse

**Prozesse** ermöglicht Ihnen das Verwalten von ausgeführten Prozessen auf einem Computer oder Server.

### <a name="features"></a>Features

Die folgenden Funktionen werden in Prozessen unterstützt:

- Durchsuchen Sie zum Ausführen von Prozessen
- Prozessdetails anzeigen
- Starten eines Prozesses
- Beenden eines Prozesses
- Erstellen Sie ein Speicherabbild für Prozess
- Suchen Sie Prozess-handles

[**Anzeigen von Feedback und vorgeschlagenen Features für Prozesse**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BProcesses%5D).

## <a name="registry"></a>Registrierung

**Registrierung** ermöglicht Ihnen das Verwalten von Registrierungsschlüsseln und-Werten auf einem Computer oder Server.

### <a name="features"></a>Features

Die folgenden Funktionen werden in der Registrierung unterstützt:

- Suchen von Registrierungsschlüssel und-Werte
- Hinzufügen oder Ändern von Registrierungswerten
- Löschen Sie die Registrierungswerte

[**Anzeigen von Feedback und vorgeschlagenen Features für Registrierung**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRegistry%5D).

## <a name="remote-desktop"></a>Remotedesktop

**Remotedesktop** können Sie für die Interaktion mit einem Computer oder Server über eine interaktive desktopsitzung.

### <a name="features"></a>Features

Die folgenden Funktionen werden in Remote Desktop unterstützt:

- Starten Sie das Starten einer interaktiven Remotesitzung desktop
- Trennen Sie eine Remotedesktopsitzung
- Senden Sie Strg + Alt + Entf, um eine Remotedesktopsitzung

[**Anzeigen von Feedback und vorgeschlagenen Features für Remote Desktop**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRemote%20Desktop%5D).

## <a name="roles-and-features"></a>Rollen und Features

**Rollen und Features** ermöglicht Ihnen das Verwalten von Rollen und Features auf einem Server.

### <a name="features"></a>Features

Die folgenden Funktionen werden in Rollen und Features unterstützt:

- Durchsuchen Sie die Liste der Rollen und Features auf einem server
- Rolle oder Feature-Details anzeigen
- Installieren einer Rolle oder feature
- Entfernen einer Rolle oder feature

[**Anzeigen von Feedback und vorgeschlagenen Features für Rollen und Features**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRoles%20and%20Features%5D).

## <a name="scheduled-tasks"></a>Geplante Tasks

**Geplante Tasks** ermöglicht Ihnen das Verwalten der geplanten Tasks auf einem Computer oder Server.

### <a name="features"></a>Features

Die folgenden Funktionen werden in geplante Vorgänge unterstützt:

- Durchsuchen Sie die Task Scheduler-Bibliothek
- Bearbeiten geplante Aufgaben
- Aktivieren und Deaktivieren von geplanten Aufgaben
- Geplante Tasks Beenden & starten
- Geplante Tasks zu erstellen

[**Anzeigen von Feedback und vorgeschlagenen Funktionen für geplante Aufgaben**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BScheduled%20Tasks%5D).

## <a name="services"></a>Dienste

**Dienste** ermöglicht Ihnen das Verwalten von Diensten auf einem Computer oder Server.

### <a name="features"></a>Features

Die folgenden Funktionen werden in Dienste unterstützt:

- Suchen und Durchsuchen von Diensten auf einem server
- Anzeigen von Details eines Diensts
- Starten eines Diensts
- Anhalten von Diensten
- Bearbeiten Sie die Eigenschaften eines Diensts

[**Anzeigen von Feedback und vorgeschlagenen Features für Dienste**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BServices%5D).

## <a name="storage"></a>Speicher

**Storage** ermöglicht Ihnen das Verwalten der Speichergeräte auf einem Computer oder Server.

### <a name="features"></a>Features

Die folgenden Funktionen werden im Speicher unterstützt:

- Durchsuchen Sie vorhandene Datenträger auf einem server
- Details zum Datenträger
- Erstellen eines Volumes
- Initialisieren eines Datenträgers
- Erstellen, Anfügen und Trennen einer virtuellen Festplatte (VHD)
- Einen Datenträger offline schalten
- Formatieren eines Volumes
- Ändern der Größe eines Volumes
- Bearbeiten Sie die Volume-Eigenschaften
- Löschen eines Volumes
- Kontingentverwaltung installieren

[**Anzeigen von Feedback und vorgeschlagenen Features für Speicher**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BStorage%5D)

## <a name="storage-migration-service"></a>Speichermigrationsdienst

**Speicherung Datenbankmigrationsdienst** ermöglicht Ihnen das Migrieren von Servern und Dateifreigaben in Azure oder Windows Server-2019 – ohne Anwendungen oder Benutzer nichts ändern.
[Überblick über die Storage-Migration-Dienst](https://go.microsoft.com/fwlink/?linkid=2016155)

>[!NOTE]
>Storage-Migration-Dienst erfordert Windows Server-2019.

## <a name="storage-replica"></a>Speicherreplikat

Verwendung **Funktion "Speicherreplikat"** zum Verwalten von Server-zu-Server-Speicherreplikation.
[Erfahren Sie mehr über die Funktion "Speicherreplikat"](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-ui)

## <a name="system-insights"></a>Systemdaten

**System Insights** führt predictive Analytics, die nativ in Windows Server zu ermöglichen Ihnen den erhöht, einen Einblick in die Funktionsweise Ihres Servers.
[Bietet einen Überblick über die System-Einblicke](http://aka.ms/systeminsights)

>[!NOTE]
>System Insights erfordert Windows Server-2019.

## <a name="updates"></a>Updates

**Updates** ermöglicht Ihnen das Verwalten von Microsoft und/oder Windows-Updates auf einem Computer oder Server.

### <a name="features"></a>Features

Die folgenden Funktionen werden in Updates unterstützt:

- Anzeigen von Windows und Microsoft-Updates verfügbar
- Eine Liste der Update-Verlauf anzeigen
- Updates installieren
- Suchen Sie online nach Updates von Microsoft Update
- Verwalten von [Azure die Verwaltung von](https://docs.microsoft.com/azure/automation/automation-update-management) Integration

[**Anzeigen von Feedback und vorgeschlagenen Features für Updates**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BUpdates%5D)

## <a name="virtual-machines"></a>Virtuelle Computer

Finden Sie unter [Verwalten von virtuellen Computern mit Windows Admin Center](manage-virtual-machines.md)

## <a name="virtual-switches"></a>Virtuelle Switches

**Virtuelle Switches** ermöglicht Ihnen das Verwalten von virtuellen Hyper-V-Switches auf einem Computer oder Server.

### <a name="features"></a>Features

Die folgenden Funktionen werden in virtuellen Switches unterstützt:

- Durchsuchen Sie virtuelle Switches auf einem server
- Erstellen Sie einen neuen virtuellen Switch
- Benennen Sie einen virtuellen Switch
- Löschen einer vorhandenen virtuellen Switch
- Bearbeiten Sie die Eigenschaften eines virtuellen Switches

[**Anzeigen von Feedback und vorgeschlagenen Features für virtuelle Switches**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BVirtual%20Switch%5D)
