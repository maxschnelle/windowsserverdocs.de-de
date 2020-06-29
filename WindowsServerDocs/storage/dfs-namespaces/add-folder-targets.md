---
title: Hinzufügen von Ordnerzielen
description: In diesem Thema wird beschrieben, wie Sie Ordner Ziele (UNC-Pfade) hinzufügen.
ms.prod: windows-server
ms.author: jgerend
manager: brianlic
ms.technology: storage
ms.topic: article
author: jasongerend
ms-date: 06/05/2017
ms.openlocfilehash: 2f4e0deb82f16c905f580c13115a5214556d4f5f
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475557"
---
# <a name="add-folder-targets"></a>Ordner Ziele hinzufügen

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Ein Ordner Ziel ist der Universal Naming Convention (UNC)-Pfad eines freigegebenen Ordners oder ein anderer Namespace, der einem Ordner in einem Namespace zugeordnet ist. Das Hinzufügen mehrerer Ordner Ziele erhöht die Verfügbarkeit des Ordners im-Namespace.

## <a name="to-add-a-folder-target"></a>So fügen Sie ein Ordner Ziel hinzu

Gehen Sie folgendermaßen vor, um mithilfe der DFS-Verwaltung ein Ordner Ziel hinzuzufügen:

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolen Struktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Ordner, und klicken Sie dann auf **Ordner Ziel hinzufügen**.

3.  Geben Sie den Pfad zum Ordner Ziel ein, oder klicken Sie auf **Durchsuchen** , um das Ordner Ziel zu suchen.

4.  Wenn der Ordner mithilfe DFS-Replikation repliziert wird, können Sie angeben, ob das neue Ordner Ziel der Replikations Gruppe hinzugefügt werden soll.

> [!TIP]
> Verwenden Sie zum Hinzufügen eines Ordner Ziels mithilfe von Windows PowerShell das Cmdlet [New-dfsnfoldertarget](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnfoldertarget) . Das DFSN-Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.

> [!NOTE]
> Ordner können Ordner Ziele oder andere DFS-Ordner, aber nicht beides auf derselben Ebene in der Ordnerhierarchie enthalten.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)
-   [Replizieren von Ordner Zielen mithilfe von DFS-Replikation](replicate-folder-targets-using-dfs-replication.md)