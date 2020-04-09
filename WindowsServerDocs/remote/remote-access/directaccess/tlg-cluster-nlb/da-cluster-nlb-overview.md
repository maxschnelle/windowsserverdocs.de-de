---
title: Übersicht über das Testumgebungsszenario für DirectAccess-Cluster-NLB
description: Dieses Thema ist Teil der Test Umgebungs Anleitung zum Veranschaulichen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: cd1e9efd-19e9-49e7-8432-881f661c9792
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 7394562ce7a5c08a81fb3c243fb8671d281d8370
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819043"
---
# <a name="overview-of-the-directaccess-cluster-nlb-test-lab-scenario"></a>Übersicht über das Testumgebungsszenario für DirectAccess-Cluster-NLB

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Test Labor Szenario wird DirectAccess mit folgenden Aufgaben bereitgestellt:  
  
-   **DC1**-ein Server, der als Domänen Controller, Domain Name System (DNS)-Server und DHCP-Server (Dynamic Host Configuration Protocol) konfiguriert ist.  
  
-   **Edge1**-ein Server im internen Netzwerk, der als erster RAS-Server in einem Remote Zugriffs Server-Cluster konfiguriert ist. Dieser Server verfügt über zwei Netzwerkadapter: eine Verbindung mit dem internen Netzwerk und die andere mit dem externen Netzwerk.  
  
-   **EDGE2**-ein Server im internen Netzwerk, der als zweiter RAS-Server in einem RAS-Server Cluster konfiguriert ist. Dieser Server verfügt über zwei Netzwerkadapter: eine Verbindung mit dem internen Netzwerk und die andere mit dem externen Netzwerk.  
  
-   **App1**-ein Server im internen Netzwerk, der als Web-und Dateiserver konfiguriert ist, und als Unternehmens-Stamm Zertifizierungsstelle (Certification Authority, ca)  
  
-   **APP2**-ein Computer im internen Netzwerk, der als einziger IPv4-Web-und-Dateiserver konfiguriert ist. Mithilfe dieses Computers werden die NAT64/DNS64-Funktionen hervorgehoben.  
  
-   **INET1**-ein Server, der als Internet-DNS und DHCP-Server konfiguriert ist.  
  
-   **NAT1**-ein Client Computer, der als NAT-Gerät (Network Address Translator) mithilfe der Freigabe von Internet Verbindungen konfiguriert ist.  
  
-   **CLIENT1**-ein Client Computer, der als DirectAccess-Client konfiguriert ist und zum Testen der DirectAccess-Konnektivität bei der Umstellung zwischen dem internen Netzwerk, dem simulierten Internet und einem Heimnetzwerk verwendet wird.  
  
Die Testumgebung besteht aus drei Subnetzen, die Folgendes simulieren:  
  
-   Ein Heimnetzwerk mit dem Namen homenet (192.168.137.0/24), das durch eine NAT mit dem Internet verbunden ist.  
  
-   Das externe Netzwerk, das durch das Internet Subnetz (131.107.0.0/24) dargestellt wird.  
  
-   Ein internes Netzwerk mit dem Namen Corpnet (10.0.0.0/24; 2001: db8:1::/64), das vom Remote Zugriffs Server vom Internet getrennt ist.  
  
Computer in jedem Subnetz stellen eine Verbindung entweder über einen physischen oder einen virtuellen Hub oder Switch her, wie in der folgenden Abbildung dargestellt.  
  
![Übersicht über die Testumgebung](../../../media/Overview-of-the-Test-Lab-Scenario_5/TLG_DA_Cluster.png)  
  


