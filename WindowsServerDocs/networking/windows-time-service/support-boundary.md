---
ms.assetid: ''
title: Unterstützte Grenze für hochpräzise Uhrzeit
description: Dieser Artikel beschreibt die Unterstützung-Grenze für den Windows-Zeitdienst (W32Time) in Umgebungen, die äußerst präzise und stabile-System stets angefordert wird.
author: shortpatti
ms.author: dacuo
manager: dougkim
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 991bf4502546771dae9f092c6d5732f96b1278ab
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866271"
---
# <a name="support-boundary-for-high-accuracy-time"></a>Unterstützte Grenze für hochpräzise Uhrzeit

>Gilt für: Windows Server 2016 und Windows 10 Version 1607 oder höher

Dieser Artikel beschreibt die Grenzen der Unterstützung für den Windows-Zeitdienst (W32Time) in Umgebungen, die äußerst präzise und stabile-System stets angefordert wird.

## <a name="high-accuracy-support-for-windows-81-and-2012-r2-or-prior"></a>Unterstützung von hoher Genauigkeit für Windows 8.1 und die 2012 R2 (oder früher)

Frühere Versionen von Windows (vor Windows 10 1607 oder Windows Server 2016 1607), die äußerst präzise Zeit garantiert nicht. Der Windows-Zeitdienst auf diesen Systemen:

-   Die Genauigkeit der erforderlichen Zeit zum Erfüllen der Anforderungen an die Kerberos V5-Authentifizierung bereitgestellt

-   Lose genaue Uhrzeit angegeben, für die Windows-Clients und Server, die einen allgemeinen Active Directory-Gesamtstruktur angehören

Eine engere Genauigkeit-Anforderungen wurden außerhalb der Entwurfsspezifikation des Windows-Zeitdiensts auf diesen Betriebssystemen und wird nicht unterstützt.

## <a name="windows-10-and-windows-server-2016"></a>Windows 10 und WindowsServer 2016

In Windows 10 und Windows Server 2016-uhrzeitsynchronisierungsdienst wurde erheblich verbessert und gleichzeitig vollständige Abwärtskompatibilität NTP-Kompatibilität mit älteren Windows-Versionen. Systeme mit Windows 10 oder Windows Server 2016 und neuere Versionen können unter dem richtigen betriebsbedingungen, 1 Sekunde, 50 ms (Millisekunden), übermitteln oder 1 ms Genauigkeit.

>[!IMPORTANT]
>**Äußerst präzise Zeitquellen**<br>
>Die resultierende Uhrzeit-Genauigkeit in der Topologie ist stark abhängig von der mit einem korrekt und beständig-Stamm (Stratum 1) Zeitquelle. Es gibt Windows basiert und nicht-Windows basierend äußerst präzise Windows kompatibel ist, NTP Zeit quellhardware von 3. Drittanbietern verkauft. Überprüfen Sie den Anbieter, auf die Genauigkeit ihrer Produkte.

>[!IMPORTANT]
>**Genauigkeit der Zeit**<br>
>Genauigkeit der Zeit umfasst die End-to-End-Verteilung genaue Uhrzeit in eine äußerst präzise verbindlichen Zeitquelle, das Endgerät. Beliebiges Element, das Netzwerk Asymmetrie eingeführt wird Genauigkeit, z. B. physische Netzwerkgeräte oder hohe CPU-Auslastung auf dem Zielsystem negativ beeinflussen.

## <a name="high-accuracy-requirements"></a>Anforderungen mit hoher Genauigkeit

Der Rest dieses Dokuments wird beschrieben, die Anforderungen für die Umgebung, die erfüllt sein müssen, um die jeweiligen hoher Genauigkeit Ziele zu unterstützen.

### <a name="target-accuracy-1-second-1s"></a>Ziel-Genauigkeit: 1 Sekunde (1 s)

1 s erzielen Genauigkeit für ein bestimmtes Ziel-Computers im Vergleich zu einer äußerst präzise Zeitquelle:

-   Das Zielsystem muss Windows 10, Windows Server 2016 ausgeführt werden.

-   Das Zielsystem muss aus einer NTP-Hierarchie der Time-Server synchronisieren eine äußerst präzise Windows kompatibel NTP-Zeitquelle verbessert.

-   Alle Windows-Betriebssysteme in der oben genannten NTP-Hierarchie muss konfiguriert werden, wie in der [Konfigurieren von Systemen für hohe Genauigkeit](configuring-systems-for-high-accuracy.md) Dokumentation.

-   Die kumulative unidirektionale Netzwerklatenz zwischen Ziel und Quelle darf nicht mit 100 ms überschreiten. Die kumulative netzwerkverzögerung wird gemessen, durch das Hinzufügen der einzelnen unidirektionale Verzögerungen zwischen Paaren von NTP-Client / Server-Knoten in der Hierarchie beginnt mit dem Ziel und endet, die an der Quelle. Weitere Informationen finden Sie in der Synchronisierung des Dokuments hohe Genauigkeit.

### <a name="target-accuracy-50-milliseconds"></a>Ziel-Genauigkeit: 50 Millisekunden

Alle Anforderungen, die im Abschnitt aufgeführten **Ziel Genauigkeit: 1 Sekunde** anwenden, es sei denn, in denen strenge Kontrollen in diesem Abschnitt beschrieben werden.

Die zusätzlichen Anforderungen für die Genauigkeit von 50 ms für ein bestimmtes Zielsystem erzielen sind:

-   Der Zielcomputer muss eine bessere Leistung als 5 ms der Netzwerklatenz zwischen der Zeitquelle sein.

-   Das Zielsystem muss keine weiteren als Stratum 5 von eine äußerst präzise Zeitquelle sein.

    >[!Note]
    >Führen Sie "w32tm/Query/Status" von der Befehlszeile aus einer Schicht angezeigt.

-   Das Zielsystem muss innerhalb von 6 oder weniger Netzwerkhops, über die äußerst präzise Zeitquelle sein.

-   Die durchschnittliche CPU-Auslastung von einem Tag auf allen Stratums darf 90 % nicht überschreiten.

-   Für virtualisierte Systeme muss die eintägige durchschnittliche CPU-Auslastung des Hosts nicht 90 % überschreitet

### <a name="target-accuracy-1-millisecond"></a>Ziel-Genauigkeit: 1 Millisekunde

Alle Anforderungen, die in den Abschnitten erläuterten **Ziel Genauigkeit: 1 Sekunde** und **Genauigkeit als Ziel: 50 Millisekunden** anwenden, es sei denn, in denen strenge Kontrollen in diesem Abschnitt beschrieben werden.

Gelten zusätzlichen Anforderungen um 1 ms Genauigkeit für ein bestimmtes Zielsystem zu erreichen:

-   Der Zielcomputer muss eine bessere Leistung als 0,1 ms der Netzwerklatenz zwischen der Zeitquelle aufweisen.

-   Das Zielsystem muss keine weiteren als Stratum 5 von eine äußerst präzise Zeitquelle sein.

    >[!Note]
    >Führen Sie "w32tm/Query/Status" über die Befehlszeile, um die Stratum finden Sie unter

-   Das Zielsystem muss innerhalb von 4 oder weniger Netzwerkhops, über die äußerst präzise Zeitquelle sein.

-   Die durchschnittliche CPU-Auslastung von einem Tag über pro Schicht darf 80 % nicht überschreiten.

-   Für virtualisierte Systeme muss die eintägige durchschnittliche CPU-Auslastung des Hosts nicht 80 % überschreitet
