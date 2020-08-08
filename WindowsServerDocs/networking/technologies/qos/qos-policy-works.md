---
title: Funktionsweise der QoS-Richtlinie
description: Dieses Thema bietet einen Überblick über die Richtlinie für Quality of Service (QoS), mit der Sie Gruppenrichtlinie die Bandbreite von Netzwerk Datenverkehr für bestimmte Anwendungen und Dienste in Windows Server 2016 priorisieren können.
ms.topic: article
ms.assetid: 25097cb8-b9b1-41c9-b3c7-3610a032e0d8
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: fe91bba99000be307ed011cb5636dc49d65c389a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942530"
---
# <a name="how-qos-policy-works"></a>Funktionsweise der QoS-Richtlinie

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Beim Starten oder Abrufen aktualisierter Benutzer-oder Computer Konfigurations Gruppenrichtlinie Einstellungen für QoS erfolgt der folgende Vorgang.

1. Die Gruppenrichtlinie-Engine ruft die Konfigurations Gruppenrichtlinie Einstellungen des Benutzers oder Computers aus Active Directory ab.

2. Die Gruppenrichtlinie-Engine informiert die Client seitige QoS-Erweiterung darüber, dass Änderungen an den QoS-Richtlinien vorgenommen wurden.

3. Die Client seitige QoS-Erweiterung sendet eine QoS-Richtlinien Ereignis Benachrichtigung an das QoS-Inspektions Modul.

4. Das QoS-Inspektions Modul ruft die QoS-Richtlinien für Benutzer oder Computer ab und speichert Sie.

Wenn eine neue TCP-Verbindung mit Transport Schicht Endpunkt \( oder UDP-Datenverkehr \) erstellt wird, tritt der folgende Vorgang auf.

1. Die Transport Schicht Komponente des TCP/IP-Stapels informiert das QoS-Inspektions Modul.

2. Das QoS-Inspektions Modul vergleicht die Parameter des Transport Schicht-Endpunkts mit den gespeicherten QoS-Richtlinien.

3. Wenn eine Übereinstimmung gefunden wird, kontaktiert das QoS-Inspektions Modul Pacer.sys, um einen Flow, eine Datenstruktur, die den DSCP-Wert enthält, und die Einstellungen für die Datenverkehrs Drosselung der entsprechenden QoS-Richtlinie zu erstellen. Wenn mehrere QoS-Richtlinien vorhanden sind, die mit den Parametern des Transport Schicht-Endpunkts identisch sind, wird die spezifischere QoS-Richtlinie verwendet.

4. Pacer.sys speichert den Flow und gibt eine Fluss Nummer zurück, die dem Fluss zum QoS-Inspektions Modul entspricht.

5. Das QoS-Inspektions Modul gibt die Fluss Nummer an die Transport Schicht zurück.

6. Die Transportschicht speichert die Fluss Nummer mit dem Transport Schicht Endpunkt.

Wenn ein Paket gesendet wird, das einem mit einer Fluss Nummer markierten Transport Schicht Endpunkt entspricht, wird der folgende Vorgang durchgeführt.

1. Die Transport Schicht markiert das Paket intern mit der Fluss Nummer.

2. Die netzwerkebenenabfragen Pacer.sys für den DSCP-Wert, der der Fluss Nummer des Pakets entspricht.

3. Pacer.sys gibt den DSCP-Wert an die Netzwerkebene zurück.

4. Die Netzwerkschicht ändert das Feld IPv4-oder IPv6-Datenverkehrs Klasse in den DSCP-Wert, der durch Pacer.sys angegeben wird, und berechnet bei IPv4-Paketen die abschließende IPv4-Header Prüfsumme.

5. Die Netzwerkschicht übergibt das Paket an die Rahmen Ebene.

6. Da das Paket mit einer Fluss Nummer gekennzeichnet wurde, übergibt die Rahmen Ebene das Paket an Pacer.sys über NDIS 6. x.

7. Pacer.sys verwendet die Fluss Nummer des Pakets, um zu bestimmen, ob das Paket gedrosselt werden muss, und plant, wenn dies der Fall ist, das Paket zum Senden.

8. Pacer.sys das Paket sofort \( , wenn keine Drosselung des Datenverkehrs vorhanden ist \) , oder wie geplant \( , wenn die Datenverkehrs Drosselung \) auf NDIS 6. x zur Übertragung über die entsprechende Netzwerkkarte erfolgt.

Diese Prozesse von Richtlinien basiertem QoS bieten die folgenden Vorteile.

- Die Überprüfung des Datenverkehrs, um zu bestimmen, ob eine QoS-Richtlinie angewendet wird, erfolgt pro Transport Schicht Endpunkt und nicht pro Paket.

- Der Datenverkehr, der nicht mit einer QoS-Richtlinie identisch ist, hat keine Auswirkungen auf die Leistung.

- Anwendungen müssen nicht geändert werden, um den DSCP-basierten differenzierten Dienst oder die Drosselung des Datenverkehrs zu nutzen.

- QoS-Richtlinien können auf durch IPSec geschützte Datenverkehr angewendet werden.

Das nächste Thema in dieser Anleitung finden Sie unter [Architektur der QoS-Richtlinie](qos-policy-architecture.md).

Das erste Thema in dieser Anleitung finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).
