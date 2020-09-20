---
title: Synchronisierung des Dateiservers mit der Cloud per Azure-Dateisynchronisierung
description: Verwenden Sie Azure-Dateisynchronisierung, um die Dateifreigaben Ihrer Organisation in Azure zu zentralisieren und gleichzeitig die Flexibilität, Leistung und Kompatibilität eines lokalen Dateiservers zu erhalten. Azure-Dateisynchronisierung transformiert Windows Server in einen schnellen Cache Ihrer Azure-Dateifreigabe mit dem optionalen cloudtiering-Feature.
ms.topic: article
author: fauhse
ms.author: fauhse
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 56937ad0351a1421ab64b93351d7fa5f6d9f4fe8
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766683"
---
# <a name="sync-your-file-server-with-the-cloud-by-using-azure-file-sync"></a>Synchronisierung des Dateiservers mit der Cloud per Azure-Dateisynchronisierung

>Gilt für: Windows Admin Center, Windows Admin Center (Vorschauversion)

Verwenden Sie Azure-Dateisynchronisierung, um die Dateifreigaben Ihrer Organisation in Azure zu zentralisieren und gleichzeitig die Flexibilität, Leistung und Kompatibilität eines lokalen Dateiservers zu erhalten. Azure-Dateisynchronisierung transformiert Windows Server in einen schnellen Cache Ihrer Azure-Dateifreigabe mit dem optionalen cloudtiering-Feature. Sie können ein beliebiges Protokoll verwenden, das unter Windows Server verfügbar ist, um lokal auf Ihre Daten zuzugreifen, z.B. SMB, NFS und FTPS.

Nachdem Ihre Dateien mit der Cloud synchronisiert wurden, können Sie mehrere Server mit derselben Azure-Dateifreigabe verbinden, um die Inhalte lokal zu synchronisieren und zwischenzuspeichern – Berechtigungen (ACLs) werden stets ebenfalls übertragen. Azure Files bietet eine Momentaufnahme Funktion, mit der differenzielle Momentaufnahmen Ihrer Azure-Dateifreigabe generiert werden können. Diese Momentaufnahmen können sogar als schreibgeschützte Netzwerklaufwerke per SMB bereitgestellt werden, um das Durchsuchen und wiederherstellen zu vereinfachen. In Kombination mit cloudtiering war das Ausführen eines lokalen Dateiservers noch nie einfacher.

Weitere Informationen finden Sie unter [Planning for a Azure-Dateisynchronisierung Deployment](/azure/storage/files/storage-sync-files-planning).