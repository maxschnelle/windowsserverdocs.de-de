---
title: "Hinzufügen von Ordnerzielen"
description: "In diesem Thema wird beschrieben, wie Sie Ordnerziele (UNC-Pfade) hinzufügen"
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: brianlic
ms.technology: storage
ms.topic: article
author: jasongerend
ms-date: 06/05/2017
ms.openlocfilehash: 71305089553d622f54cb4e5608034edfaf7abc5f
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="add-folder-targets"></a>Hinzufügen von Ordnerzielen

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server2012 R2, Windows Server 2012, Windows Server2008 R2, Windows Server 2008

Ein Ordnerziel ist der Universal Naming Convention (UNC)-Pfad eines freigegebenen Ordners oder ein anderer Namespace, der einem Ordner in einem Namespace zugeordnet ist. Das Hinzufügen mehrerer Ordnerziele erhöht die Verfügbarkeit des Ordners im Namespace.

## <a name="to-add-a-folder-target"></a>So fügen Sie ein Ordnerziel hinzu

Verwenden Sie das folgende Verfahren, um mithilfe der DFS-Verwaltung ein Ordnerziel hinzuzufügen:

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Ordner, und klicken Sie anschließend auf **Ordnerziel hinzufügen**.

3.  Geben Sie den Pfad des Ordnerziels ein oder klicken Sie auf **Durchsuchen**, um das Ordnerziel zu suchen.

4.  Wenn der Ordner mit DFS-Replikation repliziert wird, können Sie angeben, ob Sie das neue Ordnerziel der Replikationsgruppe hinzuzufügen möchten.

> [!TIP]
> Verwenden Sie zum Hinzufügen eines Ordnerziels mithilfe von Windows PowerShell das Cmdlet [New-DfsnFolderTarget](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnfoldertarget). Das DFSN Windows PowerShell-Modul wurde in Windows Server2012 eingeführt.

> [!NOTE]
> Ordner können Ordnerziele oder anderen DFS-Ordner enthalten, aber nicht beide auf der gleichen Ebene in der Hierarchie der Ordner.

## <a name="see-also"></a>Weitere Informationen:

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)
-   [Replizieren von Ordnerzielen mit DFS-Replikation](replicate-folder-targets-using-dfs-replication.md)