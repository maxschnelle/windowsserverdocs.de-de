---
title: MultiPoint-Stationen
description: Erfahren Sie mehr über Stationen im MultiPoint Services, einschließlich der verschiedenen Optionen für Benutzer
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f9f9d618-ccfe-41ea-a52c-00c3c7adb51a
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: e747826a7cd84521bc62e48abedf3092bf6d844c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855651"
---
# <a name="multipoint--stations"></a>MultiPoint-Stationen
In einer Umgebung mit MultiPoint Services-System *Stationen* sind die Benutzer-Endpunkte für die Verbindung mit dem Computer, auf dem MultiPoint Services ausgeführt wird. Jede Station bietet dem Benutzer eine unabhängige Windows 10-Umgebung. Die folgenden Station-Typen werden unterstützt:  
  
-   Im Video direkt verbundene Stationen  
  
-   Stationen mit USB-0 (null)-Client-verbunden (einschließlich USB-Over-Ethernet-0 (null)-Clients)  
  
-   RDP-Over-LAN verbundene Stationen (für rich-Client oder thin Client-Computern)  
  
Vollständige PCs, auf denen das MultiPoint-Connector installiert ist außerdem überwacht werden können und mithilfe von MultiPoint-Dashboard gesteuert. Unter Windows 10 kann den MultiPoint-Connector über die Systemsteuerung für Windows-Features aktiviert werden. 

Multipoint Services unterstützt eine beliebige Kombination dieser Typen Station, aber es wird empfohlen, einer Station eine Station Direct-Video-Verbindung werden die als die primäre Station dienen kann. Der Grund für diese Empfehlung ist Unterstützung von Szenarios erwarten können. Zum Beispiel das BIOS für die Interaktion mit dem System vor dem MultiPoint Services ausgeführt wird.  
  
## <a name="primary-stations-and-standard-stations"></a>Primäre Stationen und standard-Stationen  
Einer direkt verbundenen Video Station ist definiert als die *primäre Station*. Die verbleibenden Stationen werden als bezeichnet *standard Stationen*.  
  
Die primäre Station zeigt den Startbildschirmen aus, wenn der Computer eingeschaltet ist. Es bietet Zugriff auf Konfiguration und Problembehandlung von Informationen, die während des Startvorgangs nur zur Verfügung steht. Die primäre Station muss eine Station Direct-Video-Verbindung sein. Nach dem starten können Sie die primäre Station wie alle anderen MultiPoint-Station verwenden.  
  
## <a name="direct-video-connected-stations"></a>Im Video direkt verbundene Stationen  
Der Computer mit MultiPoint Services kann mehrere Grafikkarten, enthalten, von die jedes einen oder mehrere video Ports haben kann. Dadurch können Sie Monitore für mehrere Stationen direkt an den Computer anschließen. Tastaturen und Mäusen sind über USB-Hubs verbunden, die jeder Monitor zugeordnet sind. Diese Hubs werden als bezeichnet *station Hubs*. Andere Peripheriegeräte, z. B. Referenten, Kopfhörer oder USB-Speichergeräten können auch an einen stationshub verbunden werden, und stehen nur für den Benutzer, der diese Station.  
  
> [!IMPORTANT]  
> Es muss mindestens eine *Station Direct-Video-Verbindung* pro Server fungieren, wie die primäre Station, um den Startprozess angezeigt wird, wenn der Computer eingeschaltet ist.  
  
![Layout eines MultiPoint Services-USB-basierten Systems](./media/WMSMultiPointServerUSBSystemLayout.gif)  
  
**Abbildung 1** MultiPoint services-System mit vier Stationen mit Direct-Video-Verbindung  
  
### <a name="BKMK_PS2stations"></a>PS/2-Stationen  
Mit MultiPoint Services können Sie einen direkt verbundenen Videomonitor zum Erstellen einer Station PS/2 PS/2-Tastatur und Maus auf der Hauptplatine zuordnen. HD-analoge Audio auf der Hauptplatine ist die Audioinhalte zu diesem Typ der Station. Dies gilt nicht für Computer, es keine Jacks PS/2 auf der Hauptplatine gibt.  
  
## <a name="usb-zero-client-connected-stations"></a>Stationen mit USB-0 (null)-Client-verbunden  
Stationen mit USB-0 (null)-Client-Verbindung nutzen eine *USB-0 (null) Client* als stationshub. USB-0 (null)-Clients werden manchmal als einem multifunktionshub mit Video bezeichnet. Sie einen Hub, der mit dem Computer über ein USB-Kabel verbunden sind, und den Hubs in der Regel eine video-Monitor, einer Tastatur und Maus (PS/2 oder USB), Audio- und zusätzliche USB-Geräte unterstützen. Dieses Handbuch bezieht sich auf diese spezielle Hubs als USB 0 (null) Clients.  
  
