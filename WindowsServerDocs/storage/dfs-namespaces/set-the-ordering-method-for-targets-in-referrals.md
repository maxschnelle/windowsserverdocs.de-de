---
title: Festlegen der Sortiermethode für Ziele in Verweisen
description: Dieser Artikel beschreibt die Vorgehensweise beim Festlegen der Sortiermethode für Ziele in Verweisen.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: bb42a98666941c5dfa50a8dfbf45635ad25dc767
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386143"
---
# <a name="set-the-ordering-method-for-targets-in-referrals"></a>Festlegen der Sortiermethode für Ziele in Verweisen

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Ein Verweis ist eine sortierte Zielliste, die ein Client-PC von einem Domänencontroller oder Namespaceserver empfängt, wenn der Benutzer auf einen Namespacestamm oder -ordner mit Zielen zugreift. Nach Eingang des Verweises auf dem Client wird versucht, auf das erste Ziel in der Liste zuzugreifen. Ist das Ziel nicht verfügbar, wird vom Clientcomputer versucht, auf das nächste Ziel zuzugreifen.
Ziele am Standort des Clients werden in einem Verweis immer zuerst aufgeführt. Ziele außerhalb des Standorts des Clients werden gemäß der Sortiermethode aufgelistet.

Verwenden Sie die folgenden Abschnitte, um anzugeben, in welcher Reihenfolge Ziele an Clients verwiesen werden sollen und die verschiedenen Sortiermethoden für Zielverweise zu verstehen:

## <a name="to-set-the-ordering-method-for-targets-in-namespace-root-referrals"></a>So legen Sie Sortiermethoden für Ziele in Namespacestamm-Verweisen fest

Verwenden Sie das folgende Verfahren, um die Sortiermethode für den Namespacestamm festzulegen:

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Namespace, und klicken Sie anschließend auf **Eigenschaften**.

3.  Wählen Sie eine Sortiermethode auf der Registerkarte **Verweise**.

> [!NOTE]
> Um Windows PowerShell für die Sortiermethode für Ziele in Namespacestammverweisen festzulegen, verwenden Sie das Cmdlet [Set-DfsnRoot](https://technet.microsoft.com/library/jj884281.aspx) mit einem der folgenden Parameter:
>    -   **EnableSiteCosting** gibt die Methode für die **kostengünstigste Reihenfolge** an
>    -   **EnableInsiteReferrals** gibt die Sortiermethode für **Ziele außerhalb des Standorts des Clients ausschließen**
>    -   Das Auslassen beider Parameter legt die **zufällige Reihenfolge** der Sortiermethode fest. 

Das DFSN-Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.
   
## <a name="to-set-the-ordering-method-for-targets-in-folder-referrals"></a>So legen Sie die Sortiermethode für Ziele in Ordnerverweisen fest

Ordner mit Zielen erben die Sortiermethode des Namespacestamms. Sie können die Sortiermethode mit dem folgenden Verfahren überschreiben:

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Ordner mit Zielen, und klicken Sie anschließend auf **Eigenschaften**.

3.  Wählen Sie auf der Registerkarte **Verweise** das Kontrollkästchen **Ziele außerhalb des Standorts des Clients ausschließen**.

> [!NOTE]
> Um Ordnerziele, die Ziele außerhalb des Standorts des Clients ausschließen, mit Windows PowerShell zu verwenden, verwenden Sie das Cmdlet [Set-DfsnFolder – EnableInsiteReferrals](https://technet.microsoft.com/library/jj884283.aspx).

## <a name="target-referral-ordering-methods"></a>Sortiermethoden für Zielverweise

Diese drei Sortiermethoden sind:

-   Zufällige Reihenfolge
-   Niedrigste Kosten
-   Ausschließen von Zielen außerhalb des Standorts des Clients

## <a name="random-order"></a>Zufällige Reihenfolge

Bei dieser Methode werden Ziele wie folgt sortiert:

1.  Ziele, die sich auf derselben Active Directory Verzeichnisdienste-Website (AD DS) wie der Client befinden, werden in zufälliger Reihenfolge am Anfang des Verweises aufgeführt.
2.  Ziele außerhalb des Standorts des Clients werden in zufälliger Reihenfolge aufgelistet.

Wenn keine Zielserver mit demselben Standort verfügbar sind, wird der Clientcomputer einem zufälligen Zielserver zugeordnet, unabhängig davon, wie teuer die Verbindung ist oder wie weit davon entfernt das Ziel ist.

## <a name="lowest-cost"></a>Niedrigste Kosten

Bei dieser Methode werden Ziele wie folgt sortiert:

1.  Ziele am selben Standort wie der Client werden in zufälliger Reihenfolge am oberen Rand der Verweise aufgelistet.
2.  Ziele außerhalb des Standorts des Clients werden in der Reihenfolge der niedrigste Kosten zu den höchsten Kosten aufgelistet. Verweise mit gleichen Kosten werden gruppiert zusammengefasst, und die Ziele werden in zufälliger Reihenfolge in jeder Gruppe aufgeführt.

> [!NOTE]
> Standortverknüpfungskosten werden nicht im DFS-Verwaltungs-Snap-In angezeigt. Um die Standortverknüpfungskosten zu sehen, verwenden Sie „Active Directory-Standorte und -Dienste“.

## <a name="exclude-targets-outside-of-the-clients-site"></a>Ausschließen von Zielen außerhalb des Standorts des Clients

Bei dieser Methode enthalten Die Verweise nur die Ziele, die am selben Standort wie der Client sind. Diese Ziele mit gleichem Standort werden in zufälliger Reihenfolge aufgelistet. Wenn keine Ziele mit gleichem Standort vorhanden sind, empfängt der Client keinen Verweis und kann nicht auf den Teil des Namespace zugreifen.

> [!NOTE]
> Ziele, deren Zielpriorität auf "Das erste von allen Zielen" oder "Das letzte von allen Zielen" festgelegt ist, werden weiterhin im Verweis aufgelistet, auch wenn die Sortiermethode als **Ziele außerhalb des Standorts des Clients ausschließen** festgelegt ist.

## <a name="see-also"></a>Siehe auch 

-   [Optimieren von DFS-Namespaces](tuning-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)