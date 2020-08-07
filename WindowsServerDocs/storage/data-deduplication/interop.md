---
ms.assetid: 60fca6b2-f1c0-451f-858f-2f6ab350d220
title: Interoperabilität der Datendeduplizierung
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 09/16/2016
ms.openlocfilehash: 7f99b4d12821e505a229ac02d0198a9ac2ed31fa
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936305"
---
# <a name="data-deduplication-interoperability"></a>Interoperabilität der Datendeduplizierung

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2019

## <a name="supported"></a>Unterstützt

### <a name="refs"></a>ReFS
Die Datendeduplizierung wird ab Windows Server 2019 unterstützt.

### <a name="failover-clustering"></a>Failoverclustering

[Failoverclustering](../..//failover-clustering/failover-clustering-overview.md) wird vollständig unterstützt, wenn auf jedem Knoten im Cluster das [Datendeduplizierungsfeature installiert](install-enable.md#install-dedup) ist. Andere wichtige Hinweise:

* [Manuell gestartete Datendeduplizierungsaufträge](run.md#running-dedup-jobs-manually) müssen für freigegebene Clustervolumes auf dem Besitzerknoten ausgeführt werden.
* Geplante Datendeduplizierungsaufträge werden in der Clusteraufgabe gespeichert und so geplant, dass der geplante Auftrag im nächsten geplanten Intervall angewendet wird, wenn ein dedupliziertes Volume von einem anderen Knoten übernommen wird.
* Die Datendeduplizierung interagiert vollständig mit dem Feature [Paralleles Upgrade für Clusterbetriebssystem](../..//failover-clustering/cluster-operating-system-rolling-upgrade.md).
* Die Datendeduplizierung wird auf NTFS-formatierten [Direkte Speicherplätze](../storage-spaces/storage-spaces-direct-overview.md)-Datenträgern vollständig unterstützt (Spiegelung oder Parität). Auf Volumes mit mehreren Ebenen wird die Deduplizierung nicht unterstützt. Weitere Informationen finden Sie unter [Data Deduplication auf ReFS](#unsupported).

### <a name="storage-replica"></a>Speicherreplikat
[Speicher Replikat](../storage-replica/storage-replica-overview.md) wird vollständig unterstützt. Die Datendeduplizierung sollte so konfiguriert werden, dass Sie nicht auf der sekundären Kopie ausgeführt wird.

### <a name="branchcache"></a>BranchCache
Sie können den Netzwerkzugriff auf Daten optimieren, indem Sie [BranchCache](../../networking/branchcache/branchcache.md) auf Servern und Clients aktivieren. Wenn ein BranchCache-fähiges System über ein WAN mit einem Remotedateiserver kommuniziert, auf dem die Datendeduplizierung ausgeführt wird, sind alle deduplizierten Dateien bereits indiziert und mittels Hashfunktion organisiert. Daher werden Datenanforderungen aus einer Filiale schnell berechnet. Dies ähnelt der Vorabindizierung oder Voraborganisation mittels Hashfunktion eines BranchCache-fähigen Servers.

### <a name="dfs-replication"></a>DFS-Replikation
Die Datendeduplizierung ist mit der Replikation des verteilten Dateisystems (Distributed File System, DFS) einsetzbar. Optimieren oder Deoptimieren einer Datei löst keine Replikation aus, da die Datei nicht geändert wird. DFS-Replikation verwendet Remoteunterschiedskomprimierung, nicht die Blöcke im Blockspeicher, zur Over-the-Wire-Speicherung. Die Dateien auf dem Replikat können auch mithilfe der Deduplizierung optimiert werden, wenn das Replikat die Datendeduplizierung verwendet.

### <a name="quotas"></a>Kontingente
Das Festlegen einer festen Kontingentgrenze für einen Volumestammordner, für den auch die Deduplizierung aktiviert ist, wird durch die Datendeduplizierung nicht unterstützt. Wenn für einen Volumestamm eine feste Kontingentgrenze vorhanden ist, stimmen der tatsächliche freie Speicherplatz auf dem Volume und der durch die Kontingentgrenze beschränkte Speicherplatz auf dem Volume nicht überein. Dies kann zu Fehlern bei Deduplizierungsoptimierungsaufträgen führen. Es ist jedoch möglich, eine weiche Kontingentgrenze für einen Volumestammordner festzulegen, für den die Deduplizierung aktiviert ist.

Ist ein Kontingent für ein dedupliziertes Volume aktiviert, wird die logische und nicht die physische Größe der Datei verwendet. Der Kontingentbedarf (einschließlich aller Kontingentschwellenwerte) ändert sich nicht, wenn eine Datei durch die Deduplizierung verarbeitet wird. Alle anderen Kontingentfunktionen, einschließlich weicher Volumestamm-Kontingentgrenzen und Kontingentgrenzen für Unterordner, funktionieren bei Verwendung der Deduplizierung normal.

### <a name="windows-server-backup"></a>Windows Server-Sicherung
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

    Diese Ausgabeversions-ID wird eine Datums- und Uhrzeitzeichenfolge sein, z.B. 08/18/2016-06:22.

4. Stellen Sie das gesamte Volume wieder her.
    ```PowerShell
    wbadmin start recovery –version:02/16/2012-06:22 -itemtype:Volume  -items:E: -recoveryTarget:E:
    ```

    **--Oder--**

    Wiederherstellen eines bestimmten Ordners (in diesem Fall den Ordner E:\Docs):
    ```PowerShell
    wbadmin start recovery –version:02/16/2012-06:22 -itemtype:File  -items:E:\Docs  -recursive
    ```

## <a name="unsupported"></a>Nicht unterstützt

### <a name="windows-10-client-os"></a>Windows 10 (Client Betriebssystem)
Die Datendeduplizierung wird unter Windows 10 nicht unterstützt. Es gibt mehrere beliebte Blogbeiträge in der Windows-Community, in denen beschrieben wird, wie die Binärdateien aus Windows Server 2016 entfernt und unter Windows 10 installiert werden. dieses Szenario wurde jedoch nicht im Rahmen der datendeduplizierungsentwicklung überprüft. [Stimmen Sie für dieses Element für Windows 10 vNext im Windows Server-Speicher UserVoice](https://windowsserver.uservoice.com/forums/295056-storage/suggestions/9011008-add-deduplication-support-to-client-os)ab.

### <a name="windows-search"></a>Windows-Suche
Die Datendeduplizierung wird von Windows Search nicht unterstützt. Bei der Datendeduplizierung werden Analyse Punkte verwendet, die von Windows Search nicht indiziert werden können, sodass die Windows-Suche alle deduplizierten Dateien überspringt, ausgenommen Sie aus dem Index. Daher können Suchergebnisse für deduplizierte Volumes unvollständig sein. [Stimmen Sie für dieses Element für Windows Server vNext im Windows Server-Speicher UserVoice](https://windowsserver.uservoice.com/forums/295056-storage/suggestions/17888647-make-windows-search-service-work-with-data-dedupli)ab.

### <a name="robocopy"></a>Robocopy
Die Datendeduplizierung mit Robocopy wird nicht empfohlen, da bestimmte Robocopy-Befehle Blockspeicher beschädigen können. Der Blockspeicher wird im Ordner „System Volume Information“ für ein Volume gespeichert. Wenn der Ordner gelöscht wird, werden die optimierten Dateien (Analysepunkte), die aus dem Quellvolume kopiert werden, beschädigt, weil die Datenblöcke nicht auf das Zielvolume kopiert werden.
