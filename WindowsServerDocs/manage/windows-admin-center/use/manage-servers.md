---
title: Verwalten von Servern mit dem Windows Admin Center
description: Verwalten von Servern mit dem Windows Admin Center (Project Honolulu)
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 11/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: 25edd2851638fec99b6afda0415fdf8e8c8f1699
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997190"
---
# <a name="manage-servers-with-windows-admin-center"></a>Verwalten von Servern mit dem Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

> [!Tip]
> Neu bei Windows Admin Center?
> [Weitere Informationen zum Windows Admin Center finden Sie hier](../overview.md).

## <a name="managing-windows-server-machines"></a>Verwalten von Windows Server-Computern

Sie können dem Windows Admin Center einzelne Server unter Windows Server 2012 oder höher hinzufügen, um den Server mit einem umfassenden Satz von Tools wie Zertifikaten, Geräten, Ereignissen, Prozessen, Rollen und Features, Updates, Virtual Machines und mehr zu verwalten.

![Übersichtsbildschirm der Server Verbindung](../media/manage-servers/server-overview.png)

## <a name="adding-a-server-to-windows-admin-center"></a>Hinzufügen eines Servers zum Windows Admin Center

So fügen Sie einen Server zum Windows Admin Center hinzu:

1. Klicken Sie unter alle Verbindungen auf **+ Hinzufügen** .
2. Wählen Sie die Option zum Hinzufügen einer **Server Verbindung**aus.
3. Geben Sie den Namen des Servers und, wenn Sie dazu aufgefordert werden, die zu verwendenden Anmelde Informationen ein.
4. Klicken Sie zum fertig **Stellen auf Senden** .

Der Server wird auf der Übersichtsseite zur Verbindungsliste hinzugefügt. Klicken Sie darauf, um eine Verbindung mit dem Server herzustellen.

> [!NOTE]
> Außerdem können Sie [Failovercluster](manage-failover-clusters.md) oder [hyperkonvergierte Cluster](manage-hyper-converged.md) als separate Verbindung im Windows Admin Center hinzufügen.

## <a name="tools"></a>Tools

Die folgenden Tools sind für Serververbindungen verfügbar:

