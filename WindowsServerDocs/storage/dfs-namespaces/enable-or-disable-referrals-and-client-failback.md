---
title: Aktivieren oder Deaktivieren von Verweisen und Clientfailbacks
description: In diesem Artikel wird beschrieben, wie Sie Verweise und das Client Failback aktivieren oder deaktivieren.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 15c02897df0710653a6a3663ce6f8e87bfa416b6
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471805"
---
# <a name="enable-or-disable-referrals-and-client-failback"></a>Aktivieren oder Deaktivieren von Verweisen und Clientfailbacks

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Ein Verweis ist eine geordnete Liste von Servern, die von einem Client Computer von einem Domänen Controller oder einem Namespace Server empfangen werden, wenn der Benutzer auf einen Namespace Stamm oder einen DFS-Ordner mit Zielen zugreift. Nach Eingang des Verweises auf dem Computer wird versucht, auf den ersten Server in der Liste zuzugreifen. Ist der Server nicht verfügbar, wird vom Clientcomputer versucht, auf den nächsten Server zuzugreifen. Wenn ein Server nicht mehr verfügbar ist, können Sie Clients so konfigurieren, dass ein Failback zum bevorzugten Server durchführen wird, nachdem dieser verfügbar ist.

In den folgenden Abschnitten finden Sie Informationen zum Aktivieren oder Deaktivieren von verweisen oder zum Aktivieren des Client Failbacks:

## <a name="enable-or-disable-referrals"></a>Aktivieren oder Deaktivieren von Verweisen

Durch Deaktivieren des Verweises eines Namespace Servers oder des Ordner Ziels können Sie verhindern, dass Benutzer an den Namespace Server oder das Ordner Ziel weitergeleitet werden. Dies ist von Vorteil, wenn ein Server zu Wartungszwecken vorübergehend offline geschaltet werden muss.

-   Führen Sie die folgenden Schritte aus, um Verweise auf ein Ordner Ziel zu aktivieren bzw. zu deaktivieren:

    1.  Klicken Sie in der Struktur der DFS-Verwaltungskonsole unter dem Knoten **Namespaces** auf einen Ordner mit Zielen, und klicken Sie dann im **Detail** Bereich auf die Registerkarte **Ordner Ziele** .
    2.  Klicken Sie mit der rechten Maustaste auf das Ordner Ziel, und klicken Sie dann entweder auf **Ordner Ziel deaktivieren** oder **Ordner Ziel aktivieren**.

-   Um Verweise auf einen Namespace Server zu aktivieren oder zu deaktivieren, führen Sie die folgenden Schritte aus:

    1.  Wählen Sie in der Struktur der DFS-Verwaltungskonsole den entsprechenden Namespace aus, und klicken Sie dann auf die Registerkarte **Namespace Server** .
    2.  Klicken Sie mit der rechten Maustaste auf den entsprechenden Namespace Server, und klicken Sie dann auf **Namespace Server deaktivieren** oder **Namespace Server aktivieren**.


> [!TIP]
> Um Verweise mithilfe von Windows PowerShell zu aktivieren oder zu deaktivieren, verwenden Sie die Cmdlets " [Set-dfsnroottarget – State](https://technet.microsoft.com/library/jj884266.aspx) " oder " [Set-dfsnserverconfiguration](https://technet.microsoft.com/library/jj884277.aspx) ", die in Windows Server 2012 eingeführt wurden.

## <a name="enable-client-failback"></a>Clientfailback aktivieren

Wenn ein Ziel nicht mehr verfügbar ist, können Sie Clients so konfigurieren, dass ein Failback zu dem Ziel ausgeführt wird, nachdem es wiederhergestellt wurde. Damit das Failback funktioniert, müssen die Client Computer die im folgenden Thema aufgeführten Anforderungen erfüllen: [Überprüfen von Client Anforderungen für DFS-Namespaces](https://technet.microsoft.com/library/cc771913(v=ws.11).aspx).


> [!NOTE]
> Verwenden Sie das Cmdlet [Set-dfsnroot](https://technet.microsoft.com/library/jj884281.aspx) , um das Client Failback für einen Namespace Stamm mithilfe von Windows PowerShell zu aktivieren. Verwenden Sie das Cmdlet [Set-dfsnfolder](https://technet.microsoft.com/library/jj884283.aspx) , um das Client Failback für einen DFS-Ordner zu aktivieren.


## <a name="to-enable-client-failback-for-a-namespace-root"></a>So aktivieren Sie das Clientfailback für einen Namespacestamm

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Namespace, und klicken Sie anschließend auf **Eigenschaften**.

3.  Aktivieren Sie auf der Registerkarte **Verweise** das Kontrollkästchen **Clientfailback zu bevorzugten Zielen**.

Ordner mit Zielen erben die Clientfailbackeinstellungen des Namespacestamms. Wenn das Client Failback für den Namespace Stamm deaktiviert ist, können Sie das folgende Verfahren verwenden, um dem Client zu ermöglichen, ein Failback für einen Ordner mit Zielen auszuführen.

## <a name="to-enable-client-failback-for-a-folder-with-targets"></a>So aktivieren Sie das Clientfailback zu einem Ordner mit Zielen

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Ordner mit Zielen, und klicken Sie anschließend auf **Eigenschaften**.

3.  Aktivieren Sie auf der Registerkarte **Verweise** das Kontrollkästchen **Clientfailback zu bevorzugten Zielen**.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Optimieren von DFS-Namespaces](tuning-dfs-namespaces.md)
-   [Überprüfen von Client Anforderungen für DFS-Namespaces](https://technet.microsoft.com/library/cc771913(v=ws.11).aspx)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)