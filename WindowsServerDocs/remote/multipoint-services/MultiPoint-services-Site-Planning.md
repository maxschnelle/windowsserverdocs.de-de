---
title: MultiPoint Services-Standortplanung
description: Planungsinformationen für das MultiPoint Services-Bereitstellungen in Windows Server 2016
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 063783cd-d748-489e-b175-46eadc993f7a
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 60d2e1fedc018136f5668d55a8afb2e0574d94de
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845071"
---
# <a name="multipoint-services-site-planning"></a>MultiPoint Services-Standortplanung
Sie sollten erwägen, den Speicherort, in dem einen oder mehrere Computer mit MultiPoint Services und die zugehörigen Stationen bereitgestellt wird.  
  
Der Computer mit MultiPoint Services-Rolle müssen bequemen Zugriff, um eine Stromversorgung und den Peripheriegeräten, bei denen, die direkt an die Klasse, z. B. ein Drucker verbunden sind. Darüber hinaus müssen der Computer mit MultiPoint-Dienste komfortablen Zugriff auf eine Netzwerkverbindung. Eine Netzwerkverbindung ist erforderlich, für den Zugriff auf das Internet und, sofern verfügbar, einem LAN.  
  
Die folgenden: zusätzliche Faktoren zu berücksichtigen  
  
-   MultiPoint Services-System eingerichtet in einem bestimmten Raum, oder es eingerichtet für eine parallele Warenkorb oder Tabelle, damit sie von Ort zu Ort verschoben werden kann?  
  
    > [!NOTE]  
    > Wenn Sie ein mobile-Setup verwenden möchten, können Sie *zuordnen* Stationen mit MultiPoint Services jedes Mal, wenn Sie erneut verbinden, damit sichergestellt ist, dass jede Tastatur und Maus mit den entsprechenden Monitor verknüpft ist.  
  
-   Sich die primäre Station befindet neben den anderen Stationen, oder werden separate? Z. B. wenn das MultiPoint Services-System in einem Schulungsraum eingerichtet ist, wird die primäre Station auf die der Lehrkraft Helpdesk und die standard-Stationen an anderer Stelle im Raum werden positioniert? Beim Neustart des Computers, auf dem MultiPoint Services ausgeführt wird, ist, wird die primäre Station auf die Startbildschirme zugreifen. Wenn Sie sich für diese Ebene des Zugriffs auf ein Classroom-Einstellung befürchten, empfiehlt es sich, die primäre Station in der Lehrkraft Helpdesk zu stellen.  
  
-   Wie viele Stationen im Raum passt?  
  
-   Benötigen Sie ein Netzwerk? Eine Einzelserver-Lösung verwendet direkte Video verbunden oder USB-0 (null)-Client Stationen verbunden ist nicht mit einem Netzwerk erforderlich.  
  
-   Gibt es genügend Netzwerkverbindungen im Raum unterstützen die erforderliche Anzahl von Computern, auf dem MultiPoint Services ausgeführt wird  
  
-   Wo befinden sich die Steckdosen?  
  
-   Benötigen Sie eine zusätzliche Anzeigegerät, z. B. einem Projektor? Wenn Sie einen Projektor verwenden möchten, hängt es von der Obergrenze, oder wird es für eine Tabelle werden positioniert?  
  
-   Welche Art von Kabel benötigt werden, und wie viele wird, die benötigt werden?  
  
-   Beachten Sie, wie Sie in der Zukunft erweitern möchten. Werden Sie mehrere Stationen hinzugefügt?  
  
## <a name="station-layout-and-configuration"></a>Station Layout und die Konfiguration  
Das physische Layout der Website beeinträchtigen Ihrer Wahl Station-Typs. Weitere Informationen zu den anderen Station finden Sie unter [MultiPoint-Stationen](MultiPoint-services-Stations.md) in diesem Handbuch. Mehrere Station-Typen sind in einem einzigen MultiPoint Services zulässig. Dies bietet Ihnen zusätzliche Flexibilität zur Erfüllung Ihrer Anforderungen für die Installation.  
  
