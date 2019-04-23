---
title: Neues in DHCP
description: Dieses Thema enthält eine Übersicht über neue Funktionen für Dynamic Host Configuration Protocol (DHCP) in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: c6f36998-5b64-45d1-b1f0-0f0d6604dbe3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 73cc5134f7af5063c912ad578fa7d660b3194aa1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840231"
---
# <a name="whats-new-in-dhcp"></a>Neues in DHCP

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema beschreibt die Dynamic Host Configuration Protocol (DHCP) Funktionen, die neue oder geänderte in Windows Server 2016.
  
DHCP ist ein Internet Engineering Task Force (IETF)-Standard, der den Verwaltungsaufwand und die Komplexität beim Konfigurieren von Hosts in einem TCP/IP reduzieren\-basierten Netzwerk, z. B. einem privaten Intranet. Der DHCP-Serverdienst führt den Konfigurationsprozess für TCP/IP auf DHCP-Clients automatisch durch.

Die folgenden Abschnitte enthalten Informationen zu neuen Features und Änderungen an der Funktionalität für DHCP.

## <a name="dhcp-subnet-selection-options"></a>Auswahloptionen für DHCP-Subnetz

DHCP unterstützt nun Optionen 118 und 82 \(untergeordnete option 5\). Sie können diese Optionen verwenden, um DHCP-Proxy-Clients und -Relay-Agents zum Anfordern einer IP-Adresse für ein bestimmtes Subnetz, und von einer bestimmten IP-Adressbereich und den Bereich zu ermöglichen.


Wenn Sie einen DHCP-Relay-Agent verwenden, der mit DHCP-Option 82 konfiguriert ist, sub\-option 5 der Relay-Agent kann eine IP-Adresslease für DHCP-Clients aus einem bestimmten Bereich von IP-Adresse anfordern.

Weitere Informationen finden Sie unter [DHCP-Subnetz-Auswahloptionen](dhcp-subnet-options.md).

## <a name="new-logging-events-for-dns-registration-failures-by-the-dhcp-server"></a>Neue Protokollierung von Ereignissen für DNS-Fehler bei der Registrierung vom DHCP-Server

DHCP enthält jetzt die Protokollierung von Ereignissen für Situationen, in dem sich DHCP-Server DNS-Datensatz Registrierungen auf dem DNS-Server fehl.

Weitere Informationen finden Sie unter [DHCP-Protokollierung von Ereignissen für DNS-Datensatz Registrierungen](dhcp-dns-events.md).

## <a name="dhcp-nap-is-not-supported-in-windows-server-2016"></a>DHCP-NAP wird unter WindowsServer 2016 nicht unterstützt.

Netzwerkzugriffsschutz \(NAP\) veraltetes Feature in Windows Server 2012 R2 und Windows Server 2016 die DHCP-Serverrolle NAP nicht mehr unterstützt. Weitere Informationen finden Sie unter [Features Removed or Deprecated in Windows Server 2012 R2](https://technet.microsoft.com/library/dn303411.aspx).  
  
NAP-Unterstützung wurde der DHCP-Serverrolle in Windows Server 2008 eingeführt und wird in Windows-Client und Server-Betriebssystemen vor Windows 10 und Windows Server 2016 unterstützt. Die folgende Tabelle enthält die Unterstützung für NAP in Windows Server.  
  
|Betriebssystem|NAP-Unterstützung|  
|--------------------|---------------|  
| WindowsServer 2008 |Unterstützt|  
| Windows Server 2008 R2 |Unterstützt|  
| Windows Server 2012 |Unterstützt|  
| Windows Server 2012 R2 |Unterstützt|  
| Windows Server 2016|Nicht unterstützt.|  
  
In einer NAP-Bereitstellung kann ein DHCP-Server unter einem Betriebssystem, das NAP unterstützt als eine NAP-Erzwingungspunkt für die NAP-DHCP-Erzwingungsmethode fungieren. Weitere Informationen zu DHCP nap finden Sie unter [Prüfliste: Implementieren eines DHCP-Erzwingung Entwurfs](https://technet.microsoft.com/library/dd314186.aspx).  
  
In Windows Server 2016 erzwingen DHCP-Server nicht NAP-Richtlinien und DHCP-Bereiche nicht NAP\-aktiviert. Senden von DHCP-Clientcomputer, die auch NAP-Clients ein Statement of Health \(SoH\) mit der DHCP-Anforderung. Wenn der DHCP-Server Windows Server 2016 ausgeführt wird, werden diese Anforderungen verarbeitet, als ob keine SoH vorhanden ist. Der DHCP-Server gewährt eine normalen DHCP-Clientlease an dem Client. 

Wenn Server, auf denen Windows Server 2016 ausgeführt werden, RADIUS-Proxys sind, die authentifizierungsanforderungen an einem Netzwerkrichtlinienserver weitergeleitet \(NPS\) , das NAP unterstützt, diese NAP-Clients werden ausgewertet, von NPS als nicht NAP\-fähig ist, und NAP Verarbeitung ein Fehler auftritt.
  
## <a name="see-also"></a>Siehe auch  
  
-   [Dynamic Host Configuration-Protokoll (DHCP)](Dynamic-Host-Configuration-Protocol--DHCP-.md)  
  

