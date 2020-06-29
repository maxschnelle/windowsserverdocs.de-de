---
title: Replizieren von Ordnerzielen mit DFS-Replikation
description: In diesem Artikel wird beschrieben, wie Sie mit DFS-Replikation Ordner Ziele replizieren.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 3a4f76e43c2dbf5296afd163055adeafb36a5576
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474397"
---
# <a name="replicate-folder-targets-using-dfs-replication"></a>Replizieren von Ordner Zielen mithilfe von DFS-Replikation

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008

Sie können DFS-Replikation verwenden, um den Inhalt der Ordner Ziele synchron zu halten, sodass Benutzer unabhängig davon, auf welchen Ordner das Ziel des Client Computers verwiesen wird, dieselben Dateien sehen.

## <a name="to-replicate-folder-targets-using-dfs-replication"></a>So replizieren Sie Ordner Ziele mithilfe von DFS-Replikation

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolen Struktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Ordner mit mindestens zwei Ordner Zielen, und klicken Sie dann auf **Ordner replizieren**.

3.  Befolgen Sie die Anweisungen im Assistenten zum Replizieren von Ordnern.

> [!NOTE]
> Konfigurationsänderungen werden nicht sofort auf alle Mitglieder angewendet, außer wenn die Cmdlets [Suspend-dfsreplicationgroup](https://technet.microsoft.com/itpro/powershell/windows/dfsr/suspend-dfsreplicationgroup) und [Sync-dfsreplicationgroup](https://technet.microsoft.com/itpro/powershell/windows/dfsr/sync-dfsreplicationgroup) verwendet werden. Die neue Konfiguration muss auf allen Domänencontrollern repliziert werden, und jedes Mitglied in der Replikationsgruppe muss seinen nächstgelegenen Domänencontroller zum Abrufen der Änderungen abfragen. Die benötigte Zeit hängt von der Replikations Latenz der Active Directory Directory-Dienste (AD DS) und dem langen Abruf Intervall (60 Minuten) für jedes Mitglied ab. Um Konfigurationsänderungen sofort abzurufen, öffnen Sie ein Eingabe Aufforderungs Fenster, und geben Sie dann den folgenden Befehl für jedes Mitglied der Replikations Gruppe ein: <br /> dfsrdiag.exe PollAD /Member:DOMAIN\Server1
<br />
Verwenden Sie hierzu das Cmdlet [Update-dfsrconfigurationfromad](https://technet.microsoft.com/itpro/powershell/windows/dfsr/update-dfsrconfigurationfromad) , das in Windows Server 2012 R2 eingeführt wurde.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)
-   [DFS-Replikation](../dfs-replication/dfsr-overview.md)