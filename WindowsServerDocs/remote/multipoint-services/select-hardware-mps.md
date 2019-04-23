---
title: Auswählen von Hardware für Ihr MultiPoint Services-System
description: Überlegungen zur Hardware für MultiPoint Services
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
ms.openlocfilehash: 969ab0e97b5456c71a43cc14bd82204481bdcc42
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835221"
---
# <a name="selecting-hardware-for-your-multipoint-services-system"></a>Auswählen von Hardware für Ihr MultiPoint Services-System
Wenn Sie eine MultiPoint Services-System erstellen, sollten Sie einen Computer auswählen, der die Windows Server 2016-Systemanforderungen erfüllt. Wenn es sich bei der Entscheidung, welche Komponenten auswählen, beachten Folgendes:  
  
-   Die Ziel-Preisbereich der vollständigen Projektmappe.  
  
-   Die Typen von Verwendungsszenarien, die Sie erwarten möglicherweise, für das MultiPoint Services-System, z. B., ob die Benutzer multimedia-Programme ausführen, mithilfe von textverarbeitungs- oder Produktivitätsprogramme oder Surfen im Internet sind.  
  
-   Gibt an, ob Ihr Szenario für die Verarbeitung großer oder Arbeitsspeicher hat verlangt.  
  
-   Die Anzahl der Benutzer, die das System zur gleichen Zeit verwenden kann. Wenn Sie haben viele Benutzer auf Ihrem System zur gleichen Zeit oder Benutzer, die System rechenintensive-Programme verwenden möchten, sollten Sie für höhere rechenleistung für Ihr System planen.  
  
-   Der Typ der Stationen. Wie viele USB-Anschlüsse oder video-Ports benötigen Sie?  
  
-   Pläne für zukünftige Erweiterungen. Möchten Sie die Stationen im MultiPoint Services-System zu einem späteren Zeitpunkt hinzufügen? Verfügen Sie über genügend Grafikkarte Slots, USB-Anschlüsse oder taps Netzwerk? Wie viele zusätzliche Benutzer müssen Ihre Hardware unterstützt?  
  
-   Physisches Layout. Weitere Informationen finden Sie unter [MultiPoint Services-Standortplanung](MultiPoint-services-Site-Planning.md).  
  
Ein MultiPoint Services-System enthält in der Regel die folgenden Komponenten:  
  
-   Ein Computer, der MultiPoint Services ausgeführt wird, einschließlich einer CPU, Arbeitsspeicher, Festplatten und Grafikkarten.  
  
-   Ein Monitor, stationshub, Tastatur und Maus für jede Station.  
  
-   Optionale Peripheriegeräten, bei denen für das MultiPoint Services-Stationen, einschließlich der Referenten, Kopfhörer, Mikrofone oder Speichergeräte, die nur für den Benutzer der Station aus verfügbar sind.  
  
-   Optionale Peripheriegeräten, bei denen, die für alle Benutzer des MultiPoint Services-Systems, verbunden, die direkt auf dem Hostcomputer wie z. B. Drucker, externe Festplatten und USB-Speichergeräten verfügbar sind.  
  
Verwenden Sie die folgende Informationen, um die Hardware Entscheidungen zu treffen:  
  
