---
title: Leistungstools für Netzwerkauslastungen
description: Dieses Thema ist Teil der Netzwerk-Subsystem-Leistungsoptimierung Anleitung für Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: c7789781-87e8-464e-981b-af887d01badd
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 81c31871b3dfa4644690fe074ae15eaaa680d7f2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="performance-tools-for-network-workloads"></a>Leistungstools für Netzwerkauslastungen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie Informationen zu Leistungstools, die.

Dieses Thema enthält die Abschnitte zum Server-Verkehr Tool TCP/IP-Fenstergröße und Microsoft Server Performance Advisor-Client.

##  <a name="bkmk_tuning"></a>Client Datenverkehr Server-tool

Der Client Datenverkehr Server \(ctsTraffic\) Tool bietet Ihnen die Möglichkeit zum Erstellen und Überprüfen von Netzwerkdatenverkehr.

Weitere Informationen und können das Tool herunterladen, finden Sie unter [CtsTraffic (Client-zu-Server-Datenverkehr)](http://ctstraffic.codeplex.com/).
  
##  <a name="bkmk_size"></a>TCP/IP-Fenstergröße

1-GB-Netzwerkkarten, die in der vorherigen Tabelle aufgeführten Einstellungen bietet, sollte gute da NTttcp legt die Standardgröße des TCP-64 k über einen bestimmten logischen Prozessor option \(SO_RCVBUF\) für die Verbindung. Dies bietet eine gute Leistung in einem Netzwerk mit geringer Latenz.  

Im Gegensatz dazu wird bei Netzwerken mit hoher Latenz oder 10 GB-Adapter, der TCP-Fenster Größe Standardwert für NTttcp kleiner als eine optimale Leistung. In beiden Fällen müssen Sie die TCP-Fenstergröße für das größere Bandbreite Verzögerung Produkt zulassen anpassen.  

Sie können die TCP-Fenstergröße statisch einen zu hohen Wert festlegen, mit der **-UA** Option. Diese Option deaktiviert die automatische TCP-Empfangsfensters, und es wird empfohlen, nur, wenn der Benutzer vollständig die resultierende Änderung der TCP/IP-Verhalten versteht verwenden. Standardmäßig wird die TCP-Fenstergröße ausreichend Wert festgelegt ist und passt nur bei hoher Auslastung oder über eine Verbindung mit hoher Latenz.  

##  <a name="bkmk_advisor"></a>Microsoft Server Performance Advisor

Microsoft Server Performance Advisor \(SPA\) unterstützt IT-Administratoren, die Messwerte zu identifizieren, zu vergleichen und diagnostizieren möglicher Leistungsprobleme in einer Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008-Bereitstellung. 

SPA generiert, umfassende Diagnoseberichte und Diagramme und Empfehlungen können Sie schnell Probleme analysieren und Maßnahmen zu entwickeln.  
  
 Weitere Informationen und die Advisor herunterladen, finden Sie unter [Microsoft Server Performance Advisor](https://msdn.microsoft.com/library/windows/hardware/dn481522.aspx) im Windows Hardware Dev Center.

Links zu allen Themen in diesem Handbuch finden Sie [Optimieren der Leistung mit Subsystem](net-sub-performance-top.md).