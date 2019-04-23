---
title: Glossar
description: Definiert die Wörter, Begriffe und Konzepte in MultiPoint Services
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 807bce1d-b993-49c6-9783-b01a3c55846c
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 4449d2d6fb87f74496b7d482a7a7263f703c7822
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831111"
---
# <a name="glossary"></a>Glossar
**Ordnen Sie einer station**  
Um anzugeben, welcher Monitor für die Station und Peripheriegeräte, z. B. eine Tastatur und Maus verwendet wird. Für die direkte video verbundene Stationen erfolgt dies durch Drücken von einem angegebenen Schlüssel auf der Station-Tastatur, wenn Sie dazu aufgefordert werden. Für USB verbundene zero-Client, dies geschieht in der Regel automatisch.  
  
**Bus-gestützte hub**  
Einen Hub, der alle verbundenen Möglichkeiten von USB-Schnittstelle des Computers zeichnet. Bus-gestützte Hubs erforderlich eigene Stromversorgung Verbindungen nicht. Viele Geräte funktionieren nicht bei dieser Art von Hub jedoch, da sie mehr Energie benötigen als diese Art des Hubs bietet.  
  
**Konsolenmodus**  
Einer der beiden Modi MultiPoint Services kann starten. Wenn das System im Konsolenmodus ausgeführt ist, sind keine Stationen für die Verwendung verfügbar. Stattdessen werden alle Monitore für einen einzigen erweiterte Desktop für die konsolensitzung des Computersystems behandelt. Konsolenmodus dient normalerweise zum Installieren, aktualisieren oder Konfigurieren von Software, wenn der Computer im stationsmodus ist nicht möglich. Siehe auch: *stationsmodus*.  
  
**direct-video-connected station**  
Eine MultiPoint-Station, die von einem Monitor besteht, die direkt an eine video-Ausgabe auf dem Server, und klicken Sie auf ein Minimum verbunden ist, enthält sie eine Tastatur und Maus, die über ein USB-Hub auf dem Server verbunden sind.  
  
**Domänenbenutzerkonto**  
Ein Benutzerkonto, das gehostet wird auf einem Computer. Domänenbenutzerkonten zugegriffen werden können, von einem beliebigen Computer, die mit der Domäne verbunden ist, und sie sind nicht auf einem bestimmten Computer gebunden.  
  
**Downstream-hub**  
Ein Hub, der zum Hinzufügen von mehr Ports für Geräte der Station mit einem stationshub verbunden ist. Ein downstream-Hub darf nicht mit eine Tastatur verbunden sein.  
  
**extern Stromversorgung**  
Auch bekannt als nimmt einen Hub mit eigener dieser Hub verbundenen Möglichkeiten von einer externen Netzteil; aus diesem Grund können sie volle Leistung bereitstellen (bis zu 500 mA) für jeden Port. Viele Hubs können als Bus betriebene oder extern-gestützte Hubs ausgeführt werden.  
  
**HID-Consumer-Steuerelement-Gerät**  
Ein Gerät HID (Human Interface) ist ein Gerät für Computer, die direkt mit Menschen interagiert. Sie akzeptieren Eingaben aus oder Ausgabe für Menschen übermitteln. Beispiele sind die Tastatur, Maus, Trackball, Touchpad, Zeigegerät, Grafiktabelle, Joystick, fingerabdruckscanners, Gamepad, Webcam, Kopfhörer und fahrbedingungen Simulator-Geräte. Eine HID-Consumer-Steuerelement-Gerät ist eine bestimmte Objektklasse HID-Geräte, die audio-Lautstärkeregler und Multimedia und Browser-Steuerelement-Schlüssel enthält.  
  
**zwischengeschalteter hub**  
Einen Hub, der zwischen einem *Root-Hub* auf dem Server und einen stationshub. Intermediate-Hubs werden normalerweise verwendet, um die Anzahl der verfügbaren Anschlüsse für Stationen Hubs erhöhen oder eine Erweiterung für die Entfernung Stationen auf dem Computer.  
  
**lokales Benutzerkonto**  
Ein Benutzerkonto auf einem bestimmten Computer. Ein lokales Benutzerkonto steht nur auf dem Computer, in dem das Konto definiert ist.  
  
**multifunktionshub**  
Finden Sie unter *USB-0 (null) Client*.  
  
**MultiPoint Services-system**  
Eine Auflistung von Hardware und Software, die von einem Computer besteht, die Windows Server 2016 mit aktivierter MultiPoint Services-Rolle installiert und mindestens eine MultiPoint-Station verfügt. Weitere Informationen zu den Optionen des System-Layout, finden Sie unter [MultiPoint Services-Standortplanung](MultiPoint-services-Site-Planning.md)  
  
**partition**  
Ein Abschnitt des Speicherplatzes auf einem physischen Datenträger, der Funktionen, als ob es sich um einen separaten Datenträger ist.  
  
