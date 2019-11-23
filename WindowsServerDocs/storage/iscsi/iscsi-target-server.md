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
ms.openlocfilehash: 638343abf782983020a3301898920470ffcd5952
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403055"
---
# <a name="iscsi-target-server-overview"></a>iSCSI-Ziel Server (Übersicht)

Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema enthält eine kurze Übersicht über den iSCSI-Ziel Server, einen Rollen Dienst in Windows Server, mit dem Sie Speicher über das iSCSI-Protokoll verfügbar machen können. Dies ist nützlich, um den Zugriff auf den Speicher auf dem Windows-Server für Clients bereitzustellen, die nicht über das Native Windows-Dateifreigabe Protokoll (SMB) kommunizieren können.

Der iSCSI-Zielserver eignet sich ideal für folgende Aufgaben:

* **Netzwerk-und Datenträger lose Start**   mithilfe von Start fähigen Netzwerkadaptern oder einem Software Lade Programm können Sie Hunderte von Servern ohne Datenträger bereitstellen. Der iSCSI-Zielserver ermöglicht eine schnelle Bereitstellung. Bei internen Tests von Microsoft konnten auf diese Weise 256 Computer innerhalb von 34 Minuten bereitgestellt werden. Mithilfe differenzierender virtueller Festplatten können Sie bis zu 90 % des Speicherplatzes für die Betriebssystemabbilder sparen. Dies ist ideal für große Bereitstellungen identischer Betriebssystemabbilder, z. B. auf virtuellen Computern, auf denen Hyper-V ausgeführt wird, oder in High Performance Computing (HPC)-Clustern.

* **Server Anwendungs Speicher**   einige Anwendungen erfordern Blockspeicher. Der iSCSI-Zielserver kann diesen Anwendungen fortlaufend verfügbaren Blockspeicher zur Verfügung stellen. Da der Speicher remote zugänglich ist, kann Blockspeicher auch für zentrale Standorte oder Filialen konsolidiert werden.

* **Heterogener Speicher**   iSCSI-Ziel Server unterstützt iSCSI-Initiatoren, die nicht von Microsoft unterstützt werden, sodass das Freigeben von Speicher auf Servern in einer gemischten Softwareumgebung vereinfacht wird.

* **Entwicklungs-, Test-, Demonstrations-und Lab-Umgebungen**   wenn der iSCSI-Ziel Server aktiviert ist, wird ein Computer mit dem Windows Server-Betriebssystem zu einem über das Netzwerk zugänglichen Block Speichergerät. Dies ist hilfreich, um Anwendungen zu testen, bevor sie in einem SAN (Storage Area Network) bereitgestellt werden.

## <a name="block-storage-requirements"></a>Blockspeicheranforderungen

Wenn Sie mit dem iSCSI-Zielserver Blockspeicher bereitstellen, können Sie Ihr vorhandenes Ethernet-Netzwerk nutzen. Es ist keine zusätzliche Hardware erforderlich. Falls hohe Verfügbarkeit ein wichtiges Kriterium ist, sollten Sie einen Hochverfügbarkeitscluster einrichten. Für einen Hochverfügbarkeitscluster benötigen Sie freigegebenen Speicher – entweder Hardware für Fibre Channel-Speicher oder ein SAS (Serial Attached SCSI)-Speicherarray.

Wenn Sie Gast-Clustering aktivieren, müssen Sie Blockspeicher bereitstellen. Alle Server, auf denen Windows Server-Software mit dem iSCSI-Zielserver ausgeführt wird, können Blockspeicher bereitstellen.

## <a name="see-also"></a>Weitere Informationen

[iSCSI-Ziel Block Speicher, Vorgehensweise](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh848268(v%3dws.11))  
[Neues beim iSCSI-Zielserver unter Windows Server](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn305893(v%3dws.11))

