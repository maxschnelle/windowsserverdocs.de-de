---
title: QoS-Richtlinie-Architektur
description: Dieses Thema enthält eine Übersicht über die Richtlinie für Quality of Service (QoS), können Sie mithilfe einer Gruppenrichtlinie um Datenverkehr Netzwerkbandbreite von bestimmten Anwendungen und Diensten in Windows Server2016 priorisieren.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 25097cb8-b9b1-41c9-b3c7-3610a032e0d8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 00d36604c57add6bf9f45b0166b08c1fb15be467
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="qos-policy-architecture"></a>QoS-Richtlinie-Architektur

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie über die Architektur der QoS-Richtlinie enthält.

Die folgende Abbildungzeigt die Architektur des richtlinienbasierten QoS.

![Architektur der QoS-Richtlinie](../../media/QoS/QoS-Policy-Architecture.jpg)

Die Architektur des richtlinienbasierten QoS umfasst die folgenden Komponenten:

- **Gruppenrichtlinienclient-Dienst**. Ein Windowsdienst, der Einstellungen für Benutzer- und Konfiguration von Gruppenrichtlinien verwaltet.

- **Gruppenrichtlinienmodul**. Eine Komponente von der Gruppenrichtlinienclient-Dienst, die Benutzer- und Konfiguration einer Gruppenrichtlinie Einstellungen aus Active Directory nach dem Start und in regelmäßigen Abständen abruft überprüft, ob Änderungen \ (standardmäßig alle 90 Minutes\). Wenn Änderungen erkannt werden, ruft das Gruppenrichtlinienmodul die neuen Gruppenrichtlinieneinstellungen. Das Gruppenrichtlinienmodul die eingehende Gruppenrichtlinienobjekte verarbeitet und die clientseitige Erweiterung der QoS-informiert, wenn die QoS-Richtlinien aktualisiert werden.

- **Die clientseitige Erweiterung der QoS-**. Eine Komponente von der Gruppenrichtlinienclient-Dienst, der wartet, bis eine Mitteilung durch das Gruppenrichtlinienmodul, das QoS-Richtlinien geändert wurden und informiert die QoS-Inspect-Modul.

- **TCP/IP-Stapel**. Der TCP/IP-Stapel, der verfügt über integrierte Unterstützung für IPv4 und IPv6- und Windows-Filterplattform unterstützt. 

- **QoS-Überprüfung**. Ein Modul-Komponente in den TCP/IP-Stapel, der auf Anzeichen von QoS-Richtlinie ändert sich von der QoS die clientseitige Erweiterung, wartet die QoS-Richtlinieneinstellungen abgerufen und interagiert mit der Transportschicht und Pacer.sys Datenverkehr intern zu kennzeichnen, die die QoS-Richtlinien entspricht.

- **NDIS 6.x**. Eine Standardschnittstelle zwischen Kernelmodustreiber Netzwerk und das Betriebssystem auf Windows Server und Client-Betriebssysteme. NDIS 6.x unterstützt Lightweight Filter, mit denen eine vereinfachte Treibermodell für NDIS-Treiber und -Miniporttreiber ist, die eine bessere Leistung bietet.

- **QoS-Netzwerkanbieter Schnittstelle \(NPI\)**. Eine Schnittstelle für Kernelmodustreiber Pacer.sys interagieren.

- **Pacer.sys**. Ein NDIS 6.x-Lightweight Filter-Treiber, der steuert, Paket planen für richtlinienbasierten QoS und für den Datenverkehr, der allgemeine QoS-\(GQoS\) und die Steuerung des Datenverkehrs \(TC\) APIs verwenden. Pacer.sys ersetzt Psched.sys in Windows Server2003 und Windows XP. Pacer.sys ist mit der QoS-Paketplaner-Komponente in den Eigenschaften einer Netzwerkverbindung oder der Adapter installiert.

Im nächsten Thema in diesem Handbuch, finden Sie unter [QoS-Richtlinie Szenarien](qos-policy-scenarios.md).

Das erste Thema in diesem Handbuch finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).

