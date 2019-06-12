---
title: netstat
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: c06684eb73639e7480b5bad39d4d679739682800
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437157"
---
# <a name="netstat"></a>netstat

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt die aktive TCP-Verbindungen, Ports, die auf dem der Computer überwacht, Ethernet-Statistiken, die IP-Routingtabelle, IPv4-Statistiken (für die IP-, ICMP, TCP und UDP-Protokolle) und IPv6-Statistiken (für IPv6, ICMPv6, TCP über IPv6 und UDP über IPv6-Protokolle) ist. Ohne Parameter verwendet **Netstat** aktive TCP-Verbindungen angezeigt. 

## <a name="syntax"></a>Syntax
```
netstat [-a] [-e] [-n] [-o] [-p <Protocol>] [-r] [-s] [<Interval>]
```

### <a name="parameters"></a>Parameter

|   Parameter   |                                                                                                                                              Beschreibung                                                                                                                                              |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      -a       |                                                                                                   Zeigt alle aktiven TCP-Verbindungen und die TCP- und UDP-Ports, die der Computer überwacht wird.                                                                                                   |
|      -e       |                                                                                 Zeigt die Ethernet-Statistiken, z. B. die Anzahl der Bytes und versandter und erhaltener Pakete. Dieser Parameter kann mit kombiniert werden **-s**.                                                                                  |
|      -n       |                                                                               Zeigt bei der aktive TCP-Verbindungen, jedoch Adressen und Portnummern numerisch ausgedrückt werden und wird kein Versuch unternommen, um Namen zu bestimmen.                                                                               |
|      -o       |                          Zeigt die aktiven TCP-Verbindungen an, und die Prozess-ID (PID) für jede Verbindung enthält. Sie finden die Anwendung basierend auf der PID auf der Registerkarte "Prozesse" im Windows Task-Manager. Dieser Parameter kann mit kombiniert werden **– ein**, **- n**, und **-p**.                           |
| -p <Protocol> |               Zeigt die Verbindungen für das Protokoll gemäß *Protokoll*. In diesem Fall die *Protokoll* Tcp, Udp, tcpv6 oder udpv6 werden können. Wenn dieser Parameter verwendet wird, mit **-s** anzuzeigenden Statistiken vom Netzwerkprotokoll *Protokoll* kann sein, Tcp, Udp, Icmp, Ip, tcpv6, udpv6, icmpv6 oder ipv6.                |
|      -s       | Zeigt Statistiken vom Protokoll an. Standardmäßig werden Statistiken für die TCP, UDP, ICMP- und IP-Protokolle angezeigt. Wenn das IPv6-Protokoll installiert ist, werden Statistiken für TCP über IPv6, UDP über IPv6, ICMPv6 und IPv6-Protokolle angezeigt. Die **-p** Parameter kann verwendet werden, um eine Reihe von Protokollen angeben. |
|      -r       |                                                                                                     Zeigt den Inhalt der IP-Routingtabelle. Dies ist gleichbedeutend mit dem Befehl Route print.                                                                                                     |
|  <Interval>   |                                                        Zeigt den ausgewählten Informationen jede *Intervall* Sekunden. Drücken Sie STRG + C zum Beenden der erneuten Anzeige aus. Wenn dieser Parameter ausgelassen wird, **Netstat** den ausgewählten Informationen nur einmal ausgegeben.                                                         |
|      /?       |                                                                                                                                 Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                  |

## <a name="remarks"></a>Hinweise
-   Mit diesem Befehl verwendeten Parameter müssen das Präfix mit einem Bindestrich ( **-** ) anstatt einem Schrägstrich ( **/** ).
-   **Netstat** stellt Statistiken für Folgendes bereit:
    -   Proto den Namen des Protokolls (TCP oder UDP).
    -   Lokale Adresse die IP-Adresse, von dem lokalen Computer und die Portnummer, die verwendet wird. Der Name des lokalen Computers, der die IP-Adresse entspricht und den Namen des Ports werden angezeigt, es sei denn, die **- n** Parameter angegeben ist. Wenn Sie noch nicht der Port bekannt ist, wird die Portnummer als ein Sternchen (*) angezeigt.
    -   fremde Adresse die IP-Adresse und Anschlussnummer Anzahl des Remotecomputers auf die der Socket verbunden ist. Die Namen, der die IP-Adresse und den Port entspricht werden angezeigt, es sei denn, die **- n** Parameter angegeben ist. Wenn Sie noch nicht der Port bekannt ist, wird die Portnummer als ein Sternchen (*) angezeigt.
    -   (Status) Gibt den Status einer TCP-Verbindung. Die möglichen Statuswerte sind wie folgt aus: CLOSE_WAIT wechselt geschlossen hergestellt FIN_WAIT_1 FIN_WAIT_2 LAST_ACK Lauschen SYN_RECEIVED SYN_SEND TimeD_WAIT für Weitere Informationen zu den Status einer TCP-Verbindung finden Sie in Rfc 793.
-   Dieser Befehl ist nur verfügbar, wenn das Internetprotokoll (TCP/IP)-Protokoll als Komponente in den Eigenschaften eines Netzwerkadapters in den Netzwerkverbindungen installiert ist.

## <a name="BKMK_Examples"></a>Beispiele für
Um sowohl die Ethernet-Statistiken und die Statistiken für alle Protokolle anzuzeigen, geben Sie Folgendes ein:
```
netstat -e -s
```
Um die Statistiken für nur das TCP- und UDP-Protokolle anzuzeigen, geben Sie Folgendes ein:
```
netstat -s -p tcp udp
```
Um die aktiven TCP-Verbindungen und die Prozess-IDs alle 5 Sekunden anzuzeigen, geben Sie Folgendes ein:
```
netstat -o 5
```
Zum Anzeigen von aktiven TCP-Verbindungen und den Prozess IDs, die numerische Format, geben:
```
netstat -n -o
```

## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
