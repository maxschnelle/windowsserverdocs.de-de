---
title: Erstellen eines Ordners in einem DFS-Namespace
description: In diesem Artikel wird beschrieben, wie Sie einen Ordner in einem DFS-Namespace erstellen.
ms.date: 6/5/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: d854cfcb02288f6262ee380edc0614baf9e29878
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957698"
---
# <a name="create-a-folder-in-a-dfs-namespace"></a>Erstellen eines Ordners in einem DFS-Namespace

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Sie können Ordner verwenden, um zusätzliche Ebenen der Hierarchie in einem Namespace zu erstellen. Sie können auch Ordner mit Ordner Zielen erstellen, um dem Namespace freigegebene Ordner hinzuzufügen. DFS-Ordner mit Ordner Zielen dürfen keine anderen DFS-Ordner enthalten. Wenn Sie also eine Hierarchieebene zum-Namespace hinzufügen möchten, fügen Sie dem Ordner keine Ordner Ziele hinzu.

Mithilfe des folgenden Verfahrens können Sie einen Ordner in einem Namespace mithilfe der DFS-Verwaltung erstellen:

## <a name="to-create-a-folder-in-a-dfs-namespace"></a>So erstellen Sie einen Ordner in einem DFS-Namespace

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolen Struktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Namespace oder einen Ordner innerhalb eines Namespace, und klicken Sie dann auf **neuer Ordner**.

3.  Geben Sie im Textfeld **Name** den Namen des neuen Ordners ein.

4.  Klicken Sie zum Hinzufügen eines oder mehrerer Ordner Ziele zum Ordner auf **Hinzufügen** , und geben Sie den UNC-Pfad (Universal Naming Convention) des Ordner Ziels an, und klicken Sie dann auf **OK** .


> [!TIP]
> Verwenden Sie zum Erstellen eines Ordners in einem Namespace mithilfe von Windows PowerShell das Cmdlet [New-dfsnfolder](/powershell/module/dfsn/new-dfsnfolder) . Das DFSN-Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.


## <a name="additional-references"></a>Weitere Verweise

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)
