---
title: Aktualisieren und Installieren von Gerätetreibern bei Bedarf
description: Erfahren Sie, wie Sie Gerätetreiber in Multipoint Services überprüfen und aktualisieren.
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 16be3ef9-a05b-4621-a431-5806b567e997
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 6d20aa80edeafa4311262a380cfd7aad65ae0315
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820603"
---
# <a name="update-and-install-device-drivers-if-needed"></a>Aktualisieren und Installieren von Gerätetreibern bei Bedarf
Wenn Sie USB-Clients oder Peripheriegeräte verwenden, die Treiber erfordern, sollten Sie die Treiber zu diesem Zeitpunkt installieren. Es empfiehlt sich auch, **Geräte-Manager** auf Treiber Warnungen zu überprüfen und Treiber für diese Geräte zu installieren.  
  
Im Allgemeinen sind die aktuellen Treiber für die folgenden Arten von Geräten erforderlich:  
  
-   USB-Clients  
  
-   USB-over-Ethernet-Clients (null)  
  
-   Datenträger Controller  
  
-   Netzwerkadapter  
  
-   Sound Controller  
  
-   USB-Host Controller

-   Grafikkarten


## <a name="to-check-for-driver-alerts-in-device-manager"></a>So überprüfen Sie die Treiber Warnungen in Geräte-Manager  
  
1.  Öffnen Sie den Start Bildschirm.  
  
2.  Geben Sie **Computer Verwaltung**ein, und klicken Sie dann in den Ergebnissen auf **Computer Verwaltung** .  
  
3.  Klicken Sie in der Konsolen Struktur der Computer Verwaltung auf **Geräte-Manager**.  
  
4.  Überprüfen Sie in den System Geräten auf der rechten Seite die Treiber Warnungen, die sich auf Multipoint Server auswirken können.  
  
## <a name="to-install-device-drivers-in-multipoint-manager"></a>So installieren Sie Gerätetreiber im Multipoint-Manager  
  
1.  Um den Multipoint-Manager zu öffnen, suchen Sie nach "Multipoint-Manager", und klicken Sie dann in den Ergebnissen auf **Multipoint-Manager** .  
  
2.  Klicken Sie im Multipoint-Manager auf die Registerkarte **Start** , und klicken Sie dann **auf zum Konsolenmodus wechseln**.  
  
3.  Um einen Gerätetreiber zu installieren, doppelklicken Sie auf die Treiberdatei, und befolgen Sie die Anweisungen zum Installieren des Treibers.  
  
4.  Wiederholen Sie den vorherigen Schritt, um alle erforderlichen Treiber zu installieren.  
  
    > [!NOTE]  
    > Wenn für eine Installation ein Computer Neustart erforderlich ist, müssen Sie wieder in den Konsolenmodus wechseln, bevor Sie den nächsten Treiber installieren. Der Multipoint-Server wird immer im Stations Modus gestartet. Wechseln Sie in den Konsolenmodus, und klicken Sie im Multipoint-Manager auf die Registerkarte **Home** , und klicken Sie auf **zum Konsolenmodus wechseln**.