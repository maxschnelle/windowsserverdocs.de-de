---
title: Installieren Sie | Upgrade | Migrieren Sie zu WindowsServer 2019
description: So Daten-, direktes Upgrade oder Migration zu Windows Server 2019.
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
ms.openlocfilehash: 58c363fc0a1e336519bc6ec4276651345cc2b5eb
ms.sourcegitcommit: 07ac08dea2b8f2763c2614a999dc7967018aa0b4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2018
ms.locfileid: "6121389"
---
# Installieren Sie | Upgrade | Migrieren Sie zu WindowsServer 2019

>Gilt für: WindowsServer 2019, Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer 2008

> [!IMPORTANT]
> Der erweiterte Support für Windows Server2008 R2 und Windows Server2008 endet im Januar2020. [Erfahren Sie mehr über die Upgrade-Optionen](http://aka.ms/upgradecenter).

Ist es Zeit für ein Upgrade auf eine neuere Version von Windows Server? Je nachdem, welche Option Sie derzeit ausführen, haben Sie verschiedene Möglichkeiten.

## Neuinstallation
Wenn Sie von einer älteren Version von Windows Server auf Windows Server 2019 auf derselben Hardware verschieben möchten, sollten Sie eine **Neuinstallation**hierbei Sie das neuere Betriebssystem direkt über die alte auf derselben Hardware installieren, und löschen somit Durchführen der vorherige Betriebssystem. Dies ist die einfachste Möglichkeit, aber Sie müssen zunächst Ihre Daten sichern und die erneute Installation Ihrer Apps planen. Es gibt einige Dinge, die Sie beachten müssen, z. B. die Systemanforderungen so überprüfen Sie die Details für [Windows Server 2019](https://go.microsoft.com/fwlink/?linkid=2006124), [Windows Server 2016](https://go.microsoft.com/fwlink/?LinkID=825558), [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418)und [Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx).

## Direktes Upgrade
Wenn Sie die gleiche Hardware und alle Serverrollen, die Sie eingerichtet haben, ohne den Server Glätten zu halten möchten, sollten Sie ein **direktes Upgrade**durchführen, Sie von einem älteren Betriebssystem zu einem neueren und wechseln behalten Ihre Einstellungen, Serverrollen , und die Daten unverändert. Wenn Ihr Server Windows Server 2012 R2 ausgeführt wird, können Sie es beispielsweise Windows Server 2016 oder Windows Server 2019 aktualisieren. Nicht für alle älteren Betriebssysteme gibt es aber einen Pfad zu einem neueren Betriebssystem. Finden Sie im folgenden Diagramm für die verfügbaren Upgradepfade:

![Windows Server direktes Upgrade-Pfade Diagramm](media/upgrade-paths.png)

Schritt-Anleitung zum Aktualisieren von finden Sie im [Windows Server-Upgrade-Center](http://aka.ms/upgradecenter):

<a href="http://aka.ms/upgradecenter"><img src="media/upgrade-center.png" alt="Screenshot of Windows Upgrade Center" title="Windows Server-Upgrade-Center"></a>

## Paralleles Upgrade für Clusterbetriebssysteme
Cluster OS Rolling Upgrade ermöglicht einem Administrator, das upgrade des Betriebssystems des Clusterknotens von Windows Server 2012 R2 und Windows Server 2016 ohne eine Unterbrechung von Hyper-V oder Workloads des Dateiservers mit horizontaler Skalierung durchzuführen. Mit diesem Feature können Sie Ausfallzeiten vermeiden, die die Vereinbarungen zum Servicelevel (Service Level Agreements) beeinträchtigen könnten. Dieses neue Feature wird unter [Cluster operating system rolling upgrade (Paralleles Upgrade für Clusterbetriebssysteme)](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade) näher beschrieben.

## Migration

Windows Server-Migration ist, wenn Sie eine Rolle oder Feature zu einem Zeitpunkt von einem Quellcomputer verschieben, Windows Server auf einem anderen Zielcomputer ausgeführt wird, die die gleiche oder eine neuere Version Windows Server ausgeführt wird. Zu diesem Zweck wird die Migration wie folgt definiert: Verschieben einer Rolle oder eines Features und der dazugehörigen Daten auf einen anderen Computer, ohne das Feature auf demselben Computer zu aktualisieren. 

## Konvertieren der Lizenz
Bei manchen Betriebssystemversionen können Sie eine bestimmte Edition der Version in einem einzigen Schritt mit einem einfachen Befehl und dem entsprechenden Lizenzschlüssel in eine andere Edition der gleichen Version konvertieren. Dies wird als **Konvertieren der Lizenz** bezeichnet. Wenn auf Ihrem Server beispielsweise Windows Server 2016 Standard ausgeführt wird, können Sie die Lizenz in Windows Server 2016 Datacenter konvertieren. In einigen Versionen von Windows Server können Sie mit demselben Befehl und dem passenden Schlüssel auch frei zwischen OEM-, Volumenlizenz- und Verkaufsversionen konvertieren.


 
 
