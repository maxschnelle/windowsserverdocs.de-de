---
title: Prüfliste optimieren eines DFS-Namespace
description: In diesem Artikel wird beschrieben, wie Sie optimieren, wie der DFS-Namespace Verweise behandelt und AD DS nach aktualisierten Namespace Daten abruft.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 67e272657c23926adbbf9f0db5174d00f4852137
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961752"
---
# <a name="checklist-tune-a-dfs-namespace"></a>Prüfliste: Optimieren eines DFS-Namespace

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Nachdem Sie einen Namespace erstellt und Ordner und Ziele hinzugefügt haben, verwenden Sie die folgende Prüfliste, um die Methode zu optimieren oder zu optimieren, in der der DFS-Namespace Verweise behandelt und Active Directory Domain Services (AD DS) nach aktualisierten Namespace Daten abruft.

-   Verhindern, dass Benutzerordner in einem Namespace sehen, für die Sie keine Zugriffsberechtigungen besitzen. [Aktivieren der Zugriffs basierten Enumeration für einen Namespace](enable-access-based-enumeration-on-a-namespace.md)
-   Aktivieren oder verhindern Sie, dass Benutzer auf einen Namespace oder ein Ordner Ziel verweisen, wenn Sie auf einen Ordner im-Namespace zugreifen. [Aktivieren oder Deaktivieren von Verweisen und Clientfailbacks](enable-or-disable-referrals-and-client-failback.md)
-   Passen Sie an, wie lange Clients einen Verweis zwischenspeichern, bevor Sie einen neuen anfordern. [Ändern der Zeitspanne, für die Clients Cache Verweise ausführen](change-the-amount-of-time-that-clients-cache-referrals.md)
-   Optimieren Sie, wie Namespace Server AD DS abrufen, um die aktuellsten Namespace Daten abzurufen. [Optimieren der Namespaceabfrage](optimize-namespace-polling.md)
-   Verwenden Sie geerbte Berechtigungen, um zu steuern, welche Benutzerordner in einem Namespace anzeigen können, für die die Zugriffs basierte Enumeration aktiviert ist. [Verwenden von geerbten Berechtigungen mit Zugriffs basierter Enumeration](using-inherited-permissions-with-access-based-enumeration.md)

Außerdem können Sie mithilfe einer Erweiterung für DFS-Namespaces, die als Ziel Priorität bezeichnet wird, die Priorität von Servern angeben, sodass ein bestimmter Server immer zuerst in der Liste der Server (als Verweis bezeichnet) platziert wird, die der Client empfängt, wenn er auf einen Ordner mit Zielen im-Namespace zugreift.

-   Geben Sie in der Reihenfolge an, in der die Benutzer auf Ordner Ziele verweisen möchten. [Festlegen der Sortiermethode für Ziele in Verweisen](set-the-ordering-method-for-targets-in-referrals.md)
-   Überschreiben der Verweis Reihenfolge für einen bestimmten Namespace Server oder ein bestimmtes Ordner Ziel. [Festlegen der Zielpriorität zum Überschreiben der Sortiermethode von Verweisen](set-target-priority-to-override-referral-ordering.md)

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Namespaces](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771914(v=ws.11))
-   [Prüfliste: Bereitstellen von DFS-Namespaces](checklist-deploy-dfs-namespaces.md)
-   [Optimieren von DFS-Namespaces](tuning-dfs-namespaces.md)
