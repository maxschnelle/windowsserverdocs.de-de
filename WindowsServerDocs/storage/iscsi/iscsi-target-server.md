---
title: iSCSI Target Server Overview
TOCTitle: iSCSI Target Server
ms.prod: windows-server-threshold
ms.technology: storage-iscsi
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: 14dd373b71c1be2f1a4ff157b9c631530532fc80
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837941"
---
# <a name="iscsi-target-server-overview"></a>Übersicht über die iSCSI-Zielserver

Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema enthält eine kurze Übersicht über iSCSI-Zielserver kann ein Rollendienst in Windows Server, Sie Speicher mithilfe des iSCSI-Protokolls zur Verfügung stellen können. Dies ist nützlich für die Bereitstellung von Zugriff auf den Speicher auf Ihrem Windows-Server für Clients, die nicht über die systemeigene Windows-Datei, die gemeinsame Nutzung von SMB-Protokoll kommunizieren.

Der iSCSI-Zielserver eignet sich ideal für folgende Aufgaben:

* **Netzwerk- und Start ohne Datenträger**   mit startfähigen Netzwerkadaptern oder eines softwareladeprogramms können Sie Hunderte von datenträgerlosen Servern bereitstellen können. Der iSCSI-Zielserver ermöglicht eine schnelle Bereitstellung. Bei internen Tests von Microsoft konnten auf diese Weise 256 Computer innerhalb von 34 Minuten bereitgestellt werden. Mithilfe differenzierender virtueller Festplatten können Sie bis zu 90 % des Speicherplatzes für die Betriebssystemabbilder sparen. Dies ist ideal für große Bereitstellungen identischer Betriebssystemabbilder, z. B. auf virtuellen Computern, auf denen Hyper-V ausgeführt wird, oder in High Performance Computing (HPC)-Clustern.

* **Serveranwendungsspeicher**   einige Anwendungen erfordern Blockspeicher. Der iSCSI-Zielserver kann diesen Anwendungen fortlaufend verfügbaren Blockspeicher zur Verfügung stellen. Da der Speicher remote zugänglich ist, kann Blockspeicher auch für zentrale Standorte oder Filialen konsolidiert werden.

* **Heterogener Speicher**   iSCSI-Zielserver unterstützt nicht von Microsoft stammende iSCSI-Initiatoren und vereinfacht das Freigeben von Speicher auf Servern in einer gemischten softwareumgebung.

* **Entwicklungs-, Test-, Demo und Lab-Umgebungen**   beim iSCSI-Zielserver aktiviert ist, wird ein Computer, auf denen das Betriebssystem Windows Server zu einem Netzwerk zugänglichen Blockspeichergerät. Dies ist hilfreich, um Anwendungen zu testen, bevor sie in einem SAN (Storage Area Network) bereitgestellt werden.

## <a name="block-storage-requirements"></a>Blockspeicheranforderungen

Wenn Sie mit dem iSCSI-Zielserver Blockspeicher bereitstellen, können Sie Ihr vorhandenes Ethernet-Netzwerk nutzen. Es ist keine zusätzliche Hardware erforderlich. Falls hohe Verfügbarkeit ein wichtiges Kriterium ist, sollten Sie einen Hochverfügbarkeitscluster einrichten. Für einen Hochverfügbarkeitscluster benötigen Sie freigegebenen Speicher – entweder Hardware für Fibre Channel-Speicher oder ein SAS (Serial Attached SCSI)-Speicherarray.

Wenn Sie Gast-Clustering aktivieren, müssen Sie Blockspeicher bereitstellen. Alle Server, auf denen Windows Server-Software mit dem iSCSI-Zielserver ausgeführt wird, können Blockspeicher bereitstellen.

## <a name="see-also"></a>Siehe auch

[iSCSI-Zielblockspeicher: Vorgehensweise](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh848268(v%3dws.11))  
[Was ist neu im iSCSI-Zielserver unter Windows Server](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn305893(v%3dws.11))

