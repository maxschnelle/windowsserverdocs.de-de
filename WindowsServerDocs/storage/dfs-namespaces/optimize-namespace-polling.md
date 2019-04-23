---
title: Optimieren der Namespaceabfrage
description: In diesem Artikel wird das Optimieren der Namespaceabfrage beschrieben, um auf allen Namespaceservern einen konsistenten domänenbasierten Namespace beizubehalten
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 995b01604b680746c4b0d6502b3b3968503d4210
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878271"
---
# <a name="optimize-namespace-polling"></a>Optimieren der Namespaceabfrage

> Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer 2008

Um auf allen Namespaceservern einen konsistenten domänenbasierten Namespace aufrecht zu erhalten, müssen Namespaceserver regelmäßig die Active Directory-Domänendienste (Active Directory Domain Services, AD DS) abfragen, um die aktuellen Namespacedaten abzurufen. 

## <a name="to-optimize-namespace-polling"></a>So optimieren Sie die Namespaceabfrage

Sie können die Ausführung dieser Namespaceabfrage wie im Folgenden beschrieben optimieren:

1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DFS-Verwaltung**.

2.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf einen domänenbasierten Namespace, und klicken Sie dann auf **Eigenschaften**.

3.  Wählen Sie auf der Registerkarte **Erweitert** aus, ob der Namespace für Konsistenz oder Skalierbarkeit optimiert werden soll.

    -   Wählen Sie **Für Konsistenz optimieren** aus, wenn 16 oder weniger Namespaceserver vorhanden sind, die den Namespace hosten.
    -   Wählen Sie **Für Skalierbarkeit optimieren** aus, wenn mehr als 16 Namespaceserver vorhanden sind. Dadurch wird die Last für den PDC-Emulator (primärer Domänencontroller) verringert, die zum Replizieren von Änderungen am Namespace zu allen Namespaceservern erforderliche Zeit wird aber erhöht. Bis Änderungen zu allen Servern repliziert werden, verfügen die Benutzer möglicherweise über eine uneinheitliche Ansicht des Namespaces.

> [!NOTE]
> Verwenden Sie zum Festlegen des Namespaceabfrage-Modus mithilfe von Windows PowerShell die [Set-DfsnRoot EnableRootScalability](https://technet.microsoft.com/library/jj884281.aspx) -Cmdlet, das in Windows Server 2012 eingeführt wurde.

## <a name="see-also"></a>Siehe auch

-   [Optimieren von DFS-Namespaces](tuning-dfs-namespaces.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)