Das folgende Diagramm zeigt eine MultiPoint-Server-System mit einer primären Station (direkte Video verbundene Station) und zwei zusätzliche USB-0 (null)-Client verbundene Stationen.  
  
![Verbundene USB-0 (null)-client](./media/WMS11_diagram7.gif)  
  
**Abbildung 2** MultiPoint Services-System mit einer primäre Station und zwei Stationen mit USB-0 (null)-Client-verbunden  
  
### <a name="usb-over-ethernet-zero-clients"></a>USB-Over-Ethernet-0 (null)-clients  
USB-Over-Ethernet-0 (null)-Clients sind eine Variation des USB-0 (null)-Clients, die USB über LAN an den MultiPoint Services-System zu senden. Diese Arten von USB-0 (null)-Clients auf ähnliche Weise funktionieren auf andere USB keine Clients, aber Sie sind nicht durch USB-Kabel Länge Maximalwerte beschränkt. USB-Over-Ethernet-0 (null)-Clients sind keine herkömmliche thin Clients, und sie werden als virtuelle USB-Geräte auf dem MultiPoint Services-System angezeigt. Wenn Sie diese Geräte verwenden zu können, finden Sie unter der Hersteller des Geräts für die spezifischen Leistungs- und Empfehlungen für die standortplanung. Die meisten Geräte haben eine Drittanbieter--Plug-In für MultiPoint-Manager, mit dem Sie zuordnen, und Verbinden von Geräten mit MultiPoint Services-Systems.  
  
## <a name="rdp-over-lan-connected-stations"></a>RDP-Over-LAN verbundene Stationen  
Thin Clients und traditionelle Desktop, Laptop oder Tablet-PCs können mit dem Computer mit MultiPoint Services über das lokale Netzwerk (LAN) mit Remote Desktop Protocol (RDP) oder ein proprietäres Protokoll und das Remotedesktopprotokoll verbinden. Anbieter. RDP-Verbindungen bieten eine Endbenutzer-Erfahrung, die alle anderen MultiPoint-Station sehr ähnlich ist, aber der Hardware des Computers dem lokalen Client verwendet. Erfahren Sie mehr über unsere remote desktop-Anwendungen verfügbar für Android, iOS, Mac und Windows in [Remotedesktopclients](../remote-desktop-services/clients/remote-desktop-clients.md). 
  
Clients und Geräten, auf denen Microsoft RemoteFX bieten ein umfangreiches multimedia-Erlebnis nutzen die Hardwarefunktionen Prozessor- und Video des lokalen thin-Client oder des Computers HD-Videos über das Netzwerk bereitstellen.  
  
Wenn Sie vorhandene LAN-Clients haben bieten MultiPoint Services eine schnelle und kostengünstige Möglichkeit, alle Benutzer gleichzeitig auf einem Windows 10-Benutzeroberfläche zu aktualisieren.  
  
Hinsichtlich der Bereitstellung und Verwaltung sind die folgenden Unterschiede vorhanden, bei der Verwendung von RDP-Over-LAN verbundene Stationen:  
  
-   Nicht beschränkt auf physischen entfernungen von USB-Verbindung  
  
-   Potenzial für ältere Computerhardware als Stationen wiederverwenden  
  
-   Skalierung auf eine höhere Anzahl von Stationen leichter. Jeder Client in Ihrem Netzwerk kann als Remotestation verwendet werden  
  
-   Keine Hardware, die über die MultiPoint-Manager-Konsole zur Problembehandlung  
  
