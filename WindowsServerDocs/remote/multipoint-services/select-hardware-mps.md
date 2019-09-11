---
title: Auswählen von Hardware für Ihr MultiPoint Services-System
description: Überlegungen zur Hardware für Multipoint Services
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e74961a2-bd38-48ae-b1c0-4b3eff761b4a
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 697ab9a1f97eab399dafac4e0c5fa5b641ed841c
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871399"
---
# <a name="selecting-hardware-for-your-multipoint-services-system"></a>Auswählen von Hardware für Ihr MultiPoint Services-System
Wenn Sie ein Multipoint Services-System erstellen, sollten Sie einen Computer auswählen, der die Systemanforderungen für Windows Server 2016 erfüllt. Wenn Sie entscheiden, welche Komponenten ausgewählt werden sollen, berücksichtigen Sie Folgendes:  
  
-   Der Ziel Preisbereich ihrer gesamten Lösung.  
  
-   Die Typen von Verwendungs Szenarios, die Sie möglicherweise für das Multipoint Services-System erwarten, z. b. ob die Benutzer Multimedia-Programme ausführen und Textverarbeitungs-oder Produktivitäts Programme ausführen oder das Internet durchsuchen.  
  
-   Gibt an, ob Ihr Szenario große Verarbeitungs-oder Arbeitsspeicher Anforderungen hat.  
  
-   Die Anzahl der Benutzer, die das System gleichzeitig verwenden können. Wenn Sie planen, gleichzeitig viele Benutzer in Ihrem System zu verwenden, oder Benutzer, die System intensive Programme verwenden, sollten Sie für Ihr System mehr Rechenleistung planen.  
  
-   Der Typ der Stationen. Wie viele USB-Ports oder videports benötigen Sie?  
  
-   Zukünftige Erweiterungspläne. Planen Sie, dem Multipoint Services-System zu einem späteren Zeitpunkt Stationen hinzuzufügen? Verfügen Sie über genügend Videokarten Slots, USB-Anschlüsse oder Netzwerktaps? Wie viele zusätzliche Benutzer müssen von Ihrer Hardware unterstützt werden?  
  
-   Physisches Layout. Weitere Informationen finden Sie unter [Planung von Multipoint Services-Websites](MultiPoint-services-Site-Planning.md).  
  
Ein Multipoint Services-System umfasst in der Regel die folgenden Komponenten:  
  
-   Ein Computer, auf dem Multipoint Services ausgeführt wird, der CPU, RAM, Festplattenlaufwerke und Grafikkarten umfasst.  
  
-   Einen Monitor, einen stationshub, eine Tastatur und eine Maus für jede Station.  
  
-   Optionale Peripheriegeräte für die Multipoint Services-Stationen, einschließlich Referenten, Kopfhörer, Mikrofon oder Speichergeräte, die nur für den Benutzer der Station verfügbar sind.  
  
-   Optionale Peripheriegeräte, die für alle Benutzer des Multipoint Services-Systems verfügbar sind, die direkt mit dem Host Computer verbunden sind, z. b. Drucker, externe Festplattenlaufwerke und USB-Speichergeräte.  
  
Verwenden Sie die folgenden Informationen, um Hardware Entscheidungen zu treffen:  
  
