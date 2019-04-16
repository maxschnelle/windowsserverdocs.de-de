---
title: Erstellen Sie einen Ordner in einem DFS-Namespace
description: Dieser Artikel beschreibt, wie Sie einen Ordner in einem DFS-Namespace erstellen
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 1ca9fa0b87c6e995f3f0c38abec80fef9068df90
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="create-a-folder-in-a-dfs-namespace"></a>Erstellen Sie einen Ordner in einem DFS-Namespace

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server2012 R2, Windows Server 2012, Windows Server2008 R2, Windows Server 2008

Sie können Ordner verwenden, um zusätzliche Ebenen der Hierarchie in einem Namespace zu erstellen. Sie können auch einen Ordner mit Ordnerzielen zum Hinzufügen von freigegebenen Ordnern auf den Namespace erstellen. DFS-Ordner mit Ordnerzielen dürfen keine anderen DFS-Ordner enthalten, wenn Sie daher eine Ebene der Hierarchie auf den Namespace hinzufügen möchten, sollten Sie keine Ordnerziele zum Ordner hinzufügen.

Gehen Sie wie folgt vor, um mithilfe der DFS-Verwaltung einen Ordner in einem Namespace zu erstellen.

## <a name="to-create-a-folder-in-a-dfs-namespace"></a>So erstellen Sie einen Ordner in einem DFS-Namespace

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Namespace oder einen Ordner in einem domänenbasierten Namespace, und klicken Sie dann auf **Neuer Ordner**.

3.  Geben Sie im Textfeld **Name** den Namen des neuen Ordners ein.

4.  Um eine oder mehrere Ordnerziele zum Ordner hinzuzufügen, klicken Sie auf **Hinzufügen** und geben Sie den UNC-Pfad (Universal Naming Convention) für das Ordnerziel an und klicken Sie dann auf **OK**.


> [!TIP]
> Verwenden Sie zum Erstellen eines Ordners in einem Namespace mithilfe von Windows PowerShell das Cmdlet [New-DfsnFolder](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnfolder). Das DFSN Windows PowerShell-Modul wurde in Windows Server2012 eingeführt.


## <a name="see-also"></a>Weitere Informationen:

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)


