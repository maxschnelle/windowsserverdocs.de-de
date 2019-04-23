---
title: Einrichten einer Station mit geteiltem Bildschirm
description: Beschreibt, wie MultiPoint Services einrichten, damit zwei Benutzer mit ein einzigen System freigeben können
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35d1d434-79b2-4e0a-835f-d94ed8ee6b21
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: b2d01df6175eee99fd1374cd5af270cbcc764ca8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849941"
---
# <a name="set-up-a-split-screen-station"></a>Einrichten einer Station mit geteiltem Bildschirm
Sie können einer geteilten Station einrichten, damit das System gleichzeitig in zwei Benutzer verwenden können.

Alle überwachen, die eine Auflösung von mindestens 1200 x 720, wenn eine Station angeschlossen, die die geteilten-Funktion unterstützt, kann in zwei Stationen geteilt werden. Nach dem Teilen einer Station, der Desktop, den der Monitor angezeigt haben, die auf die linke Hälfte des Bildschirms verschoben wird, und eine neue Station wird auf der rechten Hälfte des Bildschirms angezeigt. Zum Erstellen der neuen Station abgeschlossen haben, müssen Sie eine Tastatur, Maus und USB-Hub der Station zuordnen. Nach dem Teilen einer Station kann sich ein Benutzer auf der linken Station anmelden, während sich ein anderer Benutzer auf der rechten Station anmeldet.  
  
Stationen mit geteilten Bildschirmen haben mehrere Vorteile:  
  
-   Sie können die Kosten und Raumbedarf durch mehr Benutzern auf einem MultiPoint Services-System reduzieren.  
  
-   Zwei Benutzer können zusammen, parallel an einem Projekt zusammenarbeiten.  
  
-   Eine MultiPoint-Dashboardbenutzer kann ein Verfahren auf einer Station demonstrieren, während ein Student auf der anderen Station nachvollzieht.  
  
Die folgende Abbildung zeigt ein MultiPoint Services-System mit einer geteilten Bildschirms Station (rechts).  
  
![Stationen mit geteiltem Bildschirm](./media/WMS_diagram3.gif)  
   
## <a name="requirements-for-a-split-screen-station"></a>Anforderungen für eine Teilung Bildschirm station  
Zum Erstellen einer Stationen mit geteiltem Bildschirm müssen der Monitor und die Station, die folgenden Anforderungen erfüllen:  
  
-   Der Monitor benötigen eine Auflösung von 1200 X720 oder höher.  
  
-   Wenn Sie einen USB-Over-Ethernet-0 (null)-Client verwenden, wenden Sie sich an Ihren Hardwarehersteller, um herauszufinden, ob Stationen mit geteilten Bildschirmen unterstützt werden. Viele USB-Over-Ethernet-0 (null)-Client-Geräte haben Einschränkungen, die ihre Konfiguration als Stationen mit geteilten Bildschirmen zu verhindern.  
  
## <a name="setting-up-a-split-screen-station"></a>Das Einrichten einer Stationen mit geteiltem Bildschirm  
Verwenden Sie die folgenden Verfahren fügen Sie einen zweiten Hub für eine Stationen mit geteiltem Bildschirm hinzu, und klicken Sie dann teilen der MultiPoint Services-Station. Im letzten Schritt wird erläutert, wie eine geteilten Station eine einzelne Station zurückgegeben wird.  
  
> [!NOTE]  
> Wenn Sie eine Station teilen, wird die aktive Sitzung auf der Station angehalten. Der Benutzer muss melden Sie sich auf die Station erneut aus, um die Arbeit fortsetzen, nachdem die Teilung auftritt.  
  
**So fügen Sie einen zweiten Hub mit Tastatur und Maus hinzu:**  
  
1.  Verbinden Sie einen USB-Hub mit einem freien USB-Anschluss auf dem Computer, wie in der folgenden Abbildung dargestellt.  
  
    ![Abbildung des MultiPoint-Server-USB-Hub-Verbindung](./media/WMSUSBHubConnection.gif)  
  
2.  Verbinden Sie eine Tastatur und Maus, mit dem USB-Hub.  
  
    ![Anschließen von Eingabegeräten an einen USB-Hub](./media/WMSUSBDeviceConnection.gif)  
  
3.  Schließen Sie alle zusätzlichen Peripheriegeräte, (z.B. Kopfhörer) an den USB-Hub.  
  
4.  Wenn Sie einen extern ausgeschaltet Hub verwenden, verbinden Sie das Stromkabel des Hubs in eine Steckdose.  
  
**Um eine Station Teilen:**  
  
1.  MultiPoint-Manager, klicken Sie auf die **Stationen** Registerkarte.  
  
2.  Klicken Sie unter **Station**, klicken Sie auf den Namen der Station, die Sie aufteilen möchten.  
  
3.  Klicken Sie unter **ausgewählte Aufgaben für Elemente**, klicken Sie auf **Station teilen**.  
  
    Der ursprüngliche Bildschirm wird auf die linke Hälfte des Monitors verschoben, und eine neue Station-Bildschirm wird auf der rechten Hälfte des gleichen Monitors erstellt.  
  
4.  Erstellen die neue Station durch Drücken von den angegebenen Buchstaben auf der Tastatur neu hinzugefügten wie bei der **erstellen Sie eine MultiPoint Server-Station** Bildschirm wird angezeigt, in der rechten Hälfte des Monitors.  
  
Nachdem eine Station Teilen ist, kann ein Benutzer auf der linken Station anmelden, während eine andere Benutzer von der rechten Station anmeldet anmelden.  
  
**Um einer geteilten Station eine einzelne Station zurückzugeben:**  
  
1.  MultiPoint-Manager, klicken Sie auf die **Stationen** Registerkarte.  
  
2.  Klicken Sie unter **Station**, klicken Sie auf den Namen der Station aus, Sie nicht aufgeteilten möchten.  
  
3.  Klicken Sie unter **ausgewählte Aufgaben für Elemente**, klicken Sie auf **Stationsteilung**.