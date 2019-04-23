---
title: 'Prüfliste: Optimieren eines DFS-Namespaces'
description: Dieser Artikel beschreibt, wie Sie die Behandlung von DFS-Namespaces für Verweise und Abfragen von AD DS für aktualisierte Namespacedaten optimieren
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 5e2d43f75a64a6a7950539c14386c6a037bc3c45
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872641"
---
# <a name="checklist-tune-a-dfs-namespace"></a>Prüfliste: Optimieren Sie einen DFS-namespace

> Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer 2008

Nach dem Erstellen eines Namespace und Hinzufügen von Ordnern und Ziele, verwenden die folgende Checkliste anpassen oder optimieren können, der DFS-Namespace behandelt Verweise auf und fragt Active Directory Domain Services (AD DS) auf aktualisierte.

-   Verhindern Sie, dass Benutzer Ordner in einem Namespace sehen, auf die sie keine Zugriffsberechtigung haben. [Aktivieren der zugriffsbasierten Aufzählung für einen Namespace](enable-access-based-enumeration-on-a-namespace.md) 
-   Erlauben Sie oder verhindern Sie, dass Benutzer beim Zugriff auf einen Ordner im Namespace zu einem Namespace oder Ordnerziel verwiesen werden. [Verweise und Clientfailback aktivieren oder deaktivieren](enable-or-disable-referrals-and-client-failback.md) 
-   Passen Sie den Zwischenspeicherungszeitraum bis zur Anforderung eines neuen Verweises durch die Clients an. [Ändern Sie die Zeitspanne, die Zwischenspeicherung von Weiterleitungen](change-the-amount-of-time-that-clients-cache-referrals.md)
-   Optimieren Sie, wie Namespaceserver AD DS zum Erhalt der aktuellen Namespacedaten abrufen. [Namespace-Abruf zu optimieren](optimize-namespace-polling.md)
-   Verwenden Sie geerbte Berechtigungen, um zu kontrollieren, welche Benutzer die Ordner in einem Namespace sehen können, für die eine zugriffsbasierte Aufzählung aktiviert sind. [Verwenden geerbte Berechtigungen mit der zugriffsbasierten Aufzählung](using-inherited-permissions-with-access-based-enumeration.md)

Darüber hinaus können mit einer DFS-Namespaces-Erweiterung, die Zielpriorität genannt, Sie die Priorität der Server angeben, ein bestimmten Server immer zuerst oder zuletzt in der Liste von Servern (als einen Verweis bezeichnet) platziert wird, dass der Client empfängt, wenn sie einen Ordner zugreift mit Zielen im Namespace.

-   Geben Sie an, in welcher Reihenfolge Benutzer an Ordnerziele verwiesen werden sollen. [Festlegen der Sortiermethode für Ziele in verweisen](set-the-ordering-method-for-targets-in-referrals.md)
-   Überschreiben Sie die Sortiermethode für Verweise für einen bestimmten Namespace oder ein Ordnerziel. [Festlegen der Zielpriorität Verweisreihenfolge überschreiben](set-target-priority-to-override-referral-ordering.md)

## <a name="see-also"></a>Siehe auch

-   [Namespaces](https://technet.microsoft.com/library/cc771914(v=ws.11).aspx)
-   [Prüfliste: Bereitstellen von DFS-Namespaces](checklist-deploy-dfs-namespaces.md)
-   [Optimieren von DFS-Namespaces](tuning-dfs-namespaces.md)


