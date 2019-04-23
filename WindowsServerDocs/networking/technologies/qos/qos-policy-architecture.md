---
title: QoS-Richtlinie-Architektur
description: Dieses Thema enthält eine Übersicht über Quality of Service (QoS)-Richtlinie, die Gruppenrichtlinie zu verwenden, um die Netzwerkbandbreite für Datenverkehr von bestimmten Anwendungen und Diensten in Windows Server 2016 zu priorisieren kann.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 25097cb8-b9b1-41c9-b3c7-3610a032e0d8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bad37ba3558137b02ae495fe8dd9be2c903cdd97
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843141"
---
# <a name="qos-policy-architecture"></a>QoS-Richtlinie-Architektur

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, Informationen über die Architektur von QoS-Richtlinie.

Die folgende Abbildung zeigt die Architektur des richtlinienbasierten QoS.

![Architektur der QoS-Richtlinie](../../media/QoS/QoS-Policy-Architecture.jpg)

Die Architektur des richtlinienbasierten QoS umfasst die folgenden Komponenten:

- **Gruppenrichtlinienclient-Dienst Gruppe**. Ein Windows-Dienst, der Benutzer- und Konfiguration der gruppenrichtlinieneinstellungen verwaltet.

- **Gruppenrichtlinienmodul**. Eine Komponente von der Gruppenrichtlinienclient-Dienst, die Benutzer und Computer-gruppenrichtlinieneinstellungen aus Active Directory, beim Starten und in regelmäßigen Abständen abruft, sucht nach Änderungen \(standardmäßig alle 90 Minuten\). Wenn Änderungen erkannt werden, ruft die Gruppenrichtlinien-Engine die neuen gruppenrichtlinieneinstellungen ab. Die Gruppenrichtlinien-Engine verarbeitet die eingehenden GPOs und die clientseitige Erweiterung der QoS-informiert, wenn die QoS-Richtlinien aktualisiert werden.

- **Die clientseitige Erweiterung der QoS-**. Eine Komponente von der Gruppenrichtlinienclient-Dienst, der wartet, einer Angabe über das von der Gruppenrichtlinien-Engine, die die QoS-Richtlinien geändert wurden und informiert das Modul der QoS-Überprüfung.

- **TCP/IP-Stack**. Der TCP/IP-Stapel, der enthält integrierte Unterstützung für IPv4 und IPv6- und Windows-Filterplattform unterstützt. 

- **QoS-Prüfung**. Modul A-Komponente in den TCP/IP-Stapel, der wartet auf Anzeichen, dass die clientseitige Erweiterung der QoS-QoS-richtlinienänderungen, die QoS-Richtlinieneinstellungen abruft und interagiert mit der Transportschicht und Pacer.sys Datenverkehr intern zu markieren, die die QoS entspricht Richtlinien.

- **NDIS 6.x**. Eine standard-Schnittstelle zwischen Kernelmodustreiber Netzwerk und das Betriebssystem Windows Server und Client-Betriebssystemen. NDIS 6.x unterstützt einfache Filter, mit denen eine vereinfachte Treiber für NDIS-intermediate-Treiber und -Miniporttreiber ist, die eine bessere Leistung bietet.

- **QoS-Netzwerk-Anbieterschnittstelle \(NPI\)**. Eine Schnittstelle für den Kernelmodus-Treiber für die Interaktion mit Pacer.sys.

- **Pacer.sys**. Ein NDIS 6.x Filtertreiber, der steuert, paketplanung für Richtlinienbasierte QoS und für den Datenverkehr der Anwendungen, die die generische QoS \(GQoS\) und Steuerung des Datenverkehrs \(TC\) APIs. Pacer.sys ersetzt Psched.sys in Windows Server 2003 und Windows XP. Pacer.sys, die mit der QoS Packet Scheduler-Komponente in den Eigenschaften einer Netzwerkverbindung oder der Adapter installiert ist.

Im nächsten Thema in diesem Handbuch finden Sie unter [QoS-Richtlinie Szenarien](qos-policy-scenarios.md).

Das erste Thema in diesem Handbuch finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).

