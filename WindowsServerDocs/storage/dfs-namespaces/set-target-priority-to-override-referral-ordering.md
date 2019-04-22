---
title: Festlegen der Zielpriorität zum Überschreiben der Sortiermethode von Verweisen
description: Dieser Artikel beschreibt die Vorgehensweise beim Festlegen der Zielpriorität, um die Verweisreihenfolge außer Kraft zu setzen
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 59db08d5ef46b696f550a5fa0738c5c1f9375fda
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826361"
---
# <a name="set-target-priority-to-override-referral-ordering"></a>Legen Sie die Zielpriorität zum Überschreiben der Sortiermethode von Verweisen fest

> Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer 2008

Ein Verweis ist eine sortierte Zielliste, die ein Client-PC von einem Domänencontroller oder Namespaceserver empfängt, wenn der Benutzer auf einen Namespacestamm oder -ordner mit Zielen im Namespace zugreift. Die einzelnen Ziele in einem Verweis werden gemäß der Sortiermethode für den Namespacestamm oder -ordner sortiert. 

Sie können für einzelne Ziele eine Priorität festlegen, um die Sortierung der Ziele zu optimieren. Sie können z. B. angeben, dass das Ziel das erste von allen Zielen, das letzte von allen Zielen oder das erste oder letzte von allen Zielen mit gleichen Kosten ist.

## <a name="to-set-target-priority-on-a-root-target-for-a-domain-based-namespace"></a>So legen Sie die Zielpriorität eines Stammziels für einen domänenbasierten Namespace fest

Gehen Sie wie im Folgenden beschrieben vor, um die Zielpriorität eines Stammziels für einen domänenbasierten Namespace festzulegen:

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** auf den domänenbasierten Namespace für die Stammziele, für die Sie eine Priorität festlegen möchten.

3.  Klicken Sie im **Detailbereich** auf der Registerkarte **Namespaceserver** mit der rechten Maustaste auf das Stammziel mit der zu ändernden Priorität, und klicken Sie dann auf **Eigenschaften**.

4.  Klicken Sie auf der Registerkarte **Erweitert** auf **Folgende Verweisreihenfolge außer Kraft setzen**, und klicken Sie dann auf die gewünschte Priorität.

    -   **Das erste von allen Zielen** Gibt an, dass Benutzer immer an dieses Ziel verwiesen werden sollen, wenn das Ziel verfügbar ist.
    -   **Das letzte von allen Zielen** Gibt an, dass Benutzer nie an dieses Ziel verwiesen werden sollen, es sei denn, alle anderen Ziele sind nicht verfügbar.
    -   **Das erste unter den Zielen mit gleichen Kosten** Gibt an, dass Benutzer an dieses Ziel verwiesen werden sollen, bevor sie an andere Ziele mit gleichen Kosten verwiesen werden (hierbei handelt es sich gewöhnlich um weitere Ziele am selben Standort).
    -   **Das letzte Ziel bei gleichen Kosten** Gibt an, dass Benutzer nie an dieses Ziel verwiesen werden sollen, wenn andere Ziele mit gleichen Kosten verfügbar sind (hierbei handelt es sich gewöhnlich um weitere Ziele am selben Standort).

## <a name="to-set-target-priority-on-a-folder-target"></a>So legen Sie die Zielpriorität eines Ordnerziels fest

Verwenden Sie zum Festlegen der Zielpriorität eines Ordnerziels das folgende Verfahren:

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** auf den Ordner der Ziele, für die Sie eine Priorität festlegen möchten.

3.  Klicken Sie im **Detailbereich** auf der Registerkarte **Ordnerziele** mit der rechten Maustaste auf das Ordnerziel mit der zu ändernden Priorität, und klicken Sie dann auf **Eigenschaften**.

4.  Klicken Sie auf der Registerkarte **Erweitert** auf **Folgende Verweisreihenfolge außer Kraft setzen**, und klicken Sie dann auf die gewünschte Priorität.

> [!NOTE]
> Um Zielprioritäten mithilfe von Windows PowerShell festzulegen, verwenden Sie die Cmdlets [Set-DfsnRootTarget](https://technet.microsoft.com/library/jj884266.aspx) und [Set-DfsnFolderTarget](https://technet.microsoft.com/library/jj884264.aspx) mit den Parametern **ReferralPriorityClass** und **ReferralPriorityRank**. Diese Cmdlets wurden in Windows Server 2012 eingeführt.

## <a name="see-also"></a>Siehe auch

-   [Optimieren von DFS-Namespaces](tuning-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)