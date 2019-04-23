---
title: 'Rechenzentrumsfirewall: Übersicht'
description: Sie können in diesem Thema verwenden, erfahren Sie Datacenter Firewall, d.h. eine Netzwerkebene, die 5-Tupel (Protokoll, Quell- und Ziel-Portnummern, Quell- und Ziel-IP-Adressen), die statusbehaftete, mehrinstanzenfähige Firewall in Windows Server 2016.
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
ms.openlocfilehash: f1de50dc61639f4985c9d28fdde6072af650f42e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890831"
---
# <a name="datacenter-firewall-overview"></a>Rechenzentrumsfirewall: Übersicht

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Datacenter Firewall ist ein neuer Dienst in Windows Server 2016 enthalten. Es ist ein Netzwerkebene, die 5-Tupel (Protokoll, Quell- und Portnummern, Quell- und Ziel-IP-Adressen), die statusbehaftete, mehrinstanzenfähige Firewall. Wenn bereitgestellt und als einen Dienst vom Dienstanbieter angeboten, können Mandantenadministratoren installieren und Konfigurieren der Firewall-Richtlinien zum Schutz ihrer virtuellen Netzwerke mit unerwünschtem Datenverkehr aus dem Internet und der Intranetnetzwerke.  
  
![Datacenter Firewall im Netzwerkstapel](../../../media/Datacenter-Firewall-Overview/MultitenantFirewallOverview2.png)  
  
Der Administrator des Dienstanbieters oder Mandantenadministratoren kann die Datacenter Firewall-Richtlinien über den Netzwerkcontroller und die northbound-APIs verwalten.  
  
Die Datacenter Firewall bietet die folgenden Vorteile für clouddienstanbieter zur Verfügung:  
  
-   Eine hoch skalierbare, überschaubare und diagnosable Software-basierte Firewall-Lösung, die für Mandanten angeboten werden kann  
  
-   Freiheit, die Mandanten-VMs in verschiedenen Compute-Hosts zu verschieben, ohne wichtige Mandanten-Firewall-Richtlinien  
  
    -   Bereitgestellt als Firewall vSwitch-Port-Host-agent  
  
    -   Mandanten-VMs erhalten, die ihre vSwitch-Hostfirewall Agent zugewiesenen Richtlinien  
  
    -   Firewall-Regeln werden in jede vSwitch-Port, die unabhängig von der tatsächliche Host der virtuellen Computer konfiguriert.  
  
-   Bietet Schutz für virtuelle Computer unabhängig von der Mandanten-Gastbetriebssystem-Mandanten  
  
Die Datacenter Firewall bietet die folgenden Vorteile für Mandanten:  
  
-   Möglichkeit zum Definieren von Firewall-Regeln zum Schutz von Workloads in virtuellen Netzwerken mit Internetzugriff  
  
-   Möglichkeit zum Definieren von Firewall-Regeln zum Schutz von Datenverkehr zwischen virtuellen Computern im gleichen L2 virtuellen Subnetz sowie zwischen virtuellen Computern auf verschiedene L2-und virtuelle Subnetze  
  
-   Möglichkeit zum Definieren von Firewall-Regeln zum Schutz und den Netzwerkdatenverkehr zwischen Mandanten isolieren lokalen Netzwerken und ihren virtuellen Netzwerken vom Dienstanbieter  
  


