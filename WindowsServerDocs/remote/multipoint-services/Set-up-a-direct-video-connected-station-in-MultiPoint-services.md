---
title: Einrichten einer Station mit direkt Videoverbindung in Multipoint Services
description: Erfahren Sie, wie Sie eine Station mit direkt Videos in Multipoint Services erstellen.
ms.date: 07/22/2016
ms.topic: article
ms.assetid: 82ba3517-9743-4cde-8eea-63a17edb016f
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 90be4dd0f827c30419cfb30737de6e2b9aecc5be
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971767"
---
# <a name="set-up-a-direct-video-connected-station-in-multipoint-services"></a>Einrichten einer Station mit direkt Videoverbindung in Multipoint Services
Auf einer direkt mit dem Video verbundenen Station ist der Monitor direkt mit einem Videoport auf dem Multipoint Server-Computer verbunden. Eine Tastatur und eine Maus werden dann mit einem USB-Hub verbunden und dem Monitor zugeordnet.

Die folgende Abbildung zeigt eine Multipoint-Serverumgebung mit einem einzelnen Multipoint-Server Computer und vier direkt mit einem Video verbundenen Stationen. Weitere Informationen finden Sie unter [Multipoint-Server Stationen](MultiPoint-services-Stations.md).

**Multipoint Services-System mit vier direkten Video Verbindungen**

![Abbildung des USB-basierten Multipoint Services-systemlayouts](./media/WMSMultiPointServerUSBSystemLayout.gif)

> [!NOTE]
> Sie müssen eine lateinische Tastatur (z. b. eine Englisch-oder spanischsprachige Tastatur) verwenden, um eine Station mit einem direkt Video zu konfigurieren.

## <a name="to-set-up-a-direct-video-connected-station"></a>So richten Sie eine direkte Station mit Videoverbindung ein

1.  Verbinden Sie das Monitorkabel mit dem videoanzeigeport auf dem Computer, wie unten gezeigt.

    ![Anschließen von Video an einem System mit USB-Hub](./media/WMSVideoConnection.gif)

2.  Stecken Sie das Stromkabel des Videomonitors in eine Steckdose.

3.  Verbinden Sie einen USB-Hub wie unten dargestellt mit einem geöffneten USB-Anschluss auf dem Computer.

    ![Abbildung der Multipoint Services-USB-Hub-Verbindung](./media/WMSUSBHubConnection.gif)

4.  Verbinden Sie eine Tastatur und eine Maus mit dem USB-stationshub.

    ![Anschließen von Eingabegeräten an einen USB-Hub](./media/WMSUSBDeviceConnection.gif)

5.  Verbinden Sie alle zusätzlichen Peripheriegeräte, z. b. Kopfhörer, mit dem USB-Hub.

6.  Wenn Sie einen extern betriebenen Hub verwenden, verbinden Sie das Netzkabel des Hubs mit einer Stromversorgung.

    > [!IMPORTANT]
    > Wir empfehlen dringend die Verwendung eines gestützten Hubs. Ein erratisches Systemverhalten kann sich aus unter aktuellen Bedingungen ergeben.
    >
    > Benutzer dürfen keine Maus und Tastatur direkt an die USB-Anschlüsse des Computers anfügen. Dadurch wird wahrscheinlich die falsche Zuordnung mehrerer Tastaturen und Mäuse zur gleichen Station oder zu keiner Station ausgelöst.

7.  Befolgen Sie die Anweisungen, die auf dem Monitor zum Erstellen der Station angezeigt werden.

Wenn Sie Ihrer Multipoint Services-Umgebung mehr als eine direkte, mit einem Video verbundene Station hinzufügen, kann sich die primäre Station ändern. Sie können mühelos feststellen, welche direkte Videoverbindung Ihre primäre Station ist.

## <a name="to-find-out-which-direct-video-connected-station-is-the-primary-station"></a>So ermitteln Sie, welche direkte, mit dem Video verbundene Station die primäre Station ist

1.  Schalten Sie alle Monitore ein, die direkt mit den Anzeige Adaptern des Computers (Grafikkarten) verbunden sind.

2.  Starten (oder Neustarten) des Multipoint Services-Computers, und sehen Sie, welcher Monitor die Startbildschirme anzeigt. Diese Station ist die primäre Station.

    > [!NOTE]
    > In einigen Fällen werden BIOS-Startinformationen gleichzeitig auf mehreren Monitoren angezeigt. In diesem Fall kann jeder Monitor als "primäre Station" betrachtet werden, um auf das BIOS zuzugreifen.