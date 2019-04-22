---
title: Einrichten des physischen Computers und der primären Station
description: Erfahren Sie, wie Sie Ihre erste System, der primären in MultiPoint Services-Station einrichten
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e83b126-ce9a-4cd7-a0bd-6627c9e0f81b
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 6569c4963d31b72216943bf29b71411e702caf84
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812011"
---
# <a name="set-up-the-physical-computer-and-primary-station"></a>Einrichten des physischen Computers und der primären Station
Vor der Installation von MultiPoint Services müssen Sie die primäre Station für das MultiPoint Services-System einrichten. Verbinden Sie den Computer mit dem LAN, wenn Sie eine lokale Netzwerk (LAN) verwenden möchten.  
  
Ein *Station* ist ein Endpunkt mit dem MultiPoint-Dienste zugegriffen wird. Die *primäre Station* ist die erste Station, die beim start MultiPoint Server gestartet wird. Administratoren können sie zu Access-Start-Menüs und Einstellungen verwenden. Die primäre Station ermöglicht den Zugriff auf die Systemkonfiguration und Informationen, die nur während des Starts und vor dem MultiPoint Services steht zur Problembehandlung bei System ausgeführt wird. Nach dem Start können Sie die primäre Station verwenden, wie Sie eine anderen Station.  
  
Die primäre Station muss eine Station Direct-Video-Verbindung sein. Das folgende Verfahren beschreibt, wie zur Verbindung mit dem MultiPoint Services-Computer der erforderlichen Hardware wird.  
  
Weitere Informationen zu den Stationen, finden Sie unter [MultiPoint-Stationen](multipoint-services-stations.md). Hilfe bei Treffen einer Auswahl von Hardware, finden Sie unter [Auswählen der Hardware für Ihr MultiPoint Services-Systems](Selecting-Hardware-for-Your-MultiPoint-services-System.md). Weitere Informationen zum Verbinden von anderen Typen mit MultiPoint Services Kontrollstationen, finden Sie unter [zusätzliche Sender auf dem MultiPoint Services-Computer Anfügen](Attach-additional-stations-to-your-MultiPoint-services-computer.md).  
  
> [!NOTE]  
> Um eine Video-Verbindung-Station zu erstellen, müssen Sie eine Lateinische Tastatur (z. B. eine Tastatur Sprache als Englisch oder Spanisch) verwenden.  
  
## <a name="to-set-up-your-primary-station"></a>So richten Sie Ihre primäre Station ein  
  
1.  Stellen Sie sicher, dass der Computer, auf dem MultiPoint Services ausgeführt wird deaktiviert und wurde entfernt.  
  
2.  Verbinden Sie das Stromkabel des Monitors, in eine Steckdose, und das Kabel des Monitors an den Port der Videoanzeige auf dem Computer, wie unten dargestellt.  
  
    ![Abbildung einer Videoverbindung zu einem System mit USB Hub](./media/WMSVideoConnection.gif)  
  
3.  Wenn die Station USB-Tastatur und Maus verwenden möchten, führen Sie die folgenden Schritte aus:  
  
    1.  Verbinden Sie einen externen USB-Hub mit einem freien USB-Anschluss auf dem Computer, wie unten dargestellt.  
  
        ![Abbildung des MultiPoint Services-USB-Hub-Verbindung](./media/WMSUSBHubConnection.gif)  
  
    2.  Verbinden Sie USB-Tastatur und Maus, mit dem USB-Hub.  
  
        ![Anschließen von Eingabegeräten an einen USB-Hub](./media/WMSUSBDeviceConnection.gif)  
  
        > [!NOTE]  
        > Verfügt Ihr MultiPoint Services-Computer über PS/2-Ports, können Sie bei Bedarf PS/2-Tastatur und Maus, die direkt an den Computer angeschlossen verwenden. Dieses Setup hat jedoch deutliche Einschränkungen auf. Benutzer nicht verwenden, Audiogeräte, Webcams, und flash-Laufwerke auf PS/2-Stationen.  
  
    3.  Wenn Sie einen extern ausgeschaltet Hub verwenden, verbinden Sie das Stromkabel des Hubs in eine Steckdose.  
  
        > [!IMPORTANT]  
        > Wir empfehlen dringend die Verwendung eines Hubs ausgeschaltet. Unterdimensionierte aktuelle Bedingungen kann fehlerhaften Systemverhalten führen.  
        >   
        > Benutzer sollten Mäuse und Tastaturen nicht direkt auf das USB-Anschlüsse des Computers anfügen. Auf diese Weise werden wahrscheinlich die falsche Zuordnung mehrerer Tastaturen und Mäusen derselben oder keine Station überhaupt.  
  
        > [!NOTE]  
        > Der Host-audio-Gerät auf der Hauptplatine ist nur verfügbar, während MultiPoint-Dienste im Konsolenmodus ausgeführt wird. Um ohne Unterbrechung Audio für eine Station zu gewährleisten, die einen externen USB-Hub verwendet, müssen Sie ein USB-Audiogerät an den Hub angeschlossen verwenden.  
  
## <a name="to-connect-the-computer-to-the-lan"></a>Um den Computer mit dem LAN verbinden  
  
-   Wenn Sie über ein LAN haben, verbinden Sie den Computer über ein Netzwerkkabel mit Ihrem Netzwerk.