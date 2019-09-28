---
title: 'Prüfliste: Bereitstellen von DFS-Namespaces'
description: In diesem Artikel wird beschrieben, wie Sie DFS-Namespaces konfigurieren und bereitstellen.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: ab38c41c32ec88285a69fb94e62abc1453ddc3d1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402275"
---
# <a name="checklist-deploy-dfs-namespaces"></a>Prüfliste: Bereitstellen von DFS-Namespaces

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Verteiltes Dateisystem (DFS)-Namespaces und-DFS-Replikation können zum Veröffentlichen von Dokumenten, Software und Geschäftsdaten für Benutzer in einer Organisation verwendet werden. Obwohl DFS-Replikation allein ausreichend ist, um Daten zu verteilen, können Sie DFS-Namespaces verwenden, um den Namespace so zu konfigurieren, dass ein Ordner von mehreren Servern gehostet wird, von denen jeder eine aktualisierte Kopie des Ordners enthält. Dies erhöht die Verfügbarkeit der Daten und verteilt die Clientlast auf den Servern.

Wenn ein Ordner im Namespace durchsucht wird, sind sich Benutzer nicht bewusst, dass der Ordner von mehreren Servern gehostet wird. Wenn ein Benutzer den Ordner öffnet, wird der Clientcomputer automatisch auf einen Server auf dem Standort geleitet. Wenn keine Server mit demselben Standort verfügbar sind, können Sie den-Namespace so konfigurieren, dass der Client auf einen Server verweist, der über die niedrigsten Verbindungskosten verfügt, wie in Active Directory Directory Services (AD DS) definiert.

Führen Sie folgende Aufgaben aus, um DFS-Namespaces bereitzustellen:

-   Überprüfen Sie die grundlegenden Konzepte und Anforderungen des DFS-Namespaces.
[Übersicht über DFS-Namespaces](dfs-overview.md)
-   [Wählen Sie einen Namespace aus.](choose-a-namespace-type.md)
-   [Erstellen eines DFS-Namespace](create-a-dfs-namespace.md) 
-   Migrieren Sie vorhandene domänenbasierte Namespaces zu Windows Server 2008-Modus domänenbasierte Namespaces. [Migrieren eines domänenbasierten Namespace zum Windows Server 2008-Modus](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md) 
-   Verbessern Sie die Verfügbarkeit durch das Hinzufügen von Namespaceservern zu einem domänenbasierten Namespace. [Hinzufügen von Namespaceservern zu einem domänenbasierten DFS-Namespace](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   Hinzufügen von Ordnern zu Namespaces. [Erstellen eines Ordners in einem DFS-Namespace](create-a-folder-in-a-dfs-namespace.md)
-   Hinzufügen von Ordnerzielen in einem Namespace. [Hinzufügen von Ordnerzielen](add-folder-targets.md)
-   Replizieren von Inhalten zwischen Ordnerzielen mit der DFS-Replikation (optional). [Replizieren von Ordner Zielen mithilfe von DFS-Replikation](replicate-folder-targets-using-dfs-replication.md)


## <a name="see-also"></a>Siehe auch

-   [Namespaces](https://technet.microsoft.com/library/cc771914(v=ws.11).aspx)
-   [Prüfliste: Optimieren eines DFS-Namespaces](checklist-tune-a-dfs-namespace.md)
-   [Reproduktions](https://technet.microsoft.com/library/cc770278(v=ws.11).aspx)


