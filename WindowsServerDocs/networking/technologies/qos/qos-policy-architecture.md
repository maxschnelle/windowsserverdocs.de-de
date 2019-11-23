---
title: Architektur der QoS-Richtlinie
description: Dieses Thema bietet einen Überblick über die Richtlinie für Quality of Service (QoS), mit der Sie Gruppenrichtlinie die Bandbreite von Netzwerk Datenverkehr für bestimmte Anwendungen und Dienste in Windows Server 2016 priorisieren können.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 25097cb8-b9b1-41c9-b3c7-3610a032e0d8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 609d3f28465380b7d15648cfeb73070a39b9362f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71395981"
---
# <a name="qos-policy-architecture"></a>Architektur der QoS-Richtlinie

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie mehr über die Architektur der QoS-Richtlinie.

In der folgenden Abbildung wird die Architektur von Richtlinien basiertem QoS veranschaulicht.

![Architektur der QoS-Richtlinie](../../media/QoS/QoS-Policy-Architecture.jpg)

Die Architektur von Richtlinien basiertem QoS besteht aus den folgenden Komponenten:

- **Gruppenrichtlinie Client Dienst**. Ein Windows-Dienst, der die Einstellungen der Benutzer-und Computerkonfiguration Gruppenrichtlinie verwaltet.

- **Gruppenrichtlinie-Engine**. Eine Komponente des Gruppenrichtlinie Client-diensdienstanbieter, der die Benutzer-und Computerkonfiguration Gruppenrichtlinie Einstellungen von Active Directory beim Start abruft und regelmäßig alle 90\)Minuten überprüft, ob Änderungen \(. Wenn Änderungen erkannt werden, ruft die Gruppenrichtlinie-Engine die neuen Gruppenrichtlinie Einstellungen ab. Die Gruppenrichtlinie-Engine verarbeitet die eingehenden GPOs und informiert die Client seitige Erweiterung von QoS, wenn die QoS-Richtlinien aktualisiert werden.

- **Client seitige QoS-Erweiterung**. Eine Komponente des Gruppenrichtlinie Client diensdienstanbieter, die auf eine Angabe von der Gruppenrichtlinie-Engine wartet, dass die QoS-Richtlinien geändert wurden, und das QoS-Inspektions Modul informiert.

- **TCP/IP-Stapel**. Der TCP/IP-Stapel, der integrierte Unterstützung für IPv4 und IPv6 umfasst und Windows-Filter Plattform unterstützt. 

- **QoS**-Überprüfung. Modul eine Komponente im TCP/IP-Stapel, die auf Anzeichen von Änderungen der QoS-Richtlinie von der QoS-Client seitigen Erweiterung wartet, die QoS-Richtlinien Einstellungen abruft und mit der Transport Schicht und Pacer. sys interagiert, um den Datenverkehr, der den QoS-Richtlinien entspricht, intern zu markieren.

- **NDIS 6. x**. Eine Standardschnittstelle zwischen Netzwerk Treibern im Kernelmodus und dem Betriebssystem in Windows Server-und Client Betriebssystemen. NDIS 6. x unterstützt einfache Filter, bei denen es sich um ein vereinfachtes Treibermodell für NDIS-zwischen Treiber und Mini Port-Treiber handelt, das eine bessere Leistung bietet.

- **QoS-Netzwerkanbieter Schnittstelle \(NPI\)** . Eine Schnittstelle für Kernelmodustreiber für die Interaktion mit Pacer. sys.

- **Pacer. sys**. Ein NDIS 6. x-Lightweight-Filtertreiber, der die Paket Planung für Richtlinien basiertes QoS und den Datenverkehr von Anwendungen steuert, die den generischen QoS-\(GQoS-\) und die Datenverkehrs Kontrolle \(TC\) APIs verwenden. Pacer. sys ersetzte Psched. sys in Windows Server 2003 und Windows XP. Pacer. sys wird mit der QoS Packet Scheduler-Komponente aus den Eigenschaften einer Netzwerkverbindung oder eines Adapters installiert.

Das nächste Thema in dieser Anleitung finden Sie unter [Szenarien für die QoS-Richtlinie](qos-policy-scenarios.md).

Das erste Thema in dieser Anleitung finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).

