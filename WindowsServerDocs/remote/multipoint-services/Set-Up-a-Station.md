---
title: Einrichten einer Station
description: Erfahren Sie, wie Sie eine Station in Multipoint Services einrichten.
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dce05b6c-795e-43b2-9920-026550b873c5
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 95a332a3d15e82047b46cc19f168f945cdb334d2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389454"
---
# <a name="set-up-a-station"></a>Einrichten einer Station
Eine MultiPoint Server-*Station* besteht normalerweise aus einem *Stationshub*, einer Maus, einer Tastatur und einem Videomonitor. In diesem Thema wird beschrieben, wie die Hardwaregeräte mit dem Stationshub verbunden werden, um eine MultiPoint Services-Station zu erstellen.  
  
Der Stationshub ist ein Hardwaregerät, über das Peripheriegeräte an einen Computer in einem MultiPoint Services-System angeschlossen werden. MultiPoint Services unterstützt zwei Typen von Stationshubs:  
  
-   **USB-Hub:** Ein generischer Multiport-USB-erweiterungshub, der den Spezifikationen für den universellen seriellen Bus 2,0 oder höher entspricht. Solche Hubs verfügen typischerweise über zwei, vier oder mehr USB-Anschlüsse, die das Verbinden mehrerer USB-Geräte mit einem einzelnen USB-Anschluss des Computers ermöglichen. USB-Hubs sind üblicherweise separate Geräte, die extern oder im Bus betrieben werden können. Bei der Verwendung als Stationshub mit MultiPoint Services wird empfohlen, einen Hub mit vier oder mehr Anschlüssen zu verwenden.  
  
    > [!IMPORTANT]  
    > Wenn Sie beabsichtigen, andere USB-Geräte als eine Tastatur und eine Maus am Hub anzuschließen, sollten Sie einen Hub mit externer Stromversorgung verwenden, um die Leistung zu verbessern.  
  
-   **Multifunktionshub:** Ein erweiterungshub, der über einen USB-Anschluss eine Verbindung mit dem Computer herstellt und die Verbindung verschiedener nicht-USB-Geräte mit dem Hub, einschließlich eines Video Monitors, ermöglicht. Multifunktionshubs werden von bestimmten Hardwareherstellern erstellt und erfordern möglicherweise die Installation eines gerätespezifischen Treibers.  
  
Wenn Sie Ihrem MultiPoint Services-System eine Station hinzufügen möchten, müssen Sie zuerst sicherstellen, dass genügend Anschlüsse für die zu verwendende Stationshardware verfügbar sind. Außerdem müssen Sie die entsprechende Anzahl von *Client Zugriffs Lizenzen (Client Access Licenses, CALs)* für Ihr Multipoint Services-System sichern.  
  
## <a name="setting-up-station-hardware"></a>Einrichten der Stationshardware  
Die Verfahren in diesem Abschnitt beschreiben, wie MultiPoint Services-Stationshardware an die verschiedenen Typen von Stationshubs angeschlossen wird.  
  
### <a name="to-set-up-a-station-with-a-usb-hub"></a>So richten Sie eine Station mit einem USB-Hub ein  
  
1.  Bevor eine neue Station angeschlossen werden kann, *beenden* Sie alle *Benutzersitzungen*, und fahren Sie dann den Computer sowie alle anderen eingeschalteten Geräte in Ihrem MultiPoint Services-System herunter.  
  
2.  Schließen Sie das Kabel des neuen Videomonitors wie in der folgenden Abbildung gezeigt am Videoanzeigenschluss des Computers an:  
  
    ![Abbildung einer Videoverbindung zu einem System mit USB Hub](./media/WMSVideoConnection.gif)  
  
3.  Schließen Sie den neuen USB-Hub an einem freien USB-Anschluss des Computers an:  
  
    ![Anschließen eines MultiPoint Server-USB-Hubs](./media/WMSUSBHubConnection.gif)  
  
4.  Schließen Sie eine Tastatur und eine Maus an den USB-Hub an:  
  
    ![Anschließen von Eingabegeräten an einen USB-Hub](./media/WMSUSBDeviceConnection.gif)  
  
5.  Stecken Sie das Stromkabel des Videomonitors in eine Steckdose.  
  
6.  Schalten Sie den Computer ein.  
  
7.  MultiPoint Services wird gestartet. Befolgen Sie die Anweisungen, die auf dem Videomonitor der neuen Station angezeigt werden, um die Geräte der neuen Station zuzuordnen.  
  
### <a name="to-set-up-a-station-with-a-multifunction-hub"></a>So richten Sie eine Station mit einem Multifunktionshub ein  
  
1.  Bevor eine neue Station angeschlossen werden kann, beenden Sie alle Benutzersitzungen, und fahren Sie dann den Computer sowie alle anderen eingeschalteten Geräte in Ihrem MultiPoint Services-System herunter.  
  
2.  Schließen Sie das Kabel des neuen Videomonitors wie in der folgenden Abbildung gezeigt am DVI- oder VGA-Videoanzeigenschluss des Multifunktionshubs an:  
  
    ![Anschließen von Video an einen Multifunktionshub](./media/WMSMultifunctionHubVideoConnection.gif)  
  
3.  Schließen Sie den neuen Multifunktionshub an einem freien USB-Anschluss des Computers an:  
  
    ![Anschließen eines Multifunktionshubs](./media/WMSMultifunctionHubConnection.gif)  
  
4.  Schießen Sie eine Tastatur und eine Maus an den PS2- oder USB-Anschluss des Multifunktionshubs an:  
  
    ![Anschließen von PS2-Steckern an einen Multifunktionshub](./media/WMSMultifunctionHubPS2Connection.gif)  
  
5.  Stecken Sie das Stromkabel des Videomonitors in eine Steckdose.  
  
6.  Schalten Sie den Computer ein.  
  
7.  MultiPoint Services wird gestartet. Wenn Sie dazu aufgefordert werden, befolgen Sie die Anweisungen, die auf dem Videomonitor der neuen Station angezeigt werden, um die Geräte der neuen Station *zuzuordnen* .  
  
## <a name="see-also"></a>Siehe auch  
[Beenden einer Benutzersitzung](End-a-User-Session.md)  
[Neustarten oder Herunterfahren](Restart-or-Shut-Down.md)  
[Verwalten der Stationshardware](Manage-Station-Hardware.md)  
[Arbeiten mit USB-Geräten](Work-with-USB-Devices.md)