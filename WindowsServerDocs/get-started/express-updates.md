---
title: Express-Updates für Windows Server 2016 Reaktivierung für November 2018 aktualisieren
description: Enthält Informationen zu Express-Updates in Windows Server 2016
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.openlocfilehash: 1644a61c87953e465895e23c3c8454bae7f3a056
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443384"
---
# <a name="express-updates-for-windows-server-2016-re-enabled-for-november-2018-update"></a>Express-Updates für Windows Server 2016 Reaktivierung für November 2018 aktualisieren

> By Joel Frauenheim
> 
> Gilt für: Windows Server 2016

Beginnend mit vom 13. November 2018 Update Dienstag "," Windows wird erneut veröffentlichen Express-Updates für Windows Server 2016. Express-Updates für Windows Server 2016 beendet in der Mitte 2017, nachdem ein wichtiges Problem, dass gefunden wurde, die die Updates beibehalten, korrekte Installation. Zwar das Problem im November 2017 behoben wurde, hat das Update-Team einen konservativen Ansatz veröffentlichen Sie die Express-Pakete, um sicherzustellen, dass die meisten Kunden müssten das 14. November 2017-Update ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) auf ihrem Server installiert Umgebungen und nicht von dem Problem betroffen.

Systemadministratoren für WSUS und System Center Configuration Manager (SCCM) müssen beachtet werden, dass im November 2018 sie zwei Pakete für das Windows Server 2016-Update erneut angezeigt werden: ein vollständiges Update und ein Express-Update. Systemadministratoren, die Express verwenden für ihre serverumgebungen müssen, um sicherzustellen, dass das Gerät ein vollständiges Update seit dem 14. November 2017 erstellt wurde ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) um sicherzustellen, dass das Express-Update ordnungsgemäß installiert wurde. Von Geräten, die nicht aktualisiert hat, seit dem 14. November 2017 aktualisieren ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) werden wiederholte Fehler, die von Bandbreite und CPU-Ressourcen in eine Endlosschleife zu nutzen, wenn, dass Sie das Express-Update versucht wird angezeigt.  Für den Systemadministrator, beenden Sie die Übertragung des Express-Updates, und drücken Sie eine aktuelle vollständige Aktualisierung zum Beenden der Schleife Fehler wäre die Wiederherstellung für diesen Zustand.

Kunden der Express-Update werden vom 13. November 2018 eine sofortige Verringerung der Paketgröße zwischen ihrem Managementsystem und die Windows Server 2016-Endpunkte angezeigt.  