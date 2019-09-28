---
title: Unterbefehls Satz-Transportserver
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: f91cca044d4c2922791ccb63b0e3cec4af685f17
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370741"
---
# <a name="subcommand-set-transportserver"></a>Unterbefehl: Set-TransportServer

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt Konfigurationseinstellungen für einen Transport Server fest.
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
|[/Server:<Server name>]|Gibt den Namen des Transport Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Transport Servername angegeben ist, wird der lokale Server verwendet.|
|[/ObtainIpv4From: {DHCP &#124; Range}]|Legt die Quelle der IPv4-Adressen wie folgt fest:<br /><br />-[/Start: <IP address>] legt den Anfang des IP-Adress Bereichs fest. Dies ist nur erforderlich und gültig, wenn diese Option auf **Bereich**festgelegt ist.<br />-[/End: <IP address>] legt das Ende des IP-Adress Bereichs fest. Dies ist nur erforderlich und gültig, wenn diese Option auf **Bereich**festgelegt ist.<br />-[/startPort: <port>] legt den Anfang des Port Bereichs fest.<br />-[/EndPort: <port>] legt das Ende des Port Bereichs fest.|
|[/ObtainIpv6From: Bereich]|Gibt die Quelle von IPv6-Adressen an. Diese Option gilt nur für Windows Server 2008 R2, und der einzige unterstützte Wert ist **Range**.<br /><br />-[/Start: <IP address>] legt den Anfang des IP-Adress Bereichs fest. Dies ist nur erforderlich und gültig, wenn diese Option auf **Bereich**festgelegt ist.<br />-[/End: <IP address>] legt das Ende des IP-Adress Bereichs fest. Dies ist nur erforderlich und gültig, wenn diese Option auf **Bereich**festgelegt ist.<br />-[/startPort: <port>] legt den Anfang des Port Bereichs fest.<br />-[/EndPort: <port>] legt das Ende des Port Bereichs fest.|
|[/Profile: {10 Mbit &#124; /s &#124; 100 Mbit/ &#124; s 1 Gbit/s Custom}]|Gibt das zu verwendende Netzwerk Profil an. Diese Option ist nur für Server verfügbar, auf denen Windows Server 2008 oder Windows Server 2003 ausgeführt wird.|
|[/MulticastSessionPolicy]|Konfiguriert die Übertragungs Einstellungen für Multicast Übertragungen. Dieser Befehl ist nur für Windows Server 2008 R2 verfügbar.<br /><br />-[/Policy: {None &#124; Autodisconnect &#124; Multistream}] bestimmt, wie langsame Clients behandelt werden. " **None** " bedeutet, dass alle Clients in einer Sitzung mit derselben Geschwindigkeit aufbewahrt werden. **Autodisconnect** bedeutet, dass alle Clients, die unter den angegebenen **/Threshold** ablegen, getrennt werden. **Multistream** bedeutet, dass Clients in mehrere Sitzungen unterteilt werden, wie von **/StreamCount**angegeben.<br />-[/Threshold: <Speed in KBps>] legt die minimale Übertragungsrate in Kbit/s für **/Policy: Autodisconnect**fest. Clients, die diese Rate unterhalb dieses Satzes ablegen, werden von Multicast Übertragungen getrennt.<br />-[/StreamCount: {2 &#124; 3}] [/Fallback: {Yes &#124; No}] legt die Anzahl von Sitzungen für **/Policy: Multistream**fest. **2** bedeutet zwei Sitzungen (schnell und langsam) und **3** drei Sitzungen (langsam, Mittel, schnell).<br />-[/Fallback: {Yes &#124; No}] legt fest, ob Clients, die getrennt werden, die Übertragung mit einer anderen Methode (sofern vom Client unterstützt) fortgesetzt wird. Wenn Sie den WDS-Client verwenden, wird für den Computer ein Fallback auf Unicasting durchlaufen. Wdsmcast. exe unterstützt keinen Fall Back Mechanismus. Diese Option gilt auch für Clients, die **Multistream**nicht unterstützen. In diesem Fall wird der Computer auf eine andere Methode zurückgreifen, anstatt zu einer langsameren Übertragungs Sitzung zu wechseln.|
## <a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um den IPv4-Adressbereich für den Server festzulegen:
```
wdsutil /Set-TransportServer /ObtainIpv4From:Range /start:239.0.0.1 /End:239.0.0.100
```
Geben Sie Folgendes ein, um den IPv4-Adressbereich, den Port Bereich und das Profil für den Server festzulegen:
```
wdsutil /Set-TransportServer /Server:MyWDSServer /ObtainIpv4From:Range /start:239.0.0.1 /End:239.0.0.100 /startPort:12000 /EndPort:50000 /Profile:10mbps
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mit dem Befehl "deaktivierte Transportserver](using-the-disable-transportserver-command.md)" 
 mit dem Befehl "[enable-Transportserver](using-the-enable-transportserver-command.md)" 
 mit dem Befehl "[Get-](using-the-get-transportserver-command.md)Transportserver" 
[Unterbefehl: Start-TransportServer](subcommand-start-transportserver.md)
-[Unterbefehl: "stoppt-Transportserver](subcommand-stop-transportserver.md) "
