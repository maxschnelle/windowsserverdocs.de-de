---
title: Synchronisieren Sie den Dateiserver mit der Cloud mithilfe von Azure-Datei-Synchronisierung
description: Verwenden von Azure-Datei Sync Ihrer Organisation Dateifreigaben in Azure zentralisieren und gleichzeitig die Flexibilität, Leistung und Kompatibilität von einer lokalen Datei-Server. Azure-Datei Synchronisierung transformiert Windows Server in einen schnellen Cache mit Ihrer Azure Dateifreigabe mit dem optionale Cloud tiering-Feature.
ms.technology: manage
ms.topic: article
author: fauhse
ms.author: fauhse
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 93cfa469a3c14410d95b0b224cbf59b913ec9f7e
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296902"
---
# Synchronisieren Sie den Dateiserver mit der Cloud mithilfe von Azure-Datei-Synchronisierung

>Gilt für: Windows Admin Center, Windows Admin Center – Vorschau

Verwenden von Azure-Datei Sync Ihrer Organisation Dateifreigaben in Azure zentralisieren und gleichzeitig die Flexibilität, Leistung und Kompatibilität von einer lokalen Datei-Server. Azure-Datei Synchronisierung transformiert Windows Server in einen schnellen Cache mit Ihrer Azure Dateifreigabe mit dem optionale Cloud tiering-Feature. Sie können alle verwenden, die auf Windows Server Zugriff auf Ihre Daten lokal verfügbar ist einschließlich SMB, NFS und FTPS.

Nachdem Ihre Dateien in die Cloud synchronisiert haben, können Sie mehrere Server verbinden, auf die gleiche Azure Dateifreigabe synchronisieren und den Inhalt lokal zwischengespeichert werden – Berechtigungen (ACLs) werden immer sowie transportiert. Azure Files bietet eine Momentaufnahme-Funktion, die differenzielle Snapshots Ihrer Azure Dateifreigabe erstellen kann. Diese Snapshots können auch als schreibgeschützt Netzwerklaufwerke über SMB einfach surfen und Wiederherstellung bereitgestellt werden. In Kombination mit Cloud tiering kann war mit einer lokalen Dateiserver nie.

Weitere Informationen finden Sie unter [einer Azure Datei Sync-Bereitstellung planen](https://aka.ms/afs).