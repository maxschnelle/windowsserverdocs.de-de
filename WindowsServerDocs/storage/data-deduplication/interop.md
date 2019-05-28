---
ms.assetid: 60fca6b2-f1c0-451f-858f-2f6ab350d220
title: Interoperabilität der Datendeduplizierung
ms.technology: storage-deduplication
ms.prod: windows-server-threshold
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 09/16/2016
ms.openlocfilehash: 9453811b0f76b249c245990293ba82cf5a6e0867
ms.sourcegitcommit: 29ad32b9dea298a7fe81dcc33d2a42d383018e82
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65624631"
---
# <a name="data-deduplication-interoperability"></a>Interoperabilität der Datendeduplizierung

> Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, WindowsServer 2019

## <a id="supported"></a>Unterstützt

### <a id="supported-ReFS"></a>ReFS
Die Datendeduplizierung ist ab Windows Server-2019 unterstützt. 

### <a id="supported-clusters"></a>Failover-Clusterunterstützung

[Failoverclustering](../..//failover-clustering/failover-clustering-overview.md) wird vollständig unterstützt, wenn auf jedem Knoten im Cluster das [Datendeduplizierungsfeature installiert](install-enable.md#install-dedup) ist. Andere wichtige Hinweise:

* [Manuell gestartete Datendeduplizierungsaufträge](run.md#running-dedup-jobs-manually) müssen für freigegebene Clustervolumes auf dem Besitzerknoten ausgeführt werden.
* Geplante Datendeduplizierungsaufträge werden in der Clusteraufgabe gespeichert und so geplant, dass der geplante Auftrag im nächsten geplanten Intervall angewendet wird, wenn ein dedupliziertes Volume von einem anderen Knoten übernommen wird.
* Die Datendeduplizierung interagiert vollständig mit dem Feature [Paralleles Upgrade für Clusterbetriebssystem](../..//failover-clustering/cluster-operating-system-rolling-upgrade.md).
* Die Datendeduplizierung wird auf NTFS-formatierten [Direkte Speicherplätze](../storage-spaces/storage-spaces-direct-overview.md)-Datenträgern vollständig unterstützt (Spiegelung oder Parität). Auf Volumes mit mehreren Ebenen wird die Deduplizierung nicht unterstützt. Weitere Informationen finden Sie unter [Data Deduplication auf ReFS](interop.md#unsupported-refs).

### <a id="supported-storage-replica"></a>Funktion "Speicherreplikat"
[Speicherreplikat](../storage-replica/storage-replica-overview.md) wird vollständig unterstützt. Die Datendeduplizierung sollte nicht für die Ausführung auf der sekundären Kopie konfiguriert werden.

### <a id="supported-branchcache"></a>BranchCache
Sie können den Netzwerkzugriff auf Daten optimieren, indem Sie [BranchCache](../../networking/branchcache/branchcache.md) auf Servern und Clients aktivieren. Wenn ein BranchCache-fähiges System über ein WAN mit einem Remotedateiserver kommuniziert, auf dem die Datendeduplizierung ausgeführt wird, sind alle deduplizierten Dateien bereits indiziert und mittels Hashfunktion organisiert. Daher werden Datenanforderungen aus einer Filiale schnell berechnet. Dies ähnelt der Vorabindizierung oder Voraborganisation mittels Hashfunktion eines BranchCache-fähigen Servers.

### <a id="supported-dfsr"></a>DFS-Replikation
Die Datendeduplizierung ist mit der Replikation des verteilten Dateisystems (Distributed File System, DFS) einsetzbar. Optimieren oder Deoptimieren einer Datei löst keine Replikation aus, da die Datei nicht geändert wird. DFS-Replikation verwendet Remoteunterschiedskomprimierung, nicht die Blöcke im Blockspeicher, zur Over-the-Wire-Speicherung. Die Dateien auf dem Replikat können auch mithilfe der Deduplizierung optimiert werden, wenn das Replikat die Datendeduplizierung verwendet.

### <a id="supported-quotas"></a>Quotas
Das Festlegen einer festen Kontingentgrenze für einen Volumestammordner, für den auch die Deduplizierung aktiviert ist, wird durch die Datendeduplizierung nicht unterstützt. Wenn für einen Volumestamm eine feste Kontingentgrenze vorhanden ist, stimmen der tatsächliche freie Speicherplatz auf dem Volume und der durch die Kontingentgrenze beschränkte Speicherplatz auf dem Volume nicht überein. Dies kann zu Fehlern bei Deduplizierungsoptimierungsaufträgen führen. Es ist jedoch möglich, eine weiche Kontingentgrenze für einen Volumestammordner festzulegen, für den die Deduplizierung aktiviert ist. 

Ist ein Kontingent für ein dedupliziertes Volume aktiviert, wird die logische und nicht die physische Größe der Datei verwendet. Der Kontingentbedarf (einschließlich aller Kontingentschwellenwerte) ändert sich nicht, wenn eine Datei durch die Deduplizierung verarbeitet wird. Alle anderen Kontingentfunktionen, einschließlich weicher Volumestamm-Kontingentgrenzen und Kontingentgrenzen für Unterordner, funktionieren bei Verwendung der Deduplizierung normal.

### <a id="supported-windows-server-backup"></a>Windows Server-Sicherung
Die Windows Server-Sicherung kann ein optimiertes Volume in der vorliegenden Form sichern (d. h. ohne deduplizierte Daten zu entfernen). In den folgenden Schritten wird veranschaulicht, wie Sie ein Volume sichern, und wie Sie ein Volume oder ausgewählte Dateien von einem Volume wiederherstellen.
1. Installieren Sie die Windows Server-Sicherung.  
    ```PowerShell
    Install-WindowsFeature -Name Windows-Server-Backup
    ```

2. Sichern Sie das Volume „E:“ auf einem anderen Volume, indem Sie den folgenden Befehl ausführen und dabei die richtigen Volumenamen für Ihre Situation angeben.  
    ```PowerShell
    wbadmin start backup –include:E: -backuptarget:F: -quiet
    ```
3. Rufen Sie die Versions-ID der Sicherung ab, die Sie soeben erstellt haben.

    ```PowerShell
    wbadmin get versions
    ```

    Diese ausgabeversions-ID werden ein Datum und Uhrzeit-Zeichenfolge, z.B.: 08/18/2016-06:22.

4. Stellen Sie das gesamte Volume wieder her.
    ```PowerShell
    wbadmin start recovery –version:02/16/2012-06:22 -itemtype:Volume  -items:E: -recoveryTarget:E:
    ```

    **--OR--**  

    Wiederherstellen eines bestimmten Ordners (in diesem Fall den Ordner E:\Docs):
    ```PowerShell
    wbadmin start recovery –version:02/16/2012-06:22 -itemtype:File  -items:E:\Docs  -recursive
    ```

## <a id="unsupported"></a>Nicht unterstützte

### <a id="unsupported-windows-client"></a>Windows 10 (Clientbetriebssystem)
Die Datendeduplizierung wird unter Windows 10 nicht unterstützt. Es gibt verschiedene beliebte Blogbeiträge in der Windows-Community, die beschreiben, wie Sie die Binärdateien aus Windows Server 2016 entfernen und unter Windows 10 installieren. Dieses Szenario wurde aber nicht im Rahmen der Entwicklung der Datendeduplizierung bestätigt. [Stimmen Sie für Windows 10 vNext unter Windows Server Storage UserVoice für dieses Element](https://windowsserver.uservoice.com/forums/295056-storage/suggestions/9011008-add-deduplication-support-to-client-os).

### <a id="unsupported-windows-search"></a>Windows Search
Windows Search unterstützt die Datendeduplizierung nicht. Die Datendeduplizierung verwendet Analysepunkte, die Windows Search nicht indizieren kann. Daher überspringt Windows Search alle deduplizierten Dateien und schließt sie aus dem Index aus. Daher können Suchergebnisse für deduplizierte Volumes unvollständig sein. [Stimmen Sie für Windows Server vNext unter Windows Server Storage UserVoice für dieses Element](https://windowsserver.uservoice.com/forums/295056-storage/suggestions/17888647-make-windows-search-service-work-with-data-dedupli).

### <a id="unsupported-robocopy"></a>Robocopy
Die Datendeduplizierung mit Robocopy wird nicht empfohlen, da bestimmte Robocopy-Befehle Blockspeicher beschädigen können. Der Blockspeicher wird im Ordner „System Volume Information“ für ein Volume gespeichert. Wenn der Ordner gelöscht wird, werden die optimierten Dateien (Analysepunkte), die aus dem Quellvolume kopiert werden, beschädigt, weil die Datenblöcke nicht auf das Zielvolume kopiert werden.
