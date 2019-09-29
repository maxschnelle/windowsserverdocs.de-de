---
title: Optimieren von DFS-Namespaces
description: Dieser Artikel beschreibt, wie Sie DFS-Namespaces optimieren oder anpassen.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 011512deaeb99ded7d0bfc32a48f19ab3b622475
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386151"
---
# <a name="tuning-dfs-namespaces"></a>Optimieren von DFS-Namespaces

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Nachdem Sie einen Namespace erstellt und Ordner und Ziele hinzugefügt haben, lesen Sie die folgenden Abschnitte, um die Art und Weise zu optimieren oder zu optimieren, in der der DFS-Namespace Verweise behandelt und Active Directory Domain Services (AD DS) nach aktualisierten Namespace Daten abruft:

-   [Aktivieren der Zugriffs basierten Enumeration für einen Namespace](enable-access-based-enumeration-on-a-namespace.md)
-   [Aktivieren oder Deaktivieren von Verweisen und Clientfailbacks](enable-or-disable-referrals-and-client-failback.md)
-   [Ändern der Zeitspanne, für die Clients Cache Verweise ausführen](change-the-amount-of-time-that-clients-cache-referrals.md)
-   [Festlegen der Sortiermethode für Ziele in Verweisen](set-the-ordering-method-for-targets-in-referrals.md)
-   [Festlegen der Zielpriorität zum Überschreiben der Sortiermethode von Verweisen](set-target-priority-to-override-referral-ordering.md)
-   [Optimieren der Namespaceabfrage](optimize-namespace-polling.md)
-   [Verwenden von geerbten Berechtigungen mit Zugriffs basierter Enumeration](using-inherited-permissions-with-access-based-enumeration.md)

> [!NOTE]
> Um nach Ordnern oder Ordnerzielen zu suchen, wählen Sie einen Namespace, klicken Sie auf die Registerkarte **Suche**, geben Sie die Suchzeichenfolge in das Textfeld ein und klicken Sie dann auf **Suche**.