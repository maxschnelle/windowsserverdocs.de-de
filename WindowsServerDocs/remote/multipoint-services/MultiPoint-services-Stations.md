---
title: MultiPoint-Stationen
description: Erfahren Sie mehr über Stationen in Multipoint Services, einschließlich der verschiedenen Optionen für Benutzer.
ms.date: 07/22/2016
ms.topic: article
ms.assetid: f9f9d618-ccfe-41ea-a52c-00c3c7adb51a
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 6f1c313f4d8eeb4e32ec27da1c37bc1d423240d1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953816"
---
# <a name="multipoint--stations"></a>Multipoint-Stationen
In einer Multipoint Services-Systemumgebung sind *Stationen* die Benutzer Endpunkte zum Herstellen einer Verbindung mit dem Computer, auf dem Multipoint Services ausgeführt wird. Jede Station bietet dem Benutzer eine unabhängige Windows 10-Benutzeroberflächen. Die folgenden Stations Typen werden unterstützt:

-   Direkt mit Videos verbundene Stationen

-   Über USB-Verbindungen mit 0 (null) Clients verbundene Stationen (einschließlich USB-over-Ethernet-Clients)

-   RDP-über-LAN-verbundene Stationen (für Rich Client-oder Thin Client-Computer)

Vollständige PCs, auf denen der Multipoint-Connector installiert ist, können auch über das Multipoint-Dashboard überwacht und gesteuert werden. Unter Windows 10 kann der Multipoint-Connector über die Systemsteuerung für Windows-Features aktiviert werden.

Multipoint Services unterstützt eine beliebige Kombination dieser Stations Typen. es wird jedoch empfohlen, dass eine Station eine Station mit direkt Videoverbindung ist, die als primäre Station fungieren kann. Der Grund für diese Empfehlung ist, dass Sie Support Szenarien erwarten können. Beispielsweise für die Interaktion mit dem BIOS des Systems, bevor Multipoint Services ausgeführt wird.

## <a name="primary-stations-and-standard-stations"></a>Primäre Stationen und Standard Stationen
Eine Station mit direkt-Video-Verbindung ist als *primäre Station*definiert. Die verbleibenden Stationen werden als *Standard Stationen*bezeichnet.

Die primäre Station zeigt die Startbildschirme an, wenn der Computer eingeschaltet ist. Er bietet Zugriff auf Systemkonfigurations-und Problem Behandlungsinformationen, die nur während des Starts verfügbar sind. Bei der primären Station muss es sich um eine Station mit direkt Videoverbindung handeln. Nach dem Start können Sie die primäre Station wie alle anderen Multipoint-Stationen verwenden.

## <a name="direct-video-connected-stations"></a>Direkt mit Videos verbundene Stationen
Der Computer, auf dem Multipoint Services ausgeführt wird, kann mehrere Videokarten enthalten, von denen jeder über einen oder mehrere videports verfügen kann. Dadurch können Sie Monitore für mehrere Stationen direkt in den Computer einbinden. Tastaturen und Mäuse sind über USB-Hubs verbunden, die mit jedem Monitor verknüpft sind. Diese Hubs werden als *Stations Hubs*bezeichnet. Andere Peripheriegeräte, wie z. b. Sprecher, Kopfhörer oder USB-Speichergeräte, können auch mit einem stationshub verbunden werden und sind nur für den Benutzer dieser Station verfügbar.

> [!IMPORTANT]
> Es sollte mindestens eine Station mit *direkt-Video-Verbindung* pro Server vorhanden sein, die als primäre Station fungiert, um den Startprozess anzuzeigen, wenn der Computer eingeschaltet ist.

![Abbildung des USB-basierten Multipoint Services-systemlayouts](./media/WMSMultiPointServerUSBSystemLayout.gif)

**Abbildung 1** Multipoint Services-System mit vier direkt mit einem Video verbundenen Stationen

### <a name="ps2-stations"></a><a name="BKMK_PS2stations"></a>PS/2-Stationen
Mit Multipoint Services können Sie die PS/2-Tastatur und die Maus auf dem Motherboard einem direkt Video verbundenen Monitor zuordnen, um eine PS/2-Station zu erstellen. Eine hochauflösende, analoge Audiodatei auf der Hauptplatine ist das Audiomaterial, das mit dieser Art von Station verknüpft ist. Dies gilt nicht für Computer, bei denen keine PS/2-Jacks auf der Hauptplatine vorhanden sind.

