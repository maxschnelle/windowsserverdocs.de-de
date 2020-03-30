---
ms.assetid: ''
title: Unterstützte Grenze für hochpräzise Uhrzeit
description: In diesem Artikel wird die unterstützte Grenze für den Windows-Zeitdienst (W32Time) in Umgebungen beschrieben, in denen eine äußerst genaue und stabile Systemzeit erforderlich ist.
author: eross-msft
ms.author: dacuo
manager: dougkim
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 5748d598272c8f096876bab0d24142d38c2fd64b
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314963"
---
# <a name="support-boundary-for-high-accuracy-time"></a>Unterstützte Grenze für hochpräzise Uhrzeit

>Gilt für: Windows Server 2016 und Windows 10, Version 1607 oder höher

In diesem Artikel werden die unterstützten Grenzen für den Windows-Zeitdienst (W32Time) in Umgebungen beschrieben, in denen eine äußerst genaue und stabile Systemzeit erforderlich ist.

## <a name="high-accuracy-support-for-windows-81-and-2012-r2-or-prior"></a>Unterstützung für hohe Genauigkeit für Windows 8.1 und 2012 R2 (oder niedriger)

Frühere Versionen von Windows (vor Windows 10 1607 oder Windows Server 2016 1607) können keine hochgenaue Zeit garantieren. Der Windows-Zeitdienst auf diesen Systemen:

-   hat die notwendige Zeitgenauigkeit bereitgestellt, um die Authentifizierungsanforderungen von Kerberos, Version 5, zu erfüllen.

-   hat Windows-Clients und -Servern, die einer gemeinsamen Active Directory-Gesamtstruktur beigetreten sind, eine lose Zeit bereitgestellt.

Strengere Genauigkeitsanforderungen lagen außerhalb der Entwurfsspezifikation des Windows-Zeitdiensts in diesen Betriebssystemen und werden nicht unterstützt.

## <a name="windows-10-and-windows-server-2016"></a>Windows 10 und Windows Server 2016

Die Zeitgenauigkeit in Windows Server 10 und Windows Server 2016 wurde erheblich verbessert, während gleichzeitig die vollständige NTP-Abwärtskompatibilität mit älteren Windows-Versionen erhalten blieb. Unter den richtigen Betriebsbedingungen können Systeme mit Windows 10 oder Windows Server 2016 und neueren Versionen eine Genauigkeit von 1 Sekunde, 50 ms (Millisekunden) oder 1 ms bereitstellen.

>[!IMPORTANT]
>**Hochgenaue Zeitquellen**<br>
>Die sich ergebende Zeitgenauigkeit in deiner Topologie hängt stark von der Verwendung einer exakten, stabilen Stammzeitquelle (Stratum 1) ab. Es gibt Windows-basierte und nicht Windows-basierte hochexakte, Windows-kompatible NTP-Zeitquellen-Hardware, die von Drittanbietern verkauft wird. Wende dich an deinen Hersteller bezüglich der Genauigkeit ihrer Produkte.

>[!IMPORTANT]
>**Zeitgenauigkeit**<br>
>Die Zeitgenauigkeit umfasst die End-to-End-Verteilung der exakten Zeit von einer hochgenauen autoritativen Zeitquelle bis zum Endgerät. Alles, was zu einer Netzwerkasymmetrie führt, beeinflusst die Genauigkeit negativ, z. B. physische Netzwerkgeräte oder hohe CPU-Auslastung auf dem Zielsystem.

## <a name="high-accuracy-requirements"></a>Hohe Genauigkeitsanforderungen

Im weiteren Verlauf dieses Dokuments werden die Umgebungsanforderungen beschrieben, die erfüllt sein müssen, damit die entsprechenden Ziele für hohe Genauigkeit unterstützt werden.

### <a name="target-accuracy-1-second-1s"></a>Zielgenauigkeit: 1 Sekunde (1 s)

Um eine Genauigkeit von 1 s für einen bestimmten Zielcomputer im Vergleich zu einer hochpräzisen Zeitquelle zu erreichen:

-   Auf dem Zielsystem muss Windows 10, Windows Server 2016 ausgeführt werden.

-   Das Zielsystem muss die Zeit aus einer NTP-Hierarchie von Zeitservern synchronisieren, was in einer hochpräzisen, Windows-kompatiblen NTP-Zeitquelle kulminiert.

-   Alle Windows-Betriebssysteme in der oben erwähnten NTP-Hierarchie müssen so konfiguriert sein, wie in der Dokumentation [Konfigurieren von Systemen für hohe Genauigkeit](configuring-systems-for-high-accuracy.md) dokumentiert.

-   Die kumulative unidirektionale Netzwerklatenz zwischen Ziel und Quelle darf 100 ms nicht überschreiten. Die kumulative Netzwerkverzögerung wird gemessen, indem die einzelnen unidirektionalen Verzögerungen zwischen Paaren von NTP-Client-Server-Knoten in der Hierarchie addiert werden, beginnend mit dem Ziel und endend an der Quelle. Weitere Informationen findest du im Dokument zur Zeitsynchronisierung mit hoher Genauigkeit.

### <a name="target-accuracy-50-milliseconds"></a>Zielgenauigkeit: 50 Millisekunden

Alle im Abschnitt **Zielgenauigkeit:  1 Sekunde** beschriebenen Anforderungen gelten, außer wenn strengere Kontrollen in diesem Abschnitt dargelegt werden.

Die zusätzlichen Anforderungen, um eine Genauigkeit von 50 ms für ein bestimmtes Zielsystem zu erreichen, lauten:

-   Der Zielcomputer muss über eine bessere Netzwerklatenz als 5 ms zu seiner Zeitquelle verfügen.

-   Das Zielsystem darf nicht weiter entfernt von einer hochpräzisen Zeitquelle sein als Stratum 5.

    >[!Note]
    >Führe in einer Befehlszeile „w32tm /query /status“ aus, um das Stratum anzuzeigen.

-   Das Zielsystem muss innerhalb von 6 oder weniger Netzwerkhops zur hochpräzisen Zeitquelle liegen.

-   Die durchschnittliche CPU-Auslastung pro Tag in allen Strata darf nicht mehr als 90 % betragen.

-   Bei virtualisierten Systemen darf die durchschnittliche CPU-Auslastung des Hosts pro Tag nicht mehr als 90 % betragen.

### <a name="target-accuracy-1-millisecond"></a>Zielgenauigkeit: 1 Millisekunde

Alle in den Abschnitten **Zielgenauigkeit:  1 Sekunde** und **Zielgenauigkeit:  50 Millisekunden** gelten, außer wenn strengere Kontrollen in diesem Abschnitt dargelegt werden.

Die zusätzlichen Anforderungen, um eine Genauigkeit von 1 ms für ein bestimmtes Zielsystem zu erreichen, lauten:

-   Der Zielcomputer muss über eine bessere Netzwerklatenz als 0,1 ms zu seiner Zeitquelle verfügen.

-   Das Zielsystem darf nicht weiter entfernt von einer hochpräzisen Zeitquelle sein als Stratum 5.

    >[!Note]
    >Führe in einer Befehlszeile „w32tm /query /status“ aus, um das Stratum anzuzeigen.

-   Das Zielsystem muss innerhalb von 4 oder weniger Netzwerkhops zur hochpräzisen Zeitquelle liegen.

-   Die durchschnittliche CPU-Auslastung pro Tag in allen Strata darf nicht mehr als 80 % betragen.

-   Bei virtualisierten Systemen darf die durchschnittliche CPU-Auslastung des Hosts pro Tag nicht mehr als 80 % betragen.
