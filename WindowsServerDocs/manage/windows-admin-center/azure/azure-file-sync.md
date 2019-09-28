---
title: Synchronisieren Sie den Dateiserver mit der Cloud, indem Sie Azure-Dateisynchronisierung
description: Verwenden Sie Azure-Dateisynchronisierung, um die Dateifreigaben Ihrer Organisation in Azure zu zentralisieren und gleichzeitig die Flexibilität, Leistung und Kompatibilität eines lokalen Dateiservers zu erhalten. Azure-Dateisynchronisierung transformiert Windows Server in einen schnellen Cache Ihrer Azure-Dateifreigabe mit dem optionalen cloudtiering-Feature.
ms.technology: manage
ms.topic: article
author: fauhse
ms.author: fauhse
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: fe0e3337962b7d9c2f025a9d4eba826f3349c1f9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357384"
---
# <a name="sync-your-file-server-with-the-cloud-by-using-azure-file-sync"></a>Synchronisieren Sie den Dateiserver mit der Cloud, indem Sie Azure-Dateisynchronisierung

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Verwenden Sie Azure-Dateisynchronisierung, um die Dateifreigaben Ihrer Organisation in Azure zu zentralisieren und gleichzeitig die Flexibilität, Leistung und Kompatibilität eines lokalen Dateiservers zu erhalten. Azure-Dateisynchronisierung transformiert Windows Server in einen schnellen Cache Ihrer Azure-Dateifreigabe mit dem optionalen cloudtiering-Feature. Sie können ein beliebiges Protokoll verwenden, das unter Windows Server verfügbar ist, um lokal auf Ihre Daten zuzugreifen, einschließlich SMB, NFS und FTPS.

Nachdem Ihre Dateien mit der Cloud synchronisiert wurden, können Sie mehrere Server mit derselben Azure-Dateifreigabe verbinden, um die Inhalte lokal zu synchronisieren und zwischenzuspeichern – Berechtigungen (ACLs) werden stets ebenfalls übertragen. Azure Files bietet eine Momentaufnahme Funktion, mit der differenzielle Momentaufnahmen Ihrer Azure-Dateifreigabe generiert werden können. Diese Momentaufnahmen können sogar als schreibgeschützte Netzwerklaufwerke per SMB bereitgestellt werden, um das Durchsuchen und wiederherstellen zu vereinfachen. In Kombination mit cloudtiering war das Ausführen eines lokalen Dateiservers noch nie einfacher.

Weitere Informationen finden Sie unter [Planning for a Azure-Dateisynchronisierung Deployment](https://aka.ms/afs).