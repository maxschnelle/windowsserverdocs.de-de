---
title: Speichern von Dateien mit MultiPoint Services
description: Weitere Informationen zum Dateispeicher in Multipoint Services
ms.date: 07/22/2016
ms.topic: article
ms.assetid: c9eb0461-3846-4ddc-97ff-de10f03f30cf
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 6991a62fde0e0083eb5544eed6ec49fef2b10569
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951625"
---
# <a name="storing-files-with-multipoint-services"></a>Speichern von Dateien mit MultiPoint Services
Multipoint Services unterstützt das Speichern von Benutzer Dateien auf folgende Weise:

-   **In der Betriebssystem Partition des Festplatten Laufwerks.** Standardmäßig speichert Multipoint Services Benutzer Dateien auf der Festplatte mit dem Betriebssystem.

-   **In einer separaten Partition des Festplatten Laufwerks.** Wenn das Multipoint Services-System erstmalig eingerichtet wird, können Sie die Festplatte *Partitionieren* . Das heißt, Sie können einen Abschnitt des Laufwerks so konfigurieren, dass er so funktioniert, als ob es sich um ein separates Laufwerk handelt. Dadurch ist es einfacher, das Betriebssystem wiederherzustellen, ohne dass sich dies auf die Benutzer Dateien auswirkt. Weitere Informationen finden Sie unter [Erstellen einer Partition oder eines logischen Laufwerks](https://go.microsoft.com/fwlink/?LinkId=182618) in der technischen Bibliothek für Windows Server.

-   **Auf einem zusätzlichen internen oder externen Festplattenlaufwerk.** Sie können zusätzliche interne oder externe Festplattenlaufwerke an Multipoint Services anfügen, um Daten zu speichern und zu sichern.

-   **In einem freigegebenen Netzwerkordner.** Um Benutzer Dateien von einer beliebigen Station aus verfügbar zu machen, können Sie einen freigegebenen Ordner im Netzwerk erstellen. Dies erfordert zusätzlich zum Computer, auf dem Multipoint Services ausgeführt wird, einen anderen Computer oder Server. Dies ist die empfohlene Methode zum Speichern von Dateien, wenn ein Dateiserver verfügbar ist.

    Bei kleinen Systemen mit 2-3 Computern, auf denen Multipoint Services ohne verfügbaren Dateiserver ausgeführt wird, kann einer der Multipoint Services-Computer als Dateiserver für alle Multipoint Services-Computer fungieren. Anschließend erstellen Sie Benutzerkonten für alle Benutzer in den Multipoint Services, die als Dateiserver fungieren.

