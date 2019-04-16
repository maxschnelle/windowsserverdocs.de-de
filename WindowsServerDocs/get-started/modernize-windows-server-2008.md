---
title: Aktualisieren von Windows Server2008 und Windows Server2008 R2
description: Windows Server2008 und 2008R2 werden demnächst eingestellt. Erfahren Sie, wie Sie diese lokal aktualisieren oder auf Azure erneut hosten können.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: mikeblodge
ms.author: mikeblodge
ms.date: 07/12/2018
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.localizationpriority: high
ms.openlocfilehash: 4127eab613abb429a200f513a11b944e05da0f76
ms.sourcegitcommit: 9ed4c9fe04ebf3ef488170503c9a354c992b6fde
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/03/2018
ms.locfileid: "4339368"
---
# Aktualisieren von Windows Server2008 und Windows Server2008 R2

Der erweiterte Support für Windows Server2008 und Windows Server2008 R2 wird am 14.Januar2020 beendet. Es stehen zwei Modernisierungspfade zur Verfügung: lokale Aktualisierung oder Migration durch erneutes Hosten auf Azure. **Wenn Sie sich für das Rehosten auf Azure entscheiden, können Sie Ihre vorhandenen Server-Images kostenlos migrieren.**

![Flussdiagramm zur Beschreibung der Aktualisierungspfade von Windows Server2008](media/WS08_upgrade_paths.png)


## Lokales Upgrade
Wenn Sie Ihre Server lokal halten müssen und Windows Server2008 oder Windows Server2008 R2 ausführen, müssen Sie [ein Upgrade auf Windows Server2012/2012 R2](installation-and-upgrade.md#upgrading-to-windows-server-2012-r2) durchführen, bevor Sie [auf Windows Server2016 aktualisieren](installation-and-upgrade.md#upgrading-to-windows-server-2016) können. Wenn Sie das Upgrade durchführen, haben Sie weiterhin die Möglichkeit der Migration auf Azure durch erneutes Hosten.

Weitere Informationen zu Ihren lokalen Upgrade-Optionen finden Sie unter [Ausführen eines Upgrades von Windows Server2008 R2 oder Windows Server2008](installation-and-upgrade.md#upgrading-from-windows-server-2008-r2-or-windows-server-2008).

Wenn Sie Windows Server2003 ausführen, müssen Sie [auf Windows Server2008 aktualisieren](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff972408(v%3dws.10)). Weitere Informationen zu Ihren lokalen Upgrade-Optionen finden Sie unter [Aktualisierungspfade für Windows Server2008](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd979563(v=ws.10)).


## Migrieren zu Azure
Sie können Ihren lokalen Server mit Windows Server2008 und Windows Server2008 R2 zu Azure migrieren, wo sie auf virtuellen Computern weiterhin ausgeführt werden können. Auf Azure bleibt Ihre Konformität gewahrt, haben Sie mehr Sicherheit und können Ihre Arbeit mit Cloud-Innovationen ergänzen. Die Migration zu Azure bietet folgende Vorteile:

- Sicherheitsupdates in Azure.
- Erhalten Sie kritische und wichtige Sicherheitsupdates für Windows Server 2008 R2 oder 2008 für drei weitere Jahre, ohne dass hierfür zusätzliche Kosten anfallen. 
- Kostenlose Upgrades in Azure.
- Führen Sie je nach Ihrer Bereitschaft weitere Clouddienste ein.
- Indem Sie SQL Server zu verwalteten Azure-Instanzen oder VMs migrieren, erhalten Sie kritische Sicherheitsupdates für Windows Server2008 R2 oder 2008 für drei weitere Jahre, ohne zusätzliche Kosten. 
- Nutzen Sie vorhandene SQL Server- und Windows Server-Lizenzen für Einsparungen durch die Cloud, die für Azure exklusiv sind.

<a href="uploading-specialized-WS08-image-to-azure.md"><img src="media/WS08-image-banner-small.png"></a>

Informationen zu den ersten Schritte beim Migrieren finden Sie unter [Hochladen von spezialisierten Windows Server2008/2008 R2-Images in Azure](uploading-specialized-WS08-image-to-azure.md).

Informationen zum Analysieren von vorhandenen IT-Ressourcen, zum Auswerten von vorhandenem Material, zum Identifizieren der Vorteile einer Verlagerung spezifischer Dienste und Anwendungen in die Cloud oder des Beibehaltens von Workloads vor Ort und Aktualisierens auf die aktuelle Version von Windows Server finden Sie im [Migrationshandbuch für Windows Server](https://go.microsoft.com/fwlink/?linkid=872689).


## Aktualisieren von SQL Server2008/2008 R2 parallel zu Ihren Windows-Servern

![SQL Server-Logo](media/sqlr2.jpg)

Wenn Sie SQL Server2008/2008 R2 ausführen, können Sie auf SQL Server [2016](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation?view=sql-server-2016) oder [2017](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation?view=sql-server-2017) aktualisieren.


## Zusätzliche Ressourcen
[Microsoft Azure](https://docs.microsoft.com/azure/#pivot=products)