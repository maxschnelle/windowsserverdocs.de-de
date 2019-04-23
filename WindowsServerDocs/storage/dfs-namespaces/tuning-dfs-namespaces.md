---
title: Optimieren von DFS-Namespaces
description: Dieser Artikel beschreibt, wie Sie DFS-Namespaces optimieren oder anpassen.
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: c11bbf65c3baebebe1e5143a5e694ca752500aca
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844631"
---
# <a name="tuning-dfs-namespaces"></a>Optimieren von DFS-Namespaces

> Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer 2008

Nach dem Erstellen eines Namespace und Hinzufügen von Ordnern und Ziele, finden Sie in den folgenden Abschnitten zu optimieren oder zu optimieren, wie Verweise von DFS-Namespace behandelt und fragt Active Directory Domain Services (AD DS) auf aktualisierte:

-   [Aktivieren der zugriffsbasierten Aufzählung für einen Namespace](enable-access-based-enumeration-on-a-namespace.md)
-   [Verweise und Clientfailback aktivieren oder deaktivieren](enable-or-disable-referrals-and-client-failback.md)
-   [Ändern Sie die Zeitspanne, die Zwischenspeicherung von Weiterleitungen](change-the-amount-of-time-that-clients-cache-referrals.md)
-   [Festlegen der Sortiermethode für Ziele in verweisen](set-the-ordering-method-for-targets-in-referrals.md)
-   [Festlegen der Zielpriorität Verweisreihenfolge überschreiben](set-target-priority-to-override-referral-ordering.md)
-   [Namespace-Abruf zu optimieren](optimize-namespace-polling.md)
-   [Verwenden geerbte Berechtigungen mit der zugriffsbasierten Aufzählung](using-inherited-permissions-with-access-based-enumeration.md)

> [!NOTE]
> Um nach Ordnern oder Ordnerzielen zu suchen, wählen Sie einen Namespace, klicken Sie auf die Registerkarte **Suche**, geben Sie die Suchzeichenfolge in das Textfeld ein und klicken Sie dann auf **Suche**.