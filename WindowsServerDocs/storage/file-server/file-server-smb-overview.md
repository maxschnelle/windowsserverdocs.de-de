---
title: Übersicht über die Dateifreigabe mithilfe des SMB 3-Protokolls in Windows Server
description: Eine Übersicht über die Verwendung des SMB 3-Protokolls für Dateifreigaben und Dateifreigaben mit Windows Server.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: b40c179d242a0c48c6eb176db1225979f9e6a123
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402088"
---
# <a name="overview-of-file-sharing-using-the-smb-3-protocol-in-windows-server"></a>Übersicht über die Dateifreigabe mithilfe des SMB 3-Protokolls in Windows Server

>Gilt für: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

In diesem Thema wird das SMB 3,0-Feature in Windows Server® 2012, Windows Server 2012 R2 und Windows Server 2016 beschrieben – praktische Verwendungsmöglichkeiten für das Feature, die wichtigste neue oder aktualisierte Funktionalität in dieser Version im Vergleich zu früheren Versionen und die Hardware Bedingungen.

## <a name="feature-description"></a>Featurebeschreibung

Das Server Message Block-Protokoll (SMB-Protokoll) dient der Freigabe von Netzwerkdateien und ermöglicht es Anwendungen auf einem Computer, Dateien zu lesen und in Dateien zu schreiben sowie Dienste von Serverprogrammen in einem Computernetzwerk anzufordern. Das SMB-Protokoll kann zusätzlich zu den TCP/IP-Protokollen oder anderen Netzwerkprotokollen verwendet werden. Mit dem SMB-Protokoll kann eine Anwendung (oder der Benutzer einer Anwendung) auf Dateien oder andere Ressourcen auf einem Remoteserver zugreifen. Dadurch wird es Anwendungen ermöglicht, Dateien auf dem Remoteserver zu lesen, zu erstellen und zu aktualisieren. Anwendungen können zudem mit jedem beliebigen Serverprogramm kommunizieren, das für den Empfang einer SMB-Clientanforderung eingerichtet ist. Mit Windows Server 2012 wird die neue 3,0-Version des SMB-Protokolls eingeführt.

## <a name="practical-applications"></a>Praktische Anwendungsfälle

In diesem Abschnitt werden ein paar praktische Anwendungen des neuen SMB 3.0-Protokolls vorgestellt.

* **Dateispeicher zur Virtualisierung (Hyper-V™ über SMB)** . Hyper-V kann Dateien virtueller Computer über das SMB 3.0-Protokoll in Dateifreigaben speichern. Zu diesen Dateien gehören Konfigurationsdateien, VHD-Dateien (Virtual Hard Disk, virtuelle Festplatte) und Momentaufnahmen. Dies kann sowohl für eigenständige Dateiserver als auch Clusterdateiserver, die Hyper-V zusammen mit Dateifreigabespeicher für den Cluster verwenden, genutzt werden.
* **Microsoft SQL Server über SMB**. SQL Server kann Benutzerdatenbankdateien auf SMB-Dateifreigaben speichern. Aktuell wird dies von SQL Server 2008 R2 für eigenständige SQL-Server unterstützt. Zukünftige Versionen von SQL Server werden auch die Unterstützung von gruppierten SQL-Servern und Systemdateibanken beinhalten.
* **Herkömmlicher Speicher für Endbenutzerdaten**. Das SMB 3.0-Protokoll bietet Verbesserungen für Information-Worker-Arbeitsauslastungen (oder Clientarbeitsauslastungen). Zu diesen Verbesserungen zählt die Reduzierung der Anwendungslatenz für Benutzer in Filialen, wenn diese Benutzer über ein WAN (Wide Area Network, WAN) auf Daten zugreifen, und der Schutz von Daten vor Lauschangriffen.

## <a name="new-and-changed-functionality"></a>Neue und geänderte Funktionalität

Informationen zu neuen und geänderten Funktionen in Windows Server 2012 R2 finden Sie unter [Neues in SMB unter Windows Server](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)>).