## <a name="usb-zero-client-connected-stations"></a>An einem USB-Client angeschlossene Stationen
An einem USB-Client verbundene Stationen verwenden einen *USB Zero-Client* als stationshub. USB-Clients werden manchmal auch als multifunktionshub mit Video bezeichnet. Dabei handelt es sich um einen Hub, der über ein USB-Kabel mit dem Computer verbunden ist, und diese Hubs unterstützen in der Regel einen Videomonitor, eine Maus und Tastatur (PS/2 oder USB), Audiodaten und zusätzliche USB-Geräte. Dieses Handbuch bezieht sich auf diese spezialisierten Hubs als USB-Clients.

Das folgende Diagramm zeigt ein Multipoint-Server System mit einer primären Station (Direct Video Connected Station) und zwei zusätzlichen, mit dem USB-Client verbundenen Stationen.

![Verbundene USB-Verbindungen mit Zero-Client](./media/WMS11_diagram7.gif)

**Abbildung 2** Multipoint Services-System mit einer primären Station und zwei an einem USB-Client verbundenen Stationen

### <a name="usb-over-ethernet-zero-clients"></a>USB-over-Ethernet-Clients (null)
USB-over-Ethernet-Clients stellen eine Variation von USB-Clients dar, die USB-über-LAN an das Multipoint Services-System senden. Diese Typen von USB-Clients funktionieren ähnlich wie andere USB-Clients, sind aber nicht durch maximale Länge der USB-Kabellänge beschränkt. Bei USB-over-Ethernet-Clients handelt es sich nicht um herkömmliche Thin Clients, und Sie werden als virtuelle USB-Geräte im Multipoint Services-System angezeigt. Wenn Sie diese Geräte verwenden, finden Sie unter Gerätehersteller spezifische Empfehlungen zur Leistung und Website Planung. Die meisten Geräte verfügen über ein Drittanbieter-Plug-in für Multipoint Manager, mit dem Sie Geräte dem Multipoint Services-System zuordnen und verbinden können.

## <a name="rdp-over-lan-connected-stations"></a>Verbundene RDP-over-LAN-Stationen
Thin Clients und herkömmliche Desktop-, Laptop-oder Tablet Computer können eine Verbindung mit dem Computer herstellen, auf dem Multipoint Services über das lokale Netzwerk (Local Area Network, LAN) ausgeführt wird, indem Remotedesktopprotokoll (RDP) oder ein proprietäres Protokoll und der Remotedesktopprotokoll Anbieter verwendet werden. RDP-Verbindungen bieten eine Endbenutzer Umgebung, die mit jeder anderen Multipoint-Station vergleichbar ist, aber die Hardware des lokalen Client Computers verwendet. Erfahren Sie mehr über unsere Remote Desktop-Anwendungen, die in [Remotedesktop-Clients](../remote-desktop-services/clients/remote-desktop-clients.md)für Android, Ios, Mac und Windows verfügbar sind.

Clients und Geräte, auf denen Microsoft RemoteFX ausgeführt wird, können eine umfangreiche Multimediaumgebung bereitstellen, indem Sie die Prozessor-und Video Hardwarefunktionen des lokalen Thin Client oder des lokalen Computers nutzen, um Videos mit hoher Definition über das Netzwerk bereitzustellen.

Wenn Sie über vorhandene LAN-Clients verfügen, können Sie mit Multipoint Services eine schnelle und kostengünstige Möglichkeit bereitstellen, um alle Benutzer gleichzeitig auf Windows 10 zu aktualisieren.

Aus Bereitstellungs-und Verwaltungs Sicht bestehen die folgenden Unterschiede bei der Verwendung von mit RDP-über-LAN verbundenen Stationen:

-   Nicht beschränkt auf physische USB-Verbindungs Abstände

-   Möglichkeit zur Wiederverwendung älterer Computer Hardware als Stationen

-   Die Skalierung auf eine größere Anzahl von Stationen ist einfacher. Alle Clients in Ihrem Netzwerk können möglicherweise als Remote Station verwendet werden.

-   Keine Hardwareproblem Behandlung über die Multipoint Manager-Konsole

