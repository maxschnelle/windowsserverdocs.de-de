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
ms.openlocfilehash: ee2ae5ddf40c6d8b49b9fbd40505f4e8c70fd92c
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473497"
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
> Verwenden Sie zum Hinzufügen eines Namespace Servers mithilfe von Windows PowerShell das [Cmdlet New-dfsnroottarget](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnroottarget). Das DFSN-Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Überprüfen der Server Anforderungen für DFS-Namespaces](https://technet.microsoft.com/library/cc753448(v=ws.11).aspx)
-   [Erstellen eines DFS-Namespaces](create-a-dfs-namespace.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)

