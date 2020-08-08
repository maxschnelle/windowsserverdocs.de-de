---
title: Erstellen eines DFS-Namespaces
description: In diesem Artikel wird beschrieben, wie Sie einen DFS-Namespace erstellen.
ms.date: 6/5/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 6999dec3681a765ac64fdedd2e695c8a3f7dbcfa
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939425"
---
# <a name="create-a-dfs-namespace"></a>Erstellen eines DFS-Namespace

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Zum Erstellen eines neuen Namespace können Sie Server-Manager verwenden, um den Namespace zu erstellen, wenn Sie den DFS-Namespaces-Rollen Dienst installieren. Sie können auch das [Cmdlet New-dfsnroot](/powershell/module/dfsn/new-dfsnroot) aus einer Windows PowerShell-Sitzung verwenden.

Das DFSN-Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.

Mit der folgenden Vorgehensweise können Sie nach der Installation des Rollen dienstanzdienstanbieter einen Namespace erstellen.

## <a name="to-create-a-namespace"></a>So erstellen Sie einen Namespace

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf den Knoten **Namespaces** , und klicken Sie dann auf **neuer Namespace**.

3.  Befolgen Sie die Anweisungen im **Assistenten für neue Namespaces**.

    Um einen eigenständigen Namespace auf einem Failovercluster zu erstellen, geben Sie den Namen einer Cluster Dateiserver-Instanz auf der Seite **Namespace Server** des **Assistenten für neue Namespaces** an.

> [!IMPORTANT]
> Versuchen Sie nicht, einen domänenbasierten Namespace im Windows Server 2008-Modus zu erstellen, es sei denn, die Gesamtstruktur Funktionsebene ist Windows Server 2003 oder höher. Dies kann zu einem Namespace führen, für den DFS-Ordner nicht gelöscht werden können, und die folgende Fehlermeldung wird angezeigt: "der Ordner kann nicht gelöscht werden. Diese Funktion kann nicht ausgeführt werden. "

## <a name="additional-references"></a>Weitere Verweise

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Auswählen eines Namespacetyps](choose-a-namespace-type.md)
-   [Hinzufügen von Namespaceservern zu einem domänenbasierten DFS-Namespace](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   [Delegieren von Verwaltungs Berechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md).
