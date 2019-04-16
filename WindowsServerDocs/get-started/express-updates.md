---
title: Express-Updates für Windows Server 2016 für November 2018 erneut aktiviert, aktualisieren
description: Enthält Informationen zu Updates in Windows Server 2016 Express
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.openlocfilehash: c48979440ab7c5cfa86aa1287b354a1e43692f48
ms.sourcegitcommit: 23e0a68e21985d709e029e7771d3c52d6815bcb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2018
ms.locfileid: "6507851"
---
# Express-Updates für Windows Server 2016 für November 2018 erneut aktiviert, aktualisieren

>Durch Joel Frauenheim

>Gilt für: Windows Server2016

Beginnend mit dem November 13 2018 Update Dienstag, Windows wird erneut veröffentlichen Express-Updates für Windows Server 2016. Express-Updates für Windows Server 2016 beendet Mitte 2017, nachdem ein wichtiges Thema, dass gefunden wurde, die die Updates beibehalten, ordnungsgemäß installiert. Während das Problem im November 2017 behoben wurde, nahm das Update-Team einen konservativen Ansatz zum Veröffentlichen der Express-Pakete, um sicherzustellen, dass die meisten Kunden wäre die 14 November 2017-Update ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) auf ihrem Server-Umgebungen installiert haben und nicht durch das Problem beeinträchtigt.

Systemadministratoren für WSUS und System Center Configuration Manager (SCCM) müssen Sie beachten, dass im November 2018 sie zwei Pakete für die Windows Server 2016-Update erneut angezeigt werden: eine vollständige Aktualisierung und ein Express-Update. Systemadministratoren, die Express für ihre Server-Umgebung verwenden möchten, müssen zu bestätigen, dass das Gerät, eine vollständige Aktualisierung seit 14 November 2017 ([KB 4048953 ausgeführt](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) um sicherzustellen, dass die Express-Update ordnungsgemäß installiert. Jedes Gerät auf dem nicht aktualisiert wurde, nachdem das Update vom 14 November 2017 ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) angezeigt wird wiederholt Fehler, die Bandbreite und CPU-Ressourcen in einer Endlosschleife genutzt werden, wenn, die Express-Update versucht wird.  Wartung für diesen Zustand wäre für den Systemadministrator, beenden Sie die Express-Update weggeschoben und push inzwischen eine vollständige Aktualisierung die Fehler Schleife zu beenden.

Mit dem November 13 2018 sehen Express Update Kunden eine sofortige Reduzierung der Größe des Pakets zwischen ihrem Verwaltungssystem und die Windows Server 2016-Endpunkte.  