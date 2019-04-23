---
title: Set-TransportServer Unterbefehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7863225c-f4b2-4cd0-b929-78a454bef249
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d144ed7d461cbebcd351aa4347fde20f35736c26
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886601"
---
# <a name="subcommand-set-transportserver"></a>Subcommand: set-TransportServer

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Konfigurationseinstellungen für einen Transport-Server festgelegt.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Set-TransportServer [/Server:<Server name>]
     [/ObtainIpv4From:{Dhcp | Range}]
        [/start:<starting IP address>]
        [/End:<Ending IP address>]
     [/ObtainIpv6From:Range]\n\
        [/start:<start IP address>]\n\
        [/End:<End IP address>]      
     [/startPort:<starting port>
        [/EndPort:<starting port>
     [/Profile:{10Mbps | 100Mbps | 1Gbps | Custom}]    
     [/MulticastSessionPolicy]
             [/Policy:{None | AutoDisconnect | Multistream}]
                 [/Threshold:<Speed in KBps>]
                 [/StreamCount:{2 | 3}]
                 [/Fallback:{Yes | No}]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Transport-Servers. Dies kann den NetBIOS-Namen oder den vollständig qualifizierten Domänennamen (FQDN) sein. Wenn kein Transport-Server-Name angegeben ist, wird der lokale Server verwendet.|
|[/ObtainIpv4From:{Dhcp &#124; Range}]|Die Quelle der IPv4-Adressen festgelegt wie folgt:<br /><br />-[/ start: <IP address>] legt den Anfang des IP-Adressbereichs. Dies ist erforderlich, und legen Sie nur gültig, wenn diese Option auf **Bereich**.<br />-[/ End: <IP address>] legt das Ende des IP-Adressbereichs. Dies ist erforderlich, und legen Sie nur gültig, wenn diese Option auf **Bereich**.<br />-[/ Startport-Wert: <port>] legt den Anfang der Portbereich.<br />-[/ Endport-Wert: <port>] legt das Ende der Portbereich.|
|[/ObtainIpv6From:Range]|Gibt die Quelle der IPv6-Adressen. Diese Option gilt nur für Windows Server 2008 R2 und die einzige unterstützte Wert ist **Bereich**.<br /><br />-[/ start: <IP address>] legt den Anfang des IP-Adressbereichs. Dies ist erforderlich, und legen Sie nur gültig, wenn diese Option auf **Bereich**.<br />-[/ End: <IP address>] legt das Ende des IP-Adressbereichs. Dies ist erforderlich, und legen Sie nur gültig, wenn diese Option auf **Bereich**.<br />-[/ Startport-Wert: <port>] legt den Anfang der Portbereich.<br />-[/ Endport-Wert: <port>] legt das Ende der Portbereich.|
|[/ Profile: {10 Mbit/s &#124; 100 Mbit/s &#124; 1 Gbit/s &#124; benutzerdefinierte}]|Gibt an, das Netzwerkprofil verwendet werden. Diese Option ist nur für Server mit Windows Server 2008 oder Windows Server 2003 verfügbar.|
|[/MulticastSessionPolicy]|Konfiguriert die ODX-Einstellungen für Multicastübertragungen an. Dieser Befehl ist nur für Windows Server 2008 R2 verfügbar.<br /><br />-[/ Policy: {None &#124; automatischen Verbindungsabbruch &#124; Zusatzkopie}] bestimmt, wie die langsamen Clients behandelt. **Keine** bedeutet, dass alle Clients in einer Sitzung mit derselben Geschwindigkeit zu halten. **Automatischen Verbindungsabbruch** bedeutet, dass alle Clients, die unter dem angegebenen fällt **/Threshold** werden getrennt. **Zusatzkopie** bedeutet, dass Clients in mehreren Sitzungen laut getrennt werden **/StreamCount**.<br />-[/ Schwellenwert:<Speed in KBps>] legt die minimale Übertragungsrate in Kbit/s für **/Policy:AutoDisconnect**. Clients, die unter dieser Wert fällt, werden von Multicastübertragungen getrennt.<br />-[/ StreamCount: {2 &#124; 3}] [/ Fallback: {Yes &#124; No}] bestimmt die Anzahl der Sitzungen für **/Policy:Multistream**. **2** bedeutet, dass zwei Sitzungen (schnellen und langsamen) und **3** bedeutet, dass drei Sitzungen (Fast "langsam," Mittel ",").<br />-[/ Fallback: {Yes &#124; No}] bestimmt, ob Clients Tha sind getrennt bleiben die Übertragung mithilfe von einer anderen Methode (wenn vom Client unterstützt). Wenn Sie den WDS-Clients verwenden, wird der Computer auf Unicasting zurückgreifen. Einen Fallbackmechanismus unterstützt Wdsmcast.exe nicht. Diese Option gilt auch für Clients, die nicht unterstützen **Zusatzkopie**. In diesem Fall wird der Computer auf eine andere Methode anstelle der Wechsel zu einer langsameren übertragungssitzung zurückgreifen.|
## <a name="BKMK_examples"></a>Beispiele für
Um die IPv4-Adressbereich für den Server festzulegen, geben Sie Folgendes ein:
```
wdsutil /Set-TransportServer /ObtainIpv4From:Range /start:239.0.0.1 /End:239.0.0.100
```
Um die IPv4-Adressbereich, Portbereich und Profil für den Server festzulegen, geben Sie Folgendes ein:
```
wdsutil /Set-TransportServer /Server:MyWDSServer /ObtainIpv4From:Range /start:239.0.0.1 /End:239.0.0.100 /startPort:12000 /EndPort:50000 /Profile:10mbps
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Disable-TransportServer-Befehl](using-the-disable-transportserver-command.md)
[mithilfe des Befehls Enable-TransportServer](using-the-enable-transportserver-command.md) 
 [ Mit dem Befehl Get-TransportServer](using-the-get-transportserver-command.md)
[Unterbefehl: Start-TransportServer](subcommand-start-transportserver.md)
[Unterbefehl: Stop-TransportServer](subcommand-stop-transportserver.md)
