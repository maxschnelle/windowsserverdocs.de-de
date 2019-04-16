---
title: Datacenter Firewall (Übersicht)
description: In diesem Thema können Sie Informationen zu Datacenter Firewall ist eine Vermittlungsschicht, das 5-Tupel (Protokoll, Quelle und Ziel-Portnummern, Quell- und Ziel-IP-Adressen), die statusbehaftete, mehrinstanzenfähige Firewall in Windows Server2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 67576533-206b-428a-956c-ed8c53218d9b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0c9b9fb5b0fb9aa09ed783b2b66a8ad370a627c3
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="datacenter-firewall-overview"></a>Datacenter Firewall (Übersicht)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Datacenter Firewall ist ein neuer Dienst, der mit Windows Server2016 enthalten. Es ist ein Vermittlungsschicht, 5-Tupel (Protokoll, Quell- und Zielserver Portnummern, Quell- und Ziel-IP-Adressen), zustandsbehaftete, mehrinstanzenfähige Firewall. Wenn bereitgestellt und als Dienst vom Dienstanbieter angeboten, können Mandantenadministratoren installieren und Konfigurieren der Firewall-Richtlinien zum Schutz ihrer virtuellen Netzwerken von unerwünschten Datenverkehr aus dem Internet und Intranetnetzwerke.  
  
![Datacenter Firewall im Netzwerkstapel](../../../media/Datacenter-Firewall-Overview/MultitenantFirewallOverview2.png)  
  
Der Service-Anbieter-Administrator oder der mandantenadministrator kann die Datacenter Firewall-Richtlinien über den Netzwerk-Controller und die northbound-APIs verwalten.  
  
Die Datacenter Firewall bietet die folgenden Vorteile für Cloud-Dienstanbieter:  
  
-   Eine hoch skalierbaren, verwaltbaren und diagnosable softwarebasierte Firewall-Lösung, die Mandanten angeboten werden können  
  
-   Bewegungsfreiheit Mandanten virtuelle Maschinen zu anderen Hosts ohne aktuelle Mandanten-Firewall-Richtlinien  
  
    -   Als vSwitch-Port-Agent Hostfirewall bereitgestellt  
  
    -   Mandanten-VMs erhalten die Firewall-Agent-Host vSwitch zugewiesenen Richtlinien  
  
    -   Firewall-Regeln werden in jede vSwitch-Port, unabhängig von der tatsächlichen Host Ausführen des virtuellen Computers konfiguriert.  
  
-   Bietet Schutz für virtuelle Maschinen, die unabhängig vom Mandanten Gastbetriebssystem, das für den Mandanten  
  
Die Datacenter Firewall bietet die folgenden Vorteile für Mandanten:  
  
-   Definieren von Firewallregeln zum Schutz von Arbeitslasten in virtuellen Netzwerken mit Internetzugriff  
  
-   Definieren von Firewallregeln zum Schutz von Datenverkehr zwischen virtuellen Computern im selben L2-virtuellen Subnetz sowie zwischen VMs in verschiedenen virtuellen L2-Subnetzen  
  
-   Die Möglichkeit zum Definieren von Firewallregeln zum Schützen und Isolieren von Netzwerkdatenverkehr zwischen Mandanten lokale Netzwerke und ihre virtuellen Netzwerke an den Dienstanbieter  
  


