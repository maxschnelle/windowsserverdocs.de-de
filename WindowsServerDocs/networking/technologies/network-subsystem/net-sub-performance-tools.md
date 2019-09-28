---
title: Leistungstools für Netzwerkauslastungen
description: Dieses Thema ist Teil des Handbuch zur Leistungsoptimierung des Netzwerk Subsystems für Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: c7789781-87e8-464e-981b-af887d01badd
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 07/16/2018
ms.openlocfilehash: 09e775bfe956d67adbd70cf4ce3f9461e1c37cf5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405516"
---
# <a name="performance-tools-for-network-workloads"></a>Leistungstools für Netzwerkauslastungen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema finden Sie Informationen zu Leistungs Tools.

Dieses Thema enthält Abschnitte zum Tool "Client-zu-Server-Datenverkehr", "TCP/IP-Fenstergröße" und "Microsoft Server Performance Advisor".

##  <a name="bkmk_tuning"></a>Client-zu-Server-Traffic Tool

Der Client-zu-Server-Datenverkehr \(ctstraffic @ no__t-1-Tool bietet die Möglichkeit, Netzwerk Datenverkehr zu erstellen und zu überprüfen.

Weitere Informationen und zum Herunterladen des Tools finden Sie unter [ctstraffic (Client-zu-Server-Datenverkehr)](https://github.com/Microsoft/ctsTraffic).
  
##  <a name="bkmk_size"></a>Größe des TCP/IP-Fensters

Bei 1-GB-Adaptern sollten die in der vorherigen Tabelle gezeigten Einstellungen einen guten Durchsatz bereitstellen, da ntttcp für die Verbindung die standardmäßige TCP-Fenstergröße auf 64 K durch eine bestimmte logische Prozessor Option \(SO_RCVBUF @ no__t-1 festlegt. Dies ermöglicht eine gute Leistung in einem Netzwerk mit geringer Latenz.  

Im Gegensatz dazu ergibt bei Netzwerken mit hoher Latenz oder bei 10-GB-Adaptern der Standardwert für die TCP-Fenstergröße für ntttcp eine geringere Leistung als die optimale Leistung. In beiden Fällen müssen Sie die TCP-Fenstergröße anpassen, um das größere Bandbreiten Verzögerungs Produkt zuzulassen.  

Sie können die TCP-Fenstergröße mit der Option **-RB** statisch auf einen großen Wert festlegen. Mit dieser Option wird die automatische Optimierung von TCP-Fenstern deaktiviert, und es wird empfohlen, Sie nur zu verwenden, wenn der Benutzer die resultierende Änderung im TCP/IP-Verhalten vollständig versteht. Standardmäßig ist die TCP-Fenstergröße auf einen ausreichenden Wert festgelegt und passt sich nur bei hoher Last oder über Verbindungen mit hoher Latenz an.  

##  <a name="bkmk_advisor"></a>Microsoft Server Performance Advisor

Microsoft Server Performance Advisor \(spa @ no__t-1 unterstützt IT-Administratoren bei der Erfassung von Metriken zum identifizieren, vergleichen und diagnostizieren potenzieller Leistungsprobleme in Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008-Bereitstellung. 

Spa generiert umfassende Diagnose Berichte und Diagramme und bietet Empfehlungen, mit denen Sie Probleme schnell analysieren und Korrekturmaßnahmen entwickeln können.  
  
 Weitere Informationen und zum Herunterladen des Ratgebers finden Sie unter [Microsoft Server Performance Advisor](https://msdn.microsoft.com/library/windows/hardware/dn481522.aspx) im Windows Hardware dev Center.

Links zu allen Themen in diesem Handbuch finden Sie unter [Network Subsystem Performance Tuning](net-sub-performance-top.md).