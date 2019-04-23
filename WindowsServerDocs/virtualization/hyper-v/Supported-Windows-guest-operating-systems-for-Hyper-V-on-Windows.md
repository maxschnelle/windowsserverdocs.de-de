---
title: Unterstützte Windows-Gastbetriebssysteme für Hyper-V unter Windows Server
description: Listet die Windows-Betriebssysteme, die für die Verwendung als Gast auf einem virtuellen Computer unterstützt. Außerdem finden Sie Links auf ähnliche Artikel für frühere Versionen von Hyper-V.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 06b35897-2192-48b7-8c2d-125c520b0786
author: lizap
ms.author: elizapo
ms.date: 01/08/2019
ms.openlocfilehash: 5f0e91f3202f09d340154b49408c56752a9de577
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874211"
---
# <a name="supported-windows-guest-operating-systems-for-hyper-v-on-windows-server"></a>Unterstützte Windows-Gastbetriebssysteme für Hyper-V unter Windows Server

>Gilt für: WindowsServer 2016, WindowsServer 2019

Hyper-V unterstützt mehrere Versionen von Windows Server, Windows und Linux-Distributionen auf virtuellen Computern, die als Gastbetriebssysteme ausführen. Dieser Artikel behandelt die unterstützte Windows-Server und Windows-Gastbetriebssysteme. Linux und FreeBSD-Distributionen finden Sie unter [unterstützt Linux und FreeBSD-VMs für Hyper-V unter Windows](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md).  
    
Einige Betriebssysteme haben den Integrationsservices integriert. Andere erfordern, dass Sie beim Installieren oder upgrade von Integrationsservices als separater Schritt, nachdem Sie das Betriebssystem auf dem virtuellen Computer eingerichtet. Weitere Informationen finden Sie unter den folgenden Abschnitten und [Integrationsdienste](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/integration-services).  
  
## <a name="supported-windows-server-guest-operating-systems"></a>Unterstützte Gastbetriebssysteme für Windows Server  

Es folgen die Versionen von Windows Server, die als Gastbetriebssysteme für Hyper-V in Windows Server 2016 und Windows Server-2019 unterstützt werden. 
  
|Gastbetriebssystem (Server)|Maximale Anzahl virtueller Prozessoren|Integration Services|Hinweise|  
|-------------------------------------|----------------------------------------|------------------------|---------|  
|Windows Server 2019 |240 für Generation 2;<br>64 für die Generation 1|Integrierte|| 
|Windows Server 2016 |240 für Generation 2;<br>64 für die Generation 1|Integrierte|| 
|Windows Server 2012 R2 |64|Integrierte||  
|Windows Server 2012 |64|Integrierte||  
|Windows Server 2008 R2 mit Service Pack 1 (SP 1)|64|Installieren Sie alle wichtigen Windows-Updates, nach dem Einrichten des Gastbetriebssystems verfügbar.|Datacenter, Enterprise, Standard und Web Edition.|
|Windows Server 2008 mit Service Pack 2 (SP2)|8|Installieren Sie alle wichtigen Windows-Updates, nach dem Einrichten des Gastbetriebssystems verfügbar.|Datacenter, Enterprise, Standard und Web Edition (32-Bit und 64-Bit).|  
  
## <a name="supported-windows-client-guest-operating-systems"></a>Unterstützte Clients Windows-Gastbetriebssysteme  

Es folgen die Versionen des Windows-Clients, die als Gastbetriebssysteme für Hyper-V in Windows Server 2016 und Windows Server-2019 unterstützt werden.
  
|Gastbetriebssystem (Client)|Maximale Anzahl virtueller Prozessoren|Integration Services|Hinweise|  
|-------------------------------------|----------------------------------------|------------------------|---------|  
|Windows 10|32|Integrierte||  
|Windows 8.1|32|Integrierte||  
|Windows 7 mit Service Pack 1 (SP 1)|4|Aktualisieren Sie die Integrationsdienste nach dem Einrichten des Gastbetriebssystems verfügbar.|Ultimate, Enterprise und Professional Edition (32-Bit und 64-Bit).|  
  
## <a name="guest-operating-system-support-on-other-versions-of-windows"></a>Unterstützung der Gast-Betriebssystem auf andere Versionen von Windows  

Die folgende Tabelle enthält Links zu Informationen über die Gastbetriebssysteme für Hyper-V in anderen Versionen von Windows unterstützt.  
  
|Hostbetriebssystem|Thema|  
|-------------------------|---------|  
|Windows 10|[Unterstützte Gastbetriebssysteme für Hyper-V für Clients unter Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/about/supported-guest-os)|  
|Windows Server 2012 R2 und Windows 8.1|-   [Unterstützte Windows-Gastbetriebssysteme für Hyper-V in Windows Server 2012 R2 und Windows 8.1](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn792027(v=ws.11))<br />-   [Linux- und FreeBSD-Maschinen in Hyper-V](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)|  
|Windows Server 2012 und Windows 8|[Unterstützte Windows-Gastbetriebssysteme für Hyper-V in WindowsServer 2012 und Windows 8](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn792028(v=ws.11))|  
|Windows Server 2008 und Windows Server 2008 R2|[Informationen zu virtuellen Computern und Gastbetriebssystemen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc794868(v=ws.10))|  
  
## <a name="how-microsoft-provides-support-for-guest-operating-systems"></a>Wie Microsoft bietet Unterstützung für Gastbetriebssysteme  

Microsoft bietet auf folgende Weise Unterstützung für Gastbetriebssysteme:  
  
-   Der Microsoft-Support hilft beim Lösen von Problemen in Microsoft-Betriebssystemen und -Integrationsdiensten.  
  
-   Für Probleme in anderen Betriebssystemen, die vom Anbieter des Betriebssystems für die Ausführung unter Hyper-V zertifiziert wurden, wird der Support vom Anbieter geleistet.  
  
-   Andere in den Betriebssystemen ermittelte Probleme werden von Microsoft an die Supportcommunity mehrerer Anbieter weitergeleitet, [TSANet](https://www.tsanet.org/).  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Linux- und FreeBSD-Maschinen in Hyper-V](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)  
  
-   [Unterstützte Gastbetriebssysteme für Hyper-V für Clients unter Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/about/supported-guest-os)  
  



