---
title: Erstellen eines Ordners in einem DFS-Namespace
description: In diesem Artikel wird beschrieben, wie Sie einen Ordner in einem DFS-Namespace erstellen.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 18e0f1ad19e8c6ce2b6dbffe0d25c940c4f8f985
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474277"
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
> Verwenden Sie zum Erstellen eines Ordners in einem Namespace mithilfe von Windows PowerShell das Cmdlet [New-dfsnfolder](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnfolder) . Das DFSN-Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.


## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)


