---
title: Replizieren von Ordnerzielen mit DFS-Replikation
description: Dieser Artikel beschreibt das Replizieren von Ordnerzielen mit DFS-Replikation
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: ef13c338d8b13c24a02efb0468f06d5fef803cea
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="replicate-folder-targets-using-dfs-replication"></a>Replizieren von Ordnerzielen mit DFS-Replikation

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server2012 R2, Windows Server 2012, Windows Server2008 R2 und Windows Server 2008

Mit DFS-Replikation können Sie den Inhalt von Ordnerzielen synchron halten, damit Benutzer die gleichen Dateien sehen, unabhängig davon, auf welches Ordnerziel der Clientcomputer verwiesen wird.

## <a name="to-replicate-folder-targets-using-dfs-replication"></a>So replizieren Sie Ordnerziele mit DFS-Replikation

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Ordner mit zwei oder mehr Zielen, und klicken Sie anschließend auf **Ordner replizieren**.

3.  Befolgen Sie die Anweisungen im Assistenten für das Replizieren des Ordners.

> [!NOTE]
> Konfigurationsänderungen werden nicht sofort auf alle Mitglieder angewendet, es sei denn, Sie verwenden die Cmdlets [Suspend-DfsReplicationGroup](https://technet.microsoft.com/itpro/powershell/windows/dfsr/suspend-dfsreplicationgroup) und [synchronisieren DfsReplicationGroup](https://technet.microsoft.com/itpro/powershell/windows/dfsr/sync-dfsreplicationgroup). Die neue Konfiguration muss auf allen Domänencontrollern repliziert werden, und jedes Mitglied in der Replikationsgruppe muss seinen nächstgelegenen Domänencontroller zum Abrufen der Änderungen abfragen. Der dafür erforderliche Zeitaufwand hängt von der Replikationswartezeit in den Active Directory Domain Services (ADDS) und vom langen Abrufintervall (60Minuten) auf den einzelnen Mitglieder ab. Um Konfigurationsänderungen sofort abzurufen, öffnen Sie ein Eingabeaufforderungsfenster, und geben Sie den folgenden Befehl für jedes Mitglied der Replikationsgruppe ein: <br /> dfsrdiag.exe PollAD /Member:DOMAIN\Server1
<br />
Verwenden Sie von einer Windows PowerShell-Sitzung aus das Cmdlet [Update DfsrConfigurationFromAD](https://technet.microsoft.com/itpro/powershell/windows/dfsr/update-dfsrconfigurationfromad), das in Windows Server2012 R2 eingeführt wurde.

## <a name="see-also"></a>Weitere Informationen:

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)
-   [Replikation](https://technet.microsoft.com/library/cc770278(v=ws.11).aspx)