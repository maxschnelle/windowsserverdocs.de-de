---
title: Replizieren von Ordnerzielen mit DFS-Replikation
description: In diesem Artikel wird beschrieben, wie Sie mit DFS-Replikation Ordner Ziele replizieren.
ms.date: 6/5/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 8345d12c77af92999d64f63809752180a3ea91bc
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954747"
---
# <a name="replicate-folder-targets-using-dfs-replication"></a>Replizieren von Ordner Zielen mithilfe von DFS-Replikation

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008

Sie können DFS-Replikation verwenden, um den Inhalt der Ordner Ziele synchron zu halten, sodass Benutzer unabhängig davon, auf welchen Ordner das Ziel des Client Computers verwiesen wird, dieselben Dateien sehen.

## <a name="to-replicate-folder-targets-using-dfs-replication"></a>So replizieren Sie Ordner Ziele mithilfe von DFS-Replikation

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolen Struktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Ordner mit mindestens zwei Ordner Zielen, und klicken Sie dann auf **Ordner replizieren**.

3.  Befolgen Sie die Anweisungen im Assistenten zum Replizieren von Ordnern.

> [!NOTE]
> Konfigurationsänderungen werden nicht sofort auf alle Mitglieder angewendet, außer wenn die Cmdlets [Suspend-dfsreplicationgroup](/powershell/module/dfsr/suspend-dfsreplicationgroup?view=win10-ps) und [Sync-dfsreplicationgroup](/powershell/module/dfsr/sync-dfsreplicationgroup?view=win10-ps) verwendet werden. Die neue Konfiguration muss auf allen Domänencontrollern repliziert werden, und jedes Mitglied in der Replikationsgruppe muss seinen nächstgelegenen Domänencontroller zum Abrufen der Änderungen abfragen. Die benötigte Zeit hängt von der Replikations Latenz der Active Directory Directory-Dienste (AD DS) und dem langen Abruf Intervall (60 Minuten) für jedes Mitglied ab. Um Konfigurationsänderungen sofort abzurufen, öffnen Sie ein Eingabe Aufforderungs Fenster, und geben Sie dann den folgenden Befehl für jedes Mitglied der Replikations Gruppe ein: <br /> dfsrdiag.exe PollAD /Member:DOMAIN\Server1
<br />
Verwenden Sie hierzu das Cmdlet [Update-dfsrconfigurationfromad](/powershell/module/dfsr/update-dfsrconfigurationfromad?view=win10-ps) , das in Windows Server 2012 R2 eingeführt wurde.

## <a name="additional-references"></a>Weitere Verweise

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)
-   [DFS-Replikation](../dfs-replication/dfsr-overview.md)
