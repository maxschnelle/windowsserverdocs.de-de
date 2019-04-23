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
ms.openlocfilehash: 4256e124e75be72f94cbd35c182edfe38e92bc90
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847501"
---
# <a name="create-a-dfs-namespace"></a>Erstellen eines DFS-Namespaces

> Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer 2008

Um einen neuen Namespace zu erstellen, können Sie Server-Manager verwenden, um den Namespace zu erstellen, wenn Sie den DFS-Namespaces-Rollendienst installieren. Können Sie auch das [New-DfsnRoot cmdlet](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnroot) von einer Windows PowerShell-Sitzung verwenden. 

Das DFSN Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt. 

Alernativ können Sie einen Namespace nach der Installation des Rollendiensts folgendermaßen erstellen.

## <a name="to-create-a-namespace"></a>So erstellen Sie einen Namespace

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie mit der rechten Maustaste in der Konsolenstruktur auf den Knoten **Namespaces** und anschließend auf **Neuen Namespace**.

3.  Befolgen Sie die Anweisungen im **Assistenten für den neuen Namespace**.

    Um einen eigenständigen Namespace in einem Failovercluster zu erstellen, geben Sie den Namen der Clusterdateiserverinstanz auf der **Namespace Server** Seite des **Assistenten für den neuen Namespace** an.

> [!IMPORTANT]
> Versuchen Sie nicht zum Erstellen eines domänenbasierten Namespace verwenden den Windows Server 2008-Modus, wenn die Gesamtstrukturfunktionsebene auf WindowsServer 2003 oder höher ist. Auf diese Weise kann in einem Namespace führen für die Sie DFS-Ordnern nicht löschen können dies ergibt die folgende Fehlermeldung angezeigt: "Der Ordner kann nicht gelöscht werden. Der Vorgang kann nicht beendet werden."

## <a name="see-also"></a>Siehe auch

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Wählen Sie einen Namespace-Typ](choose-a-namespace-type.md)
-   [Hinzufügen von Namespace-Servern zu einem domänenbasierten DFS-Namespace](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md).


