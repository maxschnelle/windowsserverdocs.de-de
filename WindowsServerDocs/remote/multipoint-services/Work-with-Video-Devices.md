---
title: Arbeiten mit Videogeräten
description: Erfahren Sie, wie Videomonitore und Projektoren mit Stationen in Multipoint Services funktionieren.
ms.topic: article
ms.assetid: 2f7f5a97-efd2-4184-8ad3-cf029d615eab
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: d580185a2fc6adfb3bdf7acc160610aaf4d2b5b9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946833"
---
# <a name="work-with-video-devices"></a>Arbeiten mit Videogeräten
Erfahren Sie, wie Videogeräte, z.B. Monitore oder Projektoren, funktionieren, wenn sie an einen Computer in Ihrem MultiPoint Services-System oder an eine MultiPoint Services-*Station* angeschlossen werden.

## <a name="working-with-video-monitors"></a>Arbeiten mit Videomonitoren
In Abhängigkeit von Ihrer MultiPoint Services-Systemhardware gibt es zwei Möglichkeiten, um einen Videomonitor anzuschließen:

-   Verbinden Sie bei *USB-Hub-basierten Systemen*das Videomonitor Kabel mit einem geöffneten Videoport auf dem Computer, wie in der folgenden Abbildung dargestellt:

    ![Anschließen von Video an einem System mit USB-Hub](./media/WMSVideoConnection.gif)

-   Verbinden Sie das Videomonitor Kabel für *multifunktionshub-basierte Systeme* mit integrierter Videounterstützung mit dem Videoport auf dem multifunktionshub:

    ![Anschließen von Video an einen Multifunktionshub](./media/WMSMultifunctionHubVideoConnection.gif)

Weitere Informationen finden Sie im Thema [Einrichten einer Station](Set-Up-a-Station.md).

## <a name="working-with-video-projectors"></a>Arbeiten mit Videoprojektoren
Wenn ein großes Bild zur Anzeige für andere Benutzer projiziert werden soll – beispielsweise in einer Laborumgebung –, können Sie einen Videoprojektor an Ihr MultiPoint Services-System anschließen. Sowohl für USB Hub-basierte als auch für auf mehreren Funktionen basierende Hub-basierte Stationen haben Sie zwei Möglichkeiten, einen Projektor mit einer Station zu verbinden:

-   Ersetzen Sie einen Monitor durch einen Projektor, und verwenden Sie den Projektor als Anzeigegerät für diese Station, wie in der folgenden Abbildung gezeigt:

    ![Anschließen eines Projektors an einen Computer](./media/WMSVideoProjectorConnection.gif)

-   Erwerben Sie ein Video Splitter Gerät, um sowohl einen Projektor als auch einen Monitor mit dem Videoport der Station zu verbinden.

    In MultiPoint Services wird auf beiden Anzeigegeräten dasselbe Bild angezeigt. Wenn keine Projektion ausgeführt wird, können Sie den Projektor ausschalten und nur den Videomonitor verwenden.

Bei beiden Optionen müssen Sie Folgendes beachten:

-   Das Anschließen eines Videoanzeigegeräts kann erfordern, dass *die Station erneut zugeordnet* wird, damit das neue Anzeigegerät von MultiPoint Services richtig erkannt werden kann. Befolgen Sie die Anweisungen, die auf dem Videoanzeige Gerät der Station angezeigt werden.

-   Eventuell müssen Sie sich Adapter oder Konverter zur Signalumwandlung zwischen DVI- und VGA-Steckern besorgen.

-   Die Verwendung eines "Y"-Splitter Kabels kann die Videoqualität auf beiden Videogeräten verringern.

-   Wenn Sie einen Projektor und einen Monitor über ein "Y"-Splitter Kabel verwenden, passt Multipoint Services die Bildschirmauflösung beider Geräte an die niedrigste maximale Auflösung der beiden Geräte an – in der Regel den Projektor.

-   Multipoint Services unterstützt nicht die Erweiterung der Anzeige einer einzelnen Station über mehrere Monitore hinweg.

## <a name="see-also"></a>Weitere Informationen
[Verwalten der Stations Hardware](Manage-Station-Hardware.md) 
 [Einrichten einer Station](Set-Up-a-Station.md)