**primäre station**  
Die Station, die die erste gestartet wird, wenn MultiPoint Server gestartet wird. Die primäre Station kann von einem Administrator verwendet werden, Start-Menüs und Einstellungen für den Zugriff auf. Wenn es nicht vom Administrator verwendet wird, kann es als eine normale Station verwendet werden, (es muss nicht ausschließlich für die Verwaltung reserviert werden sollen). Monitor für die primäre Station muss immer direkt an eine Ausgabe der video auf dem Computer verbunden sein, das MultiPoint Services ausgeführt wird. Siehe auch: Station.  
  
**RDP-Over-LAN-Verbindung station**  
Eine Station, die eine thin Client, Sie traditionelle Desktop- oder Laptopcomputer, die mit MultiPoint Services über Remote Desktop Protocol (RDP) über das lokale Netzwerk (LAN) her.  
  
**Root-hub**  
Ein USB-Hub, der mit dem Hostcontroller, auf der Hauptplatine des Computers integriert ist.  
  
**split screen**  
Eine Station, in denen ein einzelnes Monitors verwendet werden kann, um zwei unabhängige Benutzerdesktops anzuzeigen. Zwei Sätze von Hubs, Tastaturen und Mäusen sind mit einem einzelnen Bildschirm verknüpft. Ein Satz bezieht sich auf der linken Seite des Bildschirms, und das andere ist mit der rechten Seite des Monitors verknüpft.  
  
**Standard-station**  
Im Gegensatz zu den *primäre Station*, die von einem Administrator für den Zugriff Startup-Menüs verwendet werden können, standard Stationen Start Menüs nicht angezeigt und sie können nur verwendet werden, nachdem MultiPoint Services den Startprozess abgeschlossen wurde . Siehe auch: Station.  
  
*station*  
Benutzer-Endpunkt für die Verbindung mit dem Computer, auf dem MultiPoint Services ausgeführt wird. Drei Station-Typen werden unterstützt: im Video direkt verbundene USB-0 (null)-Client-verbunden und RDP-Over-LAN-Verbindung Stationen. Weitere Informationen zu den Stationen, finden Sie unter [MultiPoint-Stationen](MultiPoint-services-Stations.md).  
  
**station hub**  
Einen USB-Hub, der einen Monitor, um das Erstellen einer MultiPoint-Station zugeordnet wurde. USB-Peripheriegeräte mit MultiPoint Services hergestellt. Siehe auch: *USB-0 (null) Client* und *USB-Hub*.  
  
**stationsmodus**  
Einer der beiden Modi MultiPoint Services kann starten. Normalerweise ist das MultiPoint Services-System im stationsmodus. Im stationsmodus, verhalten sich die MultiPoint Services-Stationen, wie bei jeder Station wird als separater Computer, der die Windows-Betriebssystem ausgeführt wird und mehrere Benutzer können das System zur gleichen Zeit verwenden. Siehe auch: *Konsolenmodus*.  
  
**USB-hub**  
Eine generische multiport USB-erweiterungshub, der mit den Spezifikationen USB (USB) 2.0 oder höher kompatibel ist. Solche Hubs verfügen typischerweise über mehrere USB-Anschlüsse, wodurch mehrere USB-Geräte mit einem einzelnen USB-Anschluss auf dem Computer verbunden sein. USB-Hubs sind üblicherweise separate Geräte, die sein können *extern unterstützt* oder *Bus betriebene*. Einige andere Geräte, z.B. manche Tastaturen oder Videomonitoren, können einen USB-Hub in ihren Entwurf integrieren. Siehe auch: *USB-0 (null) Client*.  
  
**USB-Ethernet-0 (null)-client**  
Ein USB-0 (null)-Client, der Verbindung mit dem Computer über einen USB-Anschluss, anstatt eine LAN-Verbindung. Dieser Client wird an den Server angezeigt, wie ein USB-Gerät auch über die Daten über die Ethernet-Verbindung gesendet wird.  
  
**USB-0 (null)-client**  
Ein erweiterungshub, der eine Verbindung mit dem Computer über einen USB-Anschluss und das Anschließen einer Reihe von nicht-USB-Geräte am Hub ermöglicht. USB-0 (null)-Clients werden von bestimmten Hardwareherstellern erstellt, und sie erfordern die Installation eines gerätespezifischen Treibers. USB-0 (null)-Clients unterstützen das Herstellen einer Verbindung einen Videomonitor (über VGA-Monitor, DVI- und So weiter) und Peripheriegeräte (über USB, manchmal PS/2 und analoge Audio). Die-USB-NULL-Client kann werden *extern unterstützt* oder *Bus betriebene*. Siehe auch *USB-Hubs*.  
  
**USB-0 (null)-Client eine Verbindung hergestellt station**  
Eine MultiPoint Services-Station, die aus (als mindestens) einen Monitor besteht Tastatur und eine Maus, die über ein USB-0 (null)-Client auf dem Server verbunden sind.  
  