### <a name="layout-for-direct-video-connected-stations"></a>Layout für die im Video direkt verbundene Stationen  
  
-   Für eine Station Direct-Video-Verbindung wird der Abstand zwischen den Monitoren und den Computer durch die Länge des Videos Kabel beschränkt.  
  
-   Verwendung von intermediate Hubs oder eine Daisychain-Verkettung stationshubs wird für einfache Bereitstellung unterstützt, aber die maximal empfohlene Anzahl von aufeinander folgenden Hubs ist der dritte. Dies bedeutet, dass, die der maximale Abstand zwischen dem Computer an den stationshub 15 Verbrauchseinheiten gemessen werden, da jede USB 2.0-Kabel die maximale Länge von fünf Werte aufweist.  
  
> [!IMPORTANT]  
> Es muss immer mindestens eine direkte video verbundenen Station pro Computer fungieren als primäre Station vorhanden sein.  
  
### <a name="layout-for-usb-zero-client-connected-stations"></a>Layout für USB-0 (null) Client verbundene Stationen  
  
-   Verwendung von intermediate Hubs oder eine Daisychain-Verkettung stationshubs wird für einfache Bereitstellung unterstützt, aber die maximal empfohlene Anzahl von aufeinander folgenden Hubs ist der dritte. Dies bedeutet, dass, die der maximale Abstand zwischen dem Computer an den stationshub 15 Verbrauchseinheiten gemessen werden, da jede USB 2.0-Kabel die maximale Länge von fünf Werte aufweist.  
  
-   Die maximal empfohlene Anzahl von USB-keine Clients mit einer einzelnen zwischengeschalteter Hub verbunden ist drei.  
  
    > [!NOTE]  
    > Einige Computer mit einem generischen Hub stammen, auf der Hauptplatine, die wirkt sich das Hinzufügen eines zusätzlichen Hubs zwischen den *Root-Hub* des Computers und der stationshubs.  
  
-   Wenn Video häufig verwendet werden wird, empfiehlt es sich, dass Sie nicht mehr als zwei USB-0 (null)-Clients mit einem USB-Anschluss auf dem Server verbinden. Wenn ein zwischengeschalteter Hub verwendet wird, sollten nur zwei USB-0 (null)-Clients z. B. darauf verbunden werden. Oder wenn Sie eine Daisychain sind Verketten von USB-0 (null)-Clients nur zwei USB-NULL-Clients sollten miteinander verkettet werden. Das Hinzufügen der einzelnen USB-0 (null) an den USB-Anschluss auf dem Server verringert sich die Videos verfügbare Bandbreite.  
  
-   Wenn Sie mehr als drei USB-0 (null)-Clients auf einem einzelnen USB-Anschluss auf dem Server eine Verbindung herstellen möchten, wird empfohlen, verwenden USB-3.0 zwischen dem Server und die zwischengeschalteter Hub.  
  
> [!NOTE]  
> Es wird empfohlen, dass Sie die Leistung Ihrer Anwendungen mit überprüfen und Hardware zu entscheiden, wie viele USB NULL-Clients, die Sie mit einem USB-Anschluss auf dem Server verbinden können.  
  
![Downstreamhubs](./media/WMS_diagram6.gif)  
  
**Abbildung 5** MultiPoint Services-System mit drei USB NULL Clients verbunden mit einem einzelnen intermediate-Hub  
  
### <a name="layout-for-rdp-over-lan-connected-stations"></a>Layout für RDP-Over-LAN verbundene Stationen  
Es gibt keine physische Entfernung Einschränkungen für die LAN-Clients. Solange sie sich auf das LAN befinden, können sie mit dem MultiPoint Services-System verbinden.  
  
