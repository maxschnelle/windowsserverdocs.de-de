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
ms.openlocfilehash: 93a40345d05a6230596832b2d455d36eee2401b5
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296682"
---
# Verwalten von Servern mit Windows Admin Center

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

> [!Tip]
> Neu bei Windows Admin Center?
> [Erfahren Sie mehr über Windows Admin Center](../understand/windows-admin-center.md) oder [jetzt herunterladen](https://aka.ms/windowsadmincenter).

## Verwalten von Windows Server-Computern

Sie können einzelne Server mit Windows Server 2012 oder höher bei Windows Admin Center zur Verwaltung des Servers mit einen umfassenden Satz von Tools einschließlich Zertifikaten, Geräte, Ereignisse, Prozesse, Rollen und Features, Updates, virtuelle Computer und mehr hinzufügen.

![Server-Verbindung Übersicht Bildschirm](../media/manage-servers/server-overview.png)

## Hinzufügen eines Servers zu Windows Admin Center

So fügen Sie einen Server in Windows Admin Center hinzu:

1. Klicken Sie unter alle Verbindungen auf **+ Hinzufügen** .
2. Wählen Sie zum Hinzufügen einer **Server-Verbindung**.
3. Geben Sie den Namen des Servers und, wenn Sie dazu aufgefordert werden, die Anmeldeinformationen zu verwenden.
4. Klicken Sie auf **übermitteln** zum Abschließen.

Der Server wird zur Verbindungsliste, auf der Seite "Übersicht" hinzugefügt werden. Klicken Sie auf, um die Verbindung mit dem Server.

> [!NOTE]
> Sie können auch [Failovercluster](manage-failover-clusters.md) oder [hyperkonvergenten Clustern](manage-hyper-converged.md) als separate Verbindung in Windows Admin Center hinzufügen.

## Tools

Die folgenden Tools sind für Server-Verbindungen verfügbar:

| Tool | Beschreibung |
| ---- | ----------- |
| [Übersicht](#overview) | Serverdetails anzeigen und der Zustand des Steuerelements |
| [Active Directory](#active-directory-preview) | Verwalten von Active Directory |
| [Sicherung](#backup) | Anzeigen und Konfigurieren von Azure Backup |  
| [Zertifikate](#certificates) | Anzeigen und Ändern von Zertifikaten |
| [Container](#containers) | Container anzeigen |
| [Geräte](#devices) | Anzeigen und Ändern von Geräten |
| [DHCP](#dhcp) | Zeigen Sie an und Verwalten von DHCP-Servers |
| [DNS](#dns) | Zeigen Sie an und Verwalten von DNS-Server-Konfiguration |
| [Ereignisse](#events) | Anzeigen von Ereignissen |
| [Dateien](#files) | Durchsuchen von Dateien und Ordnern |
| [Firewall](#firewall) | Zeigen Sie an und ändern Sie die Firewall-Regeln |
| [Installierte Apps](#installed-apps) | Anzeigen und installierten apps entfernen |
| [Lokale Benutzer und Gruppen](#local-users-and-groups) | Zeigen Sie an und ändern Sie lokale Benutzer und Gruppen |
| [Netzwerk](#network) | Anzeigen und Ändern von Netzwerkgeräte |
| [PowerShell](#powershell) | Interagieren Sie mit Server über PowerShell |
| [Prozesse](#processes) | Zeigen Sie an und ändern Sie die ausgeführten Prozesse |
| [Registrierung](#registry) | Zeigen Sie an und ändern Sie die Registrierungseinträge |
| [Remotedesktop](#remote-desktop) | Interagieren Sie mit Server über Remote Desktop |
| [Rollen und Features](#roles-and-features) | Anzeigen und Ändern von Rollen und features |
| [Geplante Aufgaben](#scheduled-tasks) | Anzeigen und Ändern von geplanten tasks |
| [Dienste](#services) | Anzeigen und Ändern der Dienste |
| [Einstellungen](#settings) | Anzeigen und Ändern der Dienste |
| [Speicher](#storage) | Anzeigen und Ändern von Speichergeräten |
| [Speicherdienst-Migration](#storage-migration-service) | Migrieren von Servern und Dateifreigaben für Azure oder Windows Server 2019 |
| [Speicherreplikat](#storage-replica) | Die Verwendung von Speicherreplikaten zum Verwalten von Server-zu-Server-Speicherreplikation |
| [System Insights](#system-insights) | System Insights bietet, die Sie einen Einblick in die Funktionsweise des Servers erhöht. |
| [Updates](#updates) | Ansicht installiert und nach neuen Updates suchen |
| [Virtuelle Computer](manage-virtual-machines.md) | Zeigen Sie an und Verwalten von virtuellen Computern |
| [Virtuelle Switches](#virtual-switches) | Zeigen Sie an und verwalten Sie virtuelle switches |

## Übersicht

**Übersicht über** können Sie finden Sie unter den aktuellen Zustand des CPU, Arbeitsspeicher und Leistung des Netzwerks, als auch Vorgänge ausführen, und ändern Einstellungen auf einem Zielcomputer oder Server.

### Features

Die folgenden Features werden in der Übersicht über die Server-Manager unterstützt:

- Anzeigen der Serverdetails
- Ansicht CPU-Aktivität
- Speicher-Aktivität anzeigen
- Netzwerk-Aktivität anzeigen
- Starten Sie Server neu
- Herunterfahren des Servers
- Datenträger-Metriken auf Server aktivieren
- Bearbeiten der Computer-ID auf server
- Zeigen Sie BMC-IP-Adresse mit Hyperlink (erfordert IPMI-kompatiblen BMC).

[**Ansicht Feedback und vorgeschlagenen Features für Server-Übersicht**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BOverview%5D).

## Active Directory (Vorschau)

**Active Directory** ist eine frühe Vorschau, die auf den [feed Erweiterung](../configure/using-extensions.md)verfügbar ist.

### Features

Die folgenden Active Directory-Verwaltung sind verfügbar:

- Benutzer erstellen
- Gruppe erstellen
- Suchen Sie nach dem Benutzer, Computer und Gruppen
- Detailbereich für Benutzer, Computer und Gruppen, wenn im Raster ausgewählt
- Globale Raster Aktionen Benutzer, Computer und Gruppen (aktivieren/deaktivieren, entfernen)
- Benutzerkennwort zurücksetzen
- Benutzerobjekte: Konfigurieren von grundlegenden Eigenschaften & Gruppenmitgliedschaften
- Computerobjekte: Delegierung auf einem einzelnen Computer konfigurieren
- Gruppieren Sie Objekte: Verwalten der Mitgliedschaft (Benutzer gleichzeitig hinzufügen oder Entfernen von 1)  

[**Ansicht Feedback und geplanten Funktionen für Active Directory**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BActive%20Directory%5D).

## Sicherung

**Sicherung** können Sie Ihre WindowsServer Schäden, Angriffe oder Notfällen zu schützen, durch das Sichern Ihrer Servers direkt in Microsoft Azure.
[Weitere Informationen zu Azure Backup.](https://aka.ms/windows-admin-center-backup)

[Übermitteln von Feedback für die Sicherung in Windows Admin Center](https://aka.ms/backup-wac-feedback)

### Features

Die folgenden Features sind in Sicherung unterstützt:

- Anzeigen einer Übersicht der Status Ihres Azure backup
- Konfigurieren von backup Elemente und Zeitplan
- Starten oder Beenden einer Sicherung bei ausgeführtem
- Anzeigen der Sicherung bei ausgeführtem Versionsgeschichte und status
- Wiederherstellungspunkte anzeigen und Wiederherstellen von Daten
- Löschen von backup-Daten

## Zertifikate

**Zertifikate** können Sie Zertifikatspeicher auf einem Computer oder einem Server zu verwalten.

### Features

Die folgenden Features sind in Zertifikate unterstützt:

- Hilfeartikel suchen Sie und Durchsuchen Sie vorhandene Zertifikate
- Anzeigen von Details zur Zertifikat
- Exportieren von Zertifikaten
- Zertifikate erneuern
- Neue Anfordern von Zertifikaten
- Löschen von Zertifikaten

[**Ansicht Feedback und vorgeschlagenen Features für Zertifikate**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BCertificates%5D).

## Container

**Container** können Sie die Container auf einem Windows Server-Container-Host anzeigen. Im Falle einer ausgeführten Windows Server Core-Container können Sie die Ereignisprotokolle anzeigen und Zugriff auf die CLI des Containers.

[**Ansicht Feedback und vorgeschlagenen Features für Container**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BContainers%5D).

## Geräte

**Geräte** können Sie verbundene Geräten auf einem Computer oder einem Server zu verwalten.

### Features

Die folgenden Features sind in Geräten unterstützt:

- Suchen und Durchsuchen Geräte
- Anzeigen von Details zur Gerät
- Deaktivieren eines Geräts
- Aktualisieren Sie Treiber auf einem Gerät

[**Ansicht Feedback und vorgeschlagenen Features für Geräte**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDevices%5D).

## DHCP

**DHCP** können Sie verbundene Geräten auf einem Computer oder einem Server zu verwalten.

### Features

- Erstellen und Konfigurieren von/Ansicht IPV4 und IPV6-Bereiche
- Erstellen Sie Adressenausschlüsse und konfigurieren Sie Start- und End-IP-Adresse
- Erstellen Sie Adresse Reservations und konfigurieren Sie Client MAC-Adresse (IPV4), DUID und IAID (IPV6)

[**Ansicht Feedback und vorgeschlagenen Features für DHCP**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDHCP%5D).

## DNS

**DNS** ermöglicht Ihnen, verbundene Geräte auf einem Computer oder einem Server zu verwalten.

### Features

- Anzeigen von Details zur von DNS-Forward-Lookupzonen, Reverse-Lookup-Zonen und DNS-Einträge
- Erstellen von forward-Lookupzonen (primär, sekundär oder Stub), und konfigurieren Sie die Eigenschaften der forward-Lookup-Zone
- Erstellen von Host (A oder AAAA), CNAME oder MX-Typ von DNS-Einträgen
- Konfigurieren von DNS-Ressourceneinträgen Eigenschaften
- Erstellen Sie IPV4 und IPV6-Reverse-Lookup-Zonen (primäre, sekundäre und -Stub), konfigurieren Sie die Eigenschaften der reverse-Lookup-Zone
- Erstellen von PTR, CNAME-Typ, der DNS-unter reverse-Lookupzone zeichnet.

[**Ansicht Feedback und vorgeschlagenen Features für DHCP**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDNS%5D).

## Ereignisse

**Ereignisse** können Sie die Ereignisprotokolle auf einem Computer oder einem Server zu verwalten.

### Features

Die folgenden Features werden in Ereignissen unterstützt:

- Suchen und Durchsuchen-Ereignisse
- Ereignisdetails anzeigen
- Ereignisse aus dem Protokoll löschen
- Exportieren von Ereignissen aus dem Protokoll

[**Ansicht Feedback und vorgeschlagenen Features für Ereignisse**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BEvents%5D).

## Dateien

**Dateien** können Sie Dateien und Ordner auf einem Computer oder einem Server zu verwalten.

### Features

Die folgenden Features sind in Dateien unterstützt:

- Durchsuchen von Dateien und Ordnern
- Suchen Sie nach einer Datei oder eines Ordners
- Erstellen Sie einen neuen Ordner
- Löschen einer Datei oder eines Ordners
- Herunterladen einer Datei oder eines Ordners
- Hochladen einer Datei oder eines Ordners
- Umbenennen einer Datei oder Ordner
- Extrahieren Sie die Zip-Datei
- Eigenschaften der Datei oder einen Ordner
- Resource Manager für Dateiserver [Kontingente](https://docs.microsoft.com/windows-server/storage/fsrm/quota-management) zu verwalten
- Hinzufügen, bearbeiten oder Entfernen von Dateifreigaben
- Ändern von Benutzer- und Gruppenkonten auf Dateifreigaben

[**Ansicht Feedback und vorgeschlagenen Features für Dateien**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFiles%5D).

## Firewall

**Firewall** können Sie zum Verwalten von Firewall-Einstellungen und Regeln auf einem Computer oder Server.

### Features

Die folgenden Features sind in der Firewall unterstützt:

- Anzeigen einer Übersicht der Firewall-Einstellungen
- Anzeigen von eingehenden Firewall-Regeln
- Ausgehenden Firewallregeln anzeigen
- Suche Firewall-Regeln
- Firewall-Regel-Details anzeigen
- Erstellen Sie eine neue Firewallregel
- Aktivieren Sie oder deaktivieren Sie eine Firewall-Regel
- Löschen Sie eine Firewall-Regel
- Bearbeiten Sie die Eigenschaften einer Firewall-Regel

[**Ansicht Feedback und vorgeschlagenen Features für die Firewall**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFirewall%5D).

## Installierte Apps

**Installierte Apps** können Sie zum Auflisten und Deinstallieren der Anwendung, die installiert sind.

[**Ansicht Feedback und vorgeschlagenen Features für Apps installiert**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BInstalled%20Apps%5D).

## Lokale Benutzer und Gruppen

**Lokale Benutzer und Gruppen** können Sie zum Verwalten von Sicherheitsgruppen und Benutzer, die lokal auf einem Computer oder einem Server vorhanden sind.

### Features

Die folgenden Features werden in lokale Benutzer und Gruppen unterstützt:

- Anzeigen und suchen Benutzer und Gruppen
- Erstellen eines neuen Benutzers oder einer Gruppe
- Verwalten der Gruppenmitgliedschaft eines Benutzers
- Löschen Sie einen Benutzer oder eine Gruppe
- Ändern des Kennworts eines Benutzers
- Bearbeiten Sie die Eigenschaften eines Benutzers oder einer Gruppe

[**Feedback und vorgeschlagenen Features für lokale Benutzer und Gruppen anzeigen**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BLocal%20users%20and%20Groups%5D)

## Netzwerk

**Netzwerk** können Sie Netzwerkgeräte und Einstellungen auf einem Computer oder einem Server zu verwalten.

### Features

Die folgenden Features sind im Netzwerk unterstützt:

- Hilfeartikel suchen Sie und Durchsuchen Sie vorhandene Netzwerkadapter
- Anzeigen von Details des Netzwerkadapters
- Bearbeiten der Eigenschaften eines Netzwerkadapters
- Erstellen Sie ein [Azure-Netzwerkadapter (Vorschaufeature)](https://blogs.technet.microsoft.com/networking/2018/09/05/azurenetworkadapter/)

[**Anzeigen von Feedback und vorgeschlagenen Features für Netzwerk**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BNetwork%5D)

## PowerShell

**PowerShell** können Sie mit einem Computer oder einem Server über eine PowerShell-Sitzung zu interagieren.

### Features

Die folgenden Features sind in PowerShell unterstützt:

- Erstellen Sie eine interaktive PowerShell-Sitzung auf dem server
- Trennen von PowerShell-Sitzung auf dem server

[**Anzeigen von Feedback und vorgeschlagenen Features für PowerShell**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BPowerShell%5D)

## Prozesse

**Prozesse** können Sie ausgeführten Prozesse auf einem Computer oder einem Server zu verwalten.

### Features

Die folgenden Features sind in Prozesse unterstützt:

- Suchen nach ausgeführten Prozessen
- Prozess-Details anzeigen
- Starten Sie einen Prozess
- Einen Prozess beenden
- Erstellen Sie eine prozesssicherung
- Suchen Sie Prozess behandelt

[**Ansicht Feedback und vorgeschlagenen Features für Prozesse**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BProcesses%5D).

## Registrierung

**Registrierung** können Sie die Registrierungsschlüssel und Werte auf einem Computer oder einem Server zu verwalten.

### Features

Die folgenden Features sind in der Registrierung unterstützt:

- Navigieren Sie Registrierungsschlüssel und Werte
- Hinzufügen oder Ändern von Registrierungswerten
- Registrierungswerte löschen

[**Ansicht Feedback und vorgeschlagenen Features für die Registrierung**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRegistry%5D).

## Remotedesktop

**Remote Desktop** können Sie mit einem Computer oder einem Server über eine interaktive Sitzung desktop interagieren.

### Features

Die folgenden Features sind in Remotedesktop unterstützt:

- Starten Sie eine interaktive Remotedesktopsitzung
- Trennen Sie eine Remotedesktopsitzung
- Senden Sie Strg + Alt + Entf für eine Remotedesktopsitzung

[**Ansicht Feedback und vorgeschlagenen Features für den Remotedesktop**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRemote%20Desktop%5D).

## Rollen und Features

**Rollen und Features** können Sie zum Verwalten von Rollen und Features auf einem Server.

### Features

Die folgenden Features sind in Rollen und Features unterstützt:

- Durchsuchen Sie die Liste von Rollen und Features auf einem server
- Rolle oder Feature Details anzeigen
- Installieren Sie eine Rolle oder feature
- Entfernen einer Rolle oder feature

[**Ansicht Feedback und vorgeschlagenen Features für Rollen und Features**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRoles%20and%20Features%5D).

## Geplante Aufgaben

**Geplante Aufgaben** können Sie geplante Tasks auf einem Computer oder einem Server zu verwalten.

### Features

Die folgenden Features sind in geplante Tasks unterstützt:

- Durchsuchen der Aufgabenplanungsbibliothek
- Bearbeiten Sie geplante Aufgaben
- Aktivieren von & deaktivieren, geplante Aufgaben
- Starten Sie & beenden geplante Aufgaben
- Erstellen Sie geplante Aufgaben

[**Ansicht Feedback und vorgeschlagenen Features für geplante Aufgaben**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BScheduled%20Tasks%5D).

## Dienste

**Dienste** können Sie Dienste auf einem Computer oder einem Server zu verwalten.

### Features

Die folgenden Features sind in Services unterstützt:

- Suchen und Durchsuchen Dienste auf einem server
- Anzeigen von Details zur eines Diensts
- Starten Sie einen Dienst
- Dienst anhalten
- Bearbeiten Sie die Eigenschaften eines Diensts

[**Ansicht Feedback und vorgeschlagenen Features für Dienste**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BServices%5D).

## Einstellungen

**Einstellungen** ist ein zentraler Ort zum Verwalten von Einstellungen auf einem Computer oder Server.

### Features

- Anzeigen und Ändern von Benutzer- und Umgebungsvariablen
- Zeigen Sie die Konfiguration für die Überwachung von [Azure-Monitor](azure-monitor.md) Warnungen an
- Zeigen Sie an und ändern Sie die Energiekonfiguration
- Anzeigen und Ändern von Remotedesktop-Einstellungen
- Anzeigen und Ändern von rollenbasierter Zugriff Steuerelement Einstellungen
- Anzeigen und Ändern von Hyper-V-Host-Einstellungsdatei, falls zutreffend

## Speicher

**Speicher** können Sie Speichergeräte auf einem Computer oder einem Server zu verwalten.

### Features

Die folgenden Features werden im Speicher unterstützt:

- Hilfeartikel suchen Sie und Durchsuchen Sie vorhandene Datenträger auf einem server
- Anzeigen von Details zur Datenträger
- Erstellen Sie ein volume
- Initialisieren eines Datenträgers
- Erstellen, Anfügen und Trennen einer virtuellen Festplatte (VHD)
- Schalten Sie einen Datenträger offline
- Formatieren Sie ein volume
- Ändern der Größe eines Volumes
- Bearbeiten Sie die Volume-Eigenschaften
- Löschen eines Datenträgers
- Installieren von Kontingentverwaltung

[**Anzeigen von Feedback und vorgeschlagenen Features für Speicher**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BStorage%5D)

## Speicherdienst-Migration

**Storage Migration Service** ermöglicht Ihnen das Migrieren von Servern und Dateifreigaben für Azure oder Windows Server 2019 – ohne apps oder Benutzer nichts ändern.
[Übersicht über die Storage Migration Service](https://go.microsoft.com/fwlink/?linkid=2016155)

>[!NOTE]
>Storage Migration Service erfordert Windows Server 2019.

## Speicherreplikat

Die Verwendung **Von Speicherreplikaten** zum Verwalten von Server-zu-Server-Speicherreplikation.
[Weitere Informationen zum Speicher-Replikat](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-ui)

## System Insights

**System Insights** führt vorhersehbare Analytics nativ in Windows Server zu ermöglichen Ihnen den erhöht Einblick in die Funktionsweise des Servers.
[Übersicht über die Systemeinblicke](http://aka.ms/systeminsights)

>[!NOTE]
>System Insights erfordert Windows Server 2019.

## Updates

**Updates** können Sie zum Verwalten von Microsoft und Windows-Updates auf einem Computer oder Server.

### Features

Die folgenden Features sind in Updates unterstützt:

- Anzeigen der verfügbaren Windows oder Microsoft-Updates
- Eine Liste der Updateverlauf anzeigen
- Installieren von Updates
- Online nach Updates von Microsoft Update suchen
- Verwalten von [Azure-Updateverwaltung](https://docs.microsoft.com/azure/automation/automation-update-management) -integration

[**Anzeigen von Feedback und vorgeschlagenen Features für Updates**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BUpdates%5D)

## Virtuelle Computer

Finden Sie unter [Verwalten von virtuellen Computern mit Windows Admin Center](manage-virtual-machines.md)

## Virtuelle Switches

**Virtuelle Switches** können Sie virtuelle Hyper-V-Switches auf einem Computer oder einem Server zu verwalten.

### Features

Die folgenden Features sind in virtuellen Switches unterstützt:

- Hilfeartikel suchen und Durchsuchen von virtuellen Switches auf einem server
- Erstellen Sie einen neuen virtuellen Switch
- Benennen Sie einen virtuellen Switch
- Löschen Sie einen vorhandenen virtuellen Switch
- Bearbeiten Sie die Eigenschaften eines virtuellen Switches

[**Anzeigen von Feedback und vorgeschlagenen Features für virtuelle Switches**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BVirtual%20Switch%5D)
