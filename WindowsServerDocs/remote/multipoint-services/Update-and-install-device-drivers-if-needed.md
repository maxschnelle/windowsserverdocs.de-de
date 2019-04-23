---
title: Aktualisieren und Installieren von Gerätetreibern bei Bedarf
description: Erfahren Sie, wie zum Überprüfen und Aktualisieren von Gerätetreibern in MultiPoint Services
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16be3ef9-a05b-4621-a431-5806b567e997
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 66477634e06df217656876b084ae37be8cb311c0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829131"
---
# <a name="update-and-install-device-drivers-if-needed"></a>Aktualisieren und Installieren von Gerätetreibern bei Bedarf
Wenn Sie USB-0 (null)-Clients oder Peripheriegeräte, die Treiber benötigen verwenden, sollten Sie die Treiber zu diesem Zeitpunkt installieren. Es empfiehlt sich auch, um zu überprüfen ist **-Geräte-Manager** für alle Treiber Warnungen und Installieren von Treibern für diese Geräte.  
  
Im Allgemeinen sind die aktuellen Treiber für die folgenden Arten von Geräten erforderlich:  
  
-   USB-0 (null)-clients  
  
-   USB-Over-Ethernet-0 (null)-clients  
  
-   Datenträgercontroller  
  
-   Netzwerkadapter  
  
-   Sound-Controller  
  
-   USB-Hostcontroller

-   Grafikkarten


## <a name="to-check-for-driver-alerts-in-device-manager"></a>Überprüfen Sie für die Treiber im Geräte-Manager-Warnungen  
  
1.  Bildschirm "Start" zu öffnen.  
  
2.  Typ **computerverwaltung**, und klicken Sie dann auf **Computerverwaltung** in den Ergebnissen.  
  
3.  Klicken Sie in der Konsolenstruktur Computerverwaltung auf **-Geräte-Manager**.  
  
4.  Suchen Sie in den System-Geräten auf der rechten Seite Treiber Warnungen, die MultiPoint Server auswirken.  
  
## <a name="to-install-device-drivers-in-multipoint-manager"></a>Installieren von Gerätetreibern in MultiPoint-Manager  
  
1.  Um MultiPoint-Manager zu öffnen, suchen Sie nach "MultiPoint-Manager", und klicken Sie dann auf **MultiPoint-Manager** in den Ergebnissen.  
  
2.  MultiPoint-Manager, klicken Sie auf die **Startseite** Registerkarte, und klicken Sie dann auf **wechseln Sie in den Konsolenmodus**.  
  
3.  Um einen Gerätetreiber zu installieren, doppelklicken klicken Sie auf die Treiberdatei, und befolgen Sie die Anweisungen zum Installieren des Treibers.  
  
4.  Wiederholen Sie den vorherigen Schritt, um alle erforderlichen Treiber zu installieren.  
  
    > [!NOTE]  
    > Wenn eine Installation einen Neustart des Computers erfordert, müssen Sie wieder in den Konsolenmodus zu wechseln, bevor Sie den nächsten Treiber installieren. MultiPoint-Server wird immer im stationsmodus gestartet. So wechseln Sie zu Konsolenmodus finden Sie unter den **Startseite** Registerkarte im MultiPoint-Manager, und klicken Sie auf **wechseln Sie in den Konsolenmodus**.