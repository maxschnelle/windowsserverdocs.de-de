---
title: Arbeiten mit USB-Geräten
description: Erfahren Sie, wie USB-Geräte mit Multipoint Services funktionieren.
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: a33f2b83-bbc2-4fc1-8a94-aaa985dfe1f9
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: d366e8c61da86d0e47b2ce99d08a2046c8f8bd0a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858033"
---
# <a name="work-with-usb-devices"></a>Arbeiten mit USB-Geräten
Sie können Geräte entweder an den Computer in Ihrem MultiPoint Services-System oder an einen MultiPoint-Stationshub anschließen. Der Standort, an dem ein Gerät angeschlossen wird, und die Art des Geräts wirken sich darauf aus, ob ein Gerät für alle Benutzer im System, nur für einzelne Benutzer oder für keinen Benutzer verfügbar ist. Nachfolgend finden Sie Beispiele für die verschiedenen Arten der Verbindung:  
  
-   Wenn Sie ein Gerät, wie z.B. einen Drucker oder ein USB-Massenspeichergerät, direkt an den Computer anschließen, können alle Sitzungsbenutzer im MultiPoint Services-System auf das Gerät zugreifen. Benutzer von virtuellen Desktopstationen können nicht auf direkt an den Computer angeschlossene Geräte zugreifen.  
  
-   Wenn Sie ein Gerät an einen Stationshub anschließen, z.B. eine Tastatur, eine Maus, ein *Audiogerät* oder ein Massenspeichergerät, ist das Gerät nur für den Benutzer verfügbar, der an dieser MultiPoint Services-Station angemeldet ist.  
  
-   Wenn Sie bestimmte Arten von Geräten an den Computer anschließen, z.B. eine Tastatur oder eine Maus, sind diese Geräte für keinen Benutzer im System verfügbar.  
  
