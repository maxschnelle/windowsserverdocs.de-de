---
title: Installieren Sie | Upgrade | Migrieren Sie zu WindowsServer 2019
description: Gewusst wie Neuinstallation, direkte Aktualisierung oder Migration zu Windows Server-2019.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a4e99cca754
author: coreyp-at-msft
ms.author: coreyp
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: 1fd955a640832eb161666f74b93d91bb2c3eff11
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66810819"
---
# <a name="install--upgrade--migrate-to-windows-server-2019"></a>Installieren Sie | Upgrade | Migrieren Sie zu WindowsServer 2019

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

> [!IMPORTANT]
> Der erweiterte Support für Windows Server 2008 R2 und Windows Server 2008 endet im Januar 2020. [Erfahren Sie mehr über die Optionen für die Aktualisierung](http://aka.ms/upgradecenter).

Ist es Zeit für ein Upgrade auf eine neuere Version von Windows Server? Je nachdem, welche Option Sie derzeit ausführen, haben Sie verschiedene Möglichkeiten.

## <a name="clean-install"></a>Bereinigen der Installation
Wenn Sie von einer älteren Version von Windows Server, Windows Server-2019 auf derselben Hardware verschieben möchten, gehen Sie so eine **Neuinstallation**, wobei Sie nur die neuere Betriebssystem direkt über den alten Listener auf derselben Hardware, installieren Daher wird das vorherige Betriebssystem gelöscht. Dies ist die einfachste Möglichkeit, aber Sie müssen zunächst Ihre Daten sichern und die erneute Installation Ihrer Apps planen. Es gibt einige Punkte zu beachten Sie, wie z. B. Systemanforderungen, daher sollten Sie unbedingt die Details für [Windows Server-2019](https://go.microsoft.com/fwlink/?linkid=2006124), [Windows Server 2016](https://go.microsoft.com/fwlink/?LinkID=825558), [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418) , und [unter WindowsServer 2012](https://technet.microsoft.com/library/jj134246.aspx).

## <a name="in-place-upgrade"></a>Direktes Upgrade

Wenn Sie dieselbe Hardware und alle Serverrollen, die Sie ohne vereinfachen den Server eingerichtet haben beibehalten möchten, sollten Sie Sie ein **In-Place-Aktualisierung**, von dem man von einem älteren Betriebssystem zu einer neueren, halten Sie Ihre Einstellungen, Server Rollen und Daten intakt. Wenn Ihr Server mit Windows Server 2012 R2 ausgeführt wird, können Sie es beispielsweise auf Windows Server 2016 oder Windows Server-2019 aktualisieren. Nicht für alle älteren Betriebssysteme gibt es aber einen Pfad zu einem neueren Betriebssystem. Finden Sie im folgende Diagramm für die Upgrade-Pfade zur Verfügung:

![Windows Server für ein direktes Upgrade-Pfade-Diagramm](media/upgrade-paths.png)

Schrittweise Anweisungen zum Aktualisieren, finden Sie auf die [Windows Server-Upgrade-Center](http://aka.ms/upgradecenter):

[![Screenshot der Windows Server-Upgrade-Center](media/upgrade-center.png)](http://aka.ms/upgradecenter)

## <a name="cluster-os-rolling-upgrade"></a>Paralleles Upgrade für Clusterbetriebssysteme

Cluster OS Rolling Upgrade kann ein Administrator des Betriebssystems des Clusterknotens von Windows Server 2012 R2 und Windows Server 2016 zu aktualisieren, ohne Unterbrechung von Hyper-V oder Workloads des Dateiservers für horizontales Skalieren. Mit diesem Feature können Sie Ausfallzeiten vermeiden, die die Vereinbarungen zum Servicelevel (Service Level Agreements) beeinträchtigen könnten. Dieses neue Feature wird unter [Cluster operating system rolling upgrade (Paralleles Upgrade für Clusterbetriebssysteme)](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade) näher beschrieben.

## <a name="migration"></a>Migration

Windows Server-Migration ist, wenn Sie eine Rolle oder ein Feature gleichzeitig von einem Quellcomputer verschieben, die auf einem anderen Zielcomputer, auf denen Windows Server, die gleiche oder eine neuere Version ausgeführt wird, Windows Server ausgeführt wird. Zu diesem Zweck wird die Migration wie folgt definiert: Verschieben einer Rolle oder eines Features und der dazugehörigen Daten auf einen anderen Computer, ohne das Feature auf demselben Computer zu aktualisieren. 

## <a name="license-conversion"></a>Konvertieren der Lizenz
Bei manchen Betriebssystemversionen können Sie eine bestimmte Edition der Version in einem einzigen Schritt mit einem einfachen Befehl und dem entsprechenden Lizenzschlüssel in eine andere Edition der gleichen Version konvertieren. Dies wird als **Konvertieren der Lizenz** bezeichnet. Wenn auf Ihrem Server beispielsweise Windows Server 2016 Standard ausgeführt wird, können Sie die Lizenz in Windows Server 2016 Datacenter konvertieren. Denken Sie daran, dass während Sie in Server 2016 Standard in Server 2016 Datacenter Sie verschieben können Sie nicht zum Umkehren des Prozesses, und wechseln vom Rechenzentrum zum Standard. In einigen Versionen von Windows Server können Sie mit demselben Befehl und dem passenden Schlüssel auch frei zwischen OEM-, Volumenlizenz- und Verkaufsversionen konvertieren.


 
 
