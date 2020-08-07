---
title: Architektur der QoS-Richtlinie
description: Dieses Thema bietet einen Überblick über die Richtlinie für Quality of Service (QoS), mit der Sie Gruppenrichtlinie die Bandbreite von Netzwerk Datenverkehr für bestimmte Anwendungen und Dienste in Windows Server 2016 priorisieren können.
ms.topic: article
ms.assetid: 25097cb8-b9b1-41c9-b3c7-3610a032e0d8
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: eca49b5b20e34aca9c5e65b1544f2308295d7445
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953866"
---
# <a name="qos-policy-architecture"></a>Architektur der QoS-Richtlinie

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie mehr über die Architektur der QoS-Richtlinie.

In der folgenden Abbildung wird die Architektur von Richtlinien basiertem QoS veranschaulicht.

![Architektur der QoS-Richtlinie](../../media/QoS/QoS-Policy-Architecture.jpg)

Die Architektur von Richtlinien basiertem QoS besteht aus den folgenden Komponenten:

- **Gruppenrichtlinie Client Dienst**. Ein Windows-Dienst, der die Einstellungen der Benutzer-und Computerkonfiguration Gruppenrichtlinie verwaltet.

- **Gruppenrichtlinie-Engine**. Eine Komponente des Gruppenrichtlinie Client-diensdienstanbieter, der die Benutzer-und Computerkonfiguration Gruppenrichtlinie Einstellungen von Active Directory beim Start abruft und regelmäßig \( alle 90 Minuten auf Änderungen prüft \) . Wenn Änderungen erkannt werden, ruft die Gruppenrichtlinie-Engine die neuen Gruppenrichtlinie Einstellungen ab. Die Gruppenrichtlinie-Engine verarbeitet die eingehenden GPOs und informiert die Client seitige Erweiterung von QoS, wenn die QoS-Richtlinien aktualisiert werden.

- **Client seitige QoS-Erweiterung**. Eine Komponente des Gruppenrichtlinie Client diensdienstanbieter, die auf eine Angabe von der Gruppenrichtlinie-Engine wartet, dass die QoS-Richtlinien geändert wurden, und das QoS-Inspektions Modul informiert.

- **TCP/IP-Stapel**. Der TCP/IP-Stapel, der integrierte Unterstützung für IPv4 und IPv6 umfasst und Windows-Filter Plattform unterstützt.

- **QoS**-Überprüfung. Modul eine Komponente im TCP/IP-Stapel, die auf Anzeichen von QoS-Richtlinien Änderungen von der QoS-Client seitigen Erweiterung wartet, die QoS-Richtlinien Einstellungen abruft und mit der Transport Schicht interagiert und Pacer.sys, den Datenverkehr, der den QoS-Richtlinien entspricht, intern zu markieren.

- **NDIS 6. x**. Eine Standardschnittstelle zwischen Netzwerk Treibern im Kernelmodus und dem Betriebssystem in Windows Server-und Client Betriebssystemen. NDIS 6. x unterstützt einfache Filter, bei denen es sich um ein vereinfachtes Treibermodell für NDIS-zwischen Treiber und Mini Port-Treiber handelt, das eine bessere Leistung bietet.

- **QoS-Netzwerkanbieter Schnittstelle \( NPI \) **. Eine Schnittstelle für Kernelmodustreiber, um mit Pacer.sys zu interagieren.

- **Pacer.sys**. Ein NDIS 6. x-Lightweight-Filtertreiber, der die Paket Planung für Richtlinien basiertes QoS und den Datenverkehr von Anwendungen steuert, die die generischen QoS \( -GQoS \) -und Traffic Control- \( TC-APIs verwenden \) . Pacer.sys ersetzt Psched.sys in Windows Server 2003 und Windows XP. Pacer.sys wird mit der QoS-Paketplanerkomponente aus den Eigenschaften einer Netzwerkverbindung oder eines Adapters installiert.

Das nächste Thema in dieser Anleitung finden Sie unter [Szenarien für die QoS-Richtlinie](qos-policy-scenarios.md).

Das erste Thema in dieser Anleitung finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).