-   [Auswählen einer CPU](#selecting-a-cpu)  
-   [Auswählen von Hardwarekomponenten](#selecting-hardware-components)  
  
## <a name="selecting-a-cpu"></a>Auswählen einer CPU  
Ein MultiPoint Services-System ist ein Vielfaches\-benutzerumgebung für alle Benutzer, die mit einem einzigen Hostcomputer verbunden. Dies erhöht die CPU-Auslastung, da alle Benutzer auf den gleichen Computer gemeinsam nutzen. Einige Aufgaben, z. B. multimedia-Programme \(z. B. Media-Player oder Video\-Software bearbeiten\), größere Anforderungen hinsichtlich der haben. Aus diesem Grund stellen Sie sicher, dass eine CPU, die die verarbeitungsanforderungen für die Anzahl von Benutzern und Arten von Szenarien, die sie unterstützen muss behandelt werden können.  
  
MultiPoint Services erfordert x X64\-basierte CPU und erfüllt die Systemanforderungen für den Computer aus, wie in beschrieben [Hardwareanforderungen und Empfehlungen zur Leistung](Hardware-Requirements-and-Performance-Recommendations.md).  
  
Die folgenden Typen von Prozessoren wurde getestet, um für ein MultiPoint Services-System mit hoher verwendet werden\-Verarbeitung-Programme, z. B. multimedia-Programme erfordern:  
  
-   **Duale\-core-Prozessor:** Dies kann bis zu 8 Stationen unterstützen.  
-   **Quad\-core-Prozessor:** Dies kann bis zu 16 Stationen unterstützen.
-   **Quad\-core-Prozessor mit multithreading:** Dies kann bis zu 20 Stationen unterstützen.      
-   **Sechs\-core-Prozessor mit multithreading:** Dies kann bis zu 24 Stationen unterstützen.  
  
Wählen Sie anhand dieser Informationen eine CPU, die die verarbeitungsanforderungen für Ihr MultiPoint Services-System erfüllt. 
> [!NOTE] 
> Wenn Sie Videos datenintensive Anwendungen ausgeführt werden empfiehlt es sich mindestens ein Kern pro Station. 
  
## <a name="selecting-hardware-components"></a>Auswählen von Hardwarekomponenten  
Wenn Sie eine MultiPoint Services-System erstellen, berücksichtigen Sie die folgenden Hardware-Komponenten, die Sie möglicherweise:  
  
-   Grafikhardware  
  
-   MultiPoint Services-stationshardware  
  
    -   *USB-hubs*  
  
    -   USB-0 (null)-clients  
  
    -   Tastaturen und Mäusen  
  
    -   Monitore  
  
-   Peripheriegeräte  
  
    -   Audiogeräte, z. B. Lautsprecher und Kopfhörer  
  
    -   Mikrofonen  
  
    -   USB-Massenspeicher-Geräte  
  
Wenn Sie die Hardware-Komponenten für Ihr MultiPoint Services-System ausgewählt haben, stellen Sie sicher, dass Sie aktuell, 64 erhalten\-bit-Treiber für die Komponenten.  
  
Ausführliche Informationen zum Auswählen von Komponenten für Ihr MultiPoint Services-System finden Sie in den folgenden Themen:  
  
[Auswählen von video-hardware](#selecting-video-hardware)  
[Auswählen von Direct\-video\-verbunden oder USB-Station Clientgeräte auf null](#BKMK_Selectingdirect-video-connectedorUSBzeroclientstationdevices)   
[Wählen andere Station-Peripheriegeräte](#selecting-other-station-peripheral-devices)  
[Auswählen von RDP\-über\-LAN\-stationshardware angeschlossen](#BKMK_SelectingRDP-over-LAN-connectedstationhardware)  
[Audiogeräte auswählen](#selecting-audio-devices)  
  
## <a name="selecting-video-hardware"></a>Auswählen von video-hardware
Die Grafikhardware, die Sie auswählen, sollte die Anzahl der Monitore unterstützen, die Sie für die Anzahl von Benutzern erfordern funktionierende verfügen, die am MultiPoint Services-Stationen werden sollen. Darüber hinaus bieten verschiedene Arten von Videohardware eine höhere\-Performance-Lösung für Grafiken\-intensive Programme, z. B. multimedia-Inhalte.  
  
Wählen Sie die Grafikhardware, die die maximale Anzahl von Monitoren für den Typ der Leistung unterstützen kann, die das MultiPoint Services-System erforderlich sind. Stellen Sie sicher, dass Sie die Leistung der Grafikhardware, die Sie auswählen überprüfen, um sicherzustellen, dass er Ihren leistungsanforderungen entspricht.  
  
> [!NOTE]  
> Sie müssen einen Treiber installieren, der unterstützt wird, erweitern Ihren Desktop auf mehrere Monitore.  
  
Videohardware Optionen umfassen:  
  
-   Interne Grafikkarten, die eine PCI- oder eine PCIe-Bus-Schnittstelle verwenden.  
  
-   Externe video-Controllern, die über USB angeschlossen  
  
Die folgenden Abschnitte beschreiben die Funktionen der einzelnen Typen Videohardware. Grafikkarten für interne und externe Grafikcontrollern, um das System zu erstellen, das Sie möchten, können Sie kombinieren.  
  
### <a name="internal-video-cards"></a>Interne Grafikkarten  
Eine interne Grafikkarte angeschlossen\-in auf der Hauptplatine auf dem Computer. Die interne Grafikkarte ist eine Lösung, mit denen die Leistung von Grafiken kann\-intensive multimedia-Programme. Eine interne Grafikkarte erfordert jedoch einen verfügbaren PCI- oder PCIe-Steckplatz (.NET,\-in auf der Hauptplatine. Viele hohe\-Grafikkarten Leistung erfordern, einen PCIe-Slot, aber es gibt eine begrenzte Anzahl von PCIe-Slots auf einer Hauptplatine. Sie sollten wissen, welche Art von Grafikkarte Slots werden auf Ihrem Computer verfügbar, damit Sie den richtigen Typ von Grafikkarten. erwerben können.  
  
Die Anzahl der Monitore, die mit jeder Grafikkarte verbinden können, hängt von der GPU, die verwendet wird, auf der Karte und die Anzahl der Ports, die dies unterstützen, die in der Regel zwischen 2 und 6 liegt.  
  
Wählen Sie bei der Auswahl interne Grafikkarten, Grafikkarten, die die Anzahl der Monitore erforderlich, um die gewünschte Anzahl von direkten video verbundene Stationen erstellen zu unterstützen. Die maximale Anzahl von Monitoren, die unterstützt werden können, ist die Anzahl der internen Videokarten, die angeschlossen sind gleich\-in auf der Hauptplatine multipliziert die Anzahl der Monitor-Ports auf jedem dieser Grafikkarten. Wenn Sie zwei interne Grafikkarten und jede Karte zwei Monitor-Ports hatten, könnten Sie z. B. bis zu vier Monitore unterstützen.    
  
### <a name="external-video-controllers"></a>Externe video-Controllern  
USB-0 (null)-Clients enthält einen externen video-Controller, um einen Monitor an den Client eine Verbindung herzustellen. Der USB-0 (null)-Client kann auch Verbindungen für Kopfhörer, Lautsprecher, ein Mikrofon und andere Peripheriegeräte enthalten.  
  
Wählen Sie ein USB zero-Client, wenn Sie Unterstützung zusätzlicher Monitore aktivieren, ohne den Computer öffnen möchten oder wenn Sie mehrere Stationen als verfügbare Videoausgaben unterstützen möchten. Angenommen, Sie vier Monitore angeschlossen bisher\-in internen Grafikkarten, und Sie zwei weitere Monitore hinzufügen möchten, können Sie die zu lokalisierenden\-in zwei externe video-Controllern auf dem Computer und genügend Platz für zwei weitere Monitore. Auf diese Weise können Sie kombinieren, einen USB-0 (null)-Client mit der Grafikkarte und verwenden Sie nicht zusätzliche PCI oder PCIe-Slots auf der Hauptplatine.  
  
## <a name="BKMK_Selectingdirect-video-connectedorUSBzeroclientstationdevices"></a>Auswählen von Direct\-video\-verbunden oder USB-Station Clientgeräte auf null  
Eine MultiPoint Services-Station besteht aus einem stationshub oder USB-zero-Client mit einer Tastatur und Maus, die\-in, und eine Überwachung, die im Netzbetrieb befindet\-in auf dem Hostcomputer oder im an den Client ein USB-0 (null). Andere Peripheriegeräte integriert werden können,\-in der Station Hub oder einem USB-0 (null) Client, aber sie sind nicht erforderlich, um MultiPoint-Station zu erstellen. Diese anderen Peripheriegeräten, bei denen im beschrieben [auswählen andere Peripheriegeräte Station](#selecting-other-station-peripheral-devices).  
  
Die Geräte, die Sie auswählen, um eine MultiPoint Services-Station zu erstellen, müssen Mindestanforderungen gelten für die Arbeit mit MultiPoint Services erfüllen. In diesem Thema werden die Details zu den Anforderungen für die folgenden Geräte des MultiPoint Services-Station bereitgestellt:  
  
-   [Auswählen von USB-hubs](#selecting-usb-hubs)  
-   [Auswählen von USB-NULL-clients](#selecting-usb-zero-clients)  
-   [Auswählen von Tastaturen und Mäusen](#selecting-keyboards-and-mouse-devices)  
-   [Auswählen von Monitoren](#selecting-monitors)  
  
### <a name="selecting-usb-hubs"></a>Auswählen von USB-hubs  
Das USB-Hubs, die in einem MultiPoint Services-System verwendet werden, können ein generischer USB-Hub sein. Solche Hubs verfügen in der Regel vier oder mehr USB-Anschlüsse und ermöglichen mehrere USB-Geräte mit einem einzelnen USB-Anschluss auf dem Computer verbunden sein. Einige andere Geräte, wie z. B. Tastaturen und Videomonitoren, können auch einen USB-Hub in ihren Entwurf integrieren.  
  
Eine weitere Überlegung ist die Verwendung von ein *extern unterstützt* -Hub, statt eine *Bus\-unterstützt* Hub. Mit einem Bus\-ausgeschaltet-Hub, die Menge des aktuellen, die bereitgestellte vom Host Computer befinden muss ausreichend, um die Möglichkeit, alle Peripheriegeräte bereitzustellen, die integriert werden\-im an den Hub, ohne die Systemleistung beeinträchtigen. Ein extern ausgeschaltet Hub können Sie eine Verbindung herstellen mehr Peripheriegeräten und ermöglichen eine ausreichende Stromversorgung für alle von ihnen. Die Verwendung von extern ausgeschaltet Hubs können Leistungsprobleme, die Port-Fehler und andere vorübergehende Probleme zu verhindern.  
  
Wenn Sie einen USB-Hub für Ihr MultiPoint Services-System auswählen zu können, sollten Sie dessen Verwendung. Hub kann verwendet werden, als eine *stationshub*, eine *zwischenhub*, oder ein *downstream-Hub*. Verweisen Sie auf die folgende Tabelle enthält Beschreibungen zu den einzelnen Hub. Es wird empfohlen, alle USB-Geräte, USB 2.0 oder höher sein.
  
||Unterstützt|  
|-|-----------|  
|Stationshub|Bus möglich\-unterstützt, es sei denn, hohe\-Geräten (.NET-typbeibehaltung,\-in oder einem downstream-Hub wird verbunden sein,|  
|Zwischengeschalteter Hub |Sollte extern unterstützt werden|  
|Downstream-Hub|Extern ausgeschaltet werden können oder Bus mit Strom versorgt, abhängig von den Geräten, die integriert werden\-im an den Hub|  
|Aktive USB-Kabel|Aktive USB-Kabel, die einen USB-Hub enthalten, sind in der Regel Bus unterstützt; Sie werden daher nicht empfohlen, für das Anschließen von stationshubs an den Computer.|  
  
### <a name="selecting-usb-zero-clients"></a>Auswählen von USB-NULL-clients  
Ein Client USB-0 (null) ist ein USB-Hub, der eine Ausgabe der video enthält. Aus diesem Grund ermöglicht es einen Monitor mit dem Computer über eine USB-Verbindung verbunden sein. Weitere Informationen zur Verwendung von USB-0 (null)-Clients für Video finden Sie unter [auswählen Videohardware](#selecting-video-hardware) in diesem Dokument. Ein USB-0 (null)-Client können auch das Anschließen einer Reihe von USB- und nicht-\-USB-Geräte am Hub. USB-0 (null)-Clients werden von bestimmten Hardwareherstellern erzeugt und erfordern die Installation eines Geräts\-bestimmten Treiber.  
  
### <a name="selecting-keyboards-and-mouse-devices"></a>Auswählen von Tastaturen und Mäusen  
Die Tastatur und Maus-Geräte, die Sie anschließen\-in der Station in der Regel werden USB-Geräte. Einige USB NULL Clients bereitstellen PS\/2 ports, von denen in diesem Fall die Tastatur und Maus sollten PS verwenden\/2, um an den stationshub angeschlossen. Können Sie auch einen PS\/2-Tastatur und Maus, wenn Sie einen PS einrichten\/2 direkte\-video\-Station angeschlossen.  
  
Tastatur mit einem internen Hub kann als stationshub verwendet werden. Allerdings müssen alle anderen Station-Geräte über die Ports auf der Tastatur an den internen Hub verbinden. Wenn diese eine Tastatur an den Computer über einen anderen Hub verbunden ist, wird diesem Hub als ein zwischengeschalteter Hub behandelt.  
  
Bei Verwendung von Split\-Bildschirm Stationen, Sie sollten in Betracht, eine Mini-Tastatur, die keine Zehnertastatur, damit die beiden Tastaturen vor der Monitor verwendet werden können.  
  
### <a name="selecting-monitors"></a>Auswählen von Monitoren  
Es sollte einen Monitor, die für jede MultiPoint Services-Station bereitgestellt sein, es sei denn, eine Teilung\-Bildschirm ist geplant. Monitore sind die Grafikkarte auf dem Computer, den Client USB-0 (null) oder das LAN angeschlossen\--basierte Client. Jede Art von Monitor, der von der Grafikkarte, USB-0 (null) Client oder LAN unterstützt wird\-basierender Client kann verwendet werden, einschließlich der CRT-Monitore.  
  
Einige spezielle Monitore enthalten ein internes LAN\-basierend-Clients oder Clients von USB-0 (null). Diese Monitore enthalten in der Regel Audioeingabe\/Jacks und internen USB-Hubs für die Verbindung von Tastaturen und Mäusen ausgeben. Sie eine Verbindung über ein USB- oder einer LAN-Verbindung mit dem Server herstellen.  
  
#### <a name="display-resolution"></a>Bildschirmauflösung  
Die unterstützten mindestauflösung Anzeigebereich für eine Station ist 512 x 768 Pixel. Wenn das MultiPoint Services-System gestartet wurde und ermittelt, dass der Anzeigebereich für eine Station ist kleiner als die minimale Auflösung, ein leerer Bildschirm wird auf dieser Station angezeigt werden und die Station nicht verwendet werden.  
  
Wenn Sie einen Bildschirm als geteilt durch zwei Stationen freigegeben werden soll\-Bildschirm Stationen, die Mindestanforderung für die Anzeige mit 1024 x 768, ist, damit die sich ergebende einzelne Station Bildschirmbereiche mindestens 512 x 768 erforderlich sind. Für die optimale split\-Bildschirm benutzerfreundlichkeit Standardbildschirm mit einem Minimum an die Auflösung von 1600 x 900 wird empfohlen.  
  
## <a name="selecting-other-station-peripheral-devices"></a>Wählen andere Station-Peripheriegeräte  
MultiPoint Services unterstützt Peripheriegeräte, bei denen, die an einen stationshub, einem USB-0 (null)-Client oder direkt auf dem Computer verbunden sind. Geräte, die an einen stationshub angeschlossen werden, bestimmten Station zugeordnet werden. Andere Geräte sind für jede Station aus, wenn direkt an den Computer angeschlossen verfügbar. LAN-Clients können auch Peripheriegeräte unterstützen.  
  
> [!IMPORTANT]  
> Eine Tastatur kann nicht mit einem downstream-Hub angeschlossen werden \(z. B. einen Hub, der an einen stationshub angeschlossen ist\). Wenn Sie eine Tastatur, um eine downstream-Hub, Peripheriegeräten anschließen, die integriert werden\-im an den downstream-Hub werden nicht mehr für diese Station verfügbar. Dieses Verhalten ermöglicht die Unterstützung der Skalierbarkeit\-stationshubs verkettet.  
  
**Für alle Stationen** ein USB-Gerät, das an den Computer angeschlossen ist \(z. B. nicht über einen stationshub\) ist für alle Stationen verfügbar. Je nach Gerät können Sie gleichzeitig von mehreren Benutzern verwendet werden, oder nur ein Benutzer kann zu einem Zeitpunkt darauf zugreifen. In der folgende Tabelle wird erläutert, wie USB-Geräte zugegriffen werden können.  
  
> [!NOTE]  
> Die Spalte "Verbunden, Host-Computer" in der Tabelle verweist auf das Verhalten, wenn der Computer, auf dem MultiPoint Services ausgeführt wird, die im stationsmodus mit Stationen ausgeführt wird. Wenn Sie im Konsolenmodus ausgeführt werden, verhalten sich die Peripheriegeräte, die an einer beliebigen Stelle angeschlossen werden in die gleiche Weise wie einen standard-Server in einer konsolensitzung.  
  
||Mit dem Hostcomputer verbunden|Mit dem Stationshub oder Downstream-Hub verbunden sind|  
|-|------------------------------|----------------------------------------------|  
|Tastatur|Funktioniert nicht, es sei denn, er Teil einer Station PS/2 ist. |Für einzelne station<br /><br />Kann nicht mit einem downstream-Hub verbunden werden|  
|Maus|Funktioniert nicht, es sei denn, er Teil einer Station PS/2 ist. |Für einzelne station|  
|Speaker/Kopfhörer|Funktioniert nicht, es sei denn, er Teil einer Station PS/2 ist.|Für einzelne station|  
|USB-Speichergerät|Verfügbar für alle Stationen|Für einzelne station|  
|HID-Consumer-Steuerelement|Funktioniert nicht.|Für einzelne station|  
|Andere USB-Geräte, beispielsweise Kameras, dokumentieren, Leser und DVD-Laufwerke|Für alle Stationen, wenn von Windows Server 2012 unterstützt.|Auf alle Stationen, wenn von Windows Server 2008 R2 Remote Desktop Services unterstützt zur Verfügung.|  
  
## <a name="BKMK_SelectingRDP-over-LAN-connectedstationhardware"></a>Auswählen von RDP\-über\-LAN\-stationshardware angeschlossen  
Alle LAN-Client, der zum Remote Desktop Services, Herstellen von Verbindungen kann mithilfe von Remote Desktop Protocol, kann es sich um eine MultiPoint Services-Station werden.  
  
Wenn Sie auf der LAN-Client nur als eine MultiPoint-Station verwendet werden soll, empfiehlt es sich um zu Ihrem LAN-Client "Sperren". Konfigurieren Sie z. B. den thin Client, sodass es kann nur eine Verbindung mit einer MultiPoint Services-Sitzung herstellen, oder Ihre desktop-PCs konfigurieren, so dass der Zugriff auf desktop-Symbole und Menü "Start" Elemente, wie z. B. ein Webbrowser entfernt wird, um zu verhindern, dass bei der direkten Zugang zum Internet. Sie können diese Konfigurationen, die mit Ihrem LAN-Client-Konfigurationstools, Gruppe oder lokale Richtlinien vornehmen.  
  
## <a name="selecting-audio-devices"></a>Audiogeräte auswählen  
Es ist wichtig, um sicherzustellen, dass bei Auswahl von Audiogeräte sie in der stationshub, USB-0 (null)-Clients oder LAN-Clients integriert werden können. Einige USB-Hubs, USB-0 (null)-Clients und LAN-Clients müssen eine analoge audio Jack, die mit herkömmlichen analoge Audiogeräte verwendet werden kann \(z.B. Kopfhörer oder Ohrstöpsel\). Stationshubs, die keine analogen Jacks können USB-Audiogeräte.  
  
Wenn Sie einen PS konfiguriert haben\/2 direkte\-video\-über PS verbunden Station\/2 Ports auf der Hauptplatine des Computers für die Tastatur und Maus, müssen Sie das analoge Audio auf der Hauptplatine des Computers in verwenden Damit das audio-Gerät auf dieser Station verfügbar sein, wenn das MultiPoint Services-System im stationsmodus ausgeführt wird.  
  
Wenn Sie nicht mit einem PS verfügen\/2 direkte\-video\-verbundenen Station, die Host-audio-Gerät auf der Hauptplatine stehen nur, wenn das MultiPoint Services-System im Konsolenmodus ausgeführt wird.  