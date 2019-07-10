---
title: Installation | Upgrade | Migration zu Windows Server 2019
description: Informationen zu Neuinstallation, direktem Upgrade oder Migration zu Windows Server 2019).
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
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "66810819"
---
# <a name="install--upgrade--migrate-to-windows-server-2019"></a>Installation | Upgrade | Migration zu Windows Server 2019

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

> [!IMPORTANT]
> Der erweiterte Support für Windows Server 2008 R2 und Windows Server 2008 endet im Januar 2020. Informationen zu den verfügbaren Upgradeoptionen findest du [hier](http://aka.ms/upgradecenter).

Ist es Zeit für eine neuere Version von Windows Server? Je nachdem, was du momentan verwendest, gibt es verschiedene Möglichkeiten.

## <a name="clean-install"></a>Neuinstallation
Wenn du von einer älteren Windows Server-Version zu Windows Server 2019 wechseln und die Hardware beibehalten möchtest, solltest du eine **Neuinstallation** durchführen. Hierbei installierst du das neuere Betriebssystem auf der gleichen Hardware direkt über das alte Betriebssystem und löschst somit das vorherige Betriebssystem. Das ist die einfachste Möglichkeit. Allerdings musst du zuerst deine Daten sichern und die erneute Installation deiner Anwendungen planen. Es gibt einige Dinge, die du beachten musst, z.B. die Systemanforderungen. Sieh dir daher die Details zu [Windows Server 2019](https://go.microsoft.com/fwlink/?linkid=2006124), [Windows Server 2016](https://go.microsoft.com/fwlink/?LinkID=825558), [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418) und [Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx) an.

## <a name="in-place-upgrade"></a>Direktes Upgrade

Wenn du die Hardware und alle eingerichteten Serverrollen behalten möchtest, solltest du ein **direktes Upgrade** durchführen. Dabei wechselst du von einem älteren Betriebssystem zu einem neueren und behältst Einstellungen, Serverrollen und Daten bei. Wenn auf einem Server beispielsweise Windows Server 2012 R2 ausgeführt wird, kannst du ein Upgrade auf Windows Server 2016 oder Windows Server 2019 durchführen. Es gibt aber nicht für alle ältere Betriebssysteme einen Pfad zu einem neueren Betriebssystem. Die verfügbaren Upgradepfade werden im folgenden Diagramm dargestellt:

![Diagramm: Pfade für direkte Upgrades von Windows Server](media/upgrade-paths.png)

Im [Windows Server Upgrade Center](http://aka.ms/upgradecenter) findest du eine Schrittanleitung zum Upgrade:

[![Screenshot von Windows Server Upgrade Center](media/upgrade-center.png)](http://aka.ms/upgradecenter)

## <a name="cluster-os-rolling-upgrade"></a>Paralleles Upgrade für Clusterbetriebssysteme

Das parallele Upgrade für Clusterbetriebssysteme ermöglicht es einem Administrator, ein Upgrade des Betriebssystems des Clusterknotens von Windows Server 2012 R2 und Windows Server 2016 ohne Unterbrechung von Hyper-V-Workloads oder Workloads des Scale-Out-Dateiservers durchzuführen. Mit diesem Feature können Sie Ausfallzeiten vermeiden, die die Vereinbarungen zum Servicelevel (Service Level Agreements) beeinträchtigen könnten. Dieses neue Feature wird unter [Cluster operating system rolling upgrade (Paralleles Upgrade für Clusterbetriebssysteme)](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade) näher beschrieben.

## <a name="migration"></a>Migration

Eine Windows Server-Migration findet statt, wenn du einzelne Rollen oder Features nacheinander von einem Quellcomputer unter Windows Server auf einen anderen Zielcomputer unter Windows Server (gleiche oder neuere Version) verlagerst. Zu diesem Zweck wird die Migration wie folgt definiert: Verschieben einer Rolle oder eines Features und der zugehörigen Daten auf einen anderen Computer, kein Upgrade des Features oder der Rolle auf dem gleichen Computer. 

## <a name="license-conversion"></a>Lizenzkonvertierung
Bei manchen Betriebssystemreleases kannst du eine bestimmte Edition des Releases in nur einem Schritt mit einem einfachen Befehl und dem entsprechenden Lizenzschlüssel in eine andere Edition des gleichen Releases konvertieren. Dies wird als **Lizenzkonvertierung** bezeichnet. Wenn auf deinem Server beispielsweise Windows Server 2016 Standard ausgeführt wird, kannst du die Lizenz in Windows Server 2016 Datacenter konvertieren. Du kannst zwar ein Upgrade von Server 2016 Standard auf Server 2016 Datacenter durchführen, aber den Prozess nicht umkehren und von Datacenter zu Standard wechseln. Bei einigen Releases von Windows Server kannst du mit dem gleichen Befehl und dem passenden Schlüssel auch frei zwischen OEM-, Volumenlizenz- und Verkaufsversionen wechseln.


 
 
