---
title: Festlegen der Sortiermethode für Ziele in Verweisen
description: In diesem Artikel wird beschrieben, wie die Bestellmethode für Ziele in verweisen festgelegt wird.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: a993d53611382dcd0007bfecae95da6221cf6016
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966802"
---
# <a name="set-the-ordering-method-for-targets-in-referrals"></a>Festlegen der Sortiermethode für Ziele in Verweisen

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Ein Verweis ist eine geordnete Liste von Zielen, die ein Client Computer von einem Domänen Controller oder einem Namespace Server empfängt, wenn der Benutzer auf einen Namespace Stamm oder-Ordner mit Zielen zugreift. Nachdem der Client den Verweis empfangen hat, versucht der Client, auf das erste Ziel in der Liste zuzugreifen. Wenn das Ziel nicht verfügbar ist, versucht der Client, auf das nächste Ziel zuzugreifen.
Ziele am Standort des Clients werden immer zuerst in einem Verweis aufgeführt. Ziele außerhalb des Client Standorts werden entsprechend der Bestellmethode aufgelistet.

Verwenden Sie die folgenden Abschnitte, um anzugeben, in welcher Reihenfolge die Ziele auf Clients verwiesen werden sollen, und um die verschiedenen Methoden zum Sortieren der Ziel Verweise zu verstehen:

## <a name="to-set-the-ordering-method-for-targets-in-namespace-root-referrals"></a>So legen Sie die Reihenfolge Methode für Ziele in Namespace-Stamm verweisen fest

Verwenden Sie das folgende Verfahren, um die Reihen folgen Methode für den Namespace Stamm festzulegen:

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Namespace, und klicken Sie anschließend auf **Eigenschaften**.

3.  Wählen Sie auf der Registerkarte **Verweise** eine Bestellmethode aus.

> [!NOTE]
> Verwenden Sie das Cmdlet [Set-dfsnroot](/powershell/module/dfsr/update-dfsrconfigurationfromad?view=win10-ps) mit einem der folgenden Parameter, um Windows PowerShell zum Festlegen der Anordnungs Methode für Ziele in Namespace-Stamm verweisen zu verwenden:
>    -   **Enablesitecost** gibt die **niedrigste Kosten Anordnungs** Methode an.
>    -   **Enableinsitereferrals** gibt die **Ausschluss Ziele außerhalb der Standort Anordnungs Methode des Clients an** .
>    -   Durch das Weglassen eines der beiden Parameter wird die Sortiermethode für die **zufällige Reihenfolge** der

Das DFSN-Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.

## <a name="to-set-the-ordering-method-for-targets-in-folder-referrals"></a>So legen Sie die Bestellmethode für Ziele in Ordner verweisen fest

Ordner mit Zielen erben die Bestellmethode vom Namespace Stamm. Mithilfe des folgenden Verfahrens können Sie die-Bestellmethode überschreiben:

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Ordner mit Zielen, und klicken Sie anschließend auf **Eigenschaften**.

3.  Aktivieren Sie auf der Registerkarte **Verweise** das Kontrollkästchen **Ziele außerhalb des Client Standorts ausschließen** .

> [!NOTE]
> Wenn Sie Windows PowerShell verwenden möchten, um Ordner Ziele außerhalb des Client Standorts auszuschließen, verwenden Sie das Cmdlet [Set-dfsnfolder – enableinsitereferrals](/powershell/module/dfsr/update-dfsrconfigurationfromad?view=win10-ps) .

## <a name="target-referral-ordering-methods"></a>Ziel Weiterleitungs Methoden für Verweise

Die drei Reihenfolge Methoden sind:

-   Zufällige Reihenfolge
-   Niedrigste Kosten
-   Ziele außerhalb des Client Standorts ausschließen

## <a name="random-order"></a>Zufällige Reihenfolge

In dieser Methode werden Ziele wie folgt angeordnet:

1.  Ziele, die sich auf derselben Active Directory Verzeichnisdienste-Website (AD DS) wie der Client befinden, werden in zufälliger Reihenfolge am Anfang des Verweises aufgeführt.
2.  Ziele, die sich außerhalb des Client Standorts befinden, werden in zufälliger Reihenfolge aufgelistet.

Wenn keine Zielserver auf demselben Standort verfügbar sind, wird der Client Computer auf einen zufälligen Zielserver verwiesen, unabhängig davon, wie teuer die Verbindung ist oder wie weit das Ziel liegt.

## <a name="lowest-cost"></a>Niedrigste Kosten

In dieser Methode werden Ziele wie folgt angeordnet:

1.  Ziele, die sich an demselben Standort wie der Client befinden, werden in zufälliger Reihenfolge am Anfang des Verweises aufgeführt.
2.  Ziele, die sich außerhalb des Client Standorts befinden, werden in der Reihenfolge der niedrigsten Kosten für die höchsten Kosten aufgeführt. Verweise mit denselben Kosten werden gruppiert, und die Ziele werden in zufälliger Reihenfolge in jeder Gruppe aufgeführt.

> [!NOTE]
> Die Kosten für die Standort Verknüpfung werden im DFS-Verwaltungs-Snap-in nicht angezeigt. Verwenden Sie das Snap-in "Active Directory Sites und Dienste", um die Standort Verknüpfungs Kosten anzuzeigen.

## <a name="exclude-targets-outside-of-the-clients-site"></a>Ziele außerhalb des Client Standorts ausschließen

Bei dieser Methode enthält der Verweis nur die Ziele, die sich an demselben Standort wie der Client befinden. Diese gleichen Site Ziele werden in zufälliger Reihenfolge aufgelistet. Wenn keine gleichen Standort Ziele vorhanden sind, erhält der Client keinen Verweis und kann nicht auf diesen Teil des Namespaces zugreifen.

> [!NOTE]
> Ziele, bei denen die Ziel Priorität auf "zuerst bei allen Zielen" oder "letzte für alle Ziele" festgelegt ist, werden weiterhin im Verweis aufgeführt, auch wenn die Bestellmethode auf das **Ausschließen von Zielen außerhalb des Client Standorts**festgelegt ist.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Optimieren von DFS-Namespaces](tuning-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)
