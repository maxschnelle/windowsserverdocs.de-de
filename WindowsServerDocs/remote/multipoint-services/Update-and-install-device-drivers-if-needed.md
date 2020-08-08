---
title: Aktualisieren und Installieren von Gerätetreibern bei Bedarf
description: Erfahren Sie, wie Sie Gerätetreiber in Multipoint Services überprüfen und aktualisieren.
ms.date: 07/22/2016
ms.topic: article
ms.assetid: 16be3ef9-a05b-4621-a431-5806b567e997
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 0a6d389b0c34e7e1b794431dc1b1fefa8fef3fb4
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949043"
---
# <a name="update-and-install-device-drivers-if-needed"></a>Aktualisieren und Installieren von Gerätetreibern bei Bedarf
Wenn Sie USB-Clients oder Peripheriegeräte verwenden, die Treiber erfordern, sollten Sie die Treiber zu diesem Zeitpunkt installieren. Es empfiehlt sich auch, **Geräte-Manager** auf Treiber Warnungen zu überprüfen und Treiber für diese Geräte zu installieren.

Im Allgemeinen sind die aktuellen Treiber für die folgenden Arten von Geräten erforderlich:

-   USB-Clients

-   USB-over-Ethernet-Clients (null)

-   Datenträgercontroller

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