---
title: Optimieren der Namespaceabfrage
description: In diesem Artikel wird beschrieben, wie Sie den Namespace Abruf optimieren, um einen konsistenten domänenbasierten Namespace auf den Namespace Servern beizubehalten.
ms.date: 6/5/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: cc14dd4f8d6cd833642b87caa32353d4f8940b05
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936135"
---
# <a name="optimize-namespace-polling"></a>Optimieren der Namespaceabfrage

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Um auf allen Namespaceservern einen konsistenten domänenbasierten Namespace aufrecht zu erhalten, müssen Namespaceserver regelmäßig die Active Directory-Domänendienste (Active Directory Domain Services, AD DS) abfragen, um die aktuellen Namespacedaten abzurufen.

## <a name="to-optimize-namespace-polling"></a>So optimieren Sie die Namespaceabfrage

Verwenden Sie das folgende Verfahren, um die Art der Namespace Abruf Optimierung zu optimieren:

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolen Struktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen domänenbasierten Namespace, und klicken Sie dann auf **Eigenschaften** .

3.  Wählen Sie auf der Registerkarte **erweitert** aus, ob der Namespace für Konsistenz oder Skalierbarkeit optimiert werden soll.

    -   Wählen Sie **für Konsistenz optimieren aus** , wenn 16 oder weniger Namespace Server vorhanden sind, auf denen der Namespace gehostet wird.
    -   Wählen Sie **für Skalierbarkeit optimieren aus** , wenn mehr als 16 Namespace Server vorhanden sind. Dadurch wird die Last auf dem PDC-Emulator (primärer Domänen Controller) reduziert, aber es wird die erforderliche Zeit für die Replikation von Änderungen am Namespace auf alle Namespace Server erhöht. Bis Änderungen zu allen Servern repliziert werden, verfügen die Benutzer möglicherweise über eine uneinheitliche Ansicht des Namespaces.

> [!NOTE]
> Verwenden Sie das Cmdlet [Set-dfsnroot enablerootscalability](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771913(v=ws.11)) , das in Windows Server 2012 eingeführt wurde, um den Namespace-Abruf Modus mithilfe von Windows PowerShell festzulegen.

## <a name="additional-references"></a>Weitere Verweise

-   [Optimieren von DFS-Namespaces](tuning-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)
