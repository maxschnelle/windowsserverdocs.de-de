---
title: Verwalten der Stationshardware
description: Bietet einen Überblick über die Verwaltung von Hardware für Multipoint-Stationen.
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 429b8539-b17a-4e01-9576-860600466451
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 9ca65352a6f016d5d18bdd92b39b737cdddb9057
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71395237"
---
# <a name="manage-station-hardware"></a>Verwalten der Stationshardware
Ein Multipoint Services-System besteht aus einem einzelnen Computer und mindestens einer Station. Stations Hardware besteht in der Regel aus einem stationshub, einer Maus, einer Tastatur und einem Videomonitor. Stationen sind üblicherweise physisch mit dem Computer verbunden.  
  
Die folgende Abbildung zeigt ein Beispiellayout für ein MultiPoint Services-System mit vier Stationen. Jede Station ist mit dem Multipoint Services-Computer verbunden, indem ein USB-Hub und Multi-Monitor-Grafikkarten verwendet werden. Diese Abbildung stellt keine Stationen dar, die mithilfe von multifunktionshub Hubs verbunden sind.  
   
![Abbildung des USB-basierten Multipoint Services-systemlayouts](./media/WMSMultiPointServerUSBSystemLayout.gif)  
  
In den Themen dieses Abschnitts wird beschrieben, wie Sie den Status der an das MultiPoint Services-System angeschlossenen Hardware anzeigen können. Ferner erhalten Sie detaillierte Informationen zu den Arten von USB-Geräten und anderen Hardwareperipheriegeräten, mit denen eine MultiPoint Services-Station eingerichtet werden kann. Im Folgenden finden Sie eine kurze Beschreibung der in diesem Abschnitt enthaltenen Themen, mit deren Hilfe Sie Hardware auswählen und Ihre MultiPoint Services-Station einrichten können.  
  
## <a name="view-hardware-status"></a>Anzeigen des Hardwarestatus  
Im Multipoint-Manager können Sie die Registerkarte **Stationen** verwenden, um den Status der Stationen und Hardware Geräte anzuzeigen, die mit dem Multipoint Services-Computer verbunden sind. Weitere Informationen zum Anzeigen des Status Ihres MultiPoint Services-Computers und der daran angeschlossenen Hardwaregeräte finden Sie im Thema [Anzeigen des Hardwarestatus](View-Hardware-Status.md).  
  
## <a name="work-with-usb-devices"></a>Arbeiten mit USB-Geräten  
USB-Geräte und andere Hardwareperipheriegeräte im MultiPoint Services-System funktionieren unterschiedlich, je nachdem, ob sie an den MultiPoint Services-Computer oder eine MultiPoint Services-Station angeschlossen sind. Im Thema [Arbeiten mit USB-Geräten](Work-with-USB-Devices.md) wird beschrieben, wie unterschiedliche Hardwaregeräte in diesen Szenarios funktionieren können. Zudem bietet das Thema ausführliche Informationen für die Arbeit mit Stationshubs.  
  
## <a name="work-with-video-devices"></a>Arbeiten mit Videogeräten  
Im Thema [Arbeiten mit Videogeräten](Work-with-Video-Devices.md) wird erläutert, wie Videogeräte, z.B. Monitore oder Projektoren, funktionieren, wenn sie an einen Computer in Ihrem MultiPoint Services-System oder an eine MultiPoint Services-Station angeschlossen werden.  
  
## <a name="set-up-a-station"></a>Einrichten einer Station  
Im Thema [Einrichten einer Station](Set-Up-a-Station.md) wird beschrieben, wie die Hardwareperipheriegeräte an einen MultiPoint Services-Stationshub angeschlossen werden, um eine MultiPoint Services-Station zu erstellen. MultiPoint Services unterstützt zwei Typen von Stationshubs:  
  
-   Einen extern betriebenen oder Bus gestützten *USB-Hub* mit mehreren Ports, mit dem eine Maus, Tastatur und andere USB-Peripheriegeräte unterstützt werden können  
  
-   *Multifunktionshubs*, die mit einer integrierten Grafikkarte und Anschlüssen für Maus, Tastatur und Audioperipheriegeräte ausgestattet sein können.  
  
Beide Arten von Stationshubs werden über ein USB-Kabel an den Computer angeschlossen. Mit den Verfahren im Thema [Einrichten einer Station](Set-Up-a-Station.md) wird beschrieben, wie Hardwaregeräte an die unterschiedlichen Stationshubs angeschlossen werden.  
  
## <a name="see-also"></a>Siehe auch  
[Anzeigen des Hardwarestatus](View-Hardware-Status.md)  
[Arbeiten mit USB-Geräten](Work-with-USB-Devices.md)  
[Arbeiten mit Videogeräten](Work-with-Video-Devices.md)  
[Einrichten einer Station](Set-Up-a-Station.md)