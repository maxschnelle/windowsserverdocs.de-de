---
title: Speichern von Dateien mit MultiPoint Services
description: Erfahren Sie mehr über die Dateispeicher in MultiPoint Services
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c9eb0461-3846-4ddc-97ff-de10f03f30cf
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: b432ca793b156997761f9fadab7340c394e3b553
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817341"
---
# <a name="storing-files-with-multipoint-services"></a>Speichern von Dateien mit MultiPoint Services
MultiPoint Services unterstützt das Speichern von Benutzerdateien, es gibt folgende Möglichkeiten:  
  
-   **Auf der Partition für das Betriebssystem das Festplattenlaufwerk.** Standardmäßig speichert MultiPoint Services Benutzerdateien auf der Festplatte mit dem Betriebssystem.  
  
-   **In einer separaten Partition von der Festplatte.** Wenn Sie das MultiPoint Services-System zum ersten Mal eingerichtet ist, können Sie *Partition* der Festplatte. D. h. können Sie einen Abschnitt des Laufwerks konfigurieren, damit, dass er funktioniert, als handele es sich um ein separates Laufwerk. Dies erleichtert es zum Wiederherstellen oder ein upgrade des Betriebssystems ohne Auswirkungen auf Benutzerdateien. Weitere Informationen finden Sie unter [erstellen Sie eine Partition oder ein logisches Laufwerk](https://go.microsoft.com/fwlink/?LinkId=182618) in der technischen Bibliothek für Windows Server.  
  
-   **Auf einem zusätzlichen internen oder externen Festplattenlaufwerk.** Sie können zusätzliche interne oder externe Festplattenlaufwerke mit MultiPoint Services für das Speichern und Sichern von Daten anfügen.  
  
-   **In einem freigegebenen Netzwerkordner.** Um Benutzerdateien über jede Station verfügbar zu machen, können Sie einen freigegebenen Ordner im Netzwerk erstellen. Dies erfordert einen anderen Computer oder Server zusätzlich zu dem Computer, auf dem MultiPoint Services ausgeführt wird. Dies ist die empfohlene Methode zum Speichern von Dateien aus, wenn ein Dateiserver verfügbar ist.  
  
    Für kleine Systeme 2 und 3-Computer mit MultiPoint-Dienste, die keine Dateiserver verfügbar kann einer der MultiPoint Services-Computer als Dateiserver für alle der MultiPoint Services-Computer fungieren. Sie würden dann Benutzerkonten für alle Benutzer in der MultiPoint Services erstellen, die als Dateiserver dient.  
  
