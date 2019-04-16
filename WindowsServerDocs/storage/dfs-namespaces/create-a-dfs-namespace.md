---
title: Erstellen eines DFS-Namespaces
description: Dieser Artikel beschreibt, wie Sie einen DFS-Namespace erstellen.
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: b01a83f165e0ef01c6413dcf8785435c8f3aca5a
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="create-a-dfs-namespace"></a>Erstellen eines DFS-Namespaces

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server2012 R2, Windows Server 2012, Windows Server2008 R2, Windows Server 2008

Um einen neuen Namespace zu erstellen, können Sie Server-Manager verwenden, um den Namespace zu erstellen, wenn Sie den DFS-Namespaces-Rollendienst installieren. Können Sie auch das [New-DfsnRoot cmdlet](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnroot) von einer Windows PowerShell-Sitzung verwenden. 

Das DFSN Windows PowerShell-Modul wurde in Windows Server2012 eingeführt. 

Alernativ können Sie einen Namespace nach der Installation des Rollendiensts folgendermaßen erstellen.

## <a name="to-create-a-namespace"></a>So erstellen Sie einen Namespace

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie mit der rechten Maustaste in der Konsolenstruktur auf den Knoten **Namespaces** und anschließend auf **Neuen Namespace**.

3.  Befolgen Sie die Anweisungen im **Assistenten für den neuen Namespace**.

    Um einen eigenständigen Namespace in einem Failovercluster zu erstellen, geben Sie den Namen der Clusterdateiserverinstanz auf der **Namespace Server** Seite des **Assistenten für den neuen Namespace** an.

> [!IMPORTANT]
> Versuchen Sie nicht einen domänenbasierten Namespaces mithilfe des Windows Server2008-Modus zu erstellen, es sei denn die Gesamtstrukturfunktionsebene ist Windows Server 2003 oder höher. Dies kann dazu zu einem Namespace führen, für den die DFS-Ordner nicht gelöscht werden können. Es wird folgende Fehlermeldung angezeigt: "Der Ordner kann nicht gelöscht werden. Der Vorgang kann nicht beendet werden."

## <a name="see-also"></a>Weitere Informationen:

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Namespacetyp auswählen](choose-a-namespace-type.md)
-   [Hinzufügen von Namespaceserver zu einem domänenbasierten DFS-Namespace](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md).


