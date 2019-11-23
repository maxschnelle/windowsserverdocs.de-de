---
title: Funktionsweise der QoS-Richtlinie
description: Dieses Thema bietet einen Überblick über die Richtlinie für Quality of Service (QoS), mit der Sie Gruppenrichtlinie die Bandbreite von Netzwerk Datenverkehr für bestimmte Anwendungen und Dienste in Windows Server 2016 priorisieren können.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 25097cb8-b9b1-41c9-b3c7-3610a032e0d8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4de9674e2d1700d342af380c79a611c3d5961cda
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405176"
---
# <a name="how-qos-policy-works"></a>Funktionsweise der QoS-Richtlinie

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Beim Starten oder Abrufen aktualisierter Benutzer-oder Computer Konfigurations Gruppenrichtlinie Einstellungen für QoS erfolgt der folgende Vorgang.

1. Die Gruppenrichtlinie-Engine ruft die Konfigurations Gruppenrichtlinie Einstellungen des Benutzers oder Computers aus Active Directory ab.

2. Die Gruppenrichtlinie-Engine informiert die Client seitige QoS-Erweiterung darüber, dass Änderungen an den QoS-Richtlinien vorgenommen wurden.

3. Die Client seitige QoS-Erweiterung sendet eine QoS-Richtlinien Ereignis Benachrichtigung an das QoS-Inspektions Modul.

4. Das QoS-Inspektions Modul ruft die QoS-Richtlinien für Benutzer oder Computer ab und speichert Sie.

Wenn ein neuer Transport Schicht-Endpunkt \(TCP-Verbindung oder UDP-Datenverkehr\) erstellt wird, wird der folgende Vorgang ausgeführt.

1. Die Transport Schicht Komponente des TCP/IP-Stapels informiert das QoS-Inspektions Modul.

2. Das QoS-Inspektions Modul vergleicht die Parameter des Transport Schicht-Endpunkts mit den gespeicherten QoS-Richtlinien.

3. Wenn eine Übereinstimmung gefunden wird, kontaktiert das QoS-Inspektions Modul Pacer. sys, um einen Flow zu erstellen, eine Datenstruktur, die den DSCP-Wert enthält, und die Einstellungen für die Datenverkehrs Drosselung der entsprechenden QoS-Richtlinie. Wenn mehrere QoS-Richtlinien vorhanden sind, die mit den Parametern des Transport Schicht-Endpunkts identisch sind, wird die spezifischere QoS-Richtlinie verwendet.

4. Pacer. sys speichert den Flow und gibt eine Fluss Nummer zurück, die dem Fluss zum QoS-Inspektions Modul entspricht.

5. Das QoS-Inspektions Modul gibt die Fluss Nummer an die Transport Schicht zurück.

6. Die Transportschicht speichert die Fluss Nummer mit dem Transport Schicht Endpunkt.

Wenn ein Paket gesendet wird, das einem mit einer Fluss Nummer markierten Transport Schicht Endpunkt entspricht, wird der folgende Vorgang durchgeführt.

1. Die Transport Schicht markiert das Paket intern mit der Fluss Nummer.

2. Die Netzwerkschicht fragt Pacer. sys nach dem DSCP-Wert ab, der der Fluss Nummer des Pakets entspricht.

3. Pacer. sys gibt den DSCP-Wert an die Netzwerkebene zurück.

4. Die Netzwerkschicht ändert das Feld IPv4-oder IPv6-Datenverkehrs Klasse in den von Pacer. sys angegebenen DSCP-Wert und berechnet bei IPv4-Paketen die abschließende Prüfsumme für den IPv4-Header.

5. Die Netzwerkschicht übergibt das Paket an die Rahmen Ebene.

6. Da das Paket mit einer Fluss Nummer gekennzeichnet wurde, übergibt die Rahmen Ebene das Paket über NDIS 6. x an Pacer. sys.

7. Pacer. sys verwendet die Fluss Nummer des Pakets, um zu bestimmen, ob das Paket gedrosselt werden muss, und plant, wenn dies der Fall ist, das Paket zum Senden.

8. Pacer. sys übergibt das Paket entweder sofort \(, wenn keine Datenverkehrs Drosselung\) oder wie geplant \(, wenn die Datenverkehrs Drosselung auf NDIS 6. x zur Übertragung über den entsprechenden Netzwerkadapter\).

Diese Prozesse von Richtlinien basiertem QoS bieten die folgenden Vorteile.

- Die Überprüfung des Datenverkehrs, um zu bestimmen, ob eine QoS-Richtlinie angewendet wird, erfolgt pro Transport Schicht Endpunkt und nicht pro Paket.

- Der Datenverkehr, der nicht mit einer QoS-Richtlinie identisch ist, hat keine Auswirkungen auf die Leistung.

- Anwendungen müssen nicht geändert werden, um den DSCP-basierten differenzierten Dienst oder die Drosselung des Datenverkehrs zu nutzen.

- QoS-Richtlinien können auf durch IPSec geschützte Datenverkehr angewendet werden.

Das nächste Thema in dieser Anleitung finden Sie unter [Architektur der QoS-Richtlinie](qos-policy-architecture.md).

Das erste Thema in dieser Anleitung finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).
