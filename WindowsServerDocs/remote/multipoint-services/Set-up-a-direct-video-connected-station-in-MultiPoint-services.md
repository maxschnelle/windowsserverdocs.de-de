---
title: Einrichten einer Station Direct-Video-Verbindung in MultiPoint Services
description: Erfahren Sie, wie Sie eine Station Direct-Video-Verbindung in MultiPoint Services erstellen
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82ba3517-9743-4cde-8eea-63a17edb016f
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 58197164c91ab6b69b0ef331c025287f593f94c2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850741"
---
# <a name="set-up-a-direct-video-connected-station-in-multipoint-services"></a>Einrichten einer Station Direct-Video-Verbindung in MultiPoint Services
Auf einer direkt verbundenen Video Station ist der Monitor direkt mit einer video-Port auf dem MultiPoint Server-Computer verbunden. Tastatur und Maus dann mit einem USB-Hub verbunden sind, und der Monitor zugeordnet sind.  
  
Die folgende Abbildung zeigt eine MultiPoint Server-Umgebung, die einem einzelnen MultiPoint Server-Computer und vier Stationen mit Direct-Video-Verbindung verfügt. Weitere Informationen finden Sie unter [MultiPoint Server-Stationen](MultiPoint-services-Stations.md).  
  
**MultiPoint Services-System mit vier video direct-Verbindungen**  
  
![Layout eines MultiPoint Services-USB-basierten Systems](./media/WMSMultiPointServerUSBSystemLayout.gif)  
  
> [!NOTE]  
> Um eine Station Direct-Video-Verbindung konfigurieren zu können, müssen Sie eine Lateinische Tastatur (z. B. eine Sprachtastatur Englisch oder Spanisch) verwenden.  
  
## <a name="to-set-up-a-direct-video-connected-station"></a>Zum Einrichten einer direkten Video verbundene station  
  
1.  Das Kabel des Monitors an den Port der Videoanzeige auf dem Computer, wie unten dargestellt.  
  
    ![Abbildung einer Videoverbindung zu einem System mit USB Hub](./media/WMSVideoConnection.gif) 
  
2.  Stecken Sie das Stromkabel des Videomonitors in eine Steckdose.  
  
3.  Verbinden Sie einen USB-Hub mit einem freien USB-Anschluss auf dem Computer, wie unten dargestellt.  
  
    ![Abbildung des MultiPoint Services-USB-Hub-Verbindung](./media/WMSUSBHubConnection.gif)  
  
4.  Verbinden Sie an den stationshub USB-Tastatur und Maus.  
  
    ![Anschließen von Eingabegeräten an einen USB-Hub](./media/WMSUSBDeviceConnection.gif)  
  
5.  Verbinden Sie zusätzlichen Peripheriegeräten, z. B. Kopfhörer, mit der USB-Hub an.  
  
6.  Wenn Sie einen extern ausgeschaltet Hub verwenden, verbinden Sie das Stromkabel des Hubs in eine Steckdose.  
  
    > [!IMPORTANT]  
    > Wir empfehlen dringend die Verwendung eines Hubs ausgeschaltet. Unterdimensionierte aktuelle Bedingungen kann fehlerhaften Systemverhalten führen.  
    >   
    > Benutzer sollten Mäuse und Tastaturen nicht direkt auf das USB-Anschlüsse des Computers anfügen. Auf diese Weise werden wahrscheinlich die falsche Zuordnung mehrerer Tastaturen und Mäusen derselben oder keine Station überhaupt.  
  
7.  Befolgen Sie die Anweisungen, die auf dem Bildschirm zum Erstellen der Station angezeigt werden.  
  
Wenn Sie mehr als eine direkte Station des Video-Verbindung zu Ihrem MultiPoint Services-Umgebung hinzufügen, kann die primäre Station ändern. Sie können leicht herausfinden der direkte video verbundenen Station Ihre primäre Station ist.  
  
## <a name="to-find-out-which-direct-video-connected-station-is-the-primary-station"></a>Um herauszufinden, die Station Video-Verbindung leiten, ist die primäre station  
  
1.  Aktivieren Sie alle Monitore, die direkt mit der Grafikkarte (Grafikkarten) des Computers verbunden sind.  
  
2.  Starten (oder neu starten) können die MultiPoint Services-Computer, und welcher Monitor den Startbildschirmen angezeigt. Diese Station ist die primäre Station.  
  
    > [!NOTE]  
    > In einigen Fällen ist BIOS-Startinformationen gleichzeitig auf mehreren Bildschirmen angezeigt. In diesem Fall kann die Monitore "primäre Station" betrachtet werden für den Zugriff auf das BIOS.