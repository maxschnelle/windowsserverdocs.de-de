---
title: 'Prüfliste: Bereitstellen von DFS-Namespaces'
description: In diesem Artikel wird beschrieben, wie Sie DFS-Namespaces konfigurieren und bereitstellen.
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 7f7cca6b67ff6fa8d81e88323381866315f07f33
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842121"
---
# <a name="checklist-deploy-dfs-namespaces"></a>Prüfliste: Bereitstellen von DFS-Namespaces

> Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer 2008

Distributed File System (DFS)-Namespaces und DFS-Replikation kann verwendet werden, Dokumente, Software und LOB-Daten für Benutzer in der gesamten Organisation veröffentlichen. Obwohl DFS-Replikation allein ausreichend, um Daten zu verteilen ist, können Sie die DFS-Namespaces verwenden, den Namespace so konfigurieren, dass ein Ordner von mehreren Servern gehostet wird, von denen jede eine aktualisierte Kopie des Ordners enthält. Dies erhöht die Verfügbarkeit der Daten und verteilt die Clientlast auf den Servern.

Wenn ein Ordner im Namespace durchsucht wird, sind sich Benutzer nicht bewusst, dass der Ordner von mehreren Servern gehostet wird. Wenn ein Benutzer den Ordner öffnet, wird der Clientcomputer automatisch auf einen Server auf dem Standort geleitet. Wenn keine Server am gleichen Standort verfügbar sind, können Sie konfigurieren den Namespace, um den Client auf einem Server zu verweisen, die den niedrigsten Verbindungskosten, wie in den Active Directory Directory Services (AD DS) definiert ist.

Führen Sie folgende Aufgaben aus, um DFS-Namespaces bereitzustellen:

-   Überprüfen Sie die grundlegenden Konzepte und Anforderungen des DFS-Namespaces.
[Übersicht über DFS-Namespaces](dfs-overview.md)
-   [Wählen Sie einen Namespacetyp](choose-a-namespace-type.md)
-   [Erstellen Sie einen DFS-namespace](create-a-dfs-namespace.md) 
-   Migrieren Sie vorhandene domänenbasierte Namespaces zu Windows Server 2008-Modus domänenbasierte Namespaces. [Migrieren Sie einen domänenbasierten Namespace zu Windows Server 2008-Modus](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md) 
-   Verbessern Sie die Verfügbarkeit durch das Hinzufügen von Namespaceservern zu einem domänenbasierten Namespace. [Hinzufügen von Namespace-Servern zu einem domänenbasierten DFS-Namespace](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   Hinzufügen von Ordnern zu Namespaces. [Erstellen Sie einen Ordner in einem DFS-Namespace](create-a-folder-in-a-dfs-namespace.md)
-   Hinzufügen von Ordnerzielen in einem Namespace. [Hinzufügen von Ordnerzielen](add-folder-targets.md)
-   Replizieren von Inhalten zwischen Ordnerzielen mit der DFS-Replikation (optional). [Replizieren Sie die Ordnerziele des DFS-Replikation verwenden](replicate-folder-targets-using-dfs-replication.md)


## <a name="see-also"></a>Siehe auch

-   [Namespaces](https://technet.microsoft.com/library/cc771914(v=ws.11).aspx)
-   [Prüfliste: Optimieren Sie eine DFS-Namespace](checklist-tune-a-dfs-namespace.md)
-   [Replikation](https://technet.microsoft.com/library/cc770278(v=ws.11).aspx)


