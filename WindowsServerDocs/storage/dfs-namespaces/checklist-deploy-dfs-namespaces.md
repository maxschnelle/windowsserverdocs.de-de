---
title: "Prüfliste: Bereitstellen von DFS-Namespaces"
description: In diesem Artikel wird beschrieben, wie Sie DFS-Namespaces konfigurieren und bereitstellen.
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 8f1dd7a8a44f5427d6464a6be2057a529638eca7
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="checklist-deploy-dfs-namespaces"></a>Prüfliste: Bereitstellen von DFS-Namespaces

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server2012 R2, Windows Server 2012, Windows Server2008 R2, Windows Server 2008

Distributed File System (DFS)-Namespaces und DFS-Replikation können zum Veröffentlichen von Dokumenten, Software und Branchen-Daten für Benutzer in der gesamten Organisation verwendet werden. Obwohl DFS-Replikation allein ausreicht, um Daten zu verteilen, können Sie DFS-Namespaces verwenden, um die Namespace so zu konfigurieren, dass ein Ordner von mehreren Servern gehostet wird, von denen jedes eine aktualisierte Kopie des Ordners enthält. Dies erhöht die Verfügbarkeit der Daten und verteilt die Clientlast auf den Servern.

Wenn ein Ordner im Namespace durchsucht wird, sind sich Benutzer nicht bewusst, dass der Ordner von mehreren Servern gehostet wird. Wenn ein Benutzer den Ordner öffnet, wird der Clientcomputer automatisch auf einen Server auf dem Standort geleitet. Wenn keine Server am gleichen Standort verfügbar sind, können Sie den Namespace konfigurieren, um den Client auf einen Server zu verweisen, der über die niedrigsten Verbindungskosten gemäß des Active Directory-Verzeichnisdienstes (AD DS) verfügt.

Führen Sie folgende Aufgaben aus, um DFS-Namespaces bereitzustellen:

-   Überprüfen Sie die grundlegenden Konzepte und Anforderungen des DFS-Namespaces.
[Übersicht über DFS-Namespaces](dfs-overview.md)
-   [Namespacetyp auswählen](choose-a-namespace-type.md)
-   [Erstellen eines DFS-Namespaces](create-a-dfs-namespace.md) 
-   Migrieren Sie vorhandene domänenbasierte Namespaces zu Windows Server2008-Modus domänenbasierte Namespaces. [Migrieren Sie einen domänenbasierten Namespace zum Windows Server2008-Modus](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md) 
-   Verbessern Sie die Verfügbarkeit durch das Hinzufügen von Namespaceservern zu einem domänenbasierten Namespace. [Hinzufügen von Namespaceserver zu einem domänenbasierten DFS-Namespace](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   Hinzufügen von Ordnern zu Namespaces. [Erstellen Sie einen Ordner in einem DFS-Namespace](create-a-folder-in-a-dfs-namespace.md)
-   Hinzufügen von Ordnerzielen in einem Namespace. [Hinzufügen von Ordnerzielen](add-folder-targets.md)
-   Replizieren von Inhalten zwischen Ordnerzielen mit der DFS-Replikation (optional). [Replizieren von Ordnerzielen mit DFS-Replikation](replicate-folder-targets-using-dfs-replication.md)


## <a name="see-also"></a>Weitere Informationen:

-   [Namespaces](https://technet.microsoft.com/library/cc771914(v=ws.11).aspx)
-   [Prüfliste: Optimieren eines DFS-Namespaces](checklist-tune-a-dfs-namespace.md)
-   [Replikation](https://technet.microsoft.com/library/cc770278(v=ws.11).aspx)