-   Keine geteilten-Funktionalität.  
  
    Weitere Informationen finden Sie unter [Stationen mit geteilten Bildschirmen](#a-namebkmksplitscreenstationsasplit-screen-stations) weiter unten in diesem Thema  
  
-   Keine Station umbenennen oder die Konfiguration der automatischen Anmeldung über die MultiPoint-Manager-Konsole  
  
![Verbundene USB-Station ohne Clients](./media/Diagram1.gif)  
  
**Abbildung 3** MultiPoint Services-System mit RDP-Over-LAN verbundene Stationen  
  
## <a name="additional-configuration-options"></a>Zusätzliche Konfigurationsoptionen  
  
### <a name="BKMK_SplitscreenStations"></a>Stationen mit geteilten Bildschirmen  
MultiPoint Services bietet eine Option des Split-Bildschirm auf Computern mit Stationen Direct-Video-Verbindung oder andere Stationen mit USB-0 (null)-Client-verbunden. Monitornutzung mittels Split Screen bietet die Möglichkeit, eine zusätzliche Station pro Monitor zu erstellen. Statt zwei Monitore, können Sie einen Monitor mit zwei Station Hub Setups verwenden, um zwei Stationen mit einem Monitor zu erstellen. Sie können schnell die Anzahl der verfügbaren Stationen erhöhen, ohne den Erwerb zusätzlicher Monitore, USB-0 (null)-Clients oder Grafikkarten.  
  
Die Vorteile der Verwendung einer Stationen mit geteiltem Bildschirm können Folgendes enthalten:  
  
-   Reduzieren Kosten und Raumbedarf durch mehr Benutzern auf einem MultiPoint Services-System an.  
  
-   Zwei Benutzer können die Seite-an-Seite in einem Projekt zusammenarbeiten.  
  
-   Möglichkeit für einen Lehrer, ein Verfahren auf einer Station zu zeigen, während ein Student auf der anderen Station nachvollzieht.  
  
Jeder MultiPoint Services-station überwachen, die Auflösung von 1024 x 768 oder höher in zwei stationsbildschirmen aufgeteilt werden kann. Die beste Teilung Bildschirm benutzerfreundlichkeit wird ein große Bildschirm mit einer mindestauflösung von 1600 x 900 empfohlen. Eine kleine Tastatur ohne eine Zehnertastatur wird außerdem empfohlen, die zwei Tastaturen vor der Monitor anpassen können.  
  
Um Stationen mit geteilten Bildschirmen zu erstellen, richten Sie einer Station für im Video direkt verbundene Gruppen oder USB-0 (null)-Client-verbunden. Dann fügen Sie eine zusätzliche stationshub von Plug-in-Tastatur und Maus mit einem USB-Hub, der auf dem Server verbunden ist. Sie können dann die Station in zwei Stationen konvertieren, teilen den Bildschirm, und ordnen den neuen Hub, auf die Hälfte des Monitors mithilfe von MultiPoint-Manager. Die linke Hälfte des Bildschirms wird zu einer Station, und die rechte Hälfte wird eine zweite Station.  
  
Nachdem eine Station Teilen ist, kann ein Benutzer auf der linken Station anmelden, während eine andere Benutzer von der rechten Station anmeldet anmelden.  
  
![Stationen mit geteiltem Bildschirm](./media/WMS_diagram3.gif)  
  
**Abbildung 4** MultiPoint Services-System mit geteilten Bildschirms Stationen  
  
## <a name="BKMK_StationTypeComparison"></a>Vergleich von Station  
  
||Direkte Video verbunden|Verbundene USB-0 (null)-Client|RDP-Over-LAN-Verbindung|  
|-|--------------------------|-----------------------------|----------------------------|  
|Video-Leistung|Video aus Leistungsgründen empfohlen||Verwenden Sie thin Clients, die Unterstützung von RemoteFX für verbesserte Videoqualität auf niedriger Bandbreite|  
|Physische Einschränkungen|Begrenzung durch die Länge des Videos Kabel und USB-Hub und die Länge des Kabels (15 empfohlen Meter maximale Länge)|Begrenzt durch USB-Hub und die Länge der Cable (empfohlene 15 Meter maximale Länge)|Begrenzung durch die LAN-Verteilung|  
|Anzahl von Stationen zulässig |Begrenzung durch die Anzahl der verfügbaren PCIe-Slots auf der Hauptplatine Zeiten der video-Ports pro Grafikkarte|Gesamtanzahl von USB-0 (null)-Client-Hersteller beschränkt werden kann (Weitere Informationen finden Sie auf den Hinweis, der dieser Tabelle gezeigt).|Begrenzung durch verfügbaren Ports im Netzwerk-switch|  
|Geteilten Bildschirmen|Ja|Ja|Nein|  
|MultiPoint-Manager peripheren stationsstatus, Konfiguration der automatischen Anmeldung, station umbenennen|Ja|Ja|Nein|  
|Zugriff auf Server-Start-Menüs|Ja|Nein|Nein|  
  
> [!NOTE]  
> Die Gesamtanzahl der USB-0 (null)-Clients, die auf dem Server verbunden sind, unter Umständen vom Hersteller oder die Hardwarefunktion, von dem Computer, auf dem MultiPoint Services ausgeführt wird, eingeschränkt werden.