---
title: Aktualisieren von Windows Server 2008 und Windows Server 2008 R2
description: Windows Server 2008 und 2008 R2 werden demnächst eingestellt. Erfahren Sie, wie Sie diese lokal aktualisieren oder auf Azure erneut hosten können.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: mikeblodge
ms.author: mikeblodge
ms.date: 07/12/2018
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.localizationpriority: high
ms.openlocfilehash: 9d8a8cae62a9be3384c09009dbad52e06623adb0
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222910"
---
# <a name="upgrade-windows-server-2008-and-windows-server-2008-r2"></a>Aktualisieren von Windows Server 2008 und Windows Server 2008 R2

Der erweiterte Support für Windows Server 2008 und Windows Server 2008 R2 wird am 14. Januar 2020 beendet. Es gibt zwei modernisierungspfade verfügbar: Lokales Upgrade und Migration durch erneutes Hosten in Azure. **Wenn Sie in Azure hosten, können Sie Ihre vorhandenen Server-Images, die kostenlos migrieren.**

![Flussdiagramm zur Beschreibung der Aktualisierungspfade von Windows Server 2008](media/WS08_upgrade_paths.png)


## <a name="on-premises-upgrade"></a>Lokales Upgrade
Wenn Sie Ihre Server lokal halten müssen und Windows Server 2008 oder Windows Server 2008 R2 ausführen, müssen Sie [ein Upgrade auf Windows Server 2012/2012 R2](installation-and-upgrade.md#upgrading-to-windows-server-2012-r2) durchführen, bevor Sie [auf Windows Server 2016 aktualisieren](installation-and-upgrade.md#upgrading-to-windows-server-2016) können. Wenn Sie das Upgrade durchführen, haben Sie weiterhin die Möglichkeit der Migration auf Azure durch erneutes Hosten.

Weitere Informationen zu Ihren lokalen Upgrade-Optionen finden Sie unter [Ausführen eines Upgrades von Windows Server 2008 R2 oder Windows Server 2008](installation-and-upgrade.md#upgrading-from-windows-server-2008-r2-or-windows-server-2008).

Wenn Sie Windows Server 2003 ausführen, müssen Sie [auf Windows Server 2008 aktualisieren](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff972408(v%3dws.10)). Weitere Informationen zu Ihren lokalen Upgrade-Optionen finden Sie unter [Aktualisierungspfade für Windows Server 2008](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd979563(v=ws.10)).


## <a name="migrate-to-azure"></a>Migrieren zu Azure
Sie können Ihren lokalen Server mit Windows Server 2008 und Windows Server 2008 R2 zu Azure migrieren, wo sie auf virtuellen Computern weiterhin ausgeführt werden können. Auf Azure bleibt Ihre Konformität gewahrt, haben Sie mehr Sicherheit und können Ihre Arbeit mit Cloud-Innovationen ergänzen. Die Migration zu Azure bietet folgende Vorteile:

- Sicherheitsupdates in Azure.
- Erhalten Sie kritische und wichtige Sicherheitsupdates für Windows Server 2008 R2 oder 2008 für drei weitere Jahre, ohne dass hierfür zusätzliche Kosten anfallen. 
- Kostenlose Upgrades in Azure.
- Führen Sie je nach Ihrer Bereitschaft weitere Clouddienste ein.
- Indem Sie SQL Server zu verwalteten Azure-Instanzen oder VMs migrieren, erhalten Sie kritische Sicherheitsupdates für Windows Server 2008 R2 oder 2008 für drei weitere Jahre, ohne zusätzliche Kosten. 
- Nutzen Sie vorhandene SQL Server- und Windows Server-Lizenzen für Einsparungen durch die Cloud, die für Azure exklusiv sind.

[![Starten Sie die Migration zu Azure mit einem spezialisierten image](./media/WS08-image-banner-small.png)](uploading-specialized-WS08-image-to-azure.md)

Informationen zu den ersten Schritte beim Migrieren finden Sie unter [Hochladen von spezialisierten Windows Server 2008/2008 R2-Images in Azure](uploading-specialized-WS08-image-to-azure.md).

Informationen zum Analysieren von vorhandenen IT-Ressourcen, zum Auswerten von vorhandenem Material, zum Identifizieren der Vorteile einer Verlagerung spezifischer Dienste und Anwendungen in die Cloud oder des Beibehaltens von Workloads vor Ort und Aktualisierens auf die aktuelle Version von Windows Server finden Sie im [Migrationshandbuch für Windows Server](https://go.microsoft.com/fwlink/?linkid=872689).

## <a name="upgrade-sql-server-20082008-r2-in-parallel-with-your-windows-servers"></a>Aktualisieren von SQL Server 2008/2008 R2 parallel zu Ihren Windows-Servern

![SQL Server-Logo](media/sqlr2.jpg)

Wenn Sie SQL Server 2008/2008 R2 ausführen, können Sie auf SQL Server [2016](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation?view=sql-server-2016) oder [2017](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation?view=sql-server-2017) aktualisieren.


## <a name="additional-resources"></a>Zusätzliche Ressourcen
[Microsoft Azure](https://docs.microsoft.com/azure/#pivot=products)