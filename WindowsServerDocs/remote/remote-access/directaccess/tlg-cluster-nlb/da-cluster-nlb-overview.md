---
title: Übersicht über das Testumgebungsszenario für DirectAccess-Cluster-NLB
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: Vorführen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd1e9efd-19e9-49e7-8432-881f661c9792
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a6d82713dfb12e6775402d29bfcebaa0ec8b066c
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281556"
---
# <a name="overview-of-the-directaccess-cluster-nlb-test-lab-scenario"></a>Übersicht über das Testumgebungsszenario für DirectAccess-Cluster-NLB

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Test Lab-Szenario wird DirectAccess mit bereitgestellt:  
  
-   **DC1**– einem Server, der als Domänencontroller konfiguriert ist, Domain Name System (DNS)-Server und Server mit Dynamic Host Configuration Protocol (DHCP).  
  
-   **EDGE1**– einem Server im internen Netzwerk, das als der erste RAS-Server in einem RAS-Server-Cluster konfiguriert ist. Dieser Server verfügt über zwei Netzwerkadapter; eine mit dem internen Netzwerk verbunden, und der andere mit dem externen Netzwerk verbunden.  
  
-   **EDGE2**– einem Server im internen Netzwerk, das als das zweite RAS-Server in einem RAS-Server-Cluster konfiguriert ist. Dieser Server verfügt über zwei Netzwerkadapter; eine mit dem internen Netzwerk verbunden, und der andere mit dem externen Netzwerk verbunden.  
  
-   **App1**– einem Server im internen Netzwerk, das als Web "und"-Datei, und als eine Unternehmens-Stammzertifizierungsstelle (CA) konfiguriert ist  
  
-   **APP2**- ein-Computer im internen Netzwerk, das als IPv4-nur Web- und -Server konfiguriert ist. Dieser Computer wird verwendet, um die NAT64/DNS64-Funktionen hervorzuheben.  
  
-   **INET1**– einem Server, der als Internet-DNS und DHCP-Server konfiguriert ist.  
  
-   **NAT1**– eine Client-Computer, der als ein Gerät Network Address (Translator, NAT) verwenden die gemeinsame Nutzung der Internetverbindung konfiguriert ist.  
  
-   **"Client1"** – eine Client-Computer, der als DirectAccess-Client konfiguriert ist, das verwendet wird, um die DirectAccess-Konnektivität zu testen, beim Verschieben zwischen dem internen Netzwerk, das simulierte Internet und einem Heimnetzwerk.  
  
Die-testumgebung besteht aus drei Subnetze, mit die Folgendes simuliert:  
  
-   Ein Heimnetzwerk mit dem Namen "Homenet" (192.168.137.0/24), die mit dem Internet von einem NAT-Gerät verbunden  
  
-   Das externe Netzwerk, durch die Internet-Subnetz (131.107.0.0/24) dargestellt wird.  
  
-   Ein internes Netzwerk mit dem Namen "Corpnet" (10.0.0.0/24; 2001:db8:1:: / 64) aus dem Internet durch RAS-Server getrennt.  
  
Computer in jedem Subnetz eine Verbindung herstellen, entweder mit einem physischen oder virtuellen Hub oder Switch, wie in der folgenden Abbildung dargestellt.  
  
![Übersicht über die Testumgebung](../../../media/Overview-of-the-Test-Lab-Scenario_5/TLG_DA_Cluster.png)  
  


