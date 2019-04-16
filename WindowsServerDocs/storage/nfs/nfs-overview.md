---
title: Network File System (Übersicht)
description: Erläutert, was Network File System.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: fb31cff44cac6bd66f9aa5b7234ff3fd3b215ccf
ms.sourcegitcommit: bad0692ffd0773f61ac62bd140a421cb02c68acf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/22/2019
ms.locfileid: "9099139"
---
# Network File System (Übersicht)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Dieses Thema beschreibt die Network File System-Rollendienst und Features, die mit der Datei- und Speicherdienste-Serverrolle in Windows Server enthalten. Network File System (NFS) stellt eine dateifreigabelösung für Unternehmen, die über heterogene Umgebungen, die verfügen sowohl für Windows als auch für nicht-Windows-Computern.

## Featurebeschreibung

Verwenden das NFS-Protokoll, können Sie Dateien zwischen Computern unter Windows und andere nicht-Windows-Betriebssysteme, z. B. Linux oder UNIX übertragen.

NFS in Windows Server enthält Server für NFS und Client für NFS. Ein Computer unter Windows Server können Server für NFS fungieren als Dateiserver NFS für andere nicht-Windows-Clientcomputer. Client für NFS ermöglicht einem Windows-basierten Computer unter Windows Server auf Dateien zugreifen, die auf einem nicht - Windows-NFS-Server gespeichert.

## Windows und Windows Server-Versionen

Windows unterstützt mehrere Versionen des NFS-Client und Server, je nach Version des Betriebssystems und Familie. 

| Betriebssysteme | NFS-Server-Versionen |NFS-Client-Versionen|
| ----------------- | ------------------- | ----------------- |
| Windows 7, Windows 8.1, Windows 10 | n.v. | NFS V2, NFS V3 |
| WindowsServer 2008, Windows Server 2008 R2 | NFS V2, NFS V3 | NFS V2, NFS V3 |
| Windows Server 2012, Windows Server 2012 R2, WindowsServer 2016, WindowsServer 2019 | NFS V2, NFS V3, NFSv4.1  | NFS V2, NFS V3 |

## Praktische Anwendungsfälle

Hier sind einige Möglichkeiten, die Sie NFS verwenden können:

- Verwenden Sie einen Windows-NFS-Dateiserver, um die Multi-Protokoll-Zugriff auf die gleichen Dateifreigabe über SMB sowohl NFS-Protokolle von Multi-Plattform-Clients bereitzustellen.
- Bereitstellen von einem Windows-NFS-Dateiserver in einer Umgebung vorwiegend nicht-Windows-Betriebssystem nicht-Windows-Computern auf NFS Dateifreigaben zuzugreifen.
- Migrieren Sie Anwendungen von einem Betriebssystem zu einer anderen durch Speicherung der Daten auf Dateifreigaben über SMB sowohl NFS Protokolle zugänglich.

## Neue und geänderte Funktionalität

Neue und geänderte Funktionen in Network File System enthält Unterstützung für die NFS Version 4.1 und verbesserte Bereitstellung und Verwaltung. Informationen zu Funktionen, die neue oder geänderte in Windows Server 2012 finden Sie in der folgenden Tabelle:

