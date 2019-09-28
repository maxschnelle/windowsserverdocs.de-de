---
ms.assetid: ''
title: Unterstützte Grenze für hochpräzise Uhrzeit
description: In diesem Artikel wird die Unterstützungs Grenze für den Windows-Zeit Dienst (W32Time) in Umgebungen beschrieben, die eine sehr genaue und stabile Systemzeit erfordern.
author: shortpatti
ms.author: dacuo
manager: dougkim
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 212b9c79bc2e43e966180b928c865a9053332c3f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405259"
---
# <a name="support-boundary-for-high-accuracy-time"></a>Unterstützte Grenze für hochpräzise Uhrzeit

>Gilt für: Windows Server 2016 und Windows 10, Version 1607 oder höher

In diesem Artikel werden die unterstützten Grenzen für den Windows-Zeit Dienst (W32Time) in Umgebungen beschrieben, in denen eine sehr genaue und stabile Systemzeit erforderlich ist.

## <a name="high-accuracy-support-for-windows-81-and-2012-r2-or-prior"></a>Unterstützung für hohe Genauigkeit für Windows 8.1 und 2012 R2 (oder früher)

Frühere Versionen von Windows (vor Windows 10 1607 oder Windows Server 2016 1607) können keine sehr genaue Zeit garantieren. Der Windows-Zeit Dienst auf diesen Systemen:

-   Bereitstellen der erforderlichen Zeit Genauigkeit zum erfüllen der Authentifizierungsanforderungen der Kerberos-Version 5

-   Für Windows-Clients und-Server, die einer gemeinsamen Active Directory Gesamtstruktur beigetreten sind, lose Zeitangabe

Strengere Genauigkeits Anforderungen waren außerhalb der Entwurfs Spezifikation des Windows-Zeit Dienstanbieter unter diesen Betriebssystemen und werden nicht unterstützt.

## <a name="windows-10-and-windows-server-2016"></a>Windows 10 und Windows Server 2016

Die Zeit Genauigkeit in Windows 10 und Windows Server 2016 wurde erheblich verbessert, während die NTP-Kompatibilität mit älteren Windows-Versionen vollständig abwärts aufrechterhalten wurde. Unter den richtigen Betriebsbedingungen können Systeme mit Windows 10 oder Windows Server 2016 und neueren Versionen eine Genauigkeit von 1 Sekunde, 50 ms (Millisekunden) oder 1 MS bereitzustellen.

>[!IMPORTANT]
>**Sehr genaue Zeitquellen**<br>
>Die sich ergebende Zeit Genauigkeit in der Topologie hängt stark von der Verwendung einer exakten, stabilen Stamm Zeit Quelle (Stratum 1) ab. Es gibt Windows-basierte und nicht Windows-basierte, Windows-kompatible NTP-Zeit Quell Hardware, die von Drittanbietern verkauft wird. Wenden Sie sich an Ihren Hersteller, um die Richtigkeit der Produkte zu erhalten.

>[!IMPORTANT]
>**Zeit Genauigkeit**<br>
>Die Zeit Genauigkeit umfasst die End-to-End-Verteilung der exakten Zeit von einer streng präzisen autorisierenden Zeit Quelle zum Endgerät. Alle Elemente, die sich auf die Netzwerk Asymmetrie auswirken, beeinflussen die Genauigkeit, z. b. physische Netzwerkgeräte oder eine hohe CPU-Auslastung auf dem Zielsystem.

## <a name="high-accuracy-requirements"></a>Hohe Genauigkeits Anforderungen

Im weiteren Verlauf dieses Dokuments werden die Umgebungs Anforderungen beschrieben, die erfüllt sein müssen, damit die entsprechenden Ziele mit hoher Genauigkeit unterstützt werden.

### <a name="target-accuracy-1-second-1s"></a>Zielgenauigkeit: 1 Sekunde (1 s)

