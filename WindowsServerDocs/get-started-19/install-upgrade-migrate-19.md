---
title: 'Windows Server 2019: Installation, Upgrade oder Migration'
description: Informationen zu Neuinstallation, Direktupgrade oder Migration von Windows Server
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a4e99cca754
author: jasongerend
ms.author: jgerend
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: e10d4cff4b45d1c0d3b447c63104b97ded1cd0d5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360873"
---
# <a name="install-upgrade-or-migrate-to-windows-server"></a>Windows Server: Installation, Upgrade oder Migration

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

> [!IMPORTANT]
> Der erweiterte Support für Windows Server 2008 R2 und Windows Server 2008 endet im Januar 2020. Informationen zu den verfügbaren Upgradeoptionen findest du [hier](http://aka.ms/upgradecenter). Du kannst Windows Server 2019 auf der Seite mit den [Windows Server-Evaluierungsversionen](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) herunterladen.

Ist es Zeit für eine neuere Version von Windows Server? Je nachdem, was du momentan verwendest, gibt es verschiedene Möglichkeiten.

## <a name="clean-install"></a>Neuinstallation

Die einfachste Methode zum Installieren von Windows Server ist eine Neuinstallation – dabei führst du die Installation auf einem leeren Server aus oder überschreibst ein vorhandenes Betriebssystem. Das ist die einfachste Möglichkeit. Allerdings musst du zuerst deine Daten sichern und die erneute Installation deiner Anwendungen planen. Es gibt einige Dinge, die du beachten musst, z.B. die Systemanforderungen. Sieh dir daher die Details zu [Windows Server 2019](https://go.microsoft.com/fwlink/?linkid=2006124), [Windows Server 2016](https://go.microsoft.com/fwlink/?LinkID=825558), [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418) und [Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx) an.

## <a name="in-place-upgrade"></a>Direkte Upgrades

Wenn du die Hardware und alle eingerichteten Serverrollen behalten möchtest, solltest du ein **direktes Upgrade** durchführen. Dabei wechselst du von einem älteren Betriebssystem zu einem neueren und behältst Einstellungen, Serverrollen und Daten bei. Wenn auf einem Server beispielsweise Windows Server 2012 R2 ausgeführt wird, kannst du ein Upgrade auf Windows Server 2016 oder Windows Server 2019 durchführen. Es gibt aber nicht für alle ältere Betriebssysteme einen Pfad zu einem neueren Betriebssystem. 

In der [Übersicht über Windows Server-Upgrades](../upgrade/upgrade-overview.md) findest du eine schrittweise Anleitung zum Upgraden.

## <a name="cluster-os-rolling-upgrade"></a>Paralleles Upgrade für Clusterbetriebssysteme

Das parallele Upgrade für Clusterbetriebssysteme ermöglicht es einem Administrator, ein Upgrade des Betriebssystems des Clusterknotens von Windows Server 2012 R2 und Windows Server 2016 ohne Unterbrechung von Hyper-V-Workloads oder Workloads des Scale-Out-Dateiservers durchzuführen. Mit diesem Feature können Sie Ausfallzeiten vermeiden, die die Vereinbarungen zum Servicelevel (Service Level Agreements) beeinträchtigen könnten. Dieses neue Feature wird unter [Cluster operating system rolling upgrade (Paralleles Upgrade für Clusterbetriebssysteme)](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade) näher beschrieben.

## <a name="migration"></a>Migration

Eine Windows Server-Migration findet statt, wenn du einzelne Rollen oder Features nacheinander von einem Quellcomputer unter Windows Server auf einen anderen Zielcomputer unter Windows Server (gleiche oder neuere Version) verlagerst. Zu diesem Zweck wird die Migration wie folgt definiert: Verschieben einer Rolle oder eines Features und der zugehörigen Daten auf einen anderen Computer, kein Upgrade des Features oder der Rolle auf dem gleichen Computer. 

## <a name="license-conversion"></a>Lizenzkonvertierung

Bei manchen Betriebssystemreleases kannst du eine bestimmte Edition des Releases in nur einem Schritt mit einem einfachen Befehl und dem entsprechenden Lizenzschlüssel in eine andere Edition des gleichen Releases konvertieren. Dies wird als **Lizenzkonvertierung** bezeichnet. Wenn auf deinem Server beispielsweise Windows Server 2016 Standard ausgeführt wird, kannst du die Lizenz in Windows Server 2016 Datacenter konvertieren. Du kannst zwar ein Upgrade von Server 2016 Standard auf Server 2016 Datacenter durchführen, aber den Prozess nicht umkehren und von Datacenter zu Standard wechseln. Bei einigen Releases von Windows Server kannst du mit dem gleichen Befehl und dem passenden Schlüssel auch frei zwischen OEM-, Volumenlizenz- und Verkaufsversionen wechseln.