-   [Auswählen einer CPU](#selecting-a-cpu)  
-   [Auswählen von Hardwarekomponenten](#selecting-hardware-components)  
  
## <a name="selecting-a-cpu"></a>Auswählen einer CPU  
Bei einem Multipoint Services-System handelt\-es sich um eine Umgebung mit mehreren Benutzern, bei der alle Benutzer mit einem einzelnen Host Computer verbunden sind. Dadurch erhöht sich die CPU-Auslastung, da alle Benutzer denselben Computer gemeinsam verwenden. Einige Aufgaben, z. b. \(Multimedia-Programme, z. b\-. Medien\)Player oder Videobearbeitungssoftware, haben größere Verarbeitungsanforderungen. Stellen Sie daher sicher, dass Sie eine CPU auswählen, mit der die Verarbeitungsanforderungen für die Anzahl der Benutzer und Typen von Benutzer Szenarien, die unterstützt werden müssen, erfüllt werden können.  
  
Multipoint Services erfordert eine x64\--basierte CPU und muss die Systemanforderungen für den Computer erfüllen, wie unter [Hardware Anforderungen und Empfehlungen zur Leistung](Hardware-Requirements-and-Performance-Recommendations.md)beschrieben.  
  
Die folgenden Prozessoren wurden für die Verwendung in einem Multipoint Services-System mit\-Programmen für die Bedarfs gesteuerte Verarbeitung getestet, wie z. b. Multimedia-Programme:  
  
-   **Dual\--Core-Prozessor:** Kann bis zu acht Stationen unterstützen.  
-   **Quad\--Core-Prozessor:** Unterstützt bis zu 16 Stationen.
-   **Quad\--Core-Prozessor mit Multithreading:** Unterstützt bis zu 20 Stationen.      
-   **Sechs\-Kern Prozessor mit Multithreading:** Von können bis zu 24 Stationen unterstützt werden.  
  
Wählen Sie mit diesen Informationen eine CPU aus, die den Verarbeitungsanforderungen Ihres Multipoint Services-Systems entspricht. 
> [!NOTE] 
> Wenn Sie Video intensive Anwendungen ausführen, wird empfohlen, mindestens einen Kern pro Station zu haben. 
  
## <a name="selecting-hardware-components"></a>Auswählen von Hardwarekomponenten  
Beachten Sie bei der Erstellung eines Multipoint Services-Systems die folgenden Hardwarekomponenten, die Sie möglicherweise benötigen:  
  
-   Video Hardware  
  
-   Hardware der Multipoint Services-Station  
  
    -   *USB-Hubs*  
  
    -   USB-Clients  
  
    -   Tastatur und Maus Geräte  
  
    -   Monitore  
  
-   Peripheriegeräte  
  
    -   Audiogeräte, z. b. Sprecher und Kopfhörer  
  
    -   Mikrofone  
  
    -   USB-Massenspeicher Geräte  
  
Wenn Sie die Hardwarekomponenten für das Multipoint Services-System ausgewählt haben, stellen Sie sicher, dass Sie aktuelle\-64-Bit-Treiber für die-Komponenten erhalten.  
  
Die folgenden Themen enthalten ausführliche Informationen, die Ihnen bei der Auswahl von Komponenten für Ihr Multipoint Services-System helfen:  
  
[Auswählen der Video Hardware](#selecting-video-hardware)  
[Auswählen von\-direkt\-Video verbundenen oder USB-Client Station-Geräten](#BKMK_Selectingdirect-video-connectedorUSBzeroclientstationdevices)   
[Auswählen anderer Stations Peripheriegeräte](#selecting-other-station-peripheral-devices)  
[Auswählen von\-RDP\-over\-LAN-Connected Station-Hardware](#BKMK_SelectingRDP-over-LAN-connectedstationhardware)  
[Auswählen von Audiogeräten](#selecting-audio-devices)  
  
## <a name="selecting-video-hardware"></a>Auswählen der Video Hardware
Die von Ihnen ausgewählte Video Hardware sollte die Anzahl der Monitore unterstützen, die Sie für die Anzahl der Benutzer benötigen, die an Multipoint Services-Stationen arbeiten möchten. Darüber hinaus können unterschiedliche Arten von Video Hardware eine leistungsfähigere\-Lösung für Grafik\-intensive Programme, z. b. Multimedia-Inhalte, bereitstellen.  
  
Wählen Sie die Video Hardware aus, die die maximale Anzahl von Monitoren für die Art der von Ihrem Multipoint Services-System benötigten Leistung unterstützen kann. Stellen Sie sicher, dass Sie die Leistung der Video Hardware, die Sie ausgewählt haben, überprüfen, um sicherzustellen, dass Sie Ihren Leistungsanforderungen entspricht.  
  
> [!NOTE]  
> Sie müssen einen Videotreiber installieren, der die Erweiterung des Desktops auf mehrere Monitore unterstützt.  
  
Die Video Hardware Optionen umfassen Folgendes:  
  
-   Interne Grafikkarten, die eine PCI-oder PCIe-Busschnittstelle verwenden  
  
-   Externe Videocontroller, die über USB verbunden sind  
  
In den folgenden Abschnitten werden die Funktionen der einzelnen Video Hardwaretypen beschrieben. Sie können interne Grafikkarten und externe Videocontroller kombinieren, um das gewünschte System zu erstellen.  
  
### <a name="internal-video-cards"></a>Interne Grafikkarten  
Eine interne Grafikkarte ist an\-der Hauptplatine des Computers angeschlossen. Die interne Grafikkarte ist eine Lösung, die die Leistung von Grafik\-intensiven Multimedia-Programmen unterstützen kann. Eine interne Grafikkarte erfordert jedoch einen verfügbaren PCI-oder PCIe-Slot\-, um an die Hauptplatine angeschlossen zu werden. Viele High\-Performance-Grafikkarten erfordern einen PCIe-Slot, aber es gibt eine begrenzte Anzahl von PCIe-Slots auf einem Motherboard. Sie sollten wissen, welche Art von Grafikkarten Slots auf Ihrem Computer verfügbar sind, damit Sie den richtigen Typ von Grafikkarten erwerben können.  
  
Die Anzahl der Monitore, die eine Verbindung mit den einzelnen Grafikkarten herstellen können, hängt von der GPU, die auf der Karte verwendet wird, und der Anzahl der unterstützten Ports ab, die in der Regel zwischen 2 und 6 liegen.  
  
Wenn Sie interne Grafikkarten auswählen, wählen Sie Grafikkarten aus, die die Anzahl der Monitore unterstützen, die zum Erstellen der gewünschten Anzahl an direkt mit dem Video verbundenen Stationen erforderlich sind. Die maximale Anzahl von Monitoren, die unterstützt werden können, ist gleich der Anzahl der internen Grafikkarten,\-die an die Hauptplatine angeschlossen sind, multipliziert mit der Anzahl der Überwachungsports auf den einzelnen Grafikkarten. Wenn Sie z. b. über zwei interne Grafikkarten verfügen und jede Karte über zwei Überwachungsports verfügt, können Sie bis zu vier Monitore unterstützen.    
  
### <a name="external-video-controllers"></a>Externe Videocontroller  
USB-Clients enthalten einen externen Videocontroller, um eine Verbindung zwischen einem Monitor und dem Client herzustellen. Der USB Zero-Client kann auch Verbindungen für Kopfhörer, Referenten, ein Mikrofon oder andere Peripheriegeräte enthalten.  
  
Wählen Sie einen USB-Client aus, wenn Sie die Unterstützung für zusätzliche Monitore aktivieren möchten, ohne den Computer zu öffnen, oder wenn Sie mehr Stationen als verfügbare Video Ausgaben unterstützen möchten. Wenn Sie z. b. zuvor vier Monitore an\-interne Grafikkarten angeschlossen haben und zwei weitere Monitore hinzufügen möchten, können Sie zwei externe Video\-Controller an den Computer anschließen und Platz für zwei weitere Monitore haben. Auf diese Weise können Sie einen USB-Zero-Client mit dem Videocontroller kombinieren und keine zusätzlichen PCI-oder PCIe-Slots auf der Hauptplatine verwenden.  
  
## <a name="BKMK_Selectingdirect-video-connectedorUSBzeroclientstationdevices"></a>Auswählen von\-direkt\-Video verbundenen oder USB-Client Station-Geräten  
Eine Multipoint Services-Station besteht aus einem stationshub oder einem USB-Client, bei dem\-eine Tastatur und eine Maus angeschlossen sind,\-sowie ein Monitor, der auf dem Host Computer oder an einem USB-Client angeschlossen ist. Andere Peripheriegeräte können an den\-stationshub oder den USB-Client angeschlossen werden, sind jedoch nicht erforderlich, um eine Multipoint-Station zu erstellen. Diese anderen Peripheriegeräte werden unter [Auswählen anderer Station-Peripheriegeräte](#selecting-other-station-peripheral-devices)beschrieben.  
  
Die Geräte, die Sie zum Erstellen einer Multipoint Services-Station auswählen, müssen die Mindestanforderungen erfüllen, um mit Multipoint Services arbeiten zu können. Ausführliche Informationen zu den Anforderungen für die folgenden Multipoint Services-Stations Geräte finden Sie in diesem Thema:  
  
-   [Auswählen von USB-Hubs](#selecting-usb-hubs)  
-   [Auswählen von USB-Clients](#selecting-usb-zero-clients)  
-   [Auswählen von Tastaturen und Maus Geräten](#selecting-keyboards-and-mouse-devices)  
-   [Auswählen von Monitoren](#selecting-monitors)  
  
### <a name="selecting-usb-hubs"></a>Auswählen von USB-Hubs  
Die in einem Multipoint Services-System verwendeten USB-Hubs können ein generischer USB-Hub sein. Solche Hubs verfügen in der Regel über vier oder mehr USB-Anschlüsse, sodass mehrere USB-Geräte mit einem einzelnen USB-Anschluss auf dem Computer verbunden werden können. Einige andere Geräte, wie z. b. Tastaturen und Videomonitore, können auch einen USB-Hub in Ihren Entwurf integrieren.  
  
Ein weiterer Aspekt ist die Verwendung eines *extern betriebenen* Hubs anstelle eines *busgestützten\-* Hubs. Bei einem Bus\--gestützten Hub muss die Menge an aktuellen, die vom Host Computer bereitgestellt wird, ausreichen, um allen Peripheriegeräten, die mit dem Hub\-verbunden sind, die Leistung zu gewährleisten, ohne dass die Systemleistung beeinträchtigt wird. Ein extern gestützter Hub ermöglicht es Ihnen, mehr Peripheriegeräte zu verbinden und ausreichend Leistung für alle bereitzustellen. Die Verwendung extern gestützter Hubs kann dabei helfen, Leistungsprobleme, Port Ausfälle und andere vorübergehende Probleme zu vermeiden.  
  
Wenn Sie einen USB-Hub für Ihr Multipoint Services-System auswählen, sollten Sie dessen Verwendung in Erwägung gezogen. Der Hub kann als *stationshub*, als *Zwischenhub*oder als downstreamhubverwendet werden. In der folgenden Tabelle finden Sie Beschreibungen zu den einzelnen Hub-Typen. Wir empfehlen, dass alle USB-Geräte USB-2,0 oder höher sind.
  
||Fahrzeuge|  
|-|-----------|  
|Stationshub|Kann durch Busbetrieb\-betrieben werden, es sei denn,\-es werden hoch\-geschaltete Geräte daran angeschlossen, oder ein downstreamhub wird mit dem Gerät verbunden.|  
|Zwischenhub |Sollte extern eingeschaltet werden|  
|Downstream-Hub|Kann abhängig von den Geräten, die an den Hub angeschlossen\-sind, extern oder mit Busbetrieb betrieben werden.|  
|Aktives USB-Extender-Kabel|Aktive USB-Kabel, die einen USB-Hub enthalten, werden in der Regel durch busgestützte Daher empfiehlt es sich nicht, Station Hubs mit dem Computer zu verbinden.|  
  
### <a name="selecting-usb-zero-clients"></a>Auswählen von USB-Clients  
Ein USB-Null-Client ist ein USB-Hub, der eine Videoausgabe enthält. Daher kann ein Monitor über eine USB-Verbindung mit dem Computer verbunden werden. Weitere Informationen zur Verwendung von USB-Clients für Videos finden Sie unter [Auswählen von Video Hardware](#selecting-video-hardware) in diesem Dokument. Ein USB-Null-Client kann auch die Verbindung einer Vielzahl von USB-und\-nicht-USB-Geräten mit dem Hub ermöglichen. USB-Clients werden von bestimmten Hardwareherstellern erstellt und erfordern die Installation eines Geräte\-spezifischen Treibers.  
  
### <a name="selecting-keyboards-and-mouse-devices"></a>Auswählen von Tastaturen und Maus Geräten  
Die Tastatur-und Maus Geräte, die\-Sie an die Station anschließen, sind in der Regel USB-Geräte. Einige USB-Clients stellen PS\/2-Ports bereit. in diesem Fall sollten die Tastatur und die Maus\/PS 2 verwenden, um eine Verbindung mit dem stationshub herzustellen. Sie\/können auch eine PS 2-Tastatur und-Maus verwenden, wenn Sie eine direkte\/\-PS 2-\-Video Station einrichten.  
  
Eine Tastatur mit einem internen Hub kann als stationshub verwendet werden. Allerdings müssen alle anderen Stations Geräte mithilfe von Ports auf der Tastatur eine Verbindung mit dem internen Hub herstellen. Wenn eine solche Tastatur über einen anderen Hub mit dem Computer verbunden ist, wird dieser Hub als Zwischenhub behandelt.  
  
Wenn Sie unterteilte\-Bildschirm Stationen verwenden, empfiehlt es sich, eine Mini Tastatur zu verwenden, die keinen Zahlenbereich hat, sodass die beiden Tastaturen vor dem Monitor passen.  
  
### <a name="selecting-monitors"></a>Auswählen von Monitoren  
Für jede Multipoint Services-Station sollte ein Monitor bereitgestellt werden, es sei\-denn, es ist ein geteilter Bildschirm geplant. Monitore werden mit der Grafikkarte auf dem Computer, dem USB Zero-Client oder dem LAN\--basierten Client verbunden. Alle Monitor Typen, die von der Grafikkarte, dem USB Zero-Client oder dem LAN\--basierten Client unterstützt werden, können verwendet werden, einschließlich CRT-Monitoren.  
  
Einige besondere Monitore umfassen einen internen LAN\--basierten Client oder einen USB-Client. Diese Monitore enthalten normalerweise Audioeingabe\/-Ausgabe-und interne USB-Hubs zum Verbinden von Tastaturen und Mäusen. Sie stellen eine Verbindung mit dem Server über eine USB-oder LAN-Verbindung her.  
  
#### <a name="display-resolution"></a>Anzeigeauflösung  
Die unterstützte Mindestauflösung für den Anzeigebereich einer Station beträgt 512 x 768 Pixel. Wenn das Multipoint Services-System gestartet wird und feststellt, dass der Anzeigebereich einer Station kleiner als die minimale Auflösung ist, wird ein leerer Bildschirm auf dieser Station angezeigt, und die Station kann nicht verwendet werden.  
  
Wenn ein Anzeige Monitor von zwei Stationen als geteilte\-Bildschirm Stationen gemeinsam genutzt wird, ist die Mindestanforderung für die Anzeige 1024 x 768, sodass die resultierenden einzelnen Stations Bildschirmbereiche mindestens 512 x 768 sind. Für eine optimale\-Benutzer Darstellung auf dem Bildschirm wird ein breit Bildschirm mit einer minimalen Auflösung von 1600 x 900 empfohlen.  
  
## <a name="selecting-other-station-peripheral-devices"></a>Auswählen anderer Stations Peripheriegeräte  
Multipoint Services unterstützt Peripheriegeräte, die mit einem stationshub, einem USB-Null-Client oder direkt mit dem Computer verbunden sind. Geräte, die an einen stationshub angeschlossen sind, werden dieser bestimmten Station zugeordnet. Andere Geräte sind für jede Station verfügbar, wenn Sie direkt an den Computer angeschlossen sind. LAN-Clients können auch Peripheriegeräte unterstützen.  
  
> [!IMPORTANT]  
> Eine Tastatur kann nicht mit einem downstreamhub \(verbunden werden, z\). b. einem Hub, der an einen stationshub angeschlossen ist. Wenn Sie eine Tastatur an einen Downstream-Hub anschließen, sind alle Peripheriegeräte, die\-an den downstreamhub angeschlossen sind, für diese Station nicht mehr verfügbar. Dieses Verhalten ermöglicht die Unterstützung von\-mit Daisy verketteten Stations Hubs.  
  
**Für alle Stationen verfügbar** Ein USB-Gerät, das z. b \(. an den Computer angeschlossen ist, nicht\) über einen stationshub, ist für alle Stationen verfügbar. Abhängig vom Gerät kann es von mehreren Benutzern gleichzeitig verwendet werden, oder es kann jeweils nur ein Benutzer darauf zugreifen. In der folgenden Tabelle wird erläutert, wie auf USB-Geräte zugegriffen werden kann.  
  
> [!NOTE]  
> Die Spalte "verbunden mit Host Computer" in der Tabelle bezieht sich auf das Verhalten, wenn der Computer, auf dem Multipoint Services ausgeführt wird, im Stations Modus mit Stationen ausgeführt wird. Wenn Sie im Konsolenmodus ausgeführt werden, Verhalten sich die Peripheriegeräte, die an einem beliebigen Ort angeschlossen sind, genauso wie ein Standard Server in einer Konsolen Sitzung.  
  
||Verbunden mit Host Computer|Verbunden mit stationshub oder downstreamhub|  
|-|------------------------------|----------------------------------------------|  
|Tastatur|Nicht funktionsfähig, es sei denn, Sie ist Teil einer PS/2-Station. |Für einzelne Station verfügbar<br /><br />Es kann keine Verbindung mit einem Downstream-Hub hergestellt werden.|  
|Maus|Nicht funktionsfähig, es sei denn, Sie ist Teil einer PS/2-Station. |Für einzelne Station verfügbar|  
|Redner/Kopfhörer|Nicht funktionsfähig, es sei denn, Sie ist Teil einer PS/2-Station.|Für einzelne Station verfügbar|  
|USB-Speichergerät|Für alle Stationen verfügbar|Für einzelne Station verfügbar|  
|HID-Consumersteuerelement|Nicht funktionsfähig|Für einzelne Station verfügbar|  
|Andere USB-Geräte, z. b. Kameras, Dokument Leser und DVD-Laufwerke|Verfügbar für alle Stationen, sofern von Windows Server 2012 unterstützt|Verfügbar für alle Stationen, wenn dies von Windows Server 2008 R2 unterstützt wird Remotedesktopdienste|  
  
## <a name="BKMK_SelectingRDP-over-LAN-connectedstationhardware"></a>Auswählen von\-RDP\-over\-LAN-Connected Station-Hardware  
Jeder LAN-Client, der mithilfe von Remotedesktopprotokoll eine Verbindung mit Remotedesktopdienste herstellen kann, kann zu einer Multipoint Services-Station werden.  
  
Wenn Sie möchten, dass der LAN-Client nur als Multipoint-Station verwendet werden kann, können Sie Ihren LAN-Client "Sperren". Konfigurieren Sie z. b. ihren Thin Client so, dass er nur eine Verbindung mit einer Multipoint Services-Sitzung herstellen kann, oder konfigurieren Sie die Desktop Computer so, dass der Zugriff auf Desktop Symbole und Start Menü Elemente (z. b. ein Webbrowser) entfernt wird, um direkten Internet Zugriff zu verhindern. Sie können diese Konfigurationen mit ihren LAN-Client Konfigurationstools oder-Gruppen oder lokalen Richtlinien vornehmen.  
  
## <a name="selecting-audio-devices"></a>Auswählen von Audiogeräten  
Es ist wichtig sicherzustellen, dass Sie bei der Auswahl von Audiogeräten mit dem stationshub, dem USB-Client oder dem LAN-Client verbunden werden können. Einige USB-Hubs, USB-Clients und LAN-Clients verfügen über einen analogen AudioJack, der mit herkömmlichen, analogen Audiogeräten \(wie z. b. Kopf-oder earbuden\)verwendet werden kann. Bei Station Hubs, die keine analogen Geräte enthalten, können USB-Audiogeräte verwendet werden.  
  
\/Wenn Sie eine direkte\-p-Video\-Station\/mit PS 2 für die Tastatur und die Maus auf dem Computer des Computers konfiguriert haben, müssen Sie die analoge Audiodatei auf der Hauptplatine des Computers verwenden. damit das Audiogerät für diese Station verfügbar ist, wenn das Multipoint Services-System im Stations Modus ausgeführt wird.  
  
Wenn Sie über keine direkte\/\-PS 2-Video\-Station verfügen, ist das hostaudiogerät auf der Hauptplatine des Systems nur verfügbar, wenn das Multipoint Services-System im Konsolenmodus ausgeführt wird.  