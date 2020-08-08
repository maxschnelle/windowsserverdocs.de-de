---
title: Einrichten des physischen Computers und der primären Station
description: Erfahren Sie, wie Sie Ihr erstes System, die primäre Station, in Multipoint Services einrichten.
ms.date: 07/22/2016
ms.topic: article
ms.assetid: 4e83b126-ce9a-4cd7-a0bd-6627c9e0f81b
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: b18800e2c8c7feae30f3dbcfb8904f00ef40a396
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955464"
---
# <a name="set-up-the-physical-computer-and-primary-station"></a>Einrichten des physischen Computers und der primären Station
Vor der Installation von Multipoint Services müssen Sie die primäre Station für Ihr Multipoint Services-System einrichten. Wenn Sie ein LAN (Local Area Network) verwenden, verbinden Sie den Computer mit dem LAN.

Eine *Station* ist ein Endpunkt, über den auf Multipoint Services zugegriffen wird. Die *primäre Station* ist die erste Station, die gestartet wird, wenn Multipoint Services gestartet wird. Administratoren können Sie verwenden, um auf Startmenüs und-Einstellungen zuzugreifen. Die primäre Station ermöglicht den Zugriff auf Systemkonfigurations-und Problem Behandlungsinformationen, die nur während des Starts und vor der Ausführung des Multipoint Services-Systems verfügbar sind. Nach dem Start können Sie die primäre Station wie jede andere Station verwenden.

Bei der primären Station muss es sich um eine Station mit direkt Videoverbindung handeln. Im folgenden Verfahren wird beschrieben, wie Sie die erforderliche Hardware mit Ihrem Multipoint Services-Computer verbinden.

Weitere Informationen zu Stationen finden Sie unter [Multipoint-Stationen](multipoint-services-stations.md). Hilfe zum Treffen von Hardware Auswahlen finden [Sie unter Auswählen von Hardware für Ihr Multipoint Services-System](Selecting-Hardware-for-Your-MultiPoint-services-System.md). Informationen zum Verbinden anderer Stations Typen mit Multipoint Services finden Sie unter [Anfügen zusätzlicher Stationen an Ihren Multipoint Services-Computer](Attach-additional-stations-to-your-MultiPoint-services-computer.md).

> [!NOTE]
> Um eine Station mit Videoverbindung zu erstellen, müssen Sie eine lateinische Tastatur verwenden (z. b. eine englische oder spanischsprachige Tastatur).

## <a name="to-set-up-your-primary-station"></a>So richten Sie Ihre primäre Station ein

1.  Stellen Sie sicher, dass der Computer, auf dem Multipoint Services ausgeführt wird, ausgeschaltet ist.

2.  Verbinden Sie das Netzkabel des Monitors mit einer Stromversorgung, und verbinden Sie das Monitorkabel mit dem Video anschauport auf dem Computer, wie unten gezeigt.

    ![Anschließen von Video an einem System mit USB-Hub](./media/WMSVideoConnection.gif)

3.  Wenn die Station eine USB-Tastatur und-Maus verwendet, führen Sie die folgenden Schritte aus:

    1.  Stellen Sie eine Verbindung zwischen einem externen USB-Hub und einem geöffneten USB-Anschluss auf dem Computer her (siehe unten).

        ![Abbildung der Multipoint Services-USB-Hub-Verbindung](./media/WMSUSBHubConnection.gif)

    2.  Verbinden Sie die USB-Tastatur und die Maus mit dem USB-Hub.

        ![Anschließen von Eingabegeräten an einen USB-Hub](./media/WMSUSBDeviceConnection.gif)

        > [!NOTE]
        > Wenn Ihr Multipoint Services-Computer über PS/2-Ports verfügt, können Sie bei Bedarf eine PS/2-Tastatur verwenden und die Maus direkt an den Computer angeschlossen. Diese Einrichtung hat jedoch erhebliche Einschränkungen. Benutzer können keine Audiogeräte, Web-Cams und Flash Laufwerke auf PS/2-Stationen verwenden.

    3.  Wenn Sie einen extern betriebenen Hub verwenden, verbinden Sie das Netzkabel des Hubs mit einer Stromversorgung.

        > [!IMPORTANT]
        > Wir empfehlen dringend die Verwendung eines gestützten Hubs. Ein erratisches Systemverhalten kann sich aus unter aktuellen Bedingungen ergeben.
        >
        > Benutzer dürfen keine Maus und Tastatur direkt an die USB-Anschlüsse des Computers anfügen. Dadurch wird wahrscheinlich die falsche Zuordnung mehrerer Tastaturen und Mäuse zur gleichen Station oder zu keiner Station ausgelöst.

        > [!NOTE]
        > Das hostaudiogerät auf der Hauptplatine des Systems ist nur verfügbar, wenn sich Multipoint Services im Konsolenmodus befindet. Sie müssen ein USB-Audiogerät verwenden, das mit dem Hub verbunden ist, um das ununterbrochene Audiomaterial für eine Station sicherzustellen, die einen externen USB-Hub verwendet.

## <a name="to-connect-the-computer-to-the-lan"></a>So verbinden Sie den Computer mit dem LAN

-   Wenn Sie über ein LAN verfügen, verbinden Sie Ihren Computer mit Ihrem Netzwerk über ein Netzwerkkabel.