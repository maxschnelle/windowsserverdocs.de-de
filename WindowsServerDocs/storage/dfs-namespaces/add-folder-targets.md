---
title: Hinzufügen von Ordnerzielen
description: In diesem Thema wird beschrieben, wie Sie Ordnerziele (UNC-Pfade) hinzufügen
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: brianlic
ms.technology: storage
ms.topic: article
author: jasongerend
ms-date: 06/05/2017
ms.openlocfilehash: 8cc61189076669d5c24244294b2f0eee2b783517
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831001"
---
# <a name="add-folder-targets"></a>Hinzufügen von Ordnerzielen

> Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer 2008

Ein Ordnerziel ist der Universal Naming Convention (UNC)-Pfad eines freigegebenen Ordners oder ein anderer Namespace, der einem Ordner in einem Namespace zugeordnet ist. Das Hinzufügen mehrerer Ordnerziele erhöht die Verfügbarkeit des Ordners im Namespace.

## <a name="to-add-a-folder-target"></a>So fügen Sie ein Ordnerziel hinzu

Verwenden Sie das folgende Verfahren, um mithilfe der DFS-Verwaltung ein Ordnerziel hinzuzufügen:

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Ordner, und klicken Sie anschließend auf **Ordnerziel hinzufügen**.

3.  Geben Sie den Pfad des Ordnerziels ein oder klicken Sie auf **Durchsuchen**, um das Ordnerziel zu suchen.

4.  Wenn der Ordner mit DFS-Replikation repliziert wird, können Sie angeben, ob Sie das neue Ordnerziel der Replikationsgruppe hinzuzufügen möchten.

> [!TIP]
> Verwenden Sie zum Hinzufügen eines Ordnerziels mithilfe von Windows PowerShell das Cmdlet [New-DfsnFolderTarget](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnfoldertarget). Das DFSN Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.

> [!NOTE]
> Ordner können Ordnerziele oder anderen DFS-Ordner enthalten, aber nicht beide auf der gleichen Ebene in der Hierarchie der Ordner.

## <a name="see-also"></a>Siehe auch

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)
-   [Replizieren Sie die Ordnerziele des DFS-Replikation verwenden](replicate-folder-targets-using-dfs-replication.md)