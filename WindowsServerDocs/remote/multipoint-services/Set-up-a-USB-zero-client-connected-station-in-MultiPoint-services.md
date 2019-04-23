---
title: Einrichten einer USB zero Client verbundene Station in MultiPoint Services
description: Erfahren Sie, wie ein USB keine Client-Station in MultiPoint Services erstellen
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d2908865-6be3-474d-88f1-995f40bb61d0
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 1a64373f4ed5e0d1ac96a0257ac5697ff94ffcbe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878931"
---
# <a name="set-up-a-usb-zero-client-connected-station-in-multipoint-services"></a>Einrichten einer USB zero Client verbundene Station in MultiPoint Services
Wenn Sie USB-0 (null)-Clients verwenden, um MultiPoint Services-Stationen zu erstellen, ist der Monitor für jede Station Anschluss für die Grafikkarte auf dem Client USB-0 (null) verbunden, wie in der folgenden Abbildung dargestellt. Weitere Informationen zu diesen und anderen Station-Typen finden Sie unter [MultiPoint-Stationen](MultiPoint-services-Stations.md).
  
**MultiPoint Services-System mit einer direkt verbundenen Video Station und zwei USB-0 (null) Client verbundene Stationen**  
  
![Verbundene USB-Stationen ohne Clients](./media/WMS11_diagram7.gif)  
  
> [!IMPORTANT]  
> Bevor Sie USB zero Client verbundene Stationen einrichten, achten Sie darauf, dass Sie die neuesten Treiber für Ihre Grafikkarten und den USB-0 (null)-Client zu installieren. Veraltete Treiber können verhindern, dass die MultiPoint Services-Konfiguration nicht erfolgreich abgeschlossen. Anweisungen hierzu finden Sie unter [Update und Gerätetreiber installieren, bei Bedarf](Update-and-install-device-drivers-if-needed.md).  
  
> [!IMPORTANT]  
> Wenn Sie einen USB-Over-Ethernet-0 (null)-Client verwenden, befolgen Sie die Anweisungen Ihres Anbieters, anstatt diese Prozedur, die Ethernet-Verbindung verwenden, um das Gerät im Netzwerk einzurichten.  
  
### <a name="to-set-up-a-usb-zero-client-connected-station"></a>Zum Einrichten einer USB zero Client verbundene station  
  
1.  Kabel des Videomonitors der DVI- oder VGA-videoanzeigenschluss des USB-NULL-Client wie in der folgenden Abbildung dargestellt.  
  
    ![Abbildung einer Videoverbindung zu einem System mit USB Hub](./media/WMSVideoConnection.gif)  
  
2.  Verbinden Sie den USB-0 (null)-Client mit einem freien USB-Anschluss auf dem Computer an.  
  
    ![Abbildung des MultiPoint Services-USB-Hub-Verbindung](./media/WMSUSBHubConnection.gif)  
  
3.  Verbinden Sie eine Tastatur und Maus an den Client USB-0 (null).  
  
    ![Anschließen von Eingabegeräten an einen USB-Hub](./media/WMSUSBDeviceConnection.gif)  
  
4.  Wenn Sie einen extern ausgeschaltet USB-0 (null)-Client verwenden, verbinden Sie das Stromkabel des USB-0 (null)-Clients in eine Steckdose.  
  
5.  Stecken Sie das Stromkabel des Videomonitors in eine Steckdose.  
  
6.  Wenn Sie aufgefordert werden, die Geräte der Station zuordnen, befolgen Sie die Anweisungen auf dem Bildschirm, um das Setup abzuschließen. (Im Allgemeinen werden USB zero Client verbundene Stationen zugeordnet Stationen automatisch nach dem an den Server hinzufügen.)