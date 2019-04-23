---
title: Arbeiten mit USB-Geräten
description: Erfahren Sie, wie USB-Geräte mit MultiPoint Services
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a33f2b83-bbc2-4fc1-8a94-aaa985dfe1f9
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: f961f9270183b17855151f11ce222e3a5cc8df7d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883771"
---
# <a name="work-with-usb-devices"></a>Arbeiten mit USB-Geräten
Sie können Geräte entweder auf dem Computer in Ihrem MultiPoint Services-System oder an einen stationshub mit MultiPoint verbinden. Der Standort, an dem ein Gerät angeschlossen wird, und die Art des Geräts wirken sich darauf aus, ob ein Gerät für alle Benutzer im System, nur für einzelne Benutzer oder für keinen Benutzer verfügbar ist. Nachfolgend finden Sie Beispiele für die verschiedenen Arten der Verbindung:  
  
-   Wenn Sie ein Gerät, wie z.B. einen Drucker oder ein USB-Massenspeichergerät, direkt an den Computer anschließen, können alle Sitzungsbenutzer im MultiPoint Services-System auf das Gerät zugreifen. Benutzer von virtuellen Desktopstationen können nicht auf direkt an den Computer angeschlossene Geräte zugreifen.  
  
-   Wenn Sie ein Gerät an einen Stationshub anschließen, z.B. eine Tastatur, eine Maus, ein *Audiogerät* oder ein Massenspeichergerät, ist das Gerät nur für den Benutzer verfügbar, der an dieser MultiPoint Services-Station angemeldet ist.  
  
-   Wenn Sie bestimmte Arten von Geräten an den Computer anschließen, z.B. eine Tastatur oder eine Maus, sind diese Geräte für keinen Benutzer im System verfügbar.  
  
