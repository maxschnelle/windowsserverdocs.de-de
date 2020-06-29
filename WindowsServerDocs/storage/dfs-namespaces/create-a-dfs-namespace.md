---
title: Erstellen eines DFS-Namespaces
description: In diesem Artikel wird beschrieben, wie Sie einen DFS-Namespace erstellen.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 90a6c0f72fc1a11d9070fa7866c0b64044131a07
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469715"
---
# <a name="create-a-dfs-namespace"></a>Erstellen eines DFS-Namespace

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Zum Erstellen eines neuen Namespace können Sie Server-Manager verwenden, um den Namespace zu erstellen, wenn Sie den DFS-Namespaces-Rollen Dienst installieren. Sie können auch das [Cmdlet New-dfsnroot](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnroot) aus einer Windows PowerShell-Sitzung verwenden.

Das DFSN-Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.

Mit der folgenden Vorgehensweise können Sie nach der Installation des Rollen dienstanzdienstanbieter einen Namespace erstellen.

## <a name="to-create-a-namespace"></a>So erstellen Sie einen Namespace

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf den Knoten **Namespaces** , und klicken Sie dann auf **neuer Namespace**.

3.  Befolgen Sie die Anweisungen im **Assistenten für neue Namespaces**.

    Um einen eigenständigen Namespace auf einem Failovercluster zu erstellen, geben Sie den Namen einer Cluster Dateiserver-Instanz auf der Seite **Namespace Server** des **Assistenten für neue Namespaces** an.

> [!IMPORTANT]
> Versuchen Sie nicht, einen domänenbasierten Namespace im Windows Server 2008-Modus zu erstellen, es sei denn, die Gesamtstruktur Funktionsebene ist Windows Server 2003 oder höher. Dies kann zu einem Namespace führen, für den DFS-Ordner nicht gelöscht werden können, und die folgende Fehlermeldung wird angezeigt: "der Ordner kann nicht gelöscht werden. Diese Funktion kann nicht ausgeführt werden. "

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Auswählen eines Namespacetyps](choose-a-namespace-type.md)
-   [Hinzufügen von Namespaceservern zu einem domänenbasierten DFS-Namespace](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   [Delegieren von Verwaltungs Berechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md).


