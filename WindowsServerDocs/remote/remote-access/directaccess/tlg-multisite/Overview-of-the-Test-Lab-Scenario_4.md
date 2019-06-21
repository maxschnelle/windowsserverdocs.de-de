---
title: Übersicht über das Testumgebungsszenario
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess Multisite-Bereitstellung für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9afeced4-1a9b-4cb3-9fc4-d7e44c675755
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b067d5f247f5dc13ea294d83a76f267c5a57ffe7
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283301"
---
# <a name="overview-of-the-test-lab-scenario"></a>Übersicht über das Testumgebungsszenario

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Test Lab-Szenario wird DirectAccess mit bereitgestellt:  
  
-   **DC1**– einem Server, der als Domänencontroller konfiguriert ist, DNS-Server und DHCP-Server für die Domäne "corp.contoso.com".  
  
-   **2-DC1**– einem Server, der als Domänencontroller und DNS-Server für die Domäne corp2.corp.contoso.com konfiguriert ist.  
  
-   **EDGE1 und 2-EDGE1**-zwei-Server im internen Netzwerk, der als RAS-Server konfiguriert werden. Jeder Server hat zwei Netzwerkkarten. eine mit dem internen Netzwerk verbunden, und der andere mit dem externen Netzwerk verbunden.  
  
-   **App1 und 2-APP1**– zwei Server im internen Netzwerk, die als Web- und Dateiservern konfiguriert sind.  
  
-   **APP2**- ein-Computer im internen Netzwerk, das als IPv4-nur Web- und -Server konfiguriert ist. Dieser Computer wird verwendet, um die NAT64/DNS64-Funktionen hervorzuheben.  
  
-   **ROUTER1**– ein Server, konfiguriert ist, um das routing zwischen den beiden Unternehmen internen Netzwerken bereitstellen.  
  
-   **INET1**– einem Server, der als Internet-DNS und DHCP-Server konfiguriert ist.  
  
-   **NAT1**– eine Client-Computer, der als ein Gerät Network Address (Translator, NAT) verwenden die gemeinsame Nutzung der Internetverbindung konfiguriert ist.  
  
-   **CLIENT1 und CLIENT2**-zwei Clientcomputern, die als DirectAccess-Clients konfiguriert sind, die DirectAccess-Konnektivität zu testen, beim Verschieben zwischen dem internen Netzwerk, das simulierte Internet und einem privaten Netzwerk verwendet werden. **CLIENT2** ist eine Windows 7&reg; Client.  
  
Die-testumgebung besteht aus vier Subnetzen, mit denen Folgendes simuliert:  
  
-   Ein Heimnetzwerk mit dem Namen "Homenet" (192.168.137.0/24), die mit dem Internet von einem NAT-Gerät verbunden  
  
-   Das externe Netzwerk, durch die Internet-Subnetz (131.107.0.0/24) dargestellt wird.  
  
-   Ein internes Netzwerk mit dem Namen "Corpnet" (10.0.0.0/24; 2001:db8:1:: / 64) aus dem Internet durch EDGE1-RAS-Server getrennt.  
  
-   Ein internes Netzwerk mit dem Namen 2-Corpnet1 (10.2.0.0/24; 2001:db8:2:: / 64) aus dem Internet durch 2-EDGE1 RAS-Server getrennt.  
  
Computer in jedem Subnetz eine Verbindung herstellen, entweder mit einem physischen oder virtuellen Hub oder Switch, wie in der folgenden Abbildung dargestellt.  
  
![Übersicht über die Testumgebung](../../../media/Overview-of-the-Test-Lab-Scenario_4/TLG_DA_Multisite.png)  
  


