---
title: Hinzufügen von Namespaceservern zu einem domänenbasierten DFS-Namespace
description: In diesem Artikel wird beschrieben, wie Sie zusätzliche Namespace Server angeben, um einen Namespace mithilfe der DFS-Verwaltung zu hosten.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f00a6419bae1951a7c1597212d3c37676a4db90e
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961252"
---
# <a name="add-namespace-servers-to-a-domain-based-dfs-namespace"></a>Hinzufügen von Namespace Servern zu einem domänenbasierten DFS-Namespace

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Sie können die Verfügbarkeit eines domänenbasierten Namespace erhöhen, indem Sie zusätzliche Namespace Server angeben, um den Namespace zu hosten.

## <a name="to-add-a-namespace-server-to-a-domain-based-namespace"></a>So fügen Sie einem domänenbasierten Namespace einen Namespace Server hinzu

Zum Hinzufügen eines Namespace Servers zu einem domänenbasierten Namespace mithilfe der DFS-Verwaltung verwenden Sie das folgende Verfahren:

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolen Struktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen domänenbasierten Namespace, und klicken Sie dann auf **Namespace Server hinzufügen**.

3.  Geben Sie den Pfad zu einem anderen Server ein, oder klicken Sie auf **Durchsuchen** , um einen Server zu suchen

> [!NOTE]
> Dieses Verfahren gilt nicht für eigenständige Namespaces, da Sie nur einen einzelnen Namespace Server unterstützen. Um die Verfügbarkeit eines eigenständigen Namespace zu erhöhen, geben Sie im Assistenten für neue Namespaces einen Failovercluster als Namespace Server an.


> [!TIP]
> Verwenden Sie zum Hinzufügen eines Namespace Servers mithilfe von Windows PowerShell das [Cmdlet New-dfsnroottarget](/powershell/module/dfsn/new-dfsnroottarget). Das DFSN-Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Überprüfen der Server Anforderungen für DFS-Namespaces](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753448(v=ws.11))
-   [Erstellen eines DFS-Namespaces](create-a-dfs-namespace.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)
