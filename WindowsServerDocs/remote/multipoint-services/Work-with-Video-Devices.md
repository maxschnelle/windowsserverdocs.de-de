---
title: Arbeiten mit Videogeräten
description: Erfahren Sie, wie die Video überwacht und Projektoren arbeiten mit Stationen im MultiPoint Services
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2f7f5a97-efd2-4184-8ad3-cf029d615eab
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: d828ea911aaff27a1df79d0380dfe92987c3d2aa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844201"
---
# <a name="work-with-video-devices"></a>Arbeiten mit Videogeräten
Erfahren Sie, wie Videogeräte, z.B. Monitore oder Projektoren, funktionieren, wenn sie an einen Computer in Ihrem MultiPoint Services-System oder an eine MultiPoint Services-*Station* angeschlossen werden.  
  
## <a name="working-with-video-monitors"></a>Arbeiten mit Videomonitoren  
In Abhängigkeit von Ihrer MultiPoint Services-Systemhardware gibt es zwei Möglichkeiten, um einen Videomonitor anzuschließen:  
  
-   Für *USB-Hub-basierten Systemen*, Kabel des Videomonitors einem freien Videoanschluss auf dem Computer, wie in der folgenden Abbildung gezeigt:  
  
    ![Abbildung einer Videoverbindung zu einem System mit USB Hub](./media/WMSVideoConnection.gif)  
  
-   Für *Multi-Factor-Hub-basierten Systemen* mit integrierter Unterstützung für video, das Kabel des Videomonitors an den video-Anschluss des multifunktionshubs an:  
  
    ![Anschließen von Video an einen Multifunktionshub](./media/WMSMultifunctionHubVideoConnection.gif)  
  
Weitere Informationen finden Sie im Thema [Einrichten einer Station](Set-Up-a-Station.md).  
  
## <a name="working-with-video-projectors"></a>Arbeiten mit Videoprojektoren  
Wenn ein großes Bild zur Anzeige für andere Benutzer projiziert werden soll – beispielsweise in einer Laborumgebung –, können Sie einen Videoprojektor an Ihr MultiPoint Services-System anschließen. Für beide USB-Hub-basiertes und Multi-Factor Hub-basiertes Stationen haben Sie zwei Optionen zum Herstellen einer Verbindung einer Station mit einem Projektor ein:  
  
-   Ersetzen Sie einen Monitor durch einen Projektor, und verwenden Sie den Projektor als Anzeigegerät für diese Station, wie in der folgenden Abbildung gezeigt:  
  
    ![Abbildung eines an einen Computer angeschlossenen Projektors](./media/WMSVideoProjectorConnection.gif)  
  
-   Besorgen Sie sich einen Videosplitter, um sowohl einen Projektor als auch einen Monitor mit dem Videoanschluss der Station verbinden zu können.  
  
    In MultiPoint Services wird auf beiden Anzeigegeräten dasselbe Bild angezeigt. Wenn keine Projektion ausgeführt wird, können Sie den Projektor ausschalten und nur den Videomonitor verwenden.  
  
Bei beiden Optionen müssen Sie Folgendes beachten:  
  
-   Das Anschließen eines Videoanzeigegeräts kann erfordern, dass *die Station erneut zugeordnet* wird, damit das neue Anzeigegerät von MultiPoint Services richtig erkannt werden kann. Befolgen Sie die Anleitungen, die auf dem Videoanzeigegerät der Station angezeigt werden.  
  
-   Eventuell müssen Sie sich Adapter oder Konverter zur Signalumwandlung zwischen DVI- und VGA-Steckern besorgen.  
  
-   Die Verwendung eines „Y“-Splitterkabels kann die Videoqualität auf beiden Videogeräten verschlechtern.  
  
-   Bei Verwendung eines Projektors und eines Monitors über ein „Y“-Splitterkabel passt MultiPoint Services die Bildschirmauflösung beider Geräte auf die niedrigste Maximalauflösung eines der beiden Geräte an. In der Regel ist dies der Projektor.  
  
-   Das Erweitern der Anzeige einer einzelnen Station auf mehrere Monitore wird von MultiPoint Services nicht unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
[Verwalten der Stationshardware](Manage-Station-Hardware.md)  
[Einrichten einer Station](Set-Up-a-Station.md) 