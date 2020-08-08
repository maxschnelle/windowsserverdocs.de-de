---
title: Hinzufügen von Ordnerzielen
description: In diesem Thema wird beschrieben, wie Sie Ordner Ziele (UNC-Pfade) hinzufügen.
ms.author: jgerend
manager: brianlic
ms.topic: article
author: jasongerend
ms-date: 06/05/2017
ms.openlocfilehash: bc229360a616e7fa56231e6211b4b909d45ec2de
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957818"
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
> Verwenden Sie zum Hinzufügen eines Ordner Ziels mithilfe von Windows PowerShell das Cmdlet [New-dfsnfoldertarget](/powershell/module/dfsn/new-dfsnfoldertarget) . Das DFSN-Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.

> [!NOTE]
> Ordner können Ordner Ziele oder andere DFS-Ordner, aber nicht beides auf derselben Ebene in der Ordnerhierarchie enthalten.

## <a name="additional-references"></a>Weitere Verweise

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)
-   [Replizieren von Ordner Zielen mithilfe von DFS-Replikation](replicate-folder-targets-using-dfs-replication.md)