Die folgende Tabelle zeigt wird eine Liste von Geräten mit ihrem jeweiligen Verhalten in Abhängigkeit vom Anschlussort im System. Informationen zum Verbinden von Stations Hubs finden Sie unter [Arbeiten mit Station Hubs](#working-with-station-hubs). Weitere Informationen zum Verbinden von Videomonitoren mit einer Station finden Sie unter [Arbeiten mit Videogeräten](Work-with-Video-Devices.md).  
  
|||||  
|-|-|-|-|  
|**Schutz**|**Verhalten, wenn es direkt mit dem Computer verbunden ist**|**Verhalten bei der Verbindung mit einer Station**|**Hinweise**|  
|Tastatur|Das direkte Anschließen einer Tastatur an den Computer wird nicht empfohlen.|Nur für den Stationsbenutzer verfügbar.|Wenn die Tastatur einen USB-Anschluss aufweist, wird der USB-Hub in der Tastatur möglicherweise als Stationshub verwendet. Andere mit diesem Anschluss verbundene USB-Geräte sind nur für den Benutzer verfügbar, der diese Tastatur verwendet.<p>Einige Stationshubs sind mit einem PS\/2-Mausanschluss ausgestattet, der im Hub in eine USB-Verbindung konvertiert wird.|  
|Maus|Das direkte Anschließen einer Maus an den Computer wird nicht empfohlen.|Nur für den Stationsbenutzer verfügbar.|Einige Stationshubs sind mit einem PS\/2-Mausanschluss ausgestattet, der im Hub in eine USB-Verbindung konvertiert wird.|  
|USB-Hub|Weitere Informationen finden Sie [unter Arbeiten mit Stations Hubs](#working-with-station-hubs).|Weitere Informationen finden Sie [unter Arbeiten mit Stations Hubs](#working-with-station-hubs).||  
|Videomonitor|Weitere Informationen finden Sie unter [Multipoint Services-Video Geräte](work-with-video-devices.md).|Weitere Informationen finden Sie unter [Multipoint Services-Video Geräte](work-with-video-devices.md).||  
|Audioausgabegeräte (z.B. Kopfhörer)|Das direkte Anschließen eines Audioausgabegeräts an den Computer wird nicht empfohlen.|Nur für den Stationsbenutzer verfügbar.|Einige Stationshubs sind mit einem analogen Audioanschluss ausgestattet, der im Hub in eine USB-Audioverbindung konvertiert wird.|  
|Audioeingabegeräte (z.B. Mikrofone)|Das direkte Anschließen eines Audioeingabegeräts an den Computer wird nicht empfohlen.|Nur für den Stationsbenutzer verfügbar.|Einige Stationshubs sind mit einem analogen Audioanschluss ausgestattet, der im Hub in eine USB-Audioverbindung konvertiert wird.|  
|Drucker|Für alle Benutzer im System verfügbar. *|Nur für den Stationsbenutzer verfügbar.||  
|USB-Massenspeichergerät|Für alle Benutzer im System verfügbar.\*|Nur für den Stationsbenutzer verfügbar.|Zu diesen Geräten gehören beispielsweise USB-Flashlaufwerke, externe Festplattenlaufwerke und Digitalkameras.|  
|Webkameras|Für alle Benutzer im System verfügbar. *|Nur für den Stationsbenutzer verfügbar.|Es kann immer nur ein Benutzer gleichzeitig eine Verbindung mit der Kamera herstellen.|  
  
\* Geräte, die mit dem Host Computer verbunden sind, sind für die Benutzer, die bei virtuellen Desktop Stationen angemeldet sind, nicht sichtbar.  
  
Weitere Informationen zum Einrichten einer Station finden Sie unter [Einrichten einer Station](Set-Up-a-Station.md).  
  
### <a name="working-with-station-hubs"></a>Arbeiten mit Stationshubs  
Es gibt vier Szenarien für die Verwendung eines USB-Hubs, wenn er an ein MultiPoint Services-System angeschlossen ist. Jedes der folgenden Szenarien bietet einen unterschiedlichen Zugriff auf die angeschlossenen Geräte, je nach Art des Hubs sowie des Verbindungsorts im System.  
  
-   Ein Stationshub, der mit dem Computer in Ihrem MultiPoint Services-System mit angeschlossener Tastatur verbunden ist, kann zum Erstellen einer MultiPoint Services-Station verwendet werden. Tastatur und Maus werden über die am Hub verfügbaren Anschlüsse mit dem Stationshub verbunden. Ein Videomonitor wird mit dem Videoanschluss des Computers oder, falls verfügbar, mit dem Videoadapter des Stationshubs verbunden. Tastatur, Maus und Monitor werden dann einer MultiPoint Services-Station *zugeordnet*.  
  
-   Ein USB-Hub, der mit dem Computer in Ihrem MultiPoint Services-System ohne angeschlossene Tastatur verbunden ist, kann verwendet werden, um zusätzliche Geräte an den Computer anzuschließen, wenn der Computer nicht über ausreichende Anschlüsse für die erforderlichen Geräte verfügt. Alle an diesen USB-Hub angeschlossenen Geräte sind für alle Benutzer des MultiPoint Services-Systems verfügbar. Hierbei handelt es sich nicht um einen MultiPoint Services-Stationshub.  
  
-   Über einen USB-Hub mit eigener Stromversorgung, der mit dem Computer in Ihrem MultiPoint Services-System verbunden ist – auch als Zwischenhub bezeichnet –, können zusätzliche USB-Hubs angeschlossen werden, die zum Erstellen von MultiPoint-Stationen verwendet werden.  
  
-   Über einen mit einem Stationshub verbundenen USB-Hub können zusätzliche Geräte an den Stationshub angeschlossen werden. Tastaturen müssen direkt an den Stationshub angeschlossen werden.  
  
Weitere Informationen zum Einrichten einer MultiPoint Services-Station finden Sie unter [Einrichten einer Station](Set-Up-a-Station.md).  
  
## <a name="see-also"></a>Weitere Informationen  
[Arbeiten mit Videogeräten](Work-with-Video-Devices.md)  
[Verwalten der Stationshardware](Manage-Station-Hardware.md)  
[Einrichten einer Station](Set-Up-a-Station.md)