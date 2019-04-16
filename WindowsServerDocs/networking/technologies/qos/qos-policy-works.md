---
title: Funktionsweise von QoS-Richtlinie
description: Dieses Thema enthält eine Übersicht über die Richtlinie für Quality of Service (QoS), können Sie mithilfe einer Gruppenrichtlinie um Datenverkehr Netzwerkbandbreite von bestimmten Anwendungen und Diensten in Windows Server2016 priorisieren.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 25097cb8-b9b1-41c9-b3c7-3610a032e0d8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1073308b5939e648fdcc2006acdce76ecf0331c9
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="how-qos-policy-works"></a>Funktionsweise von QoS-Richtlinie

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Beim Starten oder aktualisierte Benutzer oder Computer Konfiguration einer Gruppenrichtlinie Einstellungen für QoS erhalten, wird der folgende Prozess.

1. Das Gruppenrichtlinienmodul die Benutzer oder Computer Configuration Gruppenrichtlinieneinstellungen aus Active Directory abgerufen.

2. Das Gruppenrichtlinienmodul informiert die QoS-clientseitige Erweiterung, dass Änderungen in der QoS-Richtlinien sind.

3. Die clientseitige Erweiterung QoS sendet eine Benachrichtigung QoS-Richtlinie an QoS Inspect-Modul.

4. QoS Inspect-Modul ruft die QoS-Richtlinien für Benutzer oder Computer ab und speichert sie.

Wenn einen neuen Endpunkt für die Transportschicht \ (TCP-Verbindung oder UDP-Traffic\) erstellt, der folgende Prozess erfolgt.

1. Die Transport Layer-Komponente für den TCP/IP-Protokollstapel informiert das QoS Inspect-Modul.

2. Die QoS-Inspect-Modul vergleicht die Parameter des Endpunkts Transportschicht gespeicherte QoS-Richtlinien.

3. Wenn eine Übereinstimmung gefunden wird, kontaktiert der QoS-Inspect-Modul Pacer.sys um ein Fluss, eine Datenstruktur, die mit den DSCP-Wert und den Datenverkehr einschränkungseinstellungen der entsprechenden QoS-Richtlinie zu erstellen. Wenn es mehrere QoS-Richtlinien, die mit die Parametern des Endpunkts Transportschicht übereinstimmen gibt, wird die spezifischste QoS-Richtlinie verwendet.

4. Pacer.sys speichert den Fluss und gibt eine für den Fluss der QoS-Überprüfung Modul Fluss zurück.

5. Die QoS-Inspect-Modul gibt die Anzahl der Fluss der Transportschicht.

6. Der Transportschicht speichert die Fluss mit dem Endpunkt der Transportschicht.

Wenn ein Paket für einen Transport Layer-Endpunkt mit einer Zahl Fluss gekennzeichnet wird gesendet, der folgende Prozess erfolgt.

1. Der Transportschicht kennzeichnet intern das Paket mit der Anzahl der Fluss.

2. Der Vermittlungsschicht fragt Pacer.sys für den DSCP-Wert, der Ablauf des Pakets entspricht.

3. Pacer.sys gibt den DSCP-Wert zurück, auf der Netzwerkebene.

4. Der Vermittlungsschicht ändert sich im IPv4-TOS-Feld oder IPv6-Datenverkehrsklasse in den DSCP-Wert durch Pacer.sys angegeben und für IPv4-Pakete, berechnet die Prüfsumme der endgültige IPv4-Header.

5. Der Vermittlungsschicht übergibt das Paket an die Ebene Rahmen.

6. Da das Paket mit einer Zahl Fluss markiert wurde, übergibt der Ebene Framing das Paket an Pacer.sys über NDIS 6.x.

7. Pacer.sys wird die Anzahl der Ablauf des Pakets verwendet wird, um festzustellen, ob das Paket muss gedrosselt werden, und wenn dies der Fall, plant das Paket zu senden.

8. Pacer.sys übergibt das Paket entweder, sofort \ (wenn es ist kein Datenverkehr Throttling\) oder gemäß dem Zeitplan \ (falls vorhanden ist Datenverkehr Throttling\) auf NDIS 6.x für die Übertragung über das entsprechende Netzwerk.

Diese Prozesse des richtlinienbasierten QoS bieten folgende Vorteile.

- Die Überprüfung des Datenverkehrs, um festzustellen, ob eine QoS-Richtlinie gilt erfolgt pro-Transport Layer-Endpunkt, anstatt pro Paket.

- Es gibt keine Auswirkungen auf die Leistung für Datenverkehr, der nicht mit eine QoS-Richtlinie übereinstimmt.

- Apps müssen nicht geändert werden, um DSCP-basierten differenzierten Dienst nutzen oder Datenverkehr Einschränkung.

- QoS-Richtlinien können für den Datenverkehr mit IPsec geschützt gelten.

Im nächsten Thema in diesem Handbuch, finden Sie unter [QoS-Richtlinie Architektur](qos-policy-architecture.md).

Das erste Thema in diesem Handbuch finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).
