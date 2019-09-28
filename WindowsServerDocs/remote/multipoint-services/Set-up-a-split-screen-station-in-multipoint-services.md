---
title: Einrichten einer Station mit geteiltem Bildschirm
description: Hier wird beschrieben, wie Sie Multipoint Services einrichten, sodass zwei Benutzer ein einzelnes System gemeinsam verwenden können.
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35d1d434-79b2-4e0a-835f-d94ed8ee6b21
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: d50148e9d39fb337bf02d95d0db09b4e07ee4720
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71395039"
---
# <a name="set-up-a-split-screen-station"></a>Einrichten einer Station mit geteiltem Bildschirm
Sie können eine Split-Screen-Station einrichten, sodass zwei Benutzer gleichzeitig das System verwenden können.

Jeder Monitor mit einer Auflösung von mindestens 1200 x720, wenn er mit einer Station verbunden ist, die das Split-Screen-Feature unterstützt, kann in zwei Stationen aufgeteilt werden. Nachdem eine Station aufgeteilt wurde, wechselt der Desktop, der vom Monitor angezeigt wurde, in die linke Hälfte des Bildschirms, und in der rechten Hälfte des Bildschirms wird eine neue Station angezeigt. Um die Erstellung der neuen Station abzuschließen, müssen Sie der Station eine Tastatur, eine Maus und einen USB-Hub zuordnen. Nach dem Teilen einer Station kann sich ein Benutzer auf der linken Station anmelden, während sich ein anderer Benutzer auf der rechten Station anmeldet.  
  
Geteilte Bildschirm Stationen haben mehrere Vorteile:  
  
-   Sie können Kosten und Speicherplatz reduzieren, indem Sie mehr Benutzer in einem Multipoint Services-System berücksichtigen.  
  
-   Zwei Benutzer können nebeneinander in einem Projekt zusammenarbeiten.  
  
-   Ein Multipoint-Dashboardbenutzer kann eine Prozedur auf einer Station veranschaulichen, während ein Student auf der anderen Station dafolgt.  
  
Die folgende Abbildung zeigt ein Multipoint Services-System mit einer unterteilten Bildschirm Station (auf der rechten Seite).  
  
![Stationen mit geteiltem Bildschirm](./media/WMS_diagram3.gif)  
   
## <a name="requirements-for-a-split-screen-station"></a>Anforderungen für eine geteilte Bildschirm Station  
Zum Erstellen einer Split-Screen-Station müssen der Monitor und die Station die folgenden Anforderungen erfüllen:  
  
-   Der Monitor muss eine Auflösung von 1200 x720 oder höher aufweisen.  
  
-   Wenn Sie einen USB-over-Ethernet-Client verwenden, wenden Sie sich an den Hardwarehersteller, um herauszufinden, ob unterstützte Bildschirm Stationen unterstützt werden. Viele USB-over-Ethernet-Client Geräte verfügen über Einschränkungen, die Ihre Konfiguration als getrennte Bildschirm Stationen verhindern.  
  
## <a name="setting-up-a-split-screen-station"></a>Einrichten einer Split-Screen-Station  
Verwenden Sie die folgenden Verfahren, um einen zweiten Hub für eine Split-Screen-Station hinzuzufügen und die Station dann in Multipoint Services aufzuteilen. Das abschließende Verfahren erläutert, wie Sie eine Split-Screen-Station an eine einzelne Station zurückgeben.  
  
> [!NOTE]  
> Wenn Sie eine Station teilen, wird die aktive Sitzung auf der Station angehalten. Der Benutzer muss sich erneut bei der Station anmelden, um die Arbeit nach dem aufteilen wieder aufzunehmen.  
  
**So fügen Sie einen zweiten Hub mit Tastatur und Maus hinzu:**  
  
1.  Verbinden Sie einen USB-Hub mit einem geöffneten USB-Anschluss auf dem Computer, wie in der folgenden Abbildung dargestellt.  
  
    ![Abbildung der Multipoint Server-USB-Hub-Verbindung](./media/WMSUSBHubConnection.gif)  
  
2.  Verbinden Sie eine Tastatur und eine Maus mit dem USB-Hub.  
  
    ![Anschließen von Eingabegeräten an einen USB-Hub](./media/WMSUSBDeviceConnection.gif)  
  
3.  Verbinden Sie alle zusätzlichen Peripheriegeräte, z. b. Kopfhörer, mit dem USB-Hub.  
  
4.  Wenn Sie einen extern betriebenen Hub verwenden, verbinden Sie das Netzkabel des Hubs mit einer Stromversorgung.  
  
**So teilen Sie eine Station:**  
  
1.  Klicken Sie im Multipoint-Manager auf die Registerkarte **Stationen** .  
  
2.  Klicken Sie unter **Station**auf den Namen der Station, die Sie aufteilen möchten.  
  
3.  Klicken Sie unter **Aufgaben des ausgewählten Elements**auf **Station aufteilen**.  
  
    Der ursprüngliche Bildschirm wird in die linke Hälfte des Monitors verschoben, und auf der rechten Hälfte desselben Monitors wird der Bildschirm einer neuen Station erstellt.  
  
4.  Erstellen Sie die neue Station, indem Sie den angegebenen Buchstaben auf der neu hinzugefügten Tastatur entsprechend der Angabe anzeigen, wenn auf der rechten Hälfte des Monitors der Bildschirm zum **Erstellen einer Multipoint-Server Station** angezeigt wird.  
  
Nachdem eine Station aufgeteilt wurde, kann sich ein Benutzer an der linken Station anmelden, während sich ein anderer Benutzer an der rechten Station anmeldet.  
  
**So kehren Sie eine geteilte Station an eine einzelne Station zurück:**  
  
1.  Klicken Sie im Multipoint-Manager auf die Registerkarte **Stationen** .  
  
2.  Klicken Sie unter **Station**auf den Namen der Station, die Sie aufteilen möchten.  
  
3.  Klicken Sie unter **Aufgaben des ausgewählten Elements**auf die Option zum **Aufteilen der Station**.