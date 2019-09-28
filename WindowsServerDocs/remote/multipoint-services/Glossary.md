---
title: Glossar
description: Definiert Wörter, Begriffe und Konzepte in Multipoint Services
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 807bce1d-b993-49c6-9783-b01a3c55846c
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 0c966f0c8e1ad239769c58e4648832ae5020d0dc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389650"
---
# <a name="glossary"></a>Glossar
**Zuordnen einer Station**  
Zum Angeben des Monitors, der mit der Station und den Peripheriegeräten verwendet wird, z. b. Tastatur und Maus. Bei direkt mit dem Video verbundenen Stationen erfolgt dies durch Drücken eines angegebenen Schlüssels auf der Tastatur der Station, wenn Sie dazu aufgefordert werden. Bei USB-Verbindungen mit Clientverbindungen erfolgt dies in der Regel automatisch.  
  
**Bus-gestützter Hub**  
Ein Hub, der seine gesamte Leistung von der USB-Schnittstelle des Computers zeichnet. Für Bus gestützte Hubs sind keine separaten Stromverbindungen erforderlich. Viele Geräte funktionieren jedoch nicht mit dieser Art von Hub, da Sie mehr Energie benötigen, als diese Art von Hub bereitstellt.  
  
**Konsolenmodus**  
In einem der beiden Modi kann Multipoint Services gestartet werden. Wenn sich das System im Konsolenmodus befindet, sind keine Stationen zur Verwendung verfügbar. Stattdessen werden alle Monitore als einzelner erweiterter Desktop für die Konsolen Sitzung des Computer Systems behandelt. Der Konsolenmodus wird normalerweise verwendet, um Software zu installieren, zu aktualisieren oder zu konfigurieren, die nicht ausgeführt werden kann, wenn sich der Computer im Stations Modus befindet. Siehe auch: *Stations Modus*.  
  
**direkt mit Videos verbundene Station**  
Eine Multipoint-Station, die aus einem Monitor besteht, der direkt mit einer Videoausgabe auf dem Server verbunden ist, und mindestens eine Tastatur und eine Maus enthält, die über einen USB-Hub mit dem Server verbunden sind.  
  
**Domänen Benutzerkonto**  
Ein Benutzerkonto, das auf einem Domänen Computer gehostet wird. Der Zugriff auf Domänen Benutzerkonten kann von jedem Computer aus erfolgen, der mit der Domäne verbunden ist, und ist nicht an einen bestimmten Computer gebunden.  
  
**Downstream-Hub**  
Ein Hub, der mit einem stationshub verbunden ist, um weitere verfügbare Ports für Stations Geräte hinzuzufügen. An einen Downstream-Hub darf keine Tastatur angefügt sein.  
  
**extern gestützter Hub**  
Dieser Hub wird auch als selbst gestützter Hub bezeichnet und nutzt seine Leistungsfähigkeit von einer externen Netzteil Einheit. aus diesem Grund kann ein vollständiger Strom (bis zu 500 mA) für jeden Port bereitgestellt werden. Viele Hubs können als busgestützte oder extern betriebene Hubs betrieben werden.  
  
**HID-consumersteuerunggerät**  
Ein Eingabegeräte (HID) ist ein Computer Gerät, das direkt mit den Menschen interagiert. Es kann Eingaben aus der Eingabe oder Ausgabe an Menschen übermitteln. Beispiele hierfür sind Tastatur, Maus, Trackball, Touchpad, zeige Stick, Grafik Tabelle, Joystick, Fingerabdruckscanner, Gamepad, Webcam, Headset und Fahr simulatorgeräte. Ein geverstecktem consumersteuerunggerät ist eine bestimmte Klasse von verborgenen Geräten, die audiovolumensteuerelemente und Multimedia-und Browser-Steuerelement Tasten umfasst.  
  
**Zwischenhub**  
Ein Hub zwischen einem *Stammhub* auf dem Server und einem stationshub. Zwischen Hubs werden in der Regel verwendet, um die Anzahl der verfügbaren Ports für Stations Hubs zu erhöhen oder um die Entfernung der Stationen vom Computer zu verlängern.  
  
**lokales Benutzerkonto**  
Ein Benutzerkonto auf einem bestimmten Computer. Ein lokales Benutzerkonto ist nur auf dem Computer verfügbar, auf dem das Konto definiert ist.  
  
**multifunktionshub**  
Siehe *USB-Zero-Client*.  
  
**Multipoint Services-System**  
Eine Sammlung von Hardware und Software, die aus einem Computer besteht, auf dem Windows Server 2016 mit aktivierter Multipoint Services-Rolle und mindestens einer Multipoint-Station installiert ist. Weitere Informationen zu systemlayoutoptionen finden Sie unter [Planen von Multipoint Services-Websites](MultiPoint-services-Site-Planning.md) .  
  
**partition**  
Ein Abschnitt des Speicherplatzes auf einem physischen Datenträger, der so funktioniert, als handele es sich um einen separaten Datenträger.  
  