|Feature/Funktionalität|Neu oder aktualisiert|Beschreibung|
|---|---|---|
|[NFS Version 4.1](#nfs-version-4.1)|Neu|Erhöhte Sicherheit, Leistung und Interoperabilität im Vergleich zu NFS Version 3.|
|[NFS-Infrastruktur](#nfs-infrastructure)|Aktualisiert|Verbessert die Bereitstellung und Verwaltung und erhöht die Sicherheit.|
|[NFS Version 3 kontinuierlicher Verfügbarkeit](#nfs-version-3-continuous-availability)|Aktualisiert|Verbessert die kontinuierlichen Verfügbarkeit auf NFS Version 3-Clients.|
|[Verbesserung der Bereitstellung und Verwaltung](#deployment-and-manageability-improvements)|Aktualisiert|Können Sie auf einfache Weise bereitstellen und Verwalten von NFS mit neuen Windows PowerShell-Cmdlets und einen neuen WMI-Anbieter.|

## NFS Version 4.1

NFS Version 4.1 implementiert die erforderlichen Aspekte, zusätzlich zu einige der optionalen Aspekte, [RFC 5661](https://tools.ietf.org/html/rfc5661):

- **Pseudo-Dateisystem**, ein Dateisystem, das die physische und logische Namespace trennt und mit NFS Version 3 und NFS Version 2 kompatibel ist. Alias wird für das exportierte Dateisystem, das Pseudo-Dateisystem gehört bereitgestellt.
- **Zusammengesetzte RPCs** relevante Vorgänge kombinieren und ausgetauschten zu reduzieren.
- **-Sitzungen und Sitzung Trunking** ermöglicht nur eine Semantik und kontinuierlicher Verfügbarkeit und eine bessere Leistung bei Verwendung der mehrere Netzwerke zwischen NFS 4.1-Clients und dem NFS-Server.

## NFS-Infrastruktur

Verbesserungen für die allgemeine NFS-Infrastruktur in Windows Server 2012 sind unten aufgeführt:

- Der **Remote Procedure Call (RPC) / externen Daten Darstellung (XDR)** Transport-Infrastruktur, durch das WinSock-Netzwerkprotokoll für beide Server für NFS und Client für NFS verfügbar ist. Dies ersetzt Transport Device Interface (TDI) bietet eine bessere Unterstützung und bietet eine bessere Skalierbarkeit und erhalten Seite Skalierung (RSS).
- Das Feature **RPC-Port multiplexer** ist Firewall-freundliche (weniger Ports zum Verwalten von) und vereinfacht die Bereitstellung von NFS.
- **Caches Auto-optimiert und Threadpools** sind Resource Management-Funktionen der neuen RPC/XDR-Infrastruktur, die dynamische automatisch optimieren Caches und thread basierend auf Workload Pools. Dadurch wird der beteiligten wie schwer ausfällt vollständig entfernt, beim Optimieren der Parameter eine optimale Leistung als NFS bereitgestellt wird.
- **Neue Kerberos Datenschutz Implementierung und Authentifizierung Optionen** durch das Hinzufügen von Unterstützung des Kerberos-Datenschutz (Krb5p) zusammen mit dem vorhandenen krb5- und krb5i-Authentifizierungsoptionen.
- **Identität Zuordnung Windows PowerShell-Modul** -Cmdlets erleichtern die Identität Zuordnung verwalten, Active Directory Lightweight Directory Services (AD LDS) konfigurieren und Einrichten des UNIX und Linux Kennwort- und flache Dateien.
- **Volume Bereitstellungspunkt** ermöglicht den Zugriff auf Volumes, die unter einer NFS-Freigabe mit NFS Version 4.1 bereitgestellt.
- Das Feature **Port Multiplexing** unterstützt den RPC-Port multiplexer (Port 2049), die Firewall-freundliche und vereinfacht die NFS-Bereitstellung.

## NFS Version 3 kontinuierlicher Verfügbarkeit

NFS Version 3-Clients können schnell und transparent geplanten Failover mehr Verfügbarkeit und Ausfallzeiten reduziert. Die Failover-Verfahren ist schneller für NFS Version 3-Clients, da:

- Die clustering-Infrastruktur kann jetzt eine Ressource pro Netzwerknamen anstatt eine Ressource pro-Freigabe, die Ressourcen Failover-Zeit erheblich verbessert.
- Failover-Pfade in einem NFS-Server werden für eine bessere Leistung optimiert.
- Platzhalter-Registrierung in einem NFS-Server ist nicht mehr erforderlich, und die Failovers werden mehr optimiert.
- Netzwerk Status Monitor (NSM) Benachrichtigungen nach einem Failoverprozess gesendet werden, und Clients nicht mehr benötigen, warten Sie Timeouts TCP-Verbindung zum fehlgeschlagenen über Server.

Beachten Sie, dass der Server für NFS transparentes Failover unterstützt geplant nur, wenn manuell initiiert, in der Regel während der Wartung. Wenn ein ungeplantes Failovers auftritt, verlieren NFS-Clients ihre Verbindungen. Server für NFS verfügen nicht auch eine Integration mit dem Filter fortsetzen Schlüssel. Dies bedeutet, wenn eine lokale app oder die SMB-Sitzung versucht, auf die gleiche Datei zugreifen, die ein Client für NFS unmittelbar nach einem geplanten Failover zugreift, der NFS-Client seine Verbindungen verloren gehen möglicherweise (transparentes Failover würde nicht erfolgreich abgeschlossen).

## Verbesserung der Bereitstellung und Verwaltung

Bereitstellen und Verwalten von NFS wurde auf folgende Weise verbessert:

- Über 40 neue Windows PowerShell-Cmdlets erleichtern das Konfigurieren und Verwalten von NFS-Dateifreigaben. Weitere Informationen finden Sie unter [NFS-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps).
- Identität Zuordnung wird mit einer lokalen flache Zuordnung Dateispeicher und neue Windows PowerShell-Cmdlets zum Konfigurieren der Identität-Zuordnung verbessert.
- Die Server-Manager-Benutzeroberfläche ist einfacher zu verwenden.
- Der neuen Version 2 WMI-Anbieter ist zur einfacheren Verwaltung verfügbar.
- Der RPC-Port multiplexer (Port 2049) ist Firewall-freundliche und vereinfacht die Bereitstellung von NFS.

## Informationen zum Server-Manager

Verwenden Sie im Server-Manager- oder die neuere [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md) - Hinzufügen von Rollen und Features-Assistenten auf den Server für NFS-Rollendienst hinzuzufügen (unter der Datei- und iSCSI-Services-Rolle). Allgemeine Informationen zum Installieren von Features finden Sie unter [installieren oder Deinstallieren von Rollen, Rollendiensten oder Features](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831809(v=ws.11)>). Server für NFS Tools enthalten, die Dienste für Network Datei System MMC-Snap-in für die Verwaltung der Server für NFS und Client für NFS-Komponenten. Verwenden das Snap-In, können Sie den Server für NFS-Komponenten, die auf dem Computer installiert verwalten. Server für NFS enthält auch mehrere Windows Befehlszeilen-Verwaltungstools:

- **Bereitstellen** eine NFS Remotefreigabe (auch bekannt als eine exportieren) lokal bereitgestellt und eine Zuordnung zu einem lokalen Laufwerkbuchstaben auf dem Windows-Clientcomputer.
- **Nfsadmin** verwaltet Konfigurationseinstellungen des Servers für NFS und Client für NFS-Komponenten.
- **Nfsshare** konfiguriert NFS-Freigabe-Einstellungen für Ordner, die mit Server für NFS freigegeben wurden.
- **Nfsstat** zeigt oder setzt Statistiken von aufrufen, die vom Server für NFS empfangen.
- **Showmount** zeigt die bereitgestellte Datei-Systeme, die vom Server für NFS exportiert haben.
- **Unmount** entfernt NFS bereitgestellte Laufwerke.

NFS in Windows Server 2012 führt das NFS-Modul für Windows PowerShell mit mehrere neue Cmdlets speziell für NFS. Diese Cmdlets bieten eine einfache Möglichkeit zum Automatisieren von Verwaltungsaufgaben für NFS. Weitere Informationen finden Sie unter [NFS-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps).

## Weitere Informationen

Die folgende Tabelle enthält zusätzliche Ressourcen für das Auswerten von NFS.

|Inhaltstyp|Verweise|
|---|---|
|Bereitstellung|[Network File System bereitstellen](deploy-nfs.md)|
|Vorgänge|[NFS-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)|
|Verwandte Technologien|[Speicher in Windows Server](../storage.md)|