---
title: Neues in DHCP
description: Dieses Thema enthält eine Übersicht über neue Features für Dynamic Host Configuration Protocol (DHCP) in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: c6f36998-5b64-45d1-b1f0-0f0d6604dbe3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f67e5dfd8aefcf408a41f6fc919665419f0ff1c9
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-dhcp"></a>Neues in DHCP

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema werden die Dynamic Host Configuration-Protokoll (DHCP)-Funktionen, die neuen oder geänderten in Windows Server 2016 beschrieben.
  
DHCP ist ein Internet Engineering Task Force (IETF)-Standard, der den Verwaltungsaufwand und die Komplexität beim Konfigurieren von Hosts in einem TCP/Konfigurationsproblemen-basierten Netzwerk, z. B. einem privaten Intranet zu reduzieren. Mithilfe des DHCP-Serverdiensts führt den Konfigurationsprozess für TCP/IP auf DHCP-Clients automatisch.

Die folgenden Abschnitte enthalten Informationen zu neuen Features und Änderungen an der Funktionalität für DHCP.

## <a name="dhcp-subnet-selection-options"></a>DHCP-Subnetz Auswahloptionen

DHCP unterstützt jetzt Optionen 118 und 82 \(sub-option 5\). Diese Optionen können Sie DHCP-Proxy-Clients und -Relay-Agents eine IP-Adresse für ein bestimmtes Subnetz und von einer bestimmten IP-Adressbereich und Bereich anfordern können.

Wenn Sie einen DHCP-Proxy-Client verwenden, der mit DHCP-Option 118, z. B. ein virtuelles privates Netzwerk \(VPN\) Server konfiguriert ist, auf denen Windows Server 2016 und die RAS-Serverrolle ausgeführt wird kann VPN-Server eine IP-Adresslease für VPN-Clients aus einer bestimmten IP-Adressbereich anfordern.

Wenn Sie einen DHCP-Relay-Agent verwenden, der mit DHCP-Option 82, 5, Sub\-Option konfiguriert ist kann der Relay-Agent eine IP-Adresslease für DHCP-Clients aus einer bestimmten IP-Adressbereich anfordern.

Weitere Informationen finden Sie unter [DHCP-Subnetz Auswahloptionen](dhcp-subnet-options.md).

## <a name="new-logging-events-for-dns-registration-failures-by-the-dhcp-server"></a>Neue Protokollieren von Ereignissen für DNS-Fehler bei der Registrierung der DHCP-Server

DHCP enthält jetzt die Protokollierung von Ereignissen für Situationen, in dem sich DHCP-Server DNS-Datensatz Registrierungen auf dem DNS-Server nicht ausgeführt.

Weitere Informationen finden Sie unter [DHCP-Protokollierung Ereignisse für die DNS-Datensatz Registrierungen](dhcp-dns-events.md).

## <a name="dhcp-nap-is-not-supported-in-windows-server-2016"></a>DHCP NAP wird in WindowsServer 2016 nicht unterstützt.

Network Access Protection \(NAP\) veraltetes Feature in Windows Server 2012 R2 und in Windows Server 2016 unterstützt die DHCP-Serverrolle nicht mehr NAP. Weitere Informationen finden Sie unter [Features Removed or Deprecated in Windows Server 2012 R2](https://technet.microsoft.com/library/dn303411.aspx).  
  
NAP-Unterstützung wurde der DHCP-Serverrolle in Windows Server 2008 eingeführt und wird in Windows-Client und Server-Betriebssystemen vor Windows 10 und Windows Server 2016 unterstützt. In der folgende Tabelle werden die Unterstützung für NAP in Windows Server zusammengefasst.  
  
|Betriebssystem|NAP-Unterstützung|  
|--------------------|---------------|  
| Windows Server 2008 |Unterstützt|  
| Windows Server2008 R2 |Unterstützt|  
| Windows Server 2012 |Unterstützt|  
| Windows Server2012 R2 |Unterstützt|  
| Windows Server 2016|Nicht unterstützt|  
  
In einer NAP-Bereitstellung kann ein DHCP-Server unter einem Betriebssystem, die NAP unterstützen als NAP-Erzwingung verwendet für die DHCP-NAP-Erzwingungsmethode fungieren. Weitere Informationen zu DHCP nap finden Sie unter [Prüfliste: Implementieren eines Entwurfs einer DHCP-Erzwingung](https://technet.microsoft.com/library/dd314186.aspx).  
  
In Windows Server 2016 DHCP-Server-NAP-Richtlinien nicht erzwungen, und DHCP-Bereiche können nicht NAP\-fähig sein. DHCP-Clientcomputer, die ebenfalls NAP-Clients sind ein Statement of Health \(SoH\) mit der DHCP-Anforderung zu senden. Wenn der DHCP-Server Windows Server 2016 ausgeführt wird, werden diese Anforderungen verarbeitet, als ob keine SoH vorhanden ist. Der DHCP-Server gewährt eine normale DHCP-Lease an dem Client. 

Wenn Server, auf denen Windows Server 2016 ausgeführt werden RADIUS-Proxys, die authentifizierungsanforderungen an einem Netzwerkrichtlinienserver \(NPS\) weiterleiten, die NAP unterstützen sind, werden diese NAP-Clients von NPS als nicht NAP\-fähig und NAP-Verarbeitung fehl, ausgewertet.
  
## <a name="see-also"></a>Siehe auch  
  
-   [Dynamic Host Configuration-Protokoll (DHCP)](Dynamic-Host-Configuration-Protocol--DHCP-.md)  
  

