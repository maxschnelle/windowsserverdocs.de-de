---
title: MultiPoint Services-Standortplanung
description: Planungsinformationen für Multipoint Services-bereit Stellungen in Windows Server 2016
ms.date: 07/22/2016
ms.topic: article
ms.assetid: 063783cd-d748-489e-b175-46eadc993f7a
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 36fb9b75f2a233585893acbe2adb71ec072bc777
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949203"
---
# <a name="multipoint-services-site-planning"></a>MultiPoint Services-Standortplanung
Berücksichtigen Sie den Speicherort, an dem ein oder mehrere Computer, auf denen Multipoint Services ausgeführt wird, und die zugehörigen Stationen bereitgestellt werden.

Der Computer, auf dem die Multipoint Services-Rolle ausgeführt wird, sollte bequemen Zugang zu einer Stromversorgung und zu den Peripheriegeräten haben, die direkt mit dem Computer verbunden sind, z. b. ein Drucker. Außerdem muss der Computer, auf dem Multipoint Services ausgeführt wird, über einen bequemen Zugriff auf eine Netzwerkverbindung verfügen. Für den Zugriff auf das Internet und ggf. ein LAN ist eine Netzwerkverbindung erforderlich.

Weitere zu berücksichtigende Faktoren sind:

-   Wird das Multipoint Services-System in einem bestimmten Raum eingerichtet, oder wird es in einem Rollback oder einer Tabelle eingerichtet, sodass es von Ort zu Ort verschoben werden kann?

    > [!NOTE]
    > Wenn Sie die Verwendung einer mobilen Installation planen, können Sie die Stationen bei jedem erneuten Verbinden der Stationen mit Multipoint Services *Verknüpfen* , um sicherzustellen, dass jede Tastatur und Maus mit dem entsprechenden Monitor verknüpft ist.

-   Befindet sich die primäre Station neben den anderen Stationen oder ist sie getrennt? Wenn z. b. das Multipoint Services-System in einem Classroom eingerichtet ist, befindet sich die primäre Station im Lehrpersonal und die Standard Stationen an einer anderen Stelle im Raum? Wenn der Computer, auf dem Multipoint Services ausgeführt wird, neu gestartet wird, kann die primäre Station auf die Startbildschirme zugreifen. Wenn Sie diese Zugriffsebene in einer Classroom-Einstellung in Betracht ziehen, empfiehlt es sich, die primäre Station am Schreibtisch der Lehrkräfte zu platzieren.

-   Wie viele Stationen werden in den Raum passen?

-   Benötigen Sie ein Netzwerk? Bei einer einzelnen Serverlösung, bei der direkte Video Verbindungen oder Verbindungen mit USB-Clients verwendet werden, ist kein Netzwerk erforderlich.

-   Gibt es ausreichend Netzwerkverbindungen im Raum, um die erforderliche Anzahl von Computern zu unterstützen, auf denen Multipoint Services ausgeführt wird

-   Wo befinden sich die Energie Outlets?

-   Benötigen Sie ein zusätzliches Anzeigegerät, z. b. einen Projektor? Wenn Sie beabsichtigen, einen Projektor zu verwenden, wird er von der Obergrenze abhängen, oder er wird in einer Tabelle positioniert?

-   Welche Art von Kabeln wird benötigt, und wie viele werden benötigt?

-   Stellen Sie sich vor, wie Sie in Zukunft erweitern können. Werden Sie weitere Stationen hinzufügen?

## <a name="station-layout-and-configuration"></a>Stations Layout und-Konfiguration
Das physische Layout Ihrer Website kann sich auf die Auswahl des Stations Typs auswirken. Weitere Informationen zu den verschiedenen Stations Typen finden Sie in diesem Handbuch unter [Multipoint-Stationen](MultiPoint-services-Stations.md) . Mehrere Stations Typen sind in einem einzelnen Multipoint-Dienst zulässig. Dies bietet Ihnen zusätzliche Flexibilität, um Ihre Installationsanforderungen zu erfüllen.

### <a name="layout-for-direct-video-connected-stations"></a>Layout für direkt mit Videos verbundene Stationen

-   Bei einer Station mit direkt-Video-Verbindung wird der Abstand zwischen den Monitoren und dem Computer durch die Videokabel Länge beschränkt.

-   Die Verwendung von zwischen Hubs oder mit der Verwendung von Daisy verketteten Stations Hubs wird zur Erleichterung der Bereitstellung unterstützt, aber die empfohlene Höchstzahl von aufeinander folgenden Hubs ist drei. Dies bedeutet, dass der maximale Abstand zwischen dem Computer und dem stationshub 15 Meter beträgt, da jedes USB 2,0-Kabel über die maximale Länge von fünf Metern verfügt.

> [!IMPORTANT]
> Es sollte immer mindestens eine direkte Videoverbindung pro Computer vorhanden sein, um als primäre Station fungieren zu können.

### <a name="layout-for-usb-zero-client-connected-stations"></a>Layout für USB-Verbindungen mit Client verbundenen Stationen