## <a name="using-additional-hubs"></a>Zusätzliche Hubs verwenden  
Zusätzliche Hubs können verwendet werden, um die Installation zu erleichtern. Es gibt drei Arten von Hubs, die auf einem MultiPoint Services-System verwendet werden:  
  
-   [Stationshubs](#Station-hubs)  
  
-   [Zwischen hubs](#Intermediate-hubs)  
  
-   [Downstreamhubs](#Downstream-hubs)  
  
### <a name="station-hubs"></a>Stationshubs  
Ein stationshub ist eine externe Hub, der eine MultiPoint Services-Station zugeordnet wurde. Der stationshub müssen mindestens eine Tastatur an der es. Möglicherweise müssen sie auch zusätzliche angefügte Peripheriegeräten. Ein stationshub möglich ein generischer USB-Hub, der die USB 2.0 oder höher-Spezifikation entspricht. Stationshubs sollten extern unterstützt werden, wenn leistungsstarke Geräte-Plug-Ins werden werden.  
  
**Root-Hub** ein USB-Hub, die mit dem Hostcontroller, auf der Hauptplatine des Computers integriert ist, wird als bezeichnet ein *Root-Hub*. Stationshubs sind in der Regel im Netzbetrieb-in für den Root-Hub auf dem Computer, auf dem MultiPoint Services ausgeführt wird.  
  
> [!NOTE]  
> Root-Hubs sollten nicht als stationshubs verwendet werden. Wenn der USB-Anschlüsse in einem Computer integriert sind, kann häufig nicht um zu bestimmen, welche USB-Root-Hub intern mit verbunden sind. Wenn Sie angeschlossen-Station-Tastatur und Maus direkt auf das USB-Anschlüsse des Computers in Sie können tatsächlich unter Verwendung der-Tastatur und Maus an unterschiedliche USB-Stamm-Hubs in sein. Um sicherzustellen, dass die Tastatur und Maus auf dem gleichen Hub-Plug-in als stationshub mit USB-Anschluss des Computers, und klicken Sie dann die-Plug-Ins sind station Tastatur und Maus mit dem Hub.  
  
**Eine Daisychain-Verkettung Stationen** es möglicherweise einfacher, die nicht direkt an den Computer, sondern an einem anderen stationshub stationshubs. Dadurch können Sie die Verbindung einen USB-Hub an einen stationshub, der bereits-auf dem Computer, Netzbetrieb ist, damit Sie als stationshub mit einer anderen stationshub verbunden haben.  
  
Es darf sich nicht mehr als drei USB-0 (null)-Clients oder Station Hubs kaskadierenden nacheinander. Vorsicht, dass die USB-Bandbreite nicht überschritten wird, damit die station Hubs Wenn eine Daisychain-Verkettung.  
  
![Verketten von Stationen](./media/WMS_diagram5.gif)  
  
**Abbildung 6** MultiPoint Services-System mit Stationen eine Daisychain-Verkettung  
  
### <a name="intermediate-hubs"></a>Zwischen hubs  
Ein zwischengeschalteter Hub ist ein Hub, der zwischen dem Server und einen stationshub ist. Es wird normalerweise verwendet, um die Anzahl der Ports zu erhöhen, die für die stationshubs verfügbar sind oder eine Erweiterung für die Entfernung Stationen auf dem Computer. Es wird empfohlen, dass nicht mehr als zwei intermediate Hubs zwischen als stationshub und dem Server verwendet werden.  
  
Intermediate Hubs müssen USB 2.0 oder höher, und sie die extern ausgeschaltet werden müssen. USB 3.0 wird zwischen dem Server und die zwischenhub empfohlen, wenn Sie mehr als drei USB-0 (null)-Clients die ein zwischengeschalteter Hub verbinden.  
  
### <a name="downstream-hubs"></a>Downstreamhubs  
Ein downstream-Hub verbunden ist an einen stationshub mehr verfügbaren Ports für Geräte der Station hinzufügen. Ein downstream-Hub kann extern ausgeschaltet oder Bus betrieben, abhängig von den Geräten, die an den Hub Netzbetrieb sein.  
  
![Mehrere USB-0 (null)-Clientverbindungen](./media/WMS_diagram4.gif "WMS_diagram4")  
  
**Abbildung 7** MultiPoint Services-System mit ein zwischengeschalteter Hub als stationshub und einem downstream-Hub  
  
## <a name="users-stations-and-computers"></a>Benutzer, Computer und Stationen  
Die Anzahl der Stationen, die Sie benötigen, hängt von der Anzahl der Personen, die Zugriff auf den Computer, der MultiPoint Services zur gleichen Zeit ausgeführt hat. Ebenso hängt die Anzahl der Computer mit MultiPoint Services Sie müssen die Gesamtzahl der Stationen, die erforderlich sind. Im Video direkt verbundene Stationen, Stationen mit USB-0 (null)-Client-verbunden und RDP-Over-LAN verbundene Stationen sind alle betrachtet Stationen. Darüber hinaus: Wenn die geteilten-Funktion verwendet wird, wird jedes Halbjahr eine Station betrachtet.  
  
## <a name="power-considerations"></a>Power-Überlegungen  
Die folgenden Komponenten erfordern Zugriff auf eine Steckerleiste oder Outlet:  
  
-   Server  
-   Monitore
-   Hubs für fortgeschrittene \(verwendet\) 
-   Bei einigen USB-0 (null)-clients  
-   USB-Geräten, z. B. einige externe Speichergeräte und DVD-Laufwerke  
  
## <a name="sample-multipoint-services-system-layouts"></a>Beispiel MultiPoint Services-System-layouts  
Je nach den verfügbaren Möbel, die Größe des Raums, die Anzahl der Computer, auf dem MultiPoint-Dienste und die Stationen im Raum ausgeführt werden, gibt es eine Vielzahl von Methoden, mit denen die physische Stationen angeordnet werden können. Die folgenden Diagramme veranschaulichen die fünf mögliche Alternativen.  
  
> [!NOTE]  
> Einige diese Diagramme zeigen eines Projektors mit MultiPoint Services-System verbunden sind. Dies ist nur ein Beispiel. Das Einschließen von eines Projektors in einem MultiPoint Services-System ist optional.  
  
**Computerlabor** In diesem Setup die Stationen mit der Schüler/Studenten, die für die Wände rund um die Wände eines Raum angeordnet.  
  
![Einrichtung eines Computerkursraums](./media/WMS_ComputerLabLayout.gif)  
  
**Gruppen** In diesem Setup sind drei Computer, die mit Stationen, die auf jedem Computer gruppiert MultiPoint Services ausgeführt werden.  
  
![Mit Serverpods konfigurierter Kursraum](./media/WMS_ClassroomPods.gif)  
  
**Vortrag von Platz** In diesem Setup die Stationen werden eingerichtet in Zeilen. Ein Vorteil dieses Aufbaus ist, dass alle Studenten des Dozenten stehen.  
  
![Als Hörsaal konfigurierter Kursraum](./media/WMS_LectureRoom.gif)  
  
**Aktivitätszentrum** dieses Setup besteht aus einem herkömmlichen vorlesungsraum Layout für die Schreibtische, und kann auf einen separaten Bereich mit einem einzelnen Computer, die mit der zugehörigen Stationen MultiPoint Services ausgeführt wird.  
  
![MultiPoint Services-Aktivitätszentrum](./media/WMSActivityCenter.gif)  
  
**Kleinunternehmen Office** bei dieser Einstellung wird der Computer mit MultiPoint Services wird an einem zentralen Ort und Benutzer in der Office mit einem lokalen Netzwerk herstellen \(LAN\).  
  
![Verbundene USB-Station ohne Clients](./media/Diagram1.gif)