Die folgende Tabelle zeigt wird eine Liste von Geräten mit ihrem jeweiligen Verhalten in Abhängigkeit vom Anschlussort im System. Informationen zur Verwendung von stationshubs wird beschrieben, in [arbeiten mit stationshubs](#working-with-station-hubs). Weitere Informationen zum Herstellen von Videomonitoren an eine Station finden Sie unter [arbeiten mit Videogeräten](Work-with-Video-Devices.md).  
  
|||||  
|-|-|-|-|  
|**Gerät**|**Verhalten, wenn er direkt auf dem Computer verbunden ist**|**Verhalten, wenn sie eine Station angeschlossen ist**|**Hinweise**|  
|Tastatur|Das direkte Anschließen einer Tastatur an den Computer wird nicht empfohlen.|Nur für den Stationsbenutzer verfügbar.|Wenn die Tastatur einen USB-Anschluss aufweist, wird der USB-Hub in der Tastatur möglicherweise als Stationshub verwendet. Andere mit diesem Anschluss verbundene USB-Geräte sind nur für den Benutzer verfügbar, der diese Tastatur verwendet.<br /><br />Einige Stationshubs sind mit einem PS\/2-Mausanschluss ausgestattet, der im Hub in eine USB-Verbindung konvertiert wird.|  
|Maus|Das direkte Anschließen einer Maus an den Computer wird nicht empfohlen.|Nur für den Stationsbenutzer verfügbar.|Einige Stationshubs sind mit einem PS\/2-Mausanschluss ausgestattet, der im Hub in eine USB-Verbindung konvertiert wird.|  
|USB-Hub|Finden Sie unter [arbeiten mit stationshubs](#working-with-station-hubs).|Finden Sie unter [arbeiten mit stationshubs](#working-with-station-hubs).||  
|Videomonitor|Finden Sie unter [MultiPoint Services-Videogeräte](work-with-video-devices.md).|Finden Sie unter [MultiPoint Services-Videogeräte](work-with-video-devices.md).||  
|Audioausgabegeräte (z.B. Kopfhörer)|Das direkte Anschließen eines Audioausgabegeräts an den Computer wird nicht empfohlen.|Nur für den Stationsbenutzer verfügbar.|Einige Stationshubs sind mit einem analogen Audioanschluss ausgestattet, der im Hub in eine USB-Audioverbindung konvertiert wird.|  
|Audioeingabegeräte (z.B. Mikrofone)|Das direkte Anschließen eines Audioeingabegeräts an den Computer wird nicht empfohlen.|Nur für den Stationsbenutzer verfügbar.|Einige Stationshubs sind mit einem analogen Audioanschluss ausgestattet, der im Hub in eine USB-Audioverbindung konvertiert wird.|  
|Drucker|Zugriff für alle Benutzer auf dem System. *|Nur für den Stationsbenutzer verfügbar.||  
|USB-Massenspeichergerät|Zugriff auf alle Benutzer im System.\*|Nur für den Stationsbenutzer verfügbar.|Zu diesen Geräten gehören beispielsweise USB-Flashlaufwerke, externe Festplattenlaufwerke und Digitalkameras.|  
|Webkameras|Zugriff für alle Benutzer auf dem System. *|Nur für den Stationsbenutzer verfügbar.|Es kann immer nur ein Benutzer gleichzeitig eine Verbindung mit der Kamera herstellen.|  
  
* Geräte, die auf dem Hostcomputer verbunden sind, sind nicht sichtbar ist, für den Benutzer, die virtuellen desktopstationen angemeldet sind.  
  
Weitere Informationen zum Einrichten einer Station finden Sie unter [Einrichten einer Station](Set-Up-a-Station.md).  
  
### <a name="working-with-station-hubs"></a>Arbeiten mit Stationshubs  
Es gibt vier Szenarien für die Verwendung eines USB-Hubs, wenn er an ein MultiPoint Services-System angeschlossen ist. Jedes der folgenden Szenarien bietet einen unterschiedlichen Zugriff auf die angeschlossenen Geräte, je nach Art des Hubs sowie des Verbindungsorts im System.  
  
-   Ein Stationshub, der mit dem Computer in Ihrem MultiPoint Services-System mit angeschlossener Tastatur verbunden ist, kann zum Erstellen einer MultiPoint Services-Station verwendet werden. Tastatur und Maus werden über die am Hub verfügbaren Anschlüsse mit dem Stationshub verbunden. Ein Videomonitor wird mit dem Videoanschluss des Computers oder, falls verfügbar, mit dem Videoadapter des Stationshubs verbunden. Tastatur, Maus und Monitor werden dann einer MultiPoint Services-Station *zugeordnet*.  
  
-   Ein USB-Hub, der mit dem Computer in Ihrem MultiPoint Services-System ohne angeschlossene Tastatur verbunden ist, kann verwendet werden, um zusätzliche Geräte an den Computer anzuschließen, wenn der Computer nicht über ausreichende Anschlüsse für die erforderlichen Geräte verfügt. Alle an diesen USB-Hub angeschlossenen Geräte sind für alle Benutzer des MultiPoint Services-Systems verfügbar. Hierbei handelt es sich nicht um einen MultiPoint Services-Stationshub.  
  
-   Über einen USB-Hub mit eigener Stromversorgung, der mit dem Computer in Ihrem MultiPoint Services-System verbunden ist – auch als Zwischenhub bezeichnet –, können zusätzliche USB-Hubs angeschlossen werden, die zum Erstellen von MultiPoint-Stationen verwendet werden.  
  
-   Über einen mit einem Stationshub verbundenen USB-Hub können zusätzliche Geräte an den Stationshub angeschlossen werden. Tastaturen müssen direkt an den Stationshub angeschlossen werden.  
  
Weitere Informationen zum Einrichten einer MultiPoint Services-Station finden Sie unter [Einrichten einer Station](Set-Up-a-Station.md).  
  
## <a name="see-also"></a>Siehe auch  
[Arbeiten mit Videogeräten](Work-with-Video-Devices.md)  
[Verwalten der Stationshardware](Manage-Station-Hardware.md)  
[Einrichten einer Station](Set-Up-a-Station.md)