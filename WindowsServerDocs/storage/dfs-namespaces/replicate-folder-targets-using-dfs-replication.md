---
title: Replizieren von Ordnerzielen mit DFS-Replikation
description: Dieser Artikel beschreibt das Replizieren von Ordnerzielen mit DFS-Replikation
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: ad26b8685539869e9302eafac69df19d11778a1b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386135"
---
# <a name="replicate-folder-targets-using-dfs-replication"></a>Replizieren von Ordnerzielen mit DFS-Replikation

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008

Mit DFS-Replikation können Sie den Inhalt von Ordnerzielen synchron halten, damit Benutzer die gleichen Dateien sehen, unabhängig davon, auf welches Ordnerziel der Clientcomputer verwiesen wird.

## <a name="to-replicate-folder-targets-using-dfs-replication"></a>So replizieren Sie Ordnerziele mit DFS-Replikation

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Ordner mit zwei oder mehr Zielen, und klicken Sie anschließend auf **Ordner replizieren**.

3.  Befolgen Sie die Anweisungen im Assistenten für das Replizieren des Ordners.

> [!NOTE]
> Konfigurationsänderungen werden nicht sofort auf alle Mitglieder angewendet, es sei denn, Sie verwenden die Cmdlets [Suspend-DfsReplicationGroup](https://technet.microsoft.com/itpro/powershell/windows/dfsr/suspend-dfsreplicationgroup) und [synchronisieren DfsReplicationGroup](https://technet.microsoft.com/itpro/powershell/windows/dfsr/sync-dfsreplicationgroup). Die neue Konfiguration muss auf allen Domänencontrollern repliziert werden, und jedes Mitglied in der Replikationsgruppe muss seinen nächstgelegenen Domänencontroller zum Abrufen der Änderungen abfragen. Die benötigte Zeit hängt von der Replikations Latenz der Active Directory Directory-Dienste (AD DS) und dem langen Abruf Intervall (60 Minuten) für jedes Mitglied ab. Um Konfigurationsänderungen sofort abzurufen, öffnen Sie ein Eingabeaufforderungsfenster, und geben Sie den folgenden Befehl für jedes Mitglied der Replikationsgruppe ein: <br /> dfsrdiag.exe PollAD /Member:DOMAIN\Server1
<br />
Verwenden Sie hierzu das Cmdlet [Update-dfsrconfigurationfromad](https://technet.microsoft.com/itpro/powershell/windows/dfsr/update-dfsrconfigurationfromad) , das in Windows Server 2012 R2 eingeführt wurde.

## <a name="see-also"></a>Siehe auch

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)
-   [DFS-Replikation](../dfs-replication/dfsr-overview.md)