SMB in Windows Server 2012 und Windows Server 2016 umfasst das neue SMB 3,0-Protokoll und viele neue Verbesserungen, die in der folgenden Tabelle beschrieben werden.

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
<td><p>SMB Transparent Failover</p></td>
<td><p>Neu</p></td>
<td><p>Ermöglicht es Administratoren, Hardware- oder Softwarewartungen von Knoten in einem Clusterdateiserver durchzuführen, ohne Serveranwendungen zu unterbrechen, die Daten in diesen Dateifreigaben speichern. Wenn ein Hardware- oder Softwarefehler in einem Clusterknoten auftritt, stellen die SMB-Clients zudem die Verbindung zu einem anderen Clusterknoten transparent her, ohne Serveranwendungen zu unterbrechen, die Daten in diesen Dateifreigaben speichern.</p></td>
</tr>
<tr class="even">
<td><p>SMB Scale Out</p></td>
<td><p>Neu</p></td>
<td><p>Durch die Verwendung freigegebener Clustervolumes der Version 2 (Cluster Shared Volumes, CSV) können Administratoren Dateifreigaben erstellen, die gleichzeitigen Zugriff auf Datendateien bieten, mit direkter E/A und über alle Knoten in einem Dateiservercluster. Dadurch wird die Ausnutzung der Netzwerkbandbreite verbessert und ein besserer Lastausgleich auf den Dateiserverclients erreicht sowie die Leistung für Serveranwendungen optimiert.</p></td>
</tr>
<tr class="odd">
<td><p>SMB Multichannel</p></td>
<td><p>Neu</p></td>
<td><p>Ermöglicht die Aggregation von Netzwerkbandbreite und Netzwerkfehlertoleranz, wenn mehrere Pfade zwischen dem SMB 3.0-Client und dem SMB 3.0-Server verfügbar sind. Auf diese Weise können Serveranwendungen die verfügbare Netzwerkbandbreite voll ausnutzen und sind unempfindlich für Netzwerkausfälle.</p></td>
</tr>
<tr class="even">
<td><p>SMB Direct</p></td>
<td><p>Neu</p></td>
<td><p>Unterstützt die Verwendung von Netzwerkadaptern mit RDMA-Fähigkeit und kann bei maximaler Geschwindigkeit mit sehr niedriger Latenz arbeiten, und das bei sehr geringer CPU-Nutzung. Für Arbeitsauslastungen wie Hyper-V oder Microsoft SQL Server bedeutet dies, dass ein Remotedateiserver einem lokalen Speicher gleichkommt.</p></td>
</tr>
<tr class="odd">
<td><p>Leistungsindikatoren für Serveranwendungen</p></td>
<td><p>Neu</p></td>
<td><p>Die neuen SMB-Leistungsindikatoren liefern ausführliche, nach Freigabe unterteilte Daten über Durchsatz, Latenz und E/A pro Sekunde und ermöglichen es Administratoren, die Leistung von SMB 3.0-Dateifreigaben zu analysieren, in denen ihre Daten gespeichert sind. Diese Indikatoren sind speziell für Serveranwendungen wie Hyper-V und SQL Server konzipiert, die Dateien in Remotedateifreigaben speichern.</p></td>
</tr>
<tr class="even">
<td><p>Leistungsoptimierungen</p></td>
<td><p>Aktualisiert</p></td>
<td><p>Sowohl der SMB 3.0-Client als auch der SMB 3.0-Server sind für kleine zufällige Lese-/Schreibvorgänge optimiert worden, die bei Serveranwendungen wie SQL Server OLTP häufig vorkommen. Außerdem ist das Feature Maximum Transmission Unit (MTU) standardmäßig für große Pakete aktiviert, wodurch die Leistung bei großen sequenziellen Übertragungen, wie SQL Server Data Warehouse, Datenbanksicherung und -wiederherstellung oder dem Bereitstellen und Kopieren virtueller Festplatten, deutlich verbessert wird.</p></td>
</tr>
<tr class="odd">
<td><p>SMB-spezifische Windows PowerShell-Cmdlets</p></td>
<td><p>Neu</p></td>
<td><p>Mit Windows PowerShell-Cmdlets für SMB kann ein Administrator Dateifreigaben auf dem Dateiserver End-to-End von der Befehlszeile aus verwalten.</p></td>
</tr>
<tr class="even">
<td><p>SMB-Verschlüsselung</p></td>
<td><p>Neu</p></td>
<td><p>Sorgt für End-to-End-Verschlüsselung von SMB-Daten und schützt Daten vor Lauschangriffen in nicht vertrauenswürdigen Netzwerken. Erfordert keine weiteren Bereitstellungskosten und keine Internet Protocol-Sicherheit (IPsec), spezielle Hardware oder WAN-Beschleuniger. Sie kann auf Freigabebasis oder für den gesamten Dateiserver konfiguriert und für eine Vielzahl von Szenarios aktiviert werden, bei denen Daten über nicht vertrauenswürdige Netzwerke übertragen werden.</p></td>
</tr>
<tr class="odd">
<td><p>SMB Directory Leasing</p></td>
<td><p>Neu</p></td>
<td><p>Verbessert die Antwortzeiten von Anwendungen in Filialen. Durch die Verwendung von Verzeichnisleases werden Roundtrips vom Client zum Server reduziert, da Metadaten von einem Verzeichniscache mit längerer Lebensdauer abgerufen werden. Die Cachekohärenz bleibt erhalten, da Clients benachrichtigt werden, wenn sich Verzeichnisinformationen auf dem Server ändern. Dies funktioniert für <em>Basisordner</em> (Lesen/Schreiben ohne Freigabe) und <em>Veröffentlichung</em> (schreibgeschützt mit Freigabe).</p></td>
</tr>
</tbody>
</table>

