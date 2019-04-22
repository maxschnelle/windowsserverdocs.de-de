---
title: Leistungstools für Netzwerkauslastungen
description: Dieses Thema ist Teil des Leitfadens Netzwerk-Subsystem zur Leistungsoptimierung für Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: c7789781-87e8-464e-981b-af887d01badd
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 07/16/2018
ms.openlocfilehash: e71c5f34041145907c30b279dc91a94c03c2abed
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824931"
---
# <a name="performance-tools-for-network-workloads"></a>Leistungstools für Netzwerkauslastungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um mehr über Leistungstools erfahren.

Dieses Thema enthält die Abschnitte zum-Client-Tool, TCP/IP-Fenstergröße und Microsoft Server Performance Advisor-Datenverkehr.

##  <a name="bkmk_tuning"></a> Client-Datenverkehr-tool

Der Client-Datenverkehr \(CtsTraffic\) Tool bietet Ihnen die Möglichkeit zum Erstellen und Überprüfen des Netzwerkdatenverkehrs.

Weitere Informationen und das Tool herunterladen, finden Sie unter [CtsTraffic (Client-zu-Server-Datenverkehr)](https://github.com/Microsoft/ctsTraffic).
  
##  <a name="bkmk_size"></a> TCP/IP-Fenstergröße

Für 1 GB-Adapter, sollten die Einstellungen, die in der vorherigen Tabelle gezeigt einen guten Durchsatz bereitstellen, da NTttcp die TCP-Standardfenstergröße 64 k mithilfe eines bestimmten logischen Prozessor setzt \(SO_RCVBUF\) für die Verbindung. Dies bietet eine guten Leistung in einem Netzwerk mit geringer Latenz.  

Im Gegensatz dazu führt bei Netzwerken mit hoher Latenz oder 10 GB-Adapter, der standardmäßigen TCP-Fenster Größenwert für NTttcp kleiner als eine optimale Leistung. In beiden Fällen müssen Sie die TCP-Fenstergröße ermöglichen die größeren Bandbreite Bandwidth Delay Product anpassen.  

Sie können die TCP-Fenstergröße statisch auf einen hohen Wert festlegen, mit der **-Rb** Option. Diese Option deaktiviert die TCP-Automatische Optimierung des Empfangsfensters, und es wird empfohlen, es nur dann, wenn der Benutzer, die sich ergebende Änderung im TCP/IP-Verhalten vollständig verstanden hat. Standardmäßig wird die TCP-Fenstergröße auf einen ausreichend Wert festgelegt ist und angepasst wird nur bei hoher Auslastung oder über Verbindungen mit hoher Latenz.  

##  <a name="bkmk_advisor"></a> Microsoft Server Performance Advisor

Microsoft Server Performance Advisor \(SPA\) hilft bei der IT-Administratoren Erfassen von Metriken zu identifizieren, vergleichen und Diagnostizieren von potenziellen Leistungsproblemen in Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008-Bereitstellung. 

SPA generiert, umfassende diagnostische Berichte und Diagramme, und bietet Empfehlungen unterstützen Sie beim schnellen Probleme analysieren und korrekturmaßnahmen zu entwickeln.  
  
 Weitere Informationen und den Advisor herunterladen, finden Sie unter [Microsoft Server Performance Advisor](https://msdn.microsoft.com/library/windows/hardware/dn481522.aspx) im Windows Hardware Developer Center.

Links zu allen Themen in diesem Handbuch finden Sie [Optimieren der Leistung mit Subsystem](net-sub-performance-top.md).