So erreichen Sie eine Genauigkeit von 1 s für einen bestimmten Zielcomputer im Vergleich zu einer sehr präzisen Zeit Quelle:

-   Auf dem Zielsystem muss Windows 10, Windows Server 2016, ausgeführt werden.

-   Das Zielsystem muss die Zeit von einer NTP-Hierarchie von Zeitservern synchronisieren, die in einer überaus präzisen Windows-kompatiblen NTP-Zeit Quelle liegt.

-   Alle Windows-Betriebssysteme in der oben genannten NTP-Hierarchie müssen so konfiguriert werden, dass Sie in der Dokumentation [Konfigurieren von Systemen für hoch Genauigkeit](configuring-systems-for-high-accuracy.md) dokumentiert sind.

-   Die kumulative unidirektionale Netzwerk Latenz Zwischenziel und Quelle darf 100 MS nicht überschreiten. Die kumulative Netzwerkverzögerung wird durch das Hinzufügen einzelner unidirektionaler Verzögerungen zwischen Paaren von NTP-Client-Server-Knoten in der Hierarchie gemessen, beginnend mit dem Ziel und endet an der Quelle. Weitere Informationen finden Sie im Dokument zur Zeitsynchronisierung mit hoher Genauigkeit.

### <a name="target-accuracy-50-milliseconds"></a>Zielgenauigkeit: 50 Millisekunden

Alle Anforderungen, die im Abschnitt **target-Genauigkeit beschrieben werden: 1 Sekunde @ no__t-0 wird angewendet, es sei denn, es werden strengere Steuerelemente in diesem Abschnitt beschrieben.

Die zusätzlichen Anforderungen zum Erreichen der Genauigkeit von 50 ms für ein bestimmtes Zielsystem lauten:

-   Der Zielcomputer muss über eine Netzwerk Latenz von mehr als 5 ms zwischen seiner Zeit Quelle verfügen.

-   Das Zielsystem darf nicht größer als Stratum 5 aus einer sehr präzisen Zeit Quelle sein.

    >[!Note]
    >Führen Sie "W32tm/Query" aus/Status "über die Befehlszeile aus, um den Stratum anzuzeigen.

-   Das Zielsystem muss innerhalb von 6 oder weniger Netzwerk Hops aus der äußerst exakten Zeit Quelle liegen.

-   Die durchschnittliche CPU-Auslastung für alle stratums (1 Tag) darf nicht mehr als 90% betragen.

-   Bei virtualisierten Systemen darf die durchschnittliche CPU-Auslastung des Hosts nicht länger als 90% sein.

### <a name="target-accuracy-1-millisecond"></a>Zielgenauigkeit: 1 Millisekunde

Alle Anforderungen, die in den Abschnitten **target-Genauigkeit beschrieben werden: 1 Sekunde @ no__t-0 und **target-Genauigkeit: 50 Millisekunden @ no__t-0 anwenden, außer wenn strengere Steuerelemente in diesem Abschnitt beschrieben werden.

Die zusätzlichen Anforderungen zum Erreichen von 1 MS Genauigkeit für ein bestimmtes Zielsystem lauten:

-   Der Zielcomputer muss über eine Netzwerk Latenz von mehr als 0,1 MS zwischen seiner Zeit Quelle verfügen.

-   Das Zielsystem darf nicht größer als Stratum 5 aus einer sehr präzisen Zeit Quelle sein.

    >[!Note]
    >Führen Sie "W32tm/Query" aus/Status "über die Befehlszeile aus, um den Stratum anzuzeigen.

-   Das Zielsystem muss innerhalb von 4 oder weniger Netzwerk Hops aus der äußerst exakten Zeit Quelle liegen.

-   Die durchschnittliche CPU-Auslastung für die einzelnen stratoren darf nicht länger als 80% sein.

-   Bei virtualisierten Systemen darf die durchschnittliche CPU-Auslastung des Hosts nicht länger als 80% sein.