| Tool | BESCHREIBUNG |
| ---- | ----------- |
| [Übersicht](#overview) | Anzeigen von Server Details und Steuern des Serverstatus |
| [Active Directory](#active-directory-preview) | Verwalten von Active Directory |
| [Backup](#backup) | Azure Backup anzeigen und konfigurieren |
| [Zertifikate](#certificates) | Anzeigen und Ändern von Zertifikaten |
| [Container](#containers) | Container anzeigen |
| [Geräte](#devices) | Anzeigen und Ändern von Geräten |
| [DHCP](#dhcp) | Anzeigen und Verwalten der DHCP-Serverkonfiguration |
| [DNS](#dns) | Anzeigen und Verwalten der DNS-Serverkonfiguration |
| [Ereignisse](#events) | Anzeigen von Ereignissen |
| [Dateien](#files) | Durchsuchen von Dateien und Ordnern |
| [Firewall](#firewall) | Anzeigen und Ändern von Firewallregeln |
| [Installierte apps](#installed-apps) | Anzeigen und Entfernen installierter apps |
| [Lokale Benutzer und Gruppen](#local-users-and-groups) | Anzeigen und ändern lokaler Benutzer und Gruppen |
| [Netzwerk](#network) | Anzeigen und Ändern von Netzwerkgeräten |
| [Paket Überwachung](https://aka.ms/wac1908) | Überwachen von Netzwerk Paketen |
| [System Monitor](https://aka.ms/perfmon-blog) | Anzeigen von Leistungsindikatoren und Berichten |
| [PowerShell](#powershell) | Interagieren mit dem Server über PowerShell |
| [Prozesse](#processes) | Anzeigen und Ändern von laufenden Prozessen |
| [Registrierung](#registry) | Anzeigen und Ändern von Registrierungs Einträgen |
| [Remotedesktop](#remote-desktop) | Interagieren mit dem Server über Remotedesktop |
| [Rollen und Features](#roles-and-features) | Anzeigen und Ändern von Rollen und Features |
| [Geplante Aufgaben](#scheduled-tasks) | Anzeigen und Ändern geplanter Aufgaben |
| [Dienste](#services) | Anzeigen und Ändern von Diensten |
| [Einstellungen](#settings) | Anzeigen und Ändern von Diensten |
| [Storage](#storage) | Anzeigen und Ändern von Speichergeräten |
| [Speichermigrationsdienst](#storage-migration-service) | Migrieren von Servern und Dateifreigaben zu Azure oder Windows Server 2019 |
| [Speicherreplikat](#storage-replica) | Verwenden von Speicher Replikaten zum Verwalten der Server-zu-Server-Speicher Replikation |
| [Systemdaten](#system-insights) | Mit System Insights erhalten Sie einen besseren Einblick in die Funktionsweise des Servers. |
| [Updates](#updates) | Installierte anzeigen und nach neuen Updates suchen |
| [Virtuelle Computer](manage-virtual-machines.md) | Anzeigen und Verwalten virtueller Maschinen |
| [Virtuelle Switches](#virtual-switches) | Virtuelle Switches anzeigen und verwalten |

## <a name="overview"></a>Übersicht

In der **Übersicht** können Sie den aktuellen Status der CPU-, Arbeitsspeicher-und Netzwerkleistung anzeigen sowie Vorgänge ausführen und Einstellungen auf einem Zielcomputer oder-Server ändern.

### <a name="features"></a>Features

Die folgenden Funktionen werden in Server-Manager Übersicht unterstützt:

- Server Details anzeigen
- Anzeigen der CPU-Aktivität
- Arbeitsspeicher Aktivität anzeigen
- Netzwerkaktivität anzeigen
- Neustarten des Servers
- Server herunterfahren
- Datenträger auf dem Server aktivieren
- Computer-ID auf Server bearbeiten
- BMC-IP-Adresse mit Hyperlink anzeigen (erfordert IPMI-kompatiblen BMC).

[**Anzeigen von Feedback und vorgeschlagenen Features für Server Übersicht**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BOverview%5D).

## <a name="active-directory-preview"></a>Active Directory (Vorschau)

**Active Directory** ist eine frühe Vorschau, die im [Erweiterungs Feed](../configure/using-extensions.md)verfügbar ist.

### <a name="features"></a>Features

Die folgenden Active Directory Verwaltung sind verfügbar:

- Benutzer erstellen
- Erstellen einer Gruppe
- Suchen nach Benutzern, Computern und Gruppen
- Detailbereich für Benutzer, Computer und Gruppen, wenn diese im Raster ausgewählt sind
- Globale Raster Aktionen Benutzer, Computer und Gruppen (deaktivieren/aktivieren, entfernen)
- Benutzerkennwort zurücksetzen
- Benutzer Objekte: Konfigurieren der grundlegenden Eigenschaften & Gruppenmitgliedschaften
- Computer Objekte: Konfigurieren der Delegierung für einen einzelnen Computer
- Gruppieren von Objekten: Mitgliedschaft verwalten (1 Benutzer gleichzeitig hinzufügen/entfernen)

[**Anzeigen von Feedback und vorgeschlagenen Features für Active Directory**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BActive%20Directory%5D).

## <a name="backup"></a>Backup

Mit **Backup** können Sie Ihren Windows-Server vor Beschädigungen, Angriffen oder Notfällen schützen, indem Sie den Server direkt auf Microsoft Azure sichern.
[Erfahren Sie mehr über Azure Backup.](https://aka.ms/windows-admin-center-backup)

[Bereitstellen von Feedback für die Sicherung im Windows Admin Center](https://aka.ms/backup-wac-feedback)

### <a name="features"></a>Features

Die folgenden Funktionen werden bei der Sicherung unterstützt:

- Anzeigen einer Übersicht über den Azure Backup-Status
- Sicherungselemente und Zeitplan konfigurieren
- Starten oder Abbrechen eines Sicherungsauftrags
- Verlauf und Status des Sicherungsauftrags anzeigen
- Anzeigen von Wiederherstellungs Punkten und Wiederherstellen von Daten
- Löschen von Sicherungsdaten

## <a name="certificates"></a>Zertifikate

Mithilfe von **Zertifikaten** können Sie Zertifikat Speicher auf einem Computer oder Server verwalten.

### <a name="features"></a>Features

Die folgenden Funktionen werden in Zertifikaten unterstützt:

- Durchsuchen und Durchsuchen vorhandener Zertifikate
- Anzeigen von Zertifikat Details
- Exportieren von Zertifikaten
- Erneuern von Zertifikaten
- Neue Zertifikate anfordern
- Löschen von Zertifikaten

[**Feedback und vorgeschlagene Features für Zertifikate anzeigen**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BCertificates%5D).

## <a name="containers"></a>Container

Mithilfe von **Containern** können Sie die Container auf einem Windows Server-Container Host anzeigen. Wenn Sie einen Windows Server Core-Container ausführen, können Sie die Ereignisprotokolle anzeigen und auf die CLI des Containers zugreifen.

[**Anzeigen von Feedback und vorgeschlagenen Features für Container**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BContainers%5D).

## <a name="devices"></a>Geräte

Mithilfe von **Geräten** können Sie verbundene Geräte auf einem Computer oder Server verwalten.

### <a name="features"></a>Features

Die folgenden Funktionen werden von Geräten unterstützt:

- Suchen und suchen von Geräten
- Anzeigen von Gerätedetails
- Deaktivieren eines Geräts
- Aktualisieren eines Treibers auf einem Gerät

[**Anzeigen von Feedback und vorgeschlagenen Features für Geräte**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDevices%5D)

## <a name="dhcp"></a>DHCP

Mit **DHCP** können Sie verbundene Geräte auf einem Computer oder Server verwalten.

### <a name="features"></a>Features

- Erstellen/Konfigurieren/Anzeigen von IPv4-und IPv6-Bereichen
- Adress Ausschlüsse erstellen und Start-und End-IP-Adresse konfigurieren
- Erstellen von Adress Reservierungen und Konfigurieren der Client-MAC-Adresse (IPv4), DUID und IAID (IPv6)

[**Anzeigen von Feedback und vorgeschlagenen Features für DHCP**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDHCP%5D).

## <a name="dns"></a>DNS

Mithilfe von **DNS** können Sie verbundene Geräte auf einem Computer oder Server verwalten.

### <a name="features"></a>Features

- Details der DNS-Forward-Lookupzonen, Reverse-Lookupzonen und DNS-Einträge anzeigen
- Erstellen von Forward-Lookupzonen (primär, Sekundär oder Stub) und Konfigurieren von Forward-lookupzoneneigenschaften
- Erstellen von Host-(A-oder AAAA-), CNAME-oder MX-Typen von DNS-Einträgen
- Konfigurieren von DNS-Daten Satz Eigenschaften
- Erstellen von IPv4-und IPv6-Reverse-Lookupzonen (primär, Sekundär und Stub), Konfigurieren von Reverse-Lookupzonen-Eigenschaften
- Erstellen Sie PTR, CNAME-Typ der DNS-Einträge in der Reverse-Lookupzone.

[**Anzeigen von Feedback und vorgeschlagenen Features für DHCP**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDNS%5D).

## <a name="events"></a>Ereignisse

**Ereignisse** ermöglichen es Ihnen, Ereignisprotokolle auf einem Computer oder Server zu verwalten.

### <a name="features"></a>Features

Die folgenden Funktionen werden in Ereignissen unterstützt:

- Durchsuchen und Durchsuchen von Ereignissen
- Anzeigen von Ereignisdetails
- Ereignisse aus dem Protokoll löschen
- Ereignisse aus dem Protokoll exportieren

[**Anzeigen von Feedback und vorgeschlagenen Features für Ereignisse**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BEvents%5D).

## <a name="files"></a>Dateien

Mithilfe von **Dateien** können Sie Dateien und Ordner auf einem Computer oder Server verwalten.

### <a name="features"></a>Features

Die folgenden Funktionen werden in Dateien unterstützt:

- Durchsuchen von Dateien und Ordnern
- Nach einer Datei oder einem Ordner suchen
- Erstellen eines neuen Ordners
- Löschen einer Datei oder eines Ordners
- Herunterladen einer Datei oder eines Ordners
- Hochladen von Dateien oder Ordnern
- Umbenennen einer Datei oder eines Ordners
- Extrahieren einer ZIP-Datei
- Kopieren und Verschieben von Dateien und Ordnern
- Anzeigen von Datei-oder Ordnereigenschaften
- Hinzufügen, bearbeiten oder Entfernen von Dateifreigaben
- Ändern von Benutzer-und Gruppenberechtigungen für Dateifreigaben

[**Anzeigen von Feedback und vorgeschlagenen Features für Dateien**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFiles%5D).

## <a name="firewall"></a>Firewall

Mithilfe der **Firewall** können Sie Firewalleinstellungen und-Regeln auf einem Computer oder Server verwalten.

### <a name="features"></a>Features

Die folgenden Funktionen werden in der Firewall unterstützt:

- Anzeigen einer Übersicht über die Firewalleinstellungen
- Eingehende Firewallregeln anzeigen
- Ausgehende Firewallregeln anzeigen
- Firewallregeln suchen
- Anzeigen von firewallregeldetails
- Erstellen einer neuen Firewallregel
- Aktivieren oder Deaktivieren einer Firewallregel
- Löschen einer Firewallregel
- Bearbeiten der Eigenschaften einer Firewallregel

[**Anzeigen von Feedback und vorgeschlagenen Features für die Firewall**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFirewall%5D).

## <a name="installed-apps"></a>Installierte Apps

Mithilfe **installierter apps** können Sie installierte Anwendungen auflisten und deinstallieren.

[**Feedback und vorgeschlagene Features für installierte apps anzeigen**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BInstalled%20Apps%5D).

## <a name="local-users-and-groups"></a>Lokale Benutzer und Gruppen

**Lokale Benutzer und Gruppen** ermöglichen Ihnen das Verwalten von Sicherheitsgruppen und Benutzern, die lokal auf einem Computer oder Server vorhanden sind.

### <a name="features"></a>Features

Die folgenden Funktionen werden in lokalen Benutzern und Gruppen unterstützt:

- Anzeigen und Durchsuchen von Benutzern und Gruppen
- Neuen Benutzer oder eine neue Gruppe erstellen
- Verwalten der Gruppenmitgliedschaft eines Benutzers
- Löschen eines Benutzers oder einer Gruppe
- Ändern des Kennworts eines Benutzers
- Bearbeiten der Eigenschaften eines Benutzers oder einer Gruppe

[**Feedback und vorgeschlagene Features für lokale Benutzer und Gruppen anzeigen**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BLocal%20users%20and%20Groups%5D)

## <a name="network"></a>Netzwerk

Mit dem **Netzwerk** können Sie Netzwerkgeräte und-Einstellungen auf einem Computer oder Server verwalten.

### <a name="features"></a>Features

Die folgenden Funktionen werden im Netzwerk unterstützt:

- Durchsuchen und Durchsuchen vorhandener Netzwerkadapter
- Anzeigen der Details eines Netzwerkadapters
- Bearbeiten der Eigenschaften eines Netzwerkadapters
- Erstellen eines [Azure-Netzwerkadapters (Vorschau Feature)](https://blogs.technet.microsoft.com/networking/2018/09/05/azurenetworkadapter/)

[**Feedback und vorgeschlagene Features für das Netzwerk anzeigen**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BNetwork%5D)

## <a name="powershell"></a>PowerShell

**PowerShell** ermöglicht die Interaktion mit einem Computer oder Server über eine PowerShell-Sitzung.

### <a name="features"></a>Features

Die folgenden Funktionen werden in PowerShell unterstützt:

- Erstellen einer interaktiven PowerShell-Sitzung auf dem Server
- Trennen der Verbindung mit der PowerShell-Sitzung auf dem Server

[**Feedback und vorgeschlagene Features für PowerShell anzeigen**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BPowerShell%5D)

## <a name="processes"></a>Prozesse

Mit **Prozessen** können Sie laufende Prozesse auf einem Computer oder Server verwalten.

### <a name="features"></a>Features

Die folgenden-Funktionen werden in-Prozessen unterstützt:

- Durchsuchen und nach laufenden Prozessen suchen
- Prozessdetails anzeigen
- Starten eines Prozesses
- Beenden eines Prozesses
- Erstellen eines Prozess Abbilds
- Prozess Handles suchen

[**Anzeigen von Feedback und vorgeschlagenen Features für Prozesse**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BProcesses%5D).

## <a name="registry"></a>Registrierung

Die **Registrierung** ermöglicht es Ihnen, Registrierungsschlüssel und-Werte auf einem Computer oder Server zu verwalten.

### <a name="features"></a>Features

Die folgenden Funktionen werden in der Registrierung unterstützt:

- Durchsuchen von Registrierungs Schlüsseln und-Werten
- Registrierungs Werte hinzufügen oder ändern
- Löschen von Registrierungswerten

[**Anzeigen von Feedback und vorgeschlagenen Features für die Registrierung**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRegistry%5D).

## <a name="remote-desktop"></a>Remotedesktop

**Remotedesktop** ermöglicht es Ihnen, über eine interaktive Desktop Sitzung mit einem Computer oder Server zu interagieren.

### <a name="features"></a>Features

Die folgenden Funktionen werden in Remotedesktop unterstützt:

- Starten einer interaktiven Remote Desktop Sitzung
- Verbindung mit einer Remote Desktop Sitzung trennen
- STRG + ALT + ENTF an eine Remote Desktop Sitzung senden

[**Anzeigen von Feedback und vorgeschlagenen Features für Remotedesktop**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRemote%20Desktop%5D).

## <a name="roles-and-features"></a>Rollen und Features

Mithilfe von **Rollen und Features** können Sie Rollen und Features auf einem Server verwalten.

### <a name="features"></a>Features

Die folgenden Funktionen werden in Rollen und Features unterstützt:

- Liste der Rollen und Features auf einem Server durchsuchen
- Anzeigen von Rollen-oder Featuredetails
- Installieren einer Rolle oder eines Features
- Entfernen einer Rolle oder eines Features

[**Anzeigen von Feedback und vorgeschlagenen Features für Rollen und Features**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRoles%20and%20Features%5D).

## <a name="scheduled-tasks"></a>Geplante Tasks

Mit **geplanten Tasks** können Sie geplante Aufgaben auf einem Computer oder Server verwalten.

### <a name="features"></a>Features

Die folgenden Funktionen werden in geplanten Tasks unterstützt:

- Durchsuchen der Aufgabenplaner-Bibliothek
- Geplante Aufgaben bearbeiten
- Aktivieren & deaktivieren geplanter Aufgaben
- Starten & geplante Aufgaben Abbrechen
- Erstellen geplanter Aufgaben

[**Anzeigen von Feedback und vorgeschlagenen Features für geplante Aufgaben**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BScheduled%20Tasks%5D).

## <a name="services"></a>Dienste

**Dienste** ermöglichen es Ihnen, Dienste auf einem Computer oder Server zu verwalten.

### <a name="features"></a>Features

Die folgenden Funktionen werden in-Diensten unterstützt:

- Durchsuchen und Durchsuchen von Diensten auf einem Server
- Anzeigen von Details zu einem Dienst
- Starten eines Diensts
- Dienst anhalten
- Neustart eines Dienstanbieter
- Bearbeiten der Eigenschaften eines Dienstanbieter

[**Anzeigen von Feedback und vorgeschlagenen Features für Dienste**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BServices%5D).

## <a name="settings"></a>Einstellung

**Einstellungen** ist ein zentraler Ort zum Verwalten von Einstellungen auf einem Computer oder Server.

### <a name="features"></a>Features

- Anzeigen und Ändern von Benutzer-und System Umgebungsvariablen
- Anzeigen der Konfiguration zum Überwachen von Warnungen von [Azure Monitor](../azure/azure-monitor.md)
- Anzeigen und Ändern der Energie Konfiguration
- Anzeigen und Ändern von Remotedesktop Einstellungen
- Anzeigen und Ändern der rollenbasierten Zugriffs Steuerungseinstellungen
- Anzeigen und Ändern von Hyper-V-Host Einstellungen (falls zutreffend)

## <a name="storage"></a>Storage

Mithilfe von **Speicher** können Sie Speichergeräte auf einem Computer oder Server verwalten.

### <a name="features"></a>Features

Die folgenden Funktionen werden im Speicher unterstützt:

- Durchsuchen und Durchsuchen vorhandener Datenträger auf einem Server
- Anzeigen von Datenträger Details
- Erstellen eines Volumes
- Initialisieren eines Datenträgers
- Erstellen, Anfügen und Trennen einer virtuellen Festplatte (VHD)
- Offline schalten eines Datenträgers
- Formatieren eines Volumes
- Ändern der Größe eines Volumes
- Volumeeigenschaften bearbeiten
- Löschen von Volumes
- Installieren der Kontingent Verwaltung
- Verwalten von Dateiservern Ressourcen-Manager Kontingente [Storage->Create/Update-Kontingent](../../../storage/fsrm/quota-management.md)

[**Feedback und vorgeschlagene Features für den Speicher anzeigen**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BStorage%5D)

## <a name="storage-migration-service"></a>Speichermigrationsdienst

**Storage Migration Service** ermöglicht es Ihnen, Server und Dateifreigaben zu Azure oder Windows Server 2019 zu migrieren – ohne dass Apps oder Benutzer Änderungen vornehmen müssen.
[Verschaffen Sie sich einen Überblick über den Speicher Migrationsdienst.](https://go.microsoft.com/fwlink/?linkid=2016155)

>[!NOTE]
>Der Speicher Migrationsdienst erfordert Windows Server 2019.

## <a name="storage-replica"></a>Speicherreplikat

Verwenden Sie **Speicher** Replikate zum Verwalten der Server-zu-Server-Speicher Replikation.
 [Weitere Informationen zum Speicherreplikat](../../../storage/storage-replica/server-to-server-storage-replication.md)

## <a name="system-insights"></a>Systemdaten

**System Insights** führt Predictive Analytics nativ in Windows Server ein, um Ihnen einen besseren Einblick in die Funktionsweise des Servers zu bieten.
[Verschaffen Sie sich einen Überblick über System Einblicke](https://aka.ms/systeminsights)

>[!NOTE]
>System Insights erfordert Windows Server 2019.

## <a name="updates"></a>Aktualisierungen

Mit **Updates** können Sie Microsoft-und/oder Windows-Updates auf einem Computer oder Server verwalten.

### <a name="features"></a>Features

Die folgenden Funktionen werden bei Updates unterstützt:

- Anzeigen der verfügbaren Windows-oder Microsoft-Updates
- Anzeigen einer Liste mit Update Verlauf
- Installieren von Updates
- Online nach Updates suchen Microsoft Update
- Verwalten der Integration von [Azure Updateverwaltung](/azure/automation/automation-update-management)

[**Feedback und vorgeschlagene Features für Updates anzeigen**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BUpdates%5D)

## <a name="virtual-machines"></a>Virtual Machines

Siehe [Verwalten von Virtual Machines mit dem Windows Admin Center](manage-virtual-machines.md)

## <a name="virtual-switches"></a>Virtuelle Switches

Mit **virtuellen Switches** können Sie virtuelle Hyper-V-Switches auf einem Computer oder Server verwalten.

### <a name="features"></a>Features

Die folgenden Funktionen werden in virtuellen Switches unterstützt:

- Durchsuchen und Durchsuchen virtueller Switches auf einem Server
- Neuen virtuellen Switch erstellen
- Umbenennen eines virtuellen Switches
- Löschen eines vorhandenen virtuellen Switches
- Bearbeiten der Eigenschaften eines virtuellen Switches

[**Feedback und vorgeschlagene Features für virtuelle Switches anzeigen**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BVirtual%20Switch%5D)