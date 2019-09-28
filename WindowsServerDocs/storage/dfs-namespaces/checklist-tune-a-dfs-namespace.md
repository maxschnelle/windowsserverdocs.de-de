---
title: 'Prüfliste: Optimieren eines DFS-Namespaces'
description: Dieser Artikel beschreibt, wie Sie die Behandlung von DFS-Namespaces für Verweise und Abfragen von AD DS für aktualisierte Namespacedaten optimieren
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 8a4c581801cbb1dcfe3db2813fb66fb4514d6434
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402184"
---
# <a name="checklist-tune-a-dfs-namespace"></a>Prüfliste: Optimieren eines DFS-Namespace

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Nachdem Sie einen Namespace erstellt und Ordner und Ziele hinzugefügt haben, verwenden Sie die folgende Prüfliste, um die Methode zu optimieren oder zu optimieren, in der der DFS-Namespace Verweise behandelt und Active Directory Domain Services (AD DS) nach aktualisierten Namespace Daten abruft.

-   Verhindern Sie, dass Benutzer Ordner in einem Namespace sehen, auf die sie keine Zugriffsberechtigung haben. [Aktivieren der Zugriffs basierten Enumeration für einen Namespace](enable-access-based-enumeration-on-a-namespace.md) 
-   Erlauben Sie oder verhindern Sie, dass Benutzer beim Zugriff auf einen Ordner im Namespace zu einem Namespace oder Ordnerziel verwiesen werden. [Aktivieren oder Deaktivieren von Verweisen und Clientfailbacks](enable-or-disable-referrals-and-client-failback.md) 
-   Passen Sie den Zwischenspeicherungszeitraum bis zur Anforderung eines neuen Verweises durch die Clients an. [Ändern der Zeitspanne, für die Clients Cache Verweise ausführen](change-the-amount-of-time-that-clients-cache-referrals.md)
-   Optimieren Sie, wie Namespaceserver AD DS zum Erhalt der aktuellen Namespacedaten abrufen. [Optimieren der Namespaceabfrage](optimize-namespace-polling.md)
-   Verwenden Sie geerbte Berechtigungen, um zu kontrollieren, welche Benutzer die Ordner in einem Namespace sehen können, für die eine zugriffsbasierte Aufzählung aktiviert sind. [Verwenden von geerbten Berechtigungen mit Zugriffs basierter Enumeration](using-inherited-permissions-with-access-based-enumeration.md)

Außerdem können Sie mithilfe einer Erweiterung für DFS-Namespaces, die als Ziel Priorität bezeichnet wird, die Priorität der Server angeben, sodass ein bestimmter Server immer zuerst in der Liste der Server (als Verweis bezeichnet) platziert wird, die der Client beim Zugriff auf einen Ordner empfängt. mit Zielen im-Namespace.

-   Geben Sie an, in welcher Reihenfolge Benutzer an Ordnerziele verwiesen werden sollen. [Festlegen der Sortiermethode für Ziele in Verweisen](set-the-ordering-method-for-targets-in-referrals.md)
-   Überschreiben Sie die Sortiermethode für Verweise für einen bestimmten Namespace oder ein Ordnerziel. [Festlegen der Zielpriorität zum Überschreiben der Sortiermethode von Verweisen](set-target-priority-to-override-referral-ordering.md)

## <a name="see-also"></a>Siehe auch

-   [Namespaces](https://technet.microsoft.com/library/cc771914(v=ws.11).aspx)
-   [Prüfliste: Bereitstellen von DFS-Namespaces](checklist-deploy-dfs-namespaces.md)
-   [Optimieren von DFS-Namespaces](tuning-dfs-namespaces.md)


