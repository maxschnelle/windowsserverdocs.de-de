---
title: iSCSI Target Server Overview
TOCTitle: iSCSI Target Server
ms.prod: windows-server
ms.technology: storage-iscsi
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: 34515988c46b680701cc39b3948fcd53645741f4
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961352"
---
# <a name="iscsi-target-server-overview"></a>iSCSI-Ziel Server (Übersicht)

Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema enthält eine kurze Übersicht über den iSCSI-Ziel Server, einen Rollen Dienst in Windows Server, mit dem Sie Speicher über das iSCSI-Protokoll verfügbar machen können. Dies ist nützlich, um den Zugriff auf den Speicher auf dem Windows-Server für Clients bereitzustellen, die nicht über das Native Windows-Dateifreigabe Protokoll (SMB) kommunizieren können.

Der iSCSI-Zielserver eignet sich ideal für folgende Aufgaben:

* **Netzwerk-und Datenträger loser Start**     Mithilfe von Start fähigen Netzwerkadaptern oder einem Software Lade Programm können Sie Hunderte von Servern ohne Datenträger bereitstellen. Der iSCSI-Zielserver ermöglicht eine schnelle Bereitstellung. Bei internen Tests von Microsoft konnten auf diese Weise 256 Computer innerhalb von 34 Minuten bereitgestellt werden. Mithilfe differenzierender virtueller Festplatten können Sie bis zu 90 % des Speicherplatzes für die Betriebssystemabbilder sparen. Dies ist ideal für große Bereitstellungen identischer Betriebssystemabbilder, z. B. auf virtuellen Computern, auf denen Hyper-V ausgeführt wird, oder in High Performance Computing (HPC)-Clustern.

* **Server Anwendungs Speicher**     Einige Anwendungen erfordern Blockspeicher. Der iSCSI-Zielserver kann diesen Anwendungen fortlaufend verfügbaren Blockspeicher zur Verfügung stellen. Da der Speicher remote zugänglich ist, kann Blockspeicher auch für zentrale Standorte oder Filialen konsolidiert werden.

* **Heterogener Speicher**     der iSCSI-Ziel Server unterstützt nicht von Microsoft stammende iSCSI-Initiatoren und vereinfacht so das Freigeben von Speicher auf Servern in einer gemischten Softwareumgebung.

* **Entwicklungs-, Test-, Demonstrations-und Lab-Umgebungen**     Wenn der iSCSI-Ziel Server aktiviert ist, wird ein Computer, auf dem das Betriebssystem Windows Server ausgeführt wird, zu einem über das Netzwerk zugänglichen Block Speichergerät. Dies ist hilfreich, um Anwendungen zu testen, bevor sie in einem SAN (Storage Area Network) bereitgestellt werden.

## <a name="block-storage-requirements"></a>Blockspeicheranforderungen

Wenn Sie mit dem iSCSI-Zielserver Blockspeicher bereitstellen, können Sie Ihr vorhandenes Ethernet-Netzwerk nutzen. Es ist keine zusätzliche Hardware erforderlich. Falls hohe Verfügbarkeit ein wichtiges Kriterium ist, sollten Sie einen Hochverfügbarkeitscluster einrichten. Für einen Hochverfügbarkeitscluster benötigen Sie freigegebenen Speicher – entweder Hardware für Fibre Channel-Speicher oder ein SAS (Serial Attached SCSI)-Speicherarray.

Wenn Sie Gast-Clustering aktivieren, müssen Sie Blockspeicher bereitstellen. Alle Server, auf denen Windows Server-Software mit dem iSCSI-Zielserver ausgeführt wird, können Blockspeicher bereitstellen.

## <a name="see-also"></a>Weitere Informationen

[iSCSI-Zielblockspeicher: So wird's gemacht](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh848268(v%3dws.11))  
[Neues beim iSCSI-Zielserver unter Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn305893(v%3dws.11))
