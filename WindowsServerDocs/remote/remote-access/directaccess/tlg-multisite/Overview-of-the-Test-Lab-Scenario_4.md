---
title: Übersicht über das Testumgebungsszenario
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9afeced4-1a9b-4cb3-9fc4-d7e44c675755
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bcee25c4a13afc2b41d6b1a9a43a1489054ef43d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388409"
---
# <a name="overview-of-the-test-lab-scenario"></a>Übersicht über das Testumgebungsszenario

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Test Labor Szenario wird DirectAccess mit folgenden Aufgaben bereitgestellt:  
  
-   **DC1**-ein Server, der als Domänen Controller, DNS-Server und DHCP-Server für die Corp.contoso.com-Domäne konfiguriert ist.  
  
-   **2-DC1**: ein Server, der als Domänen Controller und DNS-Server für die corp2.Corp.contoso.com-Domäne konfiguriert ist.  
  
-   **Edge1 und 2-Edge1**-zwei Server im internen Netzwerk, die als RAS-Server konfiguriert sind. Jeder Server verfügt über zwei Netzwerkadapter: eine Verbindung mit dem internen Netzwerk und die andere mit dem externen Netzwerk.  
  
-   **App1 und 2-App1**-zwei Server im internen Netzwerk, die als Web-und Dateiserver konfiguriert sind.  
  
-   **APP2**-ein Computer im internen Netzwerk, der als einziger IPv4-Web-und-Dateiserver konfiguriert ist. Mithilfe dieses Computers werden die NAT64/DNS64-Funktionen hervorgehoben.  
  
-   **ROUTER1**-ein Server, der für die Bereitstellung eines Routings zwischen den beiden internen Unternehmensnetzwerken konfiguriert ist.  
  
-   **INET1**-ein Server, der als Internet-DNS und DHCP-Server konfiguriert ist.  
  
-   **NAT1**-ein Client Computer, der als NAT-Gerät (Network Address Translator) mithilfe der Freigabe von Internet Verbindungen konfiguriert ist.  
  
-   **CLIENT1 und CLIENT2**: zwei Client Computer, die als DirectAccess-Clients konfiguriert sind und zum Testen der DirectAccess-Konnektivität bei der Umstellung zwischen dem internen Netzwerk, dem simulierten Internet und einem Heimnetzwerk verwendet werden. **Client2** ist ein Windows 7-&reg; Client.  
  
Die Testumgebung besteht aus vier Subnetzen, die Folgendes simulieren:  
  
-   Ein Heimnetzwerk mit dem Namen homenet (192.168.137.0/24), das durch eine NAT mit dem Internet verbunden ist.  
  
-   Das externe Netzwerk, das durch das Internet Subnetz (131.107.0.0/24) dargestellt wird.  
  
-   Ein internes Netzwerk mit dem Namen Corpnet (10.0.0.0/24; 2001: db8:1::/64), das durch den Edge1-Remote Zugriffs Server vom Internet getrennt ist.  
  
-   Ein internes Netzwerk mit dem Namen 2-Corpnet1 (10.2.0.0/24; 2001: db8:2::/64), getrennt vom Internet durch den 2-Edge1-Remote Zugriffs Server.  
  
Computer in jedem Subnetz stellen eine Verbindung entweder über einen physischen oder einen virtuellen Hub oder Switch her, wie in der folgenden Abbildung dargestellt.  
  
![Übersicht über die Testumgebung](../../../media/Overview-of-the-Test-Lab-Scenario_4/TLG_DA_Multisite.png)  
  


