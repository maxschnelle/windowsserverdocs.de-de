---
title: Übersicht über Windows Server-Upgrades | Microsoft-Dokumentation
description: Allgemeine Informationen zu Windows Server zusammen mit einer Zusammenstellung der vor dem eigentlichen Upgrade zu berücksichtigenden Punkte.
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/10/2019
ms.openlocfilehash: 1aa923287c26aa75916a418b6550e2dec6bbb6cd
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939250"
---
# <a name="overview-of-windows-server-upgrades"></a>Übersicht über Windows Server-Upgrades

Abhängig vom Ausgangsbetriebssystem und der gewählten Methode kann die Vorgehensweise bei der Migration zu einer neueren Version von Windows Server stark variieren. Mithilfe der folgenden Begriffe wird zwischen verschiedenen Aktionen unterschieden, die alle eine Rolle in einer neuen Bereitstellung von Windows Server spielen können.

- **Upgrade.** Auch als „direktes Upgrade“ bezeichnet. Sie wechseln von einer älteren Version des Betriebssystems zu einer neueren Version und bleiben gleichzeitig auf derselben physischen Hardware. **Dies ist die Methode, die wir in diesem Abschnitt behandeln.**

    > [!Important]
    > Direkte Upgrades werden möglicherweise auch von privaten oder öffentlichen Cloudanbietern unterstützt, jedoch müssen Sie die Details mit Ihrem Cloudanbieter klären. Außerdem kann ein direktes Upgrade nicht für Windows Server-Instanzen ausgeführt werden, für die **Start über VHD** konfiguriert ist. Ein direktes Upgrade von Windows Storage Server-Editionen auf Windows Server 2019 wird nicht unterstützt. Stattdessen kannst du eine **Migration** oder **Installation** ausführen.

- **Installation.** Auch als „Neuinstallation“ bezeichnet. Sie wechseln von einer älteren Version des Betriebssystems zu einer neueren Version und löschen dabei das ältere Betriebssystem.

- **Migration.** Du wechselst von einer älteren Version des Betriebssystems zu einer neueren Version des Betriebssystems, indem du es auf einen anderen Hardwaresatz oder virtuelle Computer überträgst.

- **Paralleles Upgrade für Clusterbetriebssysteme.** Damit können Sie ein Upgrade des Betriebssystems der Clusterknoten vornehmen, ohne die Arbeitsauslastungen der Hyper-V- oder Scale-Out-Dateiserver zu unterbrechen. Mit diesem Feature können Sie Ausfallzeiten vermeiden, die die Vereinbarungen zum Servicelevel (Service Level Agreements) beeinträchtigen könnten. Weitere Informationen finden Sie unter [Cluster Operating System Rolling Upgrade (Paralleles Upgrade für Clusterbetriebssysteme)](../failover-clustering/cluster-operating-system-rolling-upgrade.md).

- **Lizenzkonvertierung.** Wandeln Sie eine bestimmte Edition des Releases in nur einem Schritt mit einem einfachen Befehl und dem entsprechenden Lizenzschlüssel in eine andere Edition des gleichen Releases um. Dies wird als „Konvertierung der Lizenz“ bezeichnet. Wenn auf deinem Server beispielsweise Windows Server 2016 Standard ausgeführt wird, kannst du die Lizenz in Windows Server 2016 Datacenter konvertieren.

## <a name="which-version-of-windows-server-should-i-upgrade-to"></a>Auf welche Version von Windows Server soll ich ein Upgrade ausführen?

Wir empfehlen, ein Upgrade auf die neueste Version von Windows Server vorzunehmen: Windows Server 2019. Das Ausführen der neuesten Version von Windows Server erlaubt es Ihnen, die neuesten Features zu verwenden – einschließlich der neuesten Sicherheitsfeatures – und bietet die beste Leistung.

Es ist uns jedoch bewusst, dass dies nicht immer möglich ist. Mithilfe des folgenden Diagramms können Sie herausfinden, auf welche Windows Server-Version Sie ein Upgrade ausführen können, ausgehend von der Version, mit der Sie aktuell arbeiten:

![Verfügbare direkte Aktualisierungspfade](media/upgrade-paths.png)

Windows Server kann normalerweise beim Upgrade mindestens eine Version überspringen, manchmal auch zwei. Beispielsweise kann sowohl für Windows Server 2012 R2 als auch für Windows Server 2016 ein direktes Upgrade auf Windows Server 2019 ausgeführt werden.

Außerdem können Sie von einer Evaluierungsversion des Betriebssystems auf eine Verkaufsversion, von einer älteren Verkaufsversion auf eine neuere Version oder in manchen Fällen von einer Volumenlizenzedition des Betriebssystems auf eine normale Verkaufsedition aktualisieren. Weitere Informationen zu anderen Upgradeoptionen als dem direkten Upgrade finden Sie unter [Upgrade- und Konvertierungsoptionen für Windows Server](../get-started/supported-upgrade-paths.md).
