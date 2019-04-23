---
title: Funktionsweise von QoS-Richtlinie
description: Dieses Thema enthält eine Übersicht über Quality of Service (QoS)-Richtlinie, die Gruppenrichtlinie zu verwenden, um die Netzwerkbandbreite für Datenverkehr von bestimmten Anwendungen und Diensten in Windows Server 2016 zu priorisieren kann.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 25097cb8-b9b1-41c9-b3c7-3610a032e0d8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 272272c833bb38924f1daa5561037901f6ff4e25
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864281"
---
# <a name="how-qos-policy-works"></a>Funktionsweise von QoS-Richtlinie

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Beim Starten oder Abrufen von aktualisierten Benutzer oder Computer Configuration-gruppenrichtlinieneinstellungen für QoS, geschieht Folgendes.

1. Die Gruppenrichtlinien-Engine Ruft die Benutzer oder Computer Configuration gruppenrichtlinieneinstellungen aus Active Directory ab.

2. Die Gruppenrichtlinien-Engine informiert die QoS-Client-Side Extension, dass Änderungen in den QoS-Richtlinien wurden.

3. Die QoS-Client-Side Extension sendet eine ereignisbenachrichtigung für QoS-Richtlinie für das Modul der QoS-Überprüfung.

4. Die QoS-Prüfung Modul ruft ab, die QoS-Richtlinien für Benutzer oder Computer und speichert sie.

Wenn ein neuer Endpunkt für die Transportschicht \(TCP-Verbindung oder UDP-Datenverkehr\) erstellt wird, wird der folgende Prozess durchgeführt.

1. Die Transport Layer-Komponente des TCP/IP-Stapels informiert das Modul der QoS-Überprüfung.

2. Das Modul der QoS-Überprüfung vergleicht die Parameter von der Transportschicht Endpunkt die gespeicherten QoS-Richtlinien.

3. Wenn eine Übereinstimmung gefunden wird, kontaktiert der QoS-Prüfung Modul Pacer.sys zum Erstellen eines Flows eine Datenstruktur, die den DSCP-Wert und den Datenverkehr, drosselungseinstellungen für die entsprechende QoS-Richtlinie enthält. Wenn es mehrere QoS-Richtlinien, die mit den Parametern von der Transportschicht Endpunkt übereinstimmen sind, wird die spezifischste QoS-Richtlinie verwendet.

4. Pacer.sys speichert den Flow und eine Flow-Zahl, die auf den Flow an das Modul der QoS-Prüfung entsprechenden zurückgibt.

5. Das Modul der QoS-Überprüfung werden die Flow-Anzahl an die Transportschicht zurückgegeben.

6. Die Transportschicht speichert die Flow mit dem Transport Layer-Endpunkt.

Wenn ein Paket für einen Endpunkt für die Transportschicht mit einer Reihe von Flow gekennzeichnet wird gesendet der folgende Prozess durchgeführt.

1. Die Transportschicht wird intern das Paket mit der Anzahl der Flow markiert.

2. Die Netzwerkschicht fragt Pacer.sys für den DSCP-Wert, der die Anzahl der Datenfluss des Pakets entspricht.

3. Pacer.sys gibt den DSCP-Wert zurück, auf der Netzwerkebene.

4. Ebene des Netzwerks den DSCP-Wert, der anhand des Pacer.sys nun im IPv4-TOS-Feld oder IPv6-Datenverkehr-Klasse und für IPv4-Pakete, die endgültige IPv4-Header-Prüfsumme berechnet.

5. Ebene des Netzwerks übergibt das Paket an die Framing-Ebene.

6. Da das Paket mit einer Reihe von Flow markiert wurde, übergibt die Framing-Ebene des Pakets an Pacer.sys über NDIS 6.x.

7. Pacer.sys die Flow-Anzahl des Pakets, um zu ermitteln, ob das Paket muss eingeschränkt werden, und wenn dies der Fall, plant das Paket für das Senden.

8. Pacer.sys übergibt das Paket entweder, sofort \(, wenn kein Datenverkehr Drosselung\) oder gemäß dem Zeitplan \(Wenn Datenverkehr Drosselung\) auf NDIS 6.x für die Übertragung über das entsprechende Netzwerk.

Diese Prozesse des richtlinienbasierten QoS bieten folgende Vorteile.

- Die Überprüfung des Datenverkehrs, um zu bestimmen, ob eine QoS-Richtlinie gilt erfolgt pro-Transport-Layer-Endpunkt, anstatt pro Paket.

- Es gibt keine Auswirkungen auf die Leistung für den Datenverkehr, die eine QoS-Richtlinie nicht übereinstimmen.

- Anwendungen müssen nicht geändert werden, um DSCP-basierten differenzierte Dienst zu nutzen, oder Datenverkehr Drosselung.

- QoS-Richtlinien können für den Datenverkehr mit IPsec geschützt anwenden.

Im nächsten Thema in diesem Handbuch finden Sie unter [QoS-Richtlinie Architektur](qos-policy-architecture.md).

Das erste Thema in diesem Handbuch finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).
