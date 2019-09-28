---
title: Erstellen eines DFS-Namespaces
description: Dieser Artikel beschreibt, wie Sie einen DFS-Namespace erstellen.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f4d4b86dd1a105576ac4d1749213696b319ba528
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402207"
---
# <a name="create-a-dfs-namespace"></a>Erstellen eines DFS-Namespaces

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Um einen neuen Namespace zu erstellen, können Sie Server-Manager verwenden, um den Namespace zu erstellen, wenn Sie den DFS-Namespaces-Rollendienst installieren. Können Sie auch das [New-DfsnRoot cmdlet](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnroot) von einer Windows PowerShell-Sitzung verwenden. 

Das DFSN Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt. 

Alernativ können Sie einen Namespace nach der Installation des Rollendiensts folgendermaßen erstellen.

## <a name="to-create-a-namespace"></a>So erstellen Sie einen Namespace

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie mit der rechten Maustaste in der Konsolenstruktur auf den Knoten **Namespaces** und anschließend auf **Neuen Namespace**.

3.  Befolgen Sie die Anweisungen im **Assistenten für den neuen Namespace**.

    Um einen eigenständigen Namespace in einem Failovercluster zu erstellen, geben Sie den Namen der Clusterdateiserverinstanz auf der **Namespace Server** Seite des **Assistenten für den neuen Namespace** an.

> [!IMPORTANT]
> Versuchen Sie nicht, einen domänenbasierten Namespace im Windows Server 2008-Modus zu erstellen, es sei denn, die Gesamtstruktur Funktionsebene ist Windows Server 2003 oder höher. Dies kann zu einem Namespace führen, für den DFS-Ordner nicht gelöscht werden können, und die folgende Fehlermeldung wird ausgegeben: "Der Ordner kann nicht gelöscht werden. Der Vorgang kann nicht beendet werden."

## <a name="see-also"></a>Siehe auch

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Auswählen eines Namespacetyps](choose-a-namespace-type.md)
-   [Hinzufügen von Namespaceservern zu einem domänenbasierten DFS-Namespace](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md).


