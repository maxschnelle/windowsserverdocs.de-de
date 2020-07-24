---
title: Ändern Sie den Zeitraum für die Zwischenspeicherung von Verweisen auf Clients
description: In diesem Artikel wird beschrieben, wie die Zeitspanne geändert wird, in der sich Clients im Cache befinden.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: ddbb799cc46da040bfc2f62445cc2b41945d09f1
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966292"
---
# <a name="change-the-amount-of-time-that-clients-cache-referrals"></a>Ändern der Zeitspanne, für die Clients Cache Verweise ausführen

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Ein Verweis ist eine sortierte Zielliste, die ein Client-PC von einem Domänencontroller oder Namespaceserver empfängt, wenn der Benutzer auf einen Namespacestamm oder -ordner mit Zielen im Namespace zugreift. Sie können anpassen, wie lange ein Verweis zwischen Clients zwischengespeichert werden soll, bevor Sie einen neuen anfordern.

## <a name="to-change-the-amount-of-time-that-clients-cache-namespace-root-referrals"></a>So ändern Sie die Dauer der Zwischenspeicherung von Namespacestammverweisen auf Clients

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Namespace, und klicken Sie anschließend auf **Eigenschaften**.

3.  Geben Sie auf der Registerkarte **Verweise** im Textfeld **Cachedauer (in Sekunden)** den Zeitraum (in Sekunden) ein, für den Namespacestammverweise von Clients zwischengespeichert werden sollen. Die Standardeinstellung beträgt 300 Sekunden (fünf Minuten).

> [!TIP]
> Verwenden Sie das Cmdlet [Set-dfsnroot timetolivesec](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753448(v=ws.11)) , um die Zeitspanne zu ändern, in der Clients Namespace-Stamm Verweise mithilfe von Windows PowerShell Zwischenspeichern. Diese Cmdlets wurden in Windows Server 2012 eingeführt.

## <a name="to-change-the-amount-of-time-that-clients-cache-folder-referrals"></a>So ändern Sie den Zeitraum für die Zwischenspeicherung von Ordnerverweisen auf Clients

1.  Klicken Sie auf **Start** , zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen Ordner mit Zielen, und klicken Sie anschließend auf **Eigenschaften**.

3.  Geben Sie auf der Registerkarte **Verweise** im Textfeld **Cachedauer (in Sekunden)** den Zeitraum (in Sekunden) ein, für den Ordnerverweise von Clients zwischengespeichert werden sollen. Die Standardeinstellung beträgt 1800 Sekunden (30 Minuten).

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Optimieren von DFS-Namespaces](tuning-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)
