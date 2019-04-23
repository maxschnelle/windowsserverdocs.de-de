---
title: Hinzufügen von Namespaceserver zu einem domänenbasierten DFS-Namespace
description: Dieser Artikel beschreibt, wie Sie zusätzliche Namespaceserver zum Hosten eines Namespaces mit DFS-Verwaltung angeben.
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: bb3b98e1ea687b68bbb87d0da413f9624d336370
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853331"
---
# <a name="add-namespace-servers-to-a-domain-based-dfs-namespace"></a>Hinzufügen von Namespaceserver zu einem domänenbasierten DFS-Namespace

> Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer 2008

Sie können die Verfügbarkeit eines domänenbasierten Namespaces erhöhen, indem Sie zusätzliche Namespaceserver zum Hosten des Namespaces angeben.

## <a name="to-add-a-namespace-server-to-a-domain-based-namespace"></a>So fügen Sie einen Namespaceserver zu einem domänenbasierten Namespace hinzu

Um einen domänenbasierten Namespace mit DFS-Verwaltung einem Namespaceserver hinzuzufügen, verwenden Sie das folgende Verfahren:

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen domänenbasierten Namespace, und klicken Sie dann auf **Namespaceserver hinzufügen**.

3.  Geben Sie den Pfad zu einem anderen Server an oder klicken Sie auf **Durchsuchen**, um einen Server zu suchen.

> [!NOTE]
> Dieses Verfahren gilt nicht für eigenständige Namespaces, da sie nur einen einzigen Namespaceserver unterstützen. Um die Verfügbarkeit eines eigenständigen Namespace zu erhöhen, geben Sie einen Failovercluster als Namespaceserver im Assistenten für den neuen Namespace an.


> [!TIP]
> Verwenden Sie zum Hinzufügen eines Namespaceservers mithilfe von Windows PowerShell das [New-DfsnRootTarget-Cmdlet](https://docs.microsoft.com/powershell/module/dfsn/set-dfsnroottarget). Das DFSN Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.

## <a name="see-also"></a>Siehe auch

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Überprüfen der Serveranforderungen für DFS-Namespaces](https://technet.microsoft.com/library/cc753448(v=ws.11).aspx)
-   [Erstellen Sie eine DFS-Namespace](create-a-dfs-namespace.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)

