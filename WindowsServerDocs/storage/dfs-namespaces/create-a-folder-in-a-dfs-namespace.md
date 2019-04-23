---
title: Erstellen eines Ordners in einem DFS-Namespace
description: Dieser Artikel beschreibt, wie Sie einen Ordner in einem DFS-Namespace erstellen
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 47bb13aa404cdf4fef86b7250425a92cc208ba9d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856851"
---
# <a name="create-a-folder-in-a-dfs-namespace"></a>Erstellen Sie einen Ordner in einem DFS-Namespace

> Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer 2008

Sie können Ordner verwenden, um zusätzliche Ebenen der Hierarchie in einem Namespace zu erstellen. Sie können auch einen Ordner mit Ordnerzielen zum Hinzufügen von freigegebenen Ordnern auf den Namespace erstellen. DFS-Ordner mit Ordnerzielen dürfen keine anderen DFS-Ordner enthalten, wenn Sie daher eine Ebene der Hierarchie auf den Namespace hinzufügen möchten, sollten Sie keine Ordnerziele zum Ordner hinzufügen.

Gehen Sie wie folgt vor, um mithilfe der DFS-Verwaltung einen Ordner in einem Namespace zu erstellen.

## <a name="to-create-a-folder-in-a-dfs-namespace"></a>So erstellen Sie einen Ordner in einem DFS-Namespace

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Namespace oder einen Ordner in einem domänenbasierten Namespace, und klicken Sie dann auf **Neuer Ordner**.

3.  Geben Sie im Textfeld **Name** den Namen des neuen Ordners ein.

4.  Um eine oder mehrere Ordnerziele zum Ordner hinzuzufügen, klicken Sie auf **Hinzufügen** und geben Sie den UNC-Pfad (Universal Naming Convention) für das Ordnerziel an und klicken Sie dann auf **OK**.


> [!TIP]
> Verwenden Sie zum Erstellen eines Ordners in einem Namespace mithilfe von Windows PowerShell das Cmdlet [New-DfsnFolder](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnfolder). Das DFSN Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.


## <a name="see-also"></a>Siehe auch

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)