-   Die Verwendung von zwischen Hubs oder mit der Verwendung von Daisy verketteten Stations Hubs wird zur Erleichterung der Bereitstellung unterstützt, aber die empfohlene Höchstzahl von aufeinander folgenden Hubs ist drei. Dies bedeutet, dass der maximale Abstand zwischen dem Computer und dem stationshub 15 Meter beträgt, da jedes USB 2,0-Kabel über die maximale Länge von fünf Metern verfügt.

-   Die maximal empfohlene Anzahl von USB-Clients, die mit einem einzelnen Zwischenhub verbunden sind, ist drei.

    > [!NOTE]
    > Einige Computer verfügen über einen generischen Hub auf der Hauptplatine. Dies hat Auswirkungen auf das Hinzufügen eines zusätzlichen Hubs zwischen dem *stammphub* des Computers und den Stations Hubs.

-   Wenn Videos stark verwendet werden, empfiehlt es sich, höchstens zwei USB-Clients mit einem USB-Anschluss auf dem Server zu verbinden. Wenn z. b. ein Zwischenhub verwendet wird, müssen nur zwei USB-Clients verbunden werden. Wenn Sie keine USB-Clients verketten, sollten nur zwei USB-Clients verkettet werden. Durch das Hinzufügen eines USB-Null-Clients zum USB-Anschluss auf dem Server wird die verfügbare Videobandbreite verringert.

-   Wenn Sie beabsichtigen, mehr als drei USB-Clients mit einem einzelnen USB-Anschluss auf dem Server zu verbinden, wird die Verwendung von USB 3,0 zwischen dem Server und dem Zwischenhub empfohlen.

> [!NOTE]
> Es wird empfohlen, die Leistung mithilfe Ihrer Anwendungen und Hardware zu überprüfen, um zu entscheiden, wie viele USB-Clients Sie mit einem USB-Anschluss auf dem Server verbinden können.

![Downstreamhubs](./media/WMS_diagram6.gif)

**Abbildung 5** Multipoint Services-System mit drei USB-Clients, die mit einem einzelnen Zwischenhub verbunden sind

### <a name="layout-for-rdp-over-lan-connected-stations"></a>Layout für verbundene RDP-over-LAN-Stationen
Es gibt keine Einschränkungen hinsichtlich der physischen Entfernung für LAN-Clients. Solange Sie sich im LAN befinden, können Sie eine Verbindung mit dem Multipoint Services-System herstellen.

## <a name="using-additional-hubs"></a>Verwenden zusätzlicher Hubs
Zusätzliche Hubs können verwendet werden, um die Installation zu vereinfachen. Es gibt drei Arten von Hubs, die in einem Multipoint Services-System verwendet werden:

-   [Stations Hubs](#station-hubs)

-   [Zwischen Hubs](#intermediate-hubs)

-   [Downstreamhubs](#downstream-hubs)

### <a name="station-hubs"></a>Stations Hubs
Ein stationshub ist ein externer Hub, der einer Multipoint Services-Station zugeordnet ist. Der stationshub muss mindestens über eine Tastatur eingebunden werden. Es können auch zusätzliche Peripheriegeräte angefügt werden. Ein stationshub kann ein generischer USB-Hub sein, der der Spezifikation USB 2,0 oder höher entspricht. Stations Hubs sollten extern eingeschaltet werden, wenn hoch betriebene Geräte ein Plug-in für Sie durchführt.

**Stammphub** Ein USB-Hub, der auf dem Host Controller auf der Hauptplatine eines Computers integriert ist, wird als *Stammhub*bezeichnet. Stations Hubs sind in der Regel an den Stammhub auf dem Computer angeschlossen, auf dem Multipoint Services ausgeführt wird.

> [!NOTE]
> Stamm-Hubs sollten nicht als Stations Hubs verwendet werden. Wenn USB-Ports auf einem Computer integriert sind, ist es oft nicht möglich, zu ermitteln, mit welchem USB-Stammhub eine interne Verbindung besteht. Wenn Sie also eine Station-Tastatur und die Maus direkt an die USB-Anschlüsse des Computers angeschlossen haben, können Sie die Tastatur und die Maus an verschiedene USB-Stamm Hubs anpacken. Um sicherzustellen, dass sich die Tastatur und die Maus auf demselben Hub befinden, können Sie einen stationshub in den USB-Anschluss des Computers einbinden und dann die Tastatur und die Maus an den stationshub anschließen.

**Daisy-Verkettung-Stationen** Es ist möglicherweise einfacher, Station Hubs mit einem anderen stationshub zu verbinden, als nicht direkt mit dem Computer. Dies ermöglicht es Ihnen, einen USB-Hub mit einem stationshub zu verbinden, der bereits an den Computer angeschlossen ist, sodass Sie über einen stationshub verfügen, der an einen anderen stationshub angeschlossen ist.

Es dürfen nicht mehr als drei USB-Clients oder stationshub, die in der Zwischenzeit mit einem Punkt verkettet sind Es muss darauf geachtet werden, dass die USB-Bandbreite nicht überschritten wird, wenn die-Station-Hubs für die

![Verkettungsstationen](./media/WMS_diagram5.gif)

**Abbildung 6** Multipoint Services-System mit an sich verketteten Stationen

### <a name="intermediate-hubs"></a>Zwischen Hubs
Ein Zwischenhub ist ein Hub zwischen dem Server und einem stationshub. Sie wird in der Regel verwendet, um die Anzahl der Ports zu erhöhen, die für Station Hubs verfügbar sind, oder um die Entfernung der Stationen vom Computer zu verlängern. Es wird empfohlen, zwischen einem stationshub und dem Server höchstens zwei zwischen Hubs zu verwenden.

Zwischen Hubs müssen USB 2,0 oder höher sein, und Sie müssen extern eingeschaltet werden. USB 3,0 wird zwischen dem Server und dem Zwischenhub empfohlen, wenn Sie mehr als drei USB-Clients mit einem Zwischenhub verbinden.

### <a name="downstream-hubs"></a>Downstreamhubs
Ein downstreamhub ist mit einem stationshub verbunden, um weitere verfügbare Ports für Stations Geräte hinzuzufügen. Abhängig von den Geräten, die mit dem Hub verbunden sind, kann ein downstreamhub extern oder durch Busbetrieb betrieben werden.

![Mehrere USB-Verbindungen ohne Client](./media/WMS_diagram4.gif "WMS_diagram4")

**Abbildung 7** Multipoint Services-System mit einem Zwischenhub, einem stationshub und einem Downstream-Hub

## <a name="users-stations-and-computers"></a>Benutzer, Stationen und Computer
Die Anzahl der benötigten Stationen hängt von der Anzahl der Benutzer ab, die gleichzeitig auf die Computer zugreifen müssen, auf denen Multipoint Services ausgeführt wird. Ebenso hängt die Anzahl der Computer, auf denen Multipoint Services ausgeführt wird, von der Gesamtanzahl der erforderlichen Stationen ab. An Direct-Video-Connected-Stationen, auf USB-Clients angeschlossene Stationen und an RDP-over-LAN-Verbindungen werden als Stationen angesehen. Wenn außerdem die Split-Screen-Funktionalität verwendet wird, wird jede Hälfte als Station betrachtet.

## <a name="power-considerations"></a>Energieaspekte
Die folgenden Komponenten erfordern Zugriff auf einen Strom oder eine Steckdose:

-   Server
-   Monitore
-   Zwischen Hubs \( bei Verwendung\)
-   Einige USB-Clients
-   USB-Geräte, wie z. b. externe Speichergeräte und DVD-Laufwerke

## <a name="sample-multipoint-services-system-layouts"></a>Beispiel für Multipoint Services-systemlayouts
Abhängig von den verfügbaren Möbeln, der Größe des Raums, der Anzahl der Computer, auf denen Multipoint Services ausgeführt wird, und den Stationen im Raum gibt es eine Vielzahl von Möglichkeiten, wie die physischen Stationen angeordnet werden können. In den folgenden Diagrammen werden fünf mögliche Alternativen veranschaulicht.

> [!NOTE]
> Einige dieser Diagramme zeigen einen Projektor, der mit dem Multipoint Services-System verbunden ist. Dies ist nur ein Beispiel: das Einschließen eines Projektors in ein Multipoint Services-System ist optional.

**Computer Labor** In diesem Setup werden die Stationen um die Wände des Raums angeordnet, wobei die Schüler/Studenten die Wände sehen.

![Einrichtung eines Computerkursraums](./media/WMS_ComputerLabLayout.gif)

**Gruppen** In diesem Setup sind drei Computer vorhanden, auf denen Multipoint Services ausgeführt wird, wobei Stationen um jeden Computer gruppiert sind.

![Mit Serverpods konfigurierter Kursraum](./media/WMS_ClassroomPods.gif)

**Vortragsraum** In diesem Setup werden die Stationen in Zeilen eingerichtet. Ein Vorteil dieses Setups besteht darin, dass alle Schüler/Studenten dem Dozenten ausgesetzt sind.

![Als Vorlesungsraum konfigurierter Kursraum](./media/WMS_LectureRoom.gif)

**Aktivitäts Center** Diese Einrichtung besteht aus einem herkömmlichen Vortragsraum Layout für die Schalter und verfügt über einen separaten Bereich mit einem einzelnen Computer, auf dem Multipoint Services mit den zugehörigen Stationen ausgeführt wird.

![Multipoint Services-Aktivitäts Center](./media/WMSActivityCenter.gif)

**Small Business Office** Bei diesem Setup wird der Computer, auf dem Multipoint Services ausgeführt wird, an einem zentralen Ort platziert, und die Benutzer im gesamten Büro stellen eine Verbindung mit dem Computer her, indem Sie ein \( LAN verwenden \) .

![Verbundene USB-Station ohne Clients](./media/Diagram1.gif)