**primäre Station**  
Die Station, die beim Starten von Multipoint Services zuerst gestartet werden soll. Die primäre Station kann von einem Administrator verwendet werden, um auf Startmenüs und-Einstellungen zuzugreifen. Wenn Sie nicht vom Administrator verwendet wird, kann Sie als normale Station verwendet werden (Sie muss nicht ausschließlich für die Verwaltung reserviert werden). Der Monitor der primären Station muss stets direkt mit einer Videoausgabe auf dem Computer verbunden sein, auf dem Multipoint Services ausgeführt wird. Siehe auch: Station.  
  
**RDP-über-LAN-verbundene Station**  
Eine Station, bei der es sich um einen Thin Client, herkömmlichen Desktop Computer oder Laptop Computer handelt, der mithilfe von Remotedesktopprotokoll (RDP) über das lokale Netzwerk (Local Area Network, LAN) eine Verbindung mit Multipoint Services herstellt.  
  
**stammphub**  
Ein USB-Hub, der auf dem Host Controller auf der Hauptplatine eines Computers integriert ist.  
  
**Bildschirm teilen**  
Eine Station, in der ein einzelner Monitor verwendet werden kann, um zwei unabhängige Benutzer Desktops anzuzeigen. Zwei Gruppen von Hubs, Tastaturen und Mäusen sind einem einzigen Monitor zugeordnet. Der linken Seite des Monitors wird ein Satz zugeordnet, und die andere Gruppe ist der rechten Seite des Monitors zugeordnet.  
  
**Standard Station**  
Im Gegensatz zur *primären Station*, die von einem Administrator verwendet werden kann, um auf Startmenüs zuzugreifen, werden Standard Stationen keine Startmenüs angezeigt, und Sie können erst nach Abschluss des Startvorgangs von Multipoint Services verwendet werden. Siehe auch: Station.  
  
*Senders*  
Benutzer Endpunkt zum Herstellen einer Verbindung mit dem Computer, auf dem Multipoint Services ausgeführt wird. Drei Stations Typen werden unterstützt: Direct-Video-Connected, USB-Zero-Client-Connected und RDP-over-LAN-verbundene Stationen. Weitere Informationen zu Stationen finden Sie unter [Multipoint-Stationen](MultiPoint-services-Stations.md).  
  
**stationshub**  
Ein USB-Hub, der einem Monitor zugeordnet ist, um eine Multipoint-Station zu erstellen. Er verbindet Peripheriegerät-USB-Geräte mit Multipoint Services. Siehe auch: *USB-Zero-Client* und *USB-Hub*.  
  
**Stations Modus**  
In einem der beiden Modi kann Multipoint Services gestartet werden. In der Regel befindet sich das Multipoint Services-System im Stations Modus. Im Stations Modus Verhalten sich die Multipoint Services-Stationen so, als ob jede Station ein separater Computer ist, auf dem das Windows-Betriebssystem ausgeführt wird, und mehrere Benutzer können das System gleichzeitig verwenden. Siehe auch: *Konsolenmodus*.  
  
**USB-Hub**  
Ein generischer Multiport-USB-erweiterungshub, der den Spezifikationen für den universellen seriellen Bus (USB) 2,0 oder höher entspricht. Solche Hubs verfügen in der Regel über mehrere USB-Ports, sodass mehrere USB-Geräte mit einem einzelnen USB-Anschluss auf dem Computer verbunden werden können. USB-Hubs sind in der Regel separate Geräte, die *extern* oder im *Bus betrieben*werden können. Einige andere Geräte, z. b. einige Tastaturen und Videomonitore, können einen USB-Hub in Ihren Entwurf integrieren. Siehe auch: *USB-Zero-Client*.  
  
**USB-over-Ethernet-Client**  
Ein USB-Null-Client, der über eine LAN-Verbindung anstelle eines USB-Ports eine Verbindung mit dem Computer herstellt. Dieser Client wird dem Server als USB-Gerät angezeigt, auch wenn die Daten über die Ethernet-Verbindung gesendet werden.  
  
**USB-Zero-Client**  
Ein erweiterungshub, der über einen USB-Anschluss eine Verbindung mit dem Computer herstellt und die Verbindung verschiedener nicht-USB-Geräte mit dem Hub ermöglicht. USB-Clients werden von bestimmten Hardwareherstellern erstellt und erfordern die Installation eines gerätespezifischen Treibers. USB-Null-Clients unterstützen das Verbinden eines Video Monitors (über VGA, DVI usw.) und Peripheriegeräte (über USB, manchmal PS/2 und Analoge Audiodaten). Der USB-Null-Client kann *extern* oder per *busstrom betrieben*werden. Siehe auch *USB-Hubs*.  
  
**Verbindung zwischen USB-Client und Verbindung**  
Eine Multipoint Services-Station, die (mindestens) einen Monitor, eine Tastatur und eine Maus umfasst, die über einen USB-Client mit dem Server verbunden sind.  
  
