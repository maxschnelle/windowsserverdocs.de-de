---
title: Übersicht über die Dateifreigabe über das SMB-3-Protokoll in Windows Server
description: Eine Übersicht über das SMB-3-Protokoll für Dateifreigaben und Bereitstellung von Dateien mit Windows Server.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: fc4c8b341ee78db80f862ee412400f0a930fe810
ms.sourcegitcommit: 375e94dc70c76e7aa5679c32f0f4dbc26cf7dd83
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2018
ms.locfileid: "2233486"
---
# <a name="overview-of-file-sharing-using-the-smb-3-protocol-in-windows-server"></a>Übersicht über die Dateifreigabe über das SMB-3-Protokoll in Windows Server

>Betrifft: Windows Server 2012 R2, WindowsServer 2012 und WindowsServer 2016

In diesem Thema wird das SMB 3.0-Feature in Windows Server® 2012, Windows Server 2012 R2 und Windows Server 2016 – praktischen verwendet für das Feature, das wichtigste neu oder aktualisiert Funktionen in dieser Version im Vergleich zu früheren Versionen und der Hardware Requirements.

## <a name="feature-description"></a>Featurebeschreibung

Das Server Message Block-Protokoll (SMB-Protokoll) dient der Freigabe von Netzwerkdateien und ermöglicht es Anwendungen auf einem Computer, Dateien zu lesen und in Dateien zu schreiben sowie Dienste von Serverprogrammen in einem Computernetzwerk anzufordern. Das SMB-Protokoll kann zusätzlich zu den TCP/IP-Protokollen oder anderen Netzwerkprotokollen verwendet werden. Mit dem SMB-Protokoll kann eine Anwendung (oder der Benutzer einer Anwendung) auf Dateien oder andere Ressourcen auf einem Remoteserver zugreifen. Dadurch wird es Anwendungen ermöglicht, Dateien auf dem Remoteserver zu lesen, zu erstellen und zu aktualisieren. Anwendungen können zudem mit jedem beliebigen Serverprogramm kommunizieren, das für den Empfang einer SMB-Clientanforderung eingerichtet ist. Windows Server 2012 führt die neue 3.0 Version des SMB-Protokolls.

## <a name="practical-applications"></a>Praktische Anwendungsfälle

In diesem Abschnitt werden einige neuen praktischen Verwendungsmöglichkeiten für das neue SMB 3.0-Protokoll.

* **Dateispeicher für die Virtualisierung (Hyper-V™ über SMB)**. Hyper-V kann in Dateifreigaben über das Protokoll SMB 3.0 virtueller Computerdateien wie Konfiguration, Virtual Hard Disk (VHD) Dateien und Momentaufnahmen, speichern. Dies kann für eigenständige Datei-Servern und gruppierten Dateiserver, die Verwendung von Hyper-V in Verbindung mit gemeinsam genutzte Dateispeicher für den Cluster verwendet werden.
* **Microsoft SQL Server über SMB**. SQL Server-Speicher können Benutzerdatenbankdateien auf SMB-Dateifreigaben. Derzeit ist dies für eigenständige SQL Server mit SQL Server 2008 R2 unterstützt. Kommenden Versionen von SQL Server werden Unterstützung für SQL-Servercluster und Systemdatenbanken hinzugefügt.
* **Herkömmliche Speicher für Endbenutzerdaten**. Das Protokoll SMB 3.0 bietet Verbesserungen an der Information Worker (oder Client) Arbeitslasten. Zu diesen zählen Reduzierung der Anwendung Wartezeiten beim Zugreifen auf Daten über wide Area Networks (WAN) und Schützen von Daten Ausspähen vor Angriffen durch Benutzer in Zweigstellenbüros aufgetreten ist.

## <a name="new-and-changed-functionality"></a>Neue und geänderte Funktionalität

