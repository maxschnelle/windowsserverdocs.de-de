---
title: Prehashing und Vorabladen von Inhalt auf gehosteten Cacheserver (Optional)
description: Dieses Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 5a09d9f1-1049-447f-a9bf-74adf779af27
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c3d1ed62c6dca5b1de0ff560fde0a2e43ed0d080
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="prehashing-and-preloading-content-on-hosted-cache-servers-optional"></a>Prehashing und Vorabladen von Inhalt auf gehosteten Cacheserver (Optional)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Verfahrens können Sie die Erstellung von Inhaltsinformationen - Hashes – auch für BranchCache-fähigen Web- und Dateiservern aufgerufen erzwingen. Sie können auch die Daten auf Datei- und Webserver in Pakete zu sammeln, die für remote gehosteten Cacheserver übertragen werden können.  Dies bietet Ihnen die Möglichkeit, Inhalte auf remote gehosteten Cacheserver vorab laden, damit Daten für den ersten Clientzugriff verfügbar ist.  
  
Sie müssen ein Mitglied sein **Administratoren**, oder eine gleichwertige, um dieses Verfahren auszuführen.  
  
### <a name="to-prehash-content-and-preload-the-content-on-hosted-cache-servers"></a>Um Inhalte prehashing und Vorabladen von Inhalt auf gehostete Cacheserver  
  
1.  Melden Sie sich auf die Datei oder den Webserver, der die Daten enthält, die Sie vorab laden möchten, und identifizieren Sie die Ordner und Dateien, die Sie auf einem oder mehreren remote gehosteten Cacheserver laden möchten.  
  
2.  WindowsPowerShell als Administrator ausführen. Für jeden Ordner und die Datei, führen Sie einen der `Publish-BCFileContent`Befehl oder den `Publish-BCWebContent`erhalten Sie, je nach dem Inhaltsserver, hasherzeugung auslösen und ein Datenpaket Daten hinzu.  
  
3.  Nach dem alle Daten hinzugefügt wurde das Paket mit Daten, exportieren Sie es mithilfe der `Export-BCCachePackage`Befehl aus, um eine Datei im Paket zu erstellen.  
  
4.  Verschieben Sie die Paketdatei Daten an remote gehosteten Cacheserver, mithilfe Ihrer Wahl der Übertragung der Technologie.  FTP, SMB, HTTP, DVD und externe Festplatten sind alle geeignete Transporte.  
  
5.  Importieren Sie die Datei auf dem remote gehosteten Cacheserver Paket mithilfe der `Import-BCCachePackage`Befehl.  
  

