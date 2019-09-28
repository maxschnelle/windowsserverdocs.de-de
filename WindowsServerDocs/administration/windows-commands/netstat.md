---
title: netstat
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60e2718f-93cc-4ceb-bf0e-58a6a6e4fc8b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 54bd21b7e96275d329e45e825971d9236488c793
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373263"
---
# <a name="netstat"></a>netstat

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt aktive TCP-Verbindungen, Ports an, die der Computer überwacht, Ethernet-Statistiken, die IP-Routing Tabelle, IPv4-Statistiken (für die IP-, ICMP-, TCP-und UDP-Protokolle) und IPv6-Statistiken (für IPv6, ICMPv6, TCP über IPv6 und UDP über IPv6-Protokolle). Wird ohne Parameter verwendet, zeigt **netstat** aktive TCP-Verbindungen an. 

## <a name="syntax"></a>Syntax
```
netstat [-a] [-e] [-n] [-o] [-p <Protocol>] [-r] [-s] [<Interval>]
```

### <a name="parameters"></a>Parameter

|   Parameter   |                                                                                                                                              Beschreibung                                                                                                                                              |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      -a       |                                                                                                   Zeigt alle aktiven TCP-Verbindungen und die TCP-und UDP-Ports an, die der Computer abhört.                                                                                                   |
|      -e       |                                                                                 Zeigt Ethernet-Statistiken an, z. b. die Anzahl der gesendeten und empfangenen Bytes. Dieser Parameter kann mit **-s**kombiniert werden.                                                                                  |
|      -n       |                                                                               Zeigt aktive TCP-Verbindungen an. Adressen und Portnummern werden jedoch numerisch ausgedrückt, und es wird kein Versuch unternommen, Namen zu ermitteln.                                                                               |
|      -o       |                          Zeigt aktive TCP-Verbindungen an und schließt die Prozess-ID (PID) für jede Verbindung ein. Sie finden die Anwendung auf der Grundlage der PID auf der Registerkarte "Prozesse" im Windows Task-Manager. Dieser Parameter kann mit **-a**, **-n**und **-p**kombiniert werden.                           |
| -p <Protocol> |               Zeigt Verbindungen für das Protokoll an, das durch das *Protokoll*angegeben wird. In diesem Fall kann das *Protokoll* TCP, UDP, TCPv6 oder UDPv6 sein. Wenn dieser Parameter mit **-s** verwendet wird, um Statistiken nach Protokoll anzuzeigen, kann das *Protokoll* TCP, UDP, ICMP, IP, TCPv6, UDPv6, ICMPv6 oder IPv6 sein.                |
|      -s       | Zeigt Statistiken nach Protokoll an. Standardmäßig werden Statistiken für die Protokolle TCP, UDP, ICMP und IP angezeigt. Wenn das IPv6-Protokoll installiert ist, werden Statistiken für die Protokolle TCP Over IPv6, UDP Over IPv6, ICMPv6 und IPv6 angezeigt. Der **-p-** Parameter kann verwendet werden, um einen Satz von Protokollen anzugeben. |
|      -r       |                                                                                                     Zeigt den Inhalt der IP-Routing Tabelle an. Dies entspricht dem Befehl route print.                                                                                                     |
|  <Interval>   |                                                        Zeigt die ausgewählten Informationen jedes *Intervall* in Sekunden neu an. Drücken Sie STRG + C, um die erneute Anzeige zu verhindern. Wenn dieser Parameter ausgelassen wird, druckt **netstat** die ausgewählten Informationen nur einmal.                                                         |
|      /?       |                                                                                                                                 Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                  |

## <a name="remarks"></a>Hinweise
-   Den mit diesem Befehl verwendeten Parametern muss ein Bindestrich ( **-** ) anstelle eines Schrägstrichs ( **/** ) vorangestellt werden.
-   **netstat** bietet Statistiken für Folgendes:
    -   Proto der Name des Protokolls (TCP oder UDP).
    -   Lokale Adresse die IP-Adresse des lokalen Computers und die verwendete Portnummer. Der Name des lokalen Computers, der der IP-Adresse und dem Namen des Ports entspricht, wird angezeigt, es sei denn, der Parameter " **-n** " wird angegeben. Wenn der Port noch nicht festgelegt ist, wird die Portnummer als Sternchen (*) angezeigt.
    -   fremd Adresse die IP-Adresse und die Portnummer des Remote Computers, mit dem der Socket verbunden ist. Die Namen, die der IP-Adresse und dem Port entsprechen, werden angezeigt, es sei denn, der **-n-** Parameter wird angegeben. Wenn der Port noch nicht festgelegt ist, wird die Portnummer als Sternchen (*) angezeigt.
    -   Land Gibt den Status einer TCP-Verbindung an. Folgende Zustände sind möglich: CLOSE_WAIT Closed festgelegt FIN_WAIT_1 FIN_WAIT_2 LAST_ACK Listener SYN_RECEIVED SYN_SEND timeD_WAIT Weitere Informationen zu den Zuständen einer TCP-Verbindung finden Sie unter RFC 793.
-   Dieser Befehl ist nur verfügbar, wenn das TCP/IP-Protokoll (Internet Protocol) als Komponente in den Eigenschaften eines Netzwerkadapters in Netzwerkverbindungen installiert ist.

## <a name="BKMK_Examples"></a>Beispiele
Geben Sie Folgendes ein, um sowohl die Ethernet-Statistik als auch die Statistiken für alle Protokolle anzuzeigen:
```
netstat -e -s
```
Geben Sie Folgendes ein, um die Statistiken nur für die TCP-und UDP-Protokolle anzuzeigen:
```
netstat -s -p tcp udp
```
Wenn Sie alle 5 Sekunden aktive TCP-Verbindungen und die Prozess-IDs anzeigen möchten, geben Sie Folgendes ein:
```
netstat -o 5
```
Geben Sie Folgendes ein, um aktive TCP-Verbindungen und die Prozess-IDs in numerischer Form anzuzeigen:
```
netstat -n -o
```

## <a name="additional-references"></a>Weitere Verweise
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
