---
title: Unterstützte Windows-Gast Betriebssysteme für Hyper-V unter Windows Server
description: Listet die Windows-Betriebssysteme auf, die für die Verwendung als Gast in einem virtuellen Computer unterstützt werden. Enthält auch Links zu ähnlichen Artikeln für frühere Versionen von Hyper-V.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 06b35897-2192-48b7-8c2d-125c520b0786
author: lizap
ms.author: elizapo
ms.date: 01/08/2019
ms.openlocfilehash: 34183deefef3eea94c2b1da8dcb111c2c17efd8a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857973"
---
# <a name="supported-windows-guest-operating-systems-for-hyper-v-on-windows-server"></a>Unterstützte Windows-Gast Betriebssysteme für Hyper-V unter Windows Server

>Gilt für: Windows Server 2016, Windows Server 2019

Hyper-V unterstützt mehrere Versionen von Windows Server-, Windows-und Linux-Distributionen, die auf virtuellen Computern ausgeführt werden, als Gast Betriebssysteme. In diesem Artikel werden die unterstützten Windows Server-und Windows-Gast Betriebssysteme behandelt. Informationen zu Linux-und FreeBSD-Distributionen finden Sie [unter Unterstützte virtuelle Linux-und FreeBSD-Computer für Hyper-V unter Windows](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md).  
    
Für einige Betriebssysteme ist Integration Services integriert. Andere erfordern, dass Sie Integrationsdienste in einem separaten Schritt installieren oder aktualisieren, nachdem Sie das Betriebssystem auf dem virtuellen Computer eingerichtet haben. Weitere Informationen finden Sie in den Abschnitten unten und [Integration Services](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/integration-services).  
  
## <a name="supported-windows-server-guest-operating-systems"></a>Unterstützte Gastbetriebssysteme für Windows Server  

Im folgenden finden Sie die Versionen von Windows Server, die als Gast Betriebssysteme für Hyper-V in Windows Server 2016 und Windows Server 2019 unterstützt werden. 
  
|Gastbetriebssystem (Server)|Maximale Anzahl virtueller Prozessoren|Integrationsdienste|Hinweise|  
|-------------------------------------|----------------------------------------|------------------------|---------| 
|Windows Server, Version 1909 |240 für Generation 2;<br>64 für Generation 1|Integrierte|Für die Unterstützung von mehr als 240 virtuellen Prozessoren sind Windows Server-, Version 1903-und spätere Gast Betriebssysteme erforderlich.| 
|Windows Server, Version 1903 |240 für Generation 2;<br>64 für Generation 1|Integrierte||
|Windows Server, Version 1809 |240 für Generation 2;<br>64 für Generation 1|Integrierte|| 
|Windows Server 2019 |240 für Generation 2;<br>64 für Generation 1|Integrierte||
|Windows Server, Version 1803 |240 für Generation 2;<br>64 für Generation 1|Integrierte|| 
|Windows Server 2016 |240 für Generation 2;<br>64 für Generation 1|Integrierte|| 
|Windows Server 2012 R2 |64|Integrierte||  
|Windows Server 2012 |64|Integrierte||  
|Windows Server 2008 R2 mit Service Pack 1 (SP 1)|64|Installieren Sie alle wichtigen Windows-Updates nach dem Einrichten des Gast Betriebssystems.|Datacenter, Enterprise, Standard und Web Edition.|
|Windows Server 2008 mit Service Pack 2 (SP2)|8|Installieren Sie alle wichtigen Windows-Updates nach dem Einrichten des Gast Betriebssystems.|Datacenter, Enterprise, Standard und Web Edition (32-Bit und 64-Bit).|  
  
## <a name="supported-windows-client-guest-operating-systems"></a>Unterstützte Windows Client-Gast Betriebssysteme  

Im folgenden finden Sie die Versionen des Windows-Clients, die als Gast Betriebssysteme für Hyper-V in Windows Server 2016 und Windows Server 2019 unterstützt werden.
  
|Gastbetriebssystem (Client)|Maximale Anzahl virtueller Prozessoren|Integrationsdienste|Hinweise|  
|-------------------------------------|----------------------------------------|------------------------|---------|  
|Windows 10|32|Integrierte||  
|Windows 8.1|32|Integrierte||  
|Windows 7 mit Service Pack 1 (SP 1)|4|Aktualisieren Sie die Integrationsdienste, nachdem Sie das Gast Betriebssystem eingerichtet haben.|Ultimate, Enterprise und Professional Edition (32-Bit und 64-Bit).|  
  
## <a name="guest-operating-system-support-on-other-versions-of-windows"></a>Unterstützung von Gastbetriebssystemen in anderen Versionen von Windows  

Die folgende Tabelle enthält Links zu Informationen zu Gastbetriebssystemen, die für Hyper-V unter anderen Windows-Versionen unterstützt werden.  
  
|Hostbetriebssystem|Thema|  
|-------------------------|---------|  
|Windows 10|[Unterstützte Gast Betriebssysteme für Hyper-V-Client in Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/about/supported-guest-os)|  
|Windows Server 2012 R2 und Windows 8.1|-   [unterstützte Windows-Gast Betriebssysteme für Hyper-V in Windows Server 2012 R2 und Windows 8.1](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn792027(v=ws.11))<br />-   [Linux-und FreeBSD-Virtual Machines auf Hyper-V](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)|  
|Windows Server 2012 und Windows 8|[Unterstützte Windows-Gast Betriebssysteme für Hyper-V in Windows Server 2012 und Windows 8](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn792028(v=ws.11))|  
|Windows Server 2008 und Windows Server 2008 R2|[Informationen zu Virtual Machines und Gastbetriebssystemen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc794868(v=ws.10))|  
  
## <a name="how-microsoft-provides-support-for-guest-operating-systems"></a>So bietet Microsoft Unterstützung für Gast Betriebssysteme  

Microsoft bietet auf folgende Weise Unterstützung für Gastbetriebssysteme:  
  
-   Der Microsoft-Support hilft beim Lösen von Problemen in Microsoft-Betriebssystemen und -Integrationsdiensten.  
  
-   Für Probleme in anderen Betriebssystemen, die vom Anbieter des Betriebssystems für die Ausführung unter Hyper-V zertifiziert wurden, wird der Support vom Anbieter geleistet.  
  
-   Andere in den Betriebssystemen ermittelte Probleme werden von Microsoft an die Supportcommunity mehrerer Anbieter weitergeleitet, [TSANet](https://www.tsanet.org/).  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Virtuelle Linux- und FreeBSD Computer unter Hyper-V](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)  
  
-   [Unterstützte Gast Betriebssysteme für Hyper-V-Client in Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/about/supported-guest-os)  
  



