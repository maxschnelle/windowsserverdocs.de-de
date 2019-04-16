---
title: "Prüfliste: Optimieren eines DFS-Namespaces"
description: "Dieser Artikel beschreibt, wie Sie die Behandlung von DFS-Namespaces für Verweise und Abfragen von AD DS für aktualisierte Namespacedaten optimieren"
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 827484c2ffcbb2617626129011a8b510473fe669
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="checklist-tune-a-dfs-namespace"></a>Prüfliste: Optimieren eines DFS-Namespaces

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server2012 R2, Windows Server 2012, Windows Server2008 R2, Windows Server 2008

Nach dem Erstellen eines Namespace und dem Hinzufügen von Ordnern und Zielen können Sie anhand der folgenden Prüfliste die Art und Weise optimieren oder anpassen, wie DFS-Namespace Verweise und Abfragen des Active Directory Domain Services (AD DS) für aktualisierte Namespacedaten aktualisiert.

-   Verhindern Sie, dass Benutzer Ordner in einem Namespace sehen, auf die sie keine Zugriffsberechtigung haben. [Aktivieren Sie die zugriffsbasierte Aufzählungen für einen Namespace](enable-access-based-enumeration-on-a-namespace.md) 
-   Erlauben Sie oder verhindern Sie, dass Benutzer beim Zugriff auf einen Ordner im Namespace zu einem Namespace oder Ordnerziel verwiesen werden. [Erlauben oder verhindern Sie von Verweise und Clientfailbacks](enable-or-disable-referrals-and-client-failback.md) 
-   Passen Sie den Zwischenspeicherungszeitraum bis zur Anforderung eines neuen Verweises durch die Clients an. [Ändern Sie den Zeitraum für die Zwischenspeicherung von Verweisen auf Clients](change-the-amount-of-time-that-clients-cache-referrals.md)
-   Optimieren Sie, wie Namespaceserver AD DS zum Erhalt der aktuellen Namespacedaten abrufen. [Optimieren Sie die Namespaceabfrage](optimize-namespace-polling.md)
-   Verwenden Sie geerbte Berechtigungen, um zu kontrollieren, welche Benutzer die Ordner in einem Namespace sehen können, für die eine zugriffsbasierte Aufzählung aktiviert sind. [Verwenden vererbter Berechtigungen mit zugriffsbasierter Aufzählung](using-inherited-permissions-with-access-based-enumeration.md)

Darüber hinaus können Sie mithilfe einer DFS-Namespaces-Erweiterung, die als Zielpriorität bezeichnet wird, die Priorität der Server festlegen, damit ein bestimmter Server immer zuerst oder zuletzt in der Liste der Server (eine sogenannte „Weiterleitung”) angezeigt wird, die der Client empfängt, wenn er auf einen Ordner mit Zielen im Namespace zugreift.

-   Geben Sie an, in welcher Reihenfolge Benutzer an Ordnerziele verwiesen werden sollen. [Legen Sie die Sortiermethode für Ziele in Verweisen fest](set-the-ordering-method-for-targets-in-referrals.md)
-   Überschreiben Sie die Sortiermethode für Verweise für einen bestimmten Namespace oder ein Ordnerziel. [Legen Sie die Zielpriorität zum Überschreiben der Sortiermethode von Verweisen fest](set-target-priority-to-override-referral-ordering.md)

## <a name="see-also"></a>Weitere Informationen:

-   [Namespaces](https://technet.microsoft.com/library/cc771914(v=ws.11).aspx)
-   [Prüfliste: Bereitstellen von DFS-Namespaces](checklist-deploy-dfs-namespaces.md)
-   [Optimieren von DFS-Namespaces](tuning-dfs-namespaces.md)