-   Keine Split-Screen-Funktionalität.

    Weitere Informationen finden Sie unter [Split-Screen-Stationen](#split-screen-stations) weiter unten in diesem Thema.

-   Keine Stations umbenennen oder Konfigurieren der automatischen Anmeldung über die Multipoint Manager-Konsole

![Verbundene USB-Station ohne Clients](./media/Diagram1.gif)

**Abbildung 3** Multipoint Services-System mit per RDP über LAN verbundenen Stationen

## <a name="additional-configuration-options"></a>Zusätzliche Konfigurationsoptionen

### <a name="split-screen-stations"></a>Stationen mit geteilten Bildschirmen
Multipoint Services bietet eine Split Screen-Option auf Computern mit direkt mit einem Video verbundenen Stationen oder an an einem USB-Client verbundenen Stationen. Ein geteilter Bildschirm bietet die Möglichkeit, eine zusätzliche Station pro Monitor zu erstellen. Anstatt zwei Monitore zu erfordern, können Sie einen Monitor mit zwei stationshub-Setups verwenden, um zwei Stationen mit einem Monitor zu erstellen. Sie können die Anzahl der verfügbaren Stationen schnell erhöhen, ohne zusätzliche Monitore, USB-Null-Clients oder Grafikkarten erwerben zu müssen.

Die Verwendung einer Split-Screen-Station bietet folgende Vorteile:

-   Verringern von Kosten und Speicherplatz, indem mehr Benutzer in einem Multipoint Services-System untergebracht werden.

-   Ermöglicht zwei Benutzern das parallele zusammenarbeiten mit einem Projekt.

-   Ermöglicht es einem Lehrer, eine Prozedur auf einer Station zu veranschaulichen, während ein Student auf der anderen Station zusammenhält.

Jeder Multipoint Services-Stations Monitor mit einer Auflösung von mindestens 1024 x 768 kann in zwei Stations Bildschirme aufgeteilt werden. Für eine optimale Benutzer Darstellung auf dem Bildschirm wird ein breit Bildschirm mit einer Mindestauflösung von 1600 x 900 empfohlen. Es wird auch eine Mini Tastatur ohne einen Zahlenbereich empfohlen, damit die beiden Tastaturen in den Monitor eingefügt werden können.

Zum Erstellen von Split-Screen-Stationen richten Sie eine Station mit direktem bzw. einem USB-oder-Client-Verbindung ein. Dann fügen Sie einen zusätzlichen stationshub hinzu, indem Sie eine Tastatur und eine Maus an einen USB-Hub anschließen, der mit dem Server verbunden ist. Anschließend können Sie die Station in zwei Stationen konvertieren, indem Sie den Bildschirm mithilfe von Multipoint-Manager aufteilen und den neuen Hub der Hälfte des Monitors zuordnen. Die linke Hälfte des Bildschirms wird zu einer Station, und die Rechte Hälfte wird zu einer zweiten Station.

Nachdem eine Station aufgeteilt wurde, kann sich ein Benutzer an der linken Station anmelden, während sich ein anderer Benutzer an der rechten Station anmeldet.

![Stationen mit geteilten Bildschirmen](./media/WMS_diagram3.gif)

**Abbildung 4** Multipoint Services-System mit unterteilten Bildschirm Stationen

## <a name="station-type-comparison"></a><a name="BKMK_StationTypeComparison"></a>Stations Typvergleich

| BESCHREIBUNG | Direktes Video mit Verbindung | USB-Null-Client verbunden | RDP-over-LAN-Verbindung |
|--|--|--|--|
| Video Leistung | Empfohlen für eine optimale Video Leistung |  | Verwenden von Thin Clients, die remotefx unterstützen, um die Videoqualität bei geringerer Netzwerkbandbreite zu steigern |
| Physische Einschränkungen | Begrenzt durch Grafik Kabellänge und USB-Hub und Kabellänge (empfohlene maximale Länge von 15 Metern) | Begrenzt durch USB-Hub und Kabellänge (empfohlene maximale Länge von 15 Metern) | Verteilung durch LAN-Verteilung |
| Zulässige Anzahl von Stationen | Begrenzt durch die Anzahl der verfügbaren PCIe-Slots auf den Hauptseiten der Videoanschlüsse Pro Grafikkarte | Die Gesamtanzahl kann durch den USB-Client Hersteller eingeschränkt werden. (Weitere Informationen finden Sie im Hinweis, der dieser Tabelle folgt.) | Begrenzt durch verfügbare Ports auf dem Netzwerk Switch |
| Geteilter Bildschirm | Ja | Ja | Nein |
| Peripherie Status der Multipoint Manager-Station, Konfiguration der automatischen Anmeldung, Stations umbenennen | Ja | Ja | Nein |
| Zugriff auf Serverstart Menüs | Ja | Nein | Nein |

> [!NOTE]
> Die Gesamtanzahl der USB-Clients, die mit dem Server verbunden sind, wird möglicherweise durch den Hersteller oder die Hardware Funktion des Computers beschränkt, auf dem Multipoint Services ausgeführt wird.
