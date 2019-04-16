---
title: Erlauben oder verhindern Sie von Verweise und Clientfailbacks
description: Dieser Artikel beschreibt, wie Sie Verweise und Clientfailbacks aktivieren oder deaktivieren.
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: be827ba52beb65219dad30e8c182963054cfbd16
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="enable-or-disable-referrals-and-client-failback"></a>Erlauben oder verhindern Sie von Verweise und Clientfailbacks

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server2012 R2, Windows Server 2012, Windows Server2008 R2, Windows Server 2008

Bei einem Verweis handelt es sich um eine sortierte Liste mit Servern, die ein Clientcomputer von einem Domänencontroller oder Namespaceserver erhält, wenn der Benutzer auf einen Namespacestamm oder DFS-Ordner mit Zielen zugreift. Nach Eingang des Verweises auf dem Computer wird versucht, auf den ersten Server in der Liste zuzugreifen. Ist der Server nicht verfügbar, wird vom Clientcomputer versucht, auf den nächsten Server zuzugreifen. Wenn ein Server nicht mehr verfügbar ist, können Sie Clients so konfigurieren, dass ein Failback zum bevorzugten Server ausgeführt wird, nachdem er wieder verfügbar ist.

Der folgende Abschnitt beschreibt, wie Sie Verweise und Clientfailbacks aktivieren oder deaktivieren:

## <a name="enable-or-disable-referrals"></a>Aktivieren oder Deaktivieren von Verweisen

Durch Deaktivieren eines Namespaceservers oder eines Verweises für ein Ordnerziel können Sie verhindern, dass Benutzer zu diesem Namespaceserver oder Ordnerziel weitergeleitet werden. Dies ist von Vorteil, wenn ein Server zu Wartungszwecken vorübergehend offline geschaltet werden muss.

-   Führen Sie die folgenden Schritte aus, um Verweise auf ein Ordnerziel zu aktivieren oder deaktivieren:

    1.  Klicken Sie in der Konsolenstruktur der DFS-Verwaltung unter dem Knoten **Namespaces** auf einen Ordner mit Zielen, und klicken Sie anschließend im **Detailbereich** auf die Registerkarte **Ordnerziele**.
    2.  Klicken Sie mit der rechten Maustaste auf das Ordnerziel, und klicken Sie dann entweder auf **Ordnerziel deaktivieren** oder auf **Ordnerziel aktivieren**.

-   Führen Sie die folgenden Schritte aus, um Verweise auf einem Namspaceserver zu aktivieren oder deaktivieren:

    1.  Wählen Sie in der Konsolenstruktur der DFS-Verwaltung den entsprechenden Namespace aus, und klicken Sie anschließend auf die Registerkarte **Namespaceserver**.
    2.  Klicken Sie mit der rechten Maustaste auf den entsprechenden Namespaceserver, und klicken Sie anschließend entweder auf **Namespaceserver deaktivieren** oder auf **Namespaceserver aktivieren**.


> [!TIP]
> Verwenden Sie zum Aktivieren oder Deaktivieren der Verweise mithilfe von Windows PowerShell, die Cmdlets [Set-DfsnRootTarget – Status](https://technet.microsoft.com/library/jj884266.aspx) oder [Set-DfsnServerConfiguration](https://technet.microsoft.com/library/jj884277.aspx), die in Windows Server2012 eingeführt wurden.

## <a name="enable-client-failback"></a>Clientfailback aktivieren

Wenn ein Ziel nicht mehr verfügbar ist, können Sie Clients so konfigurieren, dass ein Failback zu dem Ziel ausgeführt wird, nachdem es wiederhergestellt wurde. Damit das Failback funktioniert, müssen die Clientcomputer die im folgenden Thema [Clientanforderungen für DFS-Namespaces](https://technet.microsoft.com/library/cc771913(v=ws.11).aspx) aufgeführten Anforderungen erfüllen.


> [!NOTE]
> Um ein Clientfailback mithilfe von Windows PowerShell auf einem Namespacestamm zu aktivieren, verwenden Sie das Cmdlet [Set-DfsnRoot](https://technet.microsoft.com/library/jj884281.aspx). Um Clientfailback für einen DFS-Ordner zu aktivieren, verwenden Sie das Cmdlet [Set-DfsnFolder](https://technet.microsoft.com/library/jj884283.aspx).


## <a name="to-enable-client-failback-for-a-namespace-root"></a>So aktivieren Sie das Clientfailback für einen Namespacestamm

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Namespace, und klicken Sie anschließend auf **Eigenschaften**.

3.  Aktivieren Sie auf der Registerkarte **Verweise** das Kontrollkästchen **Clientfailback zu bevorzugten Zielen**.

Ordner mit Zielen erben die Clientfailbackeinstellungen des Namespacestamms. Wenn das Clientfailback für den Namespacestamm deaktiviert ist, können Sie dem Client mithilfe der folgenden Prozedur das Ausführen eines Failbacks auf einem Ordner mit Zielen ermöglichen.

## <a name="to-enable-client-failback-for-a-folder-with-targets"></a>So aktivieren Sie das Clientfailback zu einem Ordner mit Zielen

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Ordner mit Zielen, und klicken Sie anschließend auf **Eigenschaften**.

3.  Aktivieren Sie auf der Registerkarte **Verweise** das Kontrollkästchen **Clientfailback zu bevorzugten Zielen**.

## <a name="see-also"></a>Weitere Informationen: 

-   [Optimieren von DFS-Namespaces](tuning-dfs-namespaces.md)
-   [Lesen Sie die DFS-Namespace-Clientanforderungen](https://technet.microsoft.com/library/cc771913(v=ws.11).aspx)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)