Informationen über neue und geänderte Funktionalität in Windows Server 2012 R2 finden Sie unter [What's New in SMB in Windows Server](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)>).

SMB in Windows Server 2012 und Windows Server 2016 enthält das neue SMB 3.0-Protokoll und viele neue Verbesserungen die beschrieben werden in der folgenden Tabelle.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Feature/Funktionalität</p></th>
<th><p>Neu oder aktualisiert</p></th>
<th><p>Zusammenfassung</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Transparentes Failover SMB</p></td>
<td><p>Neu</p></td>
<td><p>Ermöglicht Administratoren, Hardware- oder Wartung von Knoten in einem gruppierten Dateiserver ausführen, ohne Unterbrechung des serveranwendungen Speichern von Daten in diese Dateifreigaben. Auch, wenn eine Hardware- oder auf einem Clusterknoten ausfällt, erneut eine Verbindung SMB-Clients transparent mit einem anderen Clusterknoten ohne Unterbrechung des Server-Anwendungen, die Daten in diesen Dateifreigaben gespeichert werden.</p></td>
</tr>
<tr class="even">
<td><p>SMB-Skalierung</p></td>
<td><p>Neu</p></td>
<td><p>Verwenden von Cluster Shared Volumes (CSV) Version 2, können Administratoren Dateifreigaben erstellen, die gleichzeitigen Zugriff auf Datendateien, direkte e/a, bis alle Knoten im Dateiservercluster bereitzustellen. Dies bietet eine bessere Nutzung der Netzwerkbandbreite und Load balancing in der Datei-Server-Clients und optimiert die Leistung für serveranwendungen.</p></td>
</tr>
<tr class="odd">
<td><p>SMB Multichannel</p></td>
<td><p>Neu</p></td>
<td><p>Aggregation der Netzwerkbandbreite und Fehlertoleranz Netzwerk ermöglicht, wenn mehrere Pfade zwischen den SMB 3.0-Client und Server SMB 3.0 verfügbar sind. Auf diese Weise serveranwendungen nutzen alle verfügbaren Netzwerkbandbreite und flexibel in Bezug auf ein Netzwerkfehler werden können.</p></td>
</tr>
<tr class="even">
<td><p>SMB Direct</p></td>
<td><p>Neu</p></td>
<td><p>Unterstützt die Verwendung von Netzwerkadaptern, die RDMA-Funktion und kann mit voller Geschwindigkeit mit sehr geringe Wartezeit bei Verwendung von nur eine sehr geringe CPU funktionieren. Für Arbeitslasten wie Hyper-V oder Microsoft SQL Server ist dies einen remote-Dateiserver, die den lokalen Speicher ähnelt.</p></td>
</tr>
<tr class="odd">
<td><p>Leistungsindikatoren für serveranwendungen</p></td>
<td><p>Neu</p></td>
<td><p>Die neue SMB-Leistung, die die Leistungsindikatoren enthalten detaillierte, pro Aktie Informationen zum Durchsatz, Latenz und e/a pro Sekunde (IOPS), dass Administratoren zum Analysieren der Leistung von SMB 3.0 Dateifreigaben, wo ihre Daten gespeichert ist. Mit diesen Zählern werden speziell für serveranwendungen wie Hyper-V und SQL Server, die Dateien in Dateifreigaben remote zu speichern.</p></td>
</tr>
<tr class="even">
<td><p>Leistungsoptimierungen</p></td>
<td><p>Aktualisiert</p></td>
<td><p>Die SMB 3.0 Client- und SMB 3.0 wurden für kleine zufälliger Lese-/Schreibzugriff e/a, optimiert ist häufig in serveranwendungen wie SQL Server OLTP. Darüber hinaus ist große Maximum Transmission Unit (MTU) in der Standardeinstellung aktiviert die Leistung in großen sequenzielle Übertragung, wie SQL Server-Datawarehouse, Sicherung oder Wiederherstellung, bereitstellen oder Kopieren von virtuellen Festplatten erheblich verbessert.</p></td>
</tr>
<tr class="odd">
<td><p>SMB-spezifische Windows PowerShell-cmdlets</p></td>
<td><p>Neu</p></td>
<td><p>Mit Windows PowerShell-Cmdlets für SMB kann Administratoren Dateifreigaben auf dem Dateiserver, End-to-End über die Befehlszeile verwalten.</p></td>
</tr>
<tr class="even">
<td><p>SMB-Verschlüsselung</p></td>
<td><p>Neu</p></td>
<td><p>Bietet eine End-to-End-Verschlüsselung der SMB-Daten und schützt Daten vor zur Vermeidung von Abhör-Vorkommen in nicht vertrauenswürdigen Netzwerken. Erfordert keine neuen Kosten für die Bereitstellung und keine Notwendigkeit zur Internet Protocol Security (IPsec), spezielle Hardware oder WAN-Beschleuniger. Es kann für einzelne pro freigeben, oder für die gesamte Dateiserver konfiguriert werden, und für eine Vielzahl von Szenarien, in dem Daten nicht vertrauenswürdige Netzwerken durchläuft, aktiviert werden kann.</p></td>
</tr>
<tr class="odd">
<td><p>SMB-Verzeichnisleasing</p></td>
<td><p>Neu</p></td>
<td><p>Verbessert die Anwendung Antwortzeiten in Zweigstellen. Mit der Verwendung von Directory Leases, Roundtrips vom Client zum Server verringert werden, da es sich bei Metadaten aus länger verdienen abgerufen wird Verzeichnisspeichers. Cachekohärenz wird beibehalten, da Clients benachrichtigt werden, wenn Verzeichnisinformationen auf dem Server geändert wird. Funktioniert mit Szenarien für <em>HomeFolder</em> (Lese-/Schreibzugriff nicht gemeinsam genutzt) und <em>Veröffentlichung</em> (schreibgeschützt mit Freigabe).</p></td>
</tr>
</tbody>
</table>

## <a name="hardware-requirements"></a>Hardwareanforderungen

Transparentes Failover SMB ist Folgendes erforderlich:

* Ein Failovercluster mit Windows Server 2012 oder Windows Server 2016 mit mindestens zwei Knoten konfiguriert. Cluster muss die Cluster enthalten in den überprüfungs-Assistenten Validierungstests.
* Dateifreigaben müssen mit der Eigenschaft kontinuierliche Verfügbarkeit (CA) erstellt werden, die der Standardwert ist.
* Dateifreigaben müssen auf CSV Volume Pfade zu erreichen SMB Skalierung erstellt werden.
* Client-Computer müssen Windows® 8 oder Windows Server 2012, die den aktualisierten SMB-Client enthalten, der ständige Verfügbarkeit unterstützt ausgeführt werden.

>[!NOTE]
>Kompatible Clients können verbinden mit Dateifreigaben, der die Zertifizierungsstellen-Eigenschaft, aber transparentes Failover für diese Clients wird nicht unterstützt.

SMB Multichannel ist Folgendes erforderlich:

* Es sind mindestens zwei Computern unter Windows Server 2012 erforderlich. Keine zusätzlichen Features installiert werden müssen – die Technologie ist standardmäßig aktiviert.
* Informationen zu den empfohlenen Konfigurationen finden Sie unter im Abschnitt Siehe auch am Ende dieses Themas Overview.

SMB Direct ist Folgendes erforderlich:

* Es sind mindestens zwei Computern unter Windows Server 2012 erforderlich. Keine zusätzlichen Features installiert werden müssen – die Technologie ist standardmäßig aktiviert.
* Netzwerkadapter mit RDMA Funktionalität sind erforderlich. Diese Adapter sind derzeit in drei verschiedene Typen verfügbar: iWARP, Infiniband oder RoCE (RDMA over Ethernet zusammengeführt).

## <a name="more-information"></a>Weitere Informationen

Die folgende Liste enthält weitere Ressourcen im Web zur SMB und verwandten Technologien in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016.

* [Speicher in Windows Server](../storage.md)
* [Horizontale Skalierung Dateiserver für Anwendungsdaten](../../failover-clustering/sofs-overview.md)
* [Verbessern der Leistung eines Dateiservers mit SMB Direct](smb-direct.md)
* [Bereitstellen von Hyper-V über SMB](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
* [Bereitstellen von SMB Multichannel](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn610980(v%3dws.11)>)
* [Bereitstellen von schnell und effizient Dateiserver für Serveranwendungen](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
* [SMB: Handbuch zur Problembehandlung](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn659439(v%3dws.11)>)