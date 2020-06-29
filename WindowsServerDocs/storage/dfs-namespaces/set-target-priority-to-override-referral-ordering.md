---
title: Festlegen der Zielpriorität zum Überschreiben der Sortiermethode von Verweisen
description: In diesem Artikel wird beschrieben, wie Sie die Ziel Priorität festlegen
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 401e15c248687c7585cb85172b1d4d57125cdc86
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475177"
---
# <a name="set-target-priority-to-override-referral-ordering"></a>Festlegen der Ziel Priorität zum Überschreiben der Verweis Anordnung

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Ein Verweis ist eine sortierte Zielliste, die ein Client-PC von einem Domänencontroller oder Namespaceserver empfängt, wenn der Benutzer auf einen Namespacestamm oder -ordner mit Zielen im Namespace zugreift. Die einzelnen Ziele in einem Verweis werden gemäß der Sortiermethode für den Namespacestamm oder -ordner sortiert.

Um die Anordnung von Zielen zu verfeinern, können Sie die Priorität für einzelne Ziele festlegen. Sie können z. b. angeben, dass das Ziel zuerst für alle Ziele, zuletzt für alle Ziele oder für alle Ziele der gleichen Kosten gleich ist.

## <a name="to-set-target-priority-on-a-root-target-for-a-domain-based-namespace"></a>So legen Sie die Zielpriorität eines Stammziels für einen domänenbasierten Namespace fest

Gehen Sie folgendermaßen vor, um die Ziel Priorität eines Stamm Ziels für einen domänenbasierten Namespace festzulegen:

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolen Struktur unter dem Knoten **Namespaces** auf den domänenbasierten Namespace für die Stamm Ziele, für die Sie die Priorität festlegen möchten.

3.  Klicken Sie im **Detail** Bereich auf der Registerkarte **Namespace Server** mit der rechten Maustaste auf das Stamm Ziel mit der Priorität, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften**.

4.  Klicken Sie auf der Registerkarte **erweitert** auf **Verweis Reihenfolge außer Kraft setzen**, und klicken Sie dann auf die gewünschte Priorität.

    -   **Erster unter allen Zielen**  Gibt an, dass Benutzer immer auf dieses Ziel verwiesen werden sollen, wenn das Ziel verfügbar ist.
    -   **Letzte zwischen allen Zielen** Gibt an, dass Benutzer nie auf dieses Ziel verwiesen werden sollten, es sei denn, alle anderen Ziele sind nicht verfügbar.
    -   **Zuerst unter den Zielen der gleichen Kosten**  Gibt an, dass Benutzer auf dieses Ziel vor anderen Zielen gleicher Kosten verwiesen werden sollen (was in der Regel andere Ziele an derselben Site bedeutet).
    -   Die **letzten Ziele der gleichen Kosten**  Gibt an, dass Benutzer nie auf dieses Ziel verwiesen werden sollen, wenn andere Ziele mit gleichen Kosten verfügbar sind (Dies bedeutet in der Regel andere Ziele am selben Standort).

## <a name="to-set-target-priority-on-a-folder-target"></a>So legen Sie die Zielpriorität eines Ordnerziels fest

Verwenden Sie das folgende Verfahren, um die Ziel Priorität für ein Ordner Ziel festzulegen:

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolen Struktur unter dem Knoten **Namespaces** auf den Ordner der Ziele, für die Sie die Priorität festlegen möchten.

3.  Klicken Sie im **Detail** Bereich auf der Registerkarte **Ordner Ziele** mit der rechten Maustaste auf das Ordner Ziel mit der Priorität, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften** .

4.  Klicken Sie auf der Registerkarte **erweitert** auf **Verweis Anordnung außer Kraft setzen** , und klicken Sie dann auf die gewünschte Priorität.

> [!NOTE]
> Um Ziel Prioritäten mithilfe von Windows PowerShell festzulegen, verwenden Sie die Cmdlets " [Set-dfsnroottarget](https://technet.microsoft.com/library/jj884266.aspx) " und " [Set-dfsnfoldertarget](https://technet.microsoft.com/library/jj884264.aspx) " mit den Parametern " **referenralpriorityclass** " und " **referralpriorityrank** ". Diese Cmdlets wurden in Windows Server 2012 eingeführt.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Optimieren von DFS-Namespaces](tuning-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)