---
title: Übersicht über Windows Server-Upgrades | Microsoft-Dokumentation
description: Informieren Sie sich über allgemeine Informationen zu Windows Server-Upgrades sowie über die Aspekte, die Sie vor dem eigentlichen Upgrade berücksichtigen sollten.
ms.prod: windows server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/10/2019
ms.openlocfilehash: 6f57e52657ca3c80c92d56c54ea87e43aabd1e99
ms.sourcegitcommit: 27f0caf74e88781054250455c3c1adf06deb6234
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/19/2019
ms.locfileid: "71124790"
---
# <a name="overview-about-windows-server-upgrades"></a>Übersicht über Windows Server-Upgrades

Der Upgradevorgang auf eine neuere Version von Windows Server kann stark variieren, je nachdem, mit welchem Betriebssystem Sie beginnen und welchen Weg Sie benötigen. Wir verwenden die folgenden Begriffe, um unterschiedliche Aktionen zu unterscheiden, von denen jede an einer neuen Windows Server-Bereitstellung beteiligt sein könnte.

- **Zuführen.** Wird auch als "direktes Upgrade" bezeichnet. Sie wechseln von einer älteren Version des Betriebssystems zu einer neueren Version und bleiben gleichzeitig auf derselben physischen Hardware. **Dies ist die Methode, die in diesem Abschnitt behandelt wird.**

    >[!Important]
    >Direkte Upgrades können auch von öffentlichen oder Private Cloud Unternehmen unterstützt werden. Sie müssen sich jedoch an Ihren cloudanbieter wenden, um die Details anzuzeigen. Außerdem ist es nicht möglich, auf einem Windows-Server, der für den **Start von**einer virtuellen Festplatte konfiguriert ist, ein direktes Upgrade durchzuführen.

- **Install.** Wird auch als "saubere Installation" bezeichnet. Sie wechseln von einer älteren Version des Betriebssystems zu einer neueren Version und löschen das ältere Betriebssystem.

- **Migration.** Sie wechseln von einer älteren Version des Betriebssystems zu einer neueren Version des Betriebssystems, indem Sie Sie auf einen anderen Satz von Hardware oder virtuellem Computer übertragen.

- **Paralleles Upgrade des Cluster Betriebssystems** Sie aktualisieren das Betriebssystem Ihrer Cluster Knoten, ohne die Hyper-V-oder die Dateiserver mit horizontaler Skalierung Arbeits Auslastungen zu beenden. Mit diesem Feature können Sie Ausfallzeiten vermeiden, die die Vereinbarungen zum Servicelevel (Service Level Agreements) beeinträchtigen könnten. Weitere Informationen finden Sie unter [Cluster Operating System Rolling Upgrade](../failover-clustering/cluster-operating-system-rolling-upgrade.md) .

- **Lizenz Konvertierung.** Konvertieren Sie eine bestimmte Edition der Version in einem einzigen Schritt mit einem einfachen Befehl und dem entsprechenden Lizenzschlüssel in eine andere Edition der gleichen Version. Dies wird als "Lizenz Konvertierung" bezeichnet. Wenn auf Ihrem Server beispielsweise Windows Server 2016 Standard ausgeführt wird, können Sie die Lizenz in Windows Server 2016 Datacenter konvertieren.

## <a name="which-version-of-windows-server-should-i-upgrade-to"></a>Für welche Version von Windows Server soll ein Upgrade auf ausgeführt werden?

Es wird empfohlen, ein Upgrade auf die neueste Version von Windows Server durchführen: Windows Server 2019. Wenn Sie die neueste Version von Windows Server ausführen, können Sie die neuesten Features – einschließlich der neuesten Sicherheitsfeatures – verwenden und die beste Leistung erzielen.

Wir wissen jedoch, dass dies nicht immer möglich ist. Mithilfe des folgenden Diagramms können Sie ermitteln, auf welche Windows Server-Version Sie ein Upgrade durchführen können, und zwar basierend auf der Version, auf der Sie sich gerade befinden:

![Verfügbare direkte Upgradepfade](media/upgrade-paths.png)

Windows Server kann in der Regel über mindestens eine und manchmal auch über zwei Versionen aktualisiert werden. Beispielsweise können Windows Server 2012 R2 und Windows Server 2016 direkt auf Windows Server 2019 aktualisiert werden.

Sie können auch ein Upgrade von einer Evaluierungsversion des Betriebssystems auf eine Verkaufsversion, von einer älteren Verkaufsversion auf eine neuere Version oder in manchen Fällen von einer Volumenlizenz Edition des Betriebssystems auf eine normale Verkaufs Edition durchführen. Weitere Informationen zu anderen Upgradeoptionen als ein direktes Upgrade finden Sie unter [upgraden und Konvertierungsoptionen für Windows Server](../get-started/supported-upgrade-paths.md).
