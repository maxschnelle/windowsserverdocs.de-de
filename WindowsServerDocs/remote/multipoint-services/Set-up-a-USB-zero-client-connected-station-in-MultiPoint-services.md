---
title: Einrichten einer Verbindung zwischen einem USB-Client und einem Client verbundenen Station in Multipoint Services
description: Erfahren Sie, wie Sie eine USB Zero-Client Station in Multipoint Services erstellen.
ms.date: 07/22/2016
ms.topic: article
ms.assetid: d2908865-6be3-474d-88f1-995f40bb61d0
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: e0db1c5013529e77aa757f086f842a1ad9007868
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953766"
---
# <a name="set-up-a-usb-zero-client-connected-station-in-multipoint-services"></a>Einrichten einer Verbindung zwischen einem USB-Client und einem Client verbundenen Station in Multipoint Services
Wenn Sie Multipoint Services-Stationen mithilfe von USB-Clients erstellen, wird der Monitor für jede Station mit dem Videoport auf dem USB Zero-Client verbunden, wie in der folgenden Abbildung dargestellt. Weitere Informationen zu diesem und anderen Stations Typen finden Sie unter [Multipoint-Stationen](MultiPoint-services-Stations.md).

**Multipoint Services-System mit einer direkt mit einem Video verbundenen Station und zwei mit zwei USB-Verbindungen verbundenen Stationen**

![Verbundene USB-Stationen ohne Clients](./media/WMS11_diagram7.gif)

> [!IMPORTANT]
> Stellen Sie sicher, dass Sie die neuesten Treiber für die Videokarten und den USB-Zero-Client installieren, bevor Sie die von einem Client verbundenen USB-Verbindungen einrichten. Veraltete Treiber können verhindern, dass die Multipoint Services-Konfiguration erfolgreich abgeschlossen wird. Anweisungen hierzu finden Sie unter [aktualisieren und Installieren von Gerätetreibern bei Bedarf](Update-and-install-device-drivers-if-needed.md).

> [!IMPORTANT]
> Wenn Sie einen USB-over-Ethernet-Client verwenden, befolgen Sie die Anweisungen Ihres Anbieters, anstatt dieses Verfahrens zu verwenden, um die Ethernet-Verbindung zum Einrichten des Geräts im Netzwerk zu verwenden.

### <a name="to-set-up-a-usb-zero-client-connected-station"></a>So richten Sie eine Verbindung mit USB-Client Verbindung ein

1.  Verbinden Sie das Videomonitor Kabel mit dem Bildschirm "DVI" oder "VGA Videodisplay Port" auf dem USB-Zero-Client, wie in der folgenden Abbildung dargestellt.

    ![Anschließen von Video an einem System mit USB-Hub](./media/WMSVideoConnection.gif)

2.  Verbinden Sie den USB-Null-Client mit einem geöffneten USB-Anschluss auf dem Computer.

    ![Abbildung der Multipoint Services-USB-Hub-Verbindung](./media/WMSUSBHubConnection.gif)

3.  Verbinden Sie eine Tastatur und eine Maus mit dem USB-Client.

    ![Anschließen von Eingabegeräten an einen USB-Hub](./media/WMSUSBDeviceConnection.gif)

4.  Wenn Sie einen extern betriebenen USB-Zero-Client verwenden, verbinden Sie das Netzkabel des USB Zero-Clients mit einer Stromversorgung.

5.  Stecken Sie das Stromkabel des Videomonitors in eine Steckdose.

6.  Wenn Sie aufgefordert werden, die Geräte der Station zuzuordnen, befolgen Sie die Anweisungen auf dem Monitor, um das Setup abzuschließen. (Im Allgemeinen werden den Stationen von USB-Clients, die mit dem Client verbunden sind, automatisch Stationen zugeordnet, wenn Sie Sie dem Server hinzufügen.)