---
title: Expressupdates für Windows Server 2016 für November 2018-Update reaktiviert
description: Enthält Informationen zu Expressupdates in Windows Server 2016
ms.topic: article
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.openlocfilehash: f6b5e90b2134e21bccb7ed3006037963a77b6338
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87941672"
---
# <a name="express-updates-for-windows-server-2016-re-enabled-for-november-2018-update"></a>Expressupdates für Windows Server 2016 für November 2018-Update reaktiviert

> Von Joel Frauenheim
>
> Gilt für: Windows Server 2016

Ab dem 13. November 2018 (Update-Dienstag) werden von Windows wieder Expressupdates für Windows Server 2016 veröffentlicht. Expressupdates für Windows Server 2016 wurden Mitte 2017 eingestellt, nachdem sie aufgrund eines erheblichen Problems nicht mehr ordnungsgemäß installiert wurden. Das Problem wurde zwar im November 2017 behoben, das Updateteam ist bei der Veröffentlichung der Expresspakete jedoch einem konservativen Ansatz gefolgt, um sicherzugehen, dass die meisten Kunden das Update vom 14. November 2017 ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) in ihrer Serverumgebung installiert haben und nicht mehr von dem Problem betroffen sind.

Systemadministratoren für WSUS und Configuration Manager werden im November 2018 wieder zwei Pakete für das Windows Server 2016-Update angezeigt: ein vollständiges Update und ein Expressupdate. Systemadministratoren, die in ihrer Serverumgebung die Expressoption verwenden möchten, müssen sich vergewissern, dass auf dem Gerät seit dem 14. November 2017 ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) ein vollständiges Update ausgeführt wurde, um sicherzustellen, dass das Expressupdate ordnungsgemäß installiert wird. Bei Geräten, die seit dem Update vom 14. November 2017 ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) nicht mehr aktualisiert wurden, treten beim Versuch, das Expressupdate anzuwenden, wiederholt Fehler auf, die Bandbreite und CPU-Ressourcen in einer Endlosschleife beanspruchen.  Zur Behebung dieses Problems muss der Systemadministrator das Pushen des Expressupdates beenden und ein aktuelles vollständiges Update pushen, um die Fehlerschleife zu beenden.

Mit dem Expressupdate vom 13. November 2018 verringert sich für Kunden unmittelbar die Paketgröße zwischen ihrem Verwaltungssystem und den Windows Server 2016-Endpunkten.