## <a name="hardware-requirements"></a>Hardwareanforderungen

Für SMB Transparent Failover gelten die folgenden Anforderungen:

* Ein Failovercluster unter Windows Server 2012 oder Windows Server 2016 mit mindestens zwei konfigurierten Knoten. Der Cluster muss die Clustervalidierungstests bestehen, die im Validierungs-Assistenten enthalten sind.
* Dateifreigaben müssen mit der Eigenschaft %%amp;quot;Fortlaufende Verfügbarkeit%%amp;quot; (Continuous Availability, CA) erstellt werden, die standardmäßig aktiviert ist.
* Dateifreigaben müssen unter CSV-Volumepfaden erstellt werden, um SMB Scale-Out zu nutzen.
* Auf Client Computern muss Windows® 8 oder Windows Server 2012 ausgeführt werden, die beide den aktualisierten SMB-Client enthalten, der fortlaufende Verfügbarkeit unterstützt.

>[!NOTE]
>Downlevelclients können eine Verbindung mit Dateifreigaben herstellen, die die ca-Eigenschaft aufweisen, das transparente Failover wird für diese Clients jedoch nicht unterstützt.

Für SMB Multichannel gelten die folgenden Anforderungen:

* Mindestens zwei Computer, auf denen Windows Server 2012 ausgeführt wird, sind erforderlich. Es müssen keine zusätzlichen Features installiert werden. Die Technologie ist standardmäßig aktiviert.
* Weitere Informationen zu empfohlenen Netzwerkkonfigurationen finden Sie im Abschnitt %%amp;quot;Siehe auch%%amp;quot; am Ende dieses Übersichtsthemas.

Für SMB Direct gelten die folgenden Anforderungen:

* Mindestens zwei Computer, auf denen Windows Server 2012 ausgeführt wird, sind erforderlich. Es müssen keine zusätzlichen Features installiert werden. Die Technologie ist standardmäßig aktiviert.
* Netzwerkadapter mit RDMA-Fähigkeit sind erforderlich. Aktuell sind diese Adapter in drei unterschiedlichen Typen erhältlich: iWARP, Infiniband und RoCE (RDMA over Converged Ethernet).

## <a name="more-information"></a>Weitere Informationen

In der folgenden Liste finden Sie weitere Ressourcen im Web zu SMB und verwandten Technologien in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016.

* [Speicher](../storage.md)
* [Dateiserver mit horizontaler Skalierung für Anwendungsdaten](../../failover-clustering/sofs-overview.md)
* [Verbessern der Leistung eines Dateiservers mit SMB Direct](smb-direct.md)
* [Bereitstellen von Hyper-V über SMB](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
* [Bereitstellen von SMB Multichannel](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn610980(v%3dws.11)>)
* [Bereitstellen schneller und effizienter Dateiserver für Server Anwendungen](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
* [SMB: Handbuch zur Problembehandlung @ no__t-0