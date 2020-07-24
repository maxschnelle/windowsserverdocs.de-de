---
title: Prüfliste Bereitstellen von DFS-Namespaces
description: In diesem Artikel wird beschrieben, wie Sie DFS-Namespaces konfigurieren und bereitstellen.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 389d02ae7269ef48ef77d066db3064759d9253c1
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961962"
---
# <a name="checklist-deploy-dfs-namespaces"></a>Prüfliste: Bereitstellen von DFS-Namespaces

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Verteiltes Dateisystem (DFS)-Namespaces und-DFS-Replikation können zum Veröffentlichen von Dokumenten, Software und Geschäftsdaten für Benutzer in einer Organisation verwendet werden. Obwohl DFS-Replikation allein ausreichend ist, um Daten zu verteilen, können Sie DFS-Namespaces verwenden, um den Namespace so zu konfigurieren, dass ein Ordner von mehreren Servern gehostet wird, von denen jeder eine aktualisierte Kopie des Ordners enthält. Dadurch wird die Datenverfügbarkeit erhöht, und die Client Auslastung wird auf die Server verteilt.

Beim Durchsuchen eines Ordners im-Namespace wissen Benutzer nicht, dass der Ordner von mehreren Servern gehostet wird. Wenn ein Benutzer den Ordner öffnet, wird der Client Computer automatisch auf dem Standort eines Servers bezeichnet. Wenn keine Server mit demselben Standort verfügbar sind, können Sie den-Namespace so konfigurieren, dass der Client auf einen Server verweist, der über die niedrigsten Verbindungskosten verfügt, wie in Active Directory Directory Services (AD DS) definiert.

Führen Sie zum Bereitstellen von DFS-Namespaces die folgenden Aufgaben aus:

-   Überprüfen Sie die Konzepte und Anforderungen von DFS-Namespaces.
[Übersicht über DFS-Namespaces](dfs-overview.md)
-   [Wählen Sie einen Namespace aus.](choose-a-namespace-type.md)
-   [Erstellen eines DFS-Namespace](create-a-dfs-namespace.md)
-   Migrieren Sie vorhandene Domänen basierte Namespaces zu domänenbasierten Namespaces im Windows Server 2008-Modus. [Migrieren eines domänenbasierten Namespace zum Windows Server 2008-Modus](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)
-   Erhöhen Sie die Verfügbarkeit, indem Sie Namespace Server zu einem domänenbasierten Namespace hinzufügen. [Hinzufügen von Namespaceservern zu einem domänenbasierten DFS-Namespace](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   Fügen Sie einem Namespace Ordner hinzu. [Erstellen eines Ordners in einem DFS-Namespace](create-a-folder-in-a-dfs-namespace.md)
-   Fügen Sie Ordnern in einem Namespace Ordner Ziele hinzu. [Hinzufügen von Ordnerzielen](add-folder-targets.md)
-   Replizieren von Inhalten zwischen Ordner Zielen mithilfe von DFS-Replikation (optional). [Replizieren von Ordner Zielen mithilfe von DFS-Replikation](replicate-folder-targets-using-dfs-replication.md)


## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Namespaces](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771914(v=ws.11))
-   [Prüfliste: Optimieren eines DFS-Namespaces](checklist-tune-a-dfs-namespace.md)
-   [Replikation](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770278(v=ws.11))
