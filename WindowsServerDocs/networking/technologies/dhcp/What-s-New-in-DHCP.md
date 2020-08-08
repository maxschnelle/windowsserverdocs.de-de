---
title: Neues in DHCP
description: Dieses Thema enthält eine Übersicht über die neuen Features für DHCP (Dynamic Host Configuration Protocol) in Windows Server 2016.
manager: brianlic
ms.topic: get-started-article
ms.assetid: c6f36998-5b64-45d1-b1f0-0f0d6604dbe3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9b0b23b6058655baf599ed66877228b39eb807f9
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87993924"
---
# <a name="whats-new-in-dhcp"></a>Neues in DHCP

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema werden die DHCP-Funktionen (Dynamic Host Configuration Protocol) beschrieben, die in Windows Server 2016 neu oder geändert wurden.

DHCP ist ein IETF (Internet Engineering Task Force)-Standard, der den Verwaltungsaufwand und die Komplexität beim Konfigurieren von Hosts in einem TCP/IP- \- basierten Netzwerk, wie z. b. einem privaten Intranet, reduziert. Der DHCP-Serverdienst führt den Konfigurationsprozess für TCP/IP auf DHCP-Clients automatisch durch.

In den folgenden Abschnitten finden Sie Informationen zu neuen Features und Funktionsänderungen für DHCP.

## <a name="new-dhcp-client-side-features-in-the-windows-10-may-2020-update"></a>Neue DHCP-Client seitige Features im Windows 10-Update von Mai 2020

Der DHCP-Client in Windows 10 wurde mit dem 10. Mai 2020-Update aktualisiert (auch als Windows 10, Version 2004). Wenn Sie einen Windows-Client ausführen und eine Verbindung mit dem Internet über ein getaktetes Android-Telefon herstellen, sollte die Verbindung als "gemessen" gekennzeichnet werden. Zuvor waren die Verbindungen als nicht gemessen gekennzeichnet. Beachten Sie, dass nicht alle Android-Mobiltelefone als getaktet erkannt werden, und einige andere Netzwerke können auch als getaktet angezeigt werden.

Außerdem wurde der Name des herkömmlichen Client Herstellers für einige Windows-basierte Geräte aktualisiert. Dieser Wert ist einfach MSFT 5,0. Einige Geräte werden nun als MSFT 5,0 Xbox angezeigt.

## <a name="dhcp-subnet-selection-options"></a>Optionen für das DHCP-subnetzauswahl

DHCP unterstützt jetzt die Option 82 \( unter Option 5 \) . Mit dieser Option können Sie DHCP-Proxy Clients und Relay-Agents gestatten, eine IP-Adresse für ein bestimmtes Subnetz anzufordern.


Wenn Sie einen DHCP-Relay-Agent verwenden, der mit der DHCP-Option 82, Sub \- Option 5 konfiguriert ist, kann der Relay-Agent eine IP-Adress Lease für DHCP-Clients von einem bestimmten IP-Adressbereich anfordern.

Weitere Informationen finden Sie unter [Auswahl Optionen für das DHCP-Subnetz](dhcp-subnet-options.md).

## <a name="new-logging-events-for-dns-registration-failures-by-the-dhcp-server"></a>Neue Protokollierungs Ereignisse für DNS-Registrierungsfehler durch den DHCP-Server

DHCP umfasst nun Protokollierungs Ereignisse für Situationen, in denen DHCP-Server-DNS-Einträge auf dem DNS-Server fehlschlagen.

Weitere Informationen finden Sie unter [DHCP-Protokollierungs Ereignisse für DNS-Daten Satz Registrierungen](dhcp-dns-events.md).

## <a name="dhcp-nap-is-not-supported-in-windows-server-2016"></a>DHCP-NAP wird in Windows Server 2016 nicht unterstützt.

Netzwerk Zugriffsschutz \( \) -NAP ist in Windows Server 2012 R2 veraltet, und in Windows Server 2016 unterstützt die DHCP-Server Rolle NAP nicht mehr. Weitere Informationen finden Sie unter [in Windows Server 2012 R2 entfernte oder veraltete Features](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303411(v=ws.11)).

Die NAP-Unterstützung wurde mit Windows Server 2008 in die DHCP-Server Rolle eingeführt und wird in Windows-Client-und Server Betriebssystemen vor Windows 10 und Windows Server 2016 unterstützt. In der folgenden Tabelle wird die Unterstützung für NAP in Windows Server zusammengefasst.

|Betriebssystem|NAP-Unterstützung|
|--------------------|---------------|
| WindowsServer 2008 |Unterstützt|
| Windows Server 2008 R2 |Unterstützt|
| Windows Server 2012 |Unterstützt|
| Windows Server 2012 R2 |Unterstützt|
| Windows Server 2016|Nicht unterstützt|

In einer NAP-Bereitstellung kann ein DHCP-Server mit einem Betriebssystem, das NAP unterstützt, als NAP-Erzwingungs Punkt für die NAP-Erzwingungs Methode fungieren. Weitere Informationen zu DHCP in NAP finden Sie unter Prüfliste [: Implementieren eines DHCP](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd314186(v=ws.10))-Erzwingungs Entwurfs.

In Windows Server 2016 erzwingen DHCP-Server keine NAP-Richtlinien, und DHCP-Bereiche können nicht NAP- \- fähig sein. DHCP-Client Computer, die auch NAP-Clients sind, senden ein \( SoH-SoH \) mit der DHCP-Anforderung. Wenn auf dem DHCP-Server Windows Server 2016 ausgeführt wird, werden diese Anforderungen so verarbeitet, als ob kein SoH vorhanden ist. Der DHCP-Server gewährt dem Client eine normale DHCP-Lease.

Wenn Server, auf denen Windows Server 2016 ausgeführt wird, RADIUS-Proxys sind, die Authentifizierungsanforderungen an einen Netzwerk Richtlinien Server weiterleiten, \( \) der NAP unterstützt, werden diese NAP-Clients von NPS als nicht NAP \- -fähig ausgewertet, und die NAP-Verarbeitung schlägt fehl.

## <a name="additional-references"></a>Weitere Verweise

-   [Dynamic Host Configuration-Protokoll (DHCP)](./dhcp-top.md)