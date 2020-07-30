---
title: Grundlagen von DHCP (Dynamic Host Configuration-Protokoll)
description: ''
ms.prod: windows-server
manager: dcscontentpm
ms.technology: server-general
ms.date: 5/26/2020
ms.topic: troubleshoot
author: Deland-Han
ms.author: delhan
ms.reviewer: ''
ms.openlocfilehash: 5a3247fad961f4b2d1cf6e354c29706708c8e330
ms.sourcegitcommit: 145cf75f89f4e7460e737861b7407b5cee7c6645
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/29/2020
ms.locfileid: "87409811"
---
# <a name="dhcp-dynamic-host-configuration-protocol-basics"></a>Grundlagen von DHCP (Dynamic Host Configuration-Protokoll)

Das Dynamic Host Configuration-Protokoll (DHCP) ist ein Standardprotokoll, das von RFC 1541 definiert wird (das durch RFC 2131 abgelöst wird), das es einem Server ermöglicht, IP-Adressierungs-und Konfigurationsinformationen dynamisch an Clients zu verteilen. Normalerweise stellt der DHCP-Server dem Client mindestens diese grundlegenden Informationen bereit:

- IP-Adresse

- Subnetzmaske

- Standardmäßige gatewayother-Informationen können auch bereitgestellt werden, z. b. Domain Name Service (DNS)-Serveradressen und WINS-Serveradressen (Windows Internet Name Service). Der Systemadministrator konfiguriert den DHCP-Server mit den Optionen, die auf dem Client analysiert werden.

## <a name="more-information"></a>Weitere Informationen

Die folgenden Microsoft-Produkte stellen DHCP-Client Funktionen bereit:

- Windows NT Server, Version 3,5, 3,51 und 4,0

- Windows NT-Arbeitsstation, Version 3,5, 3,51 und 4,0

- Windows 95

- Microsoft-Netzwerk Client Version 3,0 für MS-DOS

- Microsoft LAN Manager-Client Version 2.2 c für MS-DOS

- Microsoft TCP/IP-32 für Windows für Workgroups, Version 3,11, 3.11 a und 3.11 b

Verschiedene DHCP-Clients unterstützen verschiedene Optionen, die Sie vom DHCP-Server empfangen können.

Die folgenden Microsoft-Server Betriebssysteme stellen DHCP-Serverfunktionen bereit:

- Windows NT Server Version 3,5

- Windows NT Server Version 3,51

- Windows NT Server Version 4,0

Wenn ein Client zum ersten Mal initialisiert wird, nachdem er für den Empfang von DHCP-Informationen konfiguriert wurde, initiiert er eine Konversation mit dem Server.

Im folgenden finden Sie eine Zusammenfassungs Tabelle der Konversation zwischen Client und Server, auf die eine Beschreibung des Prozesses auf Paketebene folgt:

```
Source Dest Source Dest Packet
 MAC addr MAC addr IP addr IP addr Description
 -----------------------------------------------------------------
 Client Broadcast 0.0.0.0 255.255.255.255 DHCP Discover
 DHCPsrvr Broadcast DHCPsrvr 255.255.255.255 DHCP Offer
 Client Broadcast 0.0.0.0 255.255.255.255 DHCP Request
 DHCPsrvr Broadcast DHCPsrvr 255.255.255.255 DHCP ACK
```

Die ausführliche Konversation zwischen DHCP-Client und DHCP-Server sieht wie folgt aus:

### <a name="dhcpdiscover"></a>DHCPDISCOVER

Der Client sendet ein DHCPDISCOVER-Paket. Im folgenden finden Sie einen Auszug aus einer Netzwerkmonitor Erfassung, in der die IP-und DHCP-Teile eines DHCPDISCOVER-Pakets angezeigt werden. Im Abschnitt IP sehen Sie, dass die Zieladresse 255.255.255.255 und die Quelladresse 0.0.0.0 lautet. Der Abschnitt DHCP identifiziert das Paket als Ermittlungs Paket und identifiziert den Client an zwei Stellen mithilfe der physischen Adresse der Netzwerkkarte. Beachten Sie, dass die Werte im Feld chaddr und DHCP: clientbezeichnerfeld identisch sind.

```

IP: ID = 0x0; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 0 (0x0)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x39A6
 IP: Source Address = 0.0.0.0
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Discover (xid=21274A1D)
 DHCP: Op Code (op) = 1 (0x1)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 556223005 (0x21274A1D)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Discover
 DHCP: Client-identifier = (Type: 1) 08 00 2b 2e d8 5e
 DHCP: Host Name = JUMBO-WS
 DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
 DHCP: End of this option field

```

### <a name="dhcpoffer"></a>DHCPOFFER

Der DHCP-Server antwortet, indem er ein DHCPOFFER-Paket sendet. Im Abschnitt IP des nachfolgenden Aufzeichnungs Abschnitts ist die Quelladresse jetzt die IP-Adresse des DHCP-Servers, und die Zieladresse ist die Broadcast Adresse 255.255.255.255. Der Abschnitt DHCP identifiziert das Paket als Angebot. Das Feld "Yiaddr" wird mit der IP-Adresse aufgefüllt, die der Server dem Client anbietet. Beachten Sie, dass das Feld chaddr weiterhin die physische Adresse des anfordernden Clients enthält. Außerdem werden im Feld Abschnitt der DHCP-Option die verschiedenen Optionen angezeigt, die vom Server zusammen mit der IP-Adresse gesendet werden. In diesem Fall sendet der Server die Subnetzmaske, das Standard Gateway (Router), die Lease-Zeit, die WINS-Server Adresse (NetBIOS-Namensdienst) und den NetBIOS-Knotentyp.

```

IP: ID = 0x3C30; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 15408 (0x3C30)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x2FA8
 IP: Source Address = 157.54.48.151
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Offer (xid=21274A1D)
 DHCP: Op Code (op) = 2 (0x2)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 556223005 (0x21274A1D)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 157.54.50.5
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Offer
 DHCP: Subnet Mask = 255.255.240.0
 DHCP: Renewal Time Value (T1) = 8 Days, 0:00:00
 DHCP: Rebinding Time Value (T2) = 14 Days, 0:00:00
 DHCP: IP Address Lease Time = 16 Days, 0:00:00
 DHCP: Server Identifier = 157.54.48.151
 DHCP: Router = 157.54.48.1
 DHCP: NetBIOS Name Service = 157.54.16.154
 DHCP: NetBIOS Node Type = (Length: 1) 04
 DHCP: End of this option field

```

### <a name="dhcprequest"></a>DHCPREQUEST

Der Client antwortet auf den DHCPOFFER, indem er eine DHCPREQUEST sendet. Im IP-Abschnitt der folgenden Erfassung ist die Quelladresse des Clients weiterhin 0.0.0.0, und das Ziel für das Paket ist weiterhin 255.255.255.255. Der Client behält 0.0.0.0 bei, weil der Client die Überprüfung des Servers nicht erhalten hat, dass er mit der Verwendung der angebotenen Adresse zufrieden ist. Das Ziel wird immer noch übertragen, da mehr als ein DHCP-Server möglicherweise geantwortet hat und möglicherweise eine Reservierung für ein Angebot an den Client durchgeführt hat. Auf diese Weise können die anderen DHCP-Server wissen, dass Sie Ihre angebotenen Adressen freigeben und an die verfügbaren Pools zurückgeben können. Der Abschnitt DHCP identifiziert das Paket als Anforderung und überprüft die angebotene Adresse mithilfe des Felds DHCP: angeforderte Adresse. Das Feld DHCP: Server Bezeichner zeigt die IP-Adresse des DHCP-Servers an, der die Lease anbietet.

```

IP: ID = 0x100; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 256 (0x100)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x38A6
 IP: Source Address = 0.0.0.0
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Request (xid=21274A1D)
 DHCP: Op Code (op) = 1 (0x1)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 556223005 (0x21274A1D)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Request
 DHCP: Client-identifier = (Type: 1) 08 00 2b 2e d8 5e
 DHCP: Requested Address = 157.54.50.5
 DHCP: Server Identifier = 157.54.48.151
 DHCP: Host Name = JUMBO-WS
 DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
 DHCP: End of this option field

```

### <a name="dhcpack"></a>DHCPACK

Der DHCP-Server antwortet auf DHCPREQUEST mit einem DHCPACK und schließt somit den Initialisierungs Zyklen ab. Die Quelladresse ist die IP-Adresse des DHCP-Servers, und die Zieladresse lautet weiterhin 255.255.255.255. Das Feld "Yiaddr" enthält die Adresse des Clients, und die Felder "CHADDR" und "DHCP: Client Bezeichner" sind die physische Adresse der Netzwerkkarte im anfordernden Client. Der Abschnitt DHCP-Option identifiziert das Paket als Bestätigung.

```

IP: ID = 0x3D30; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 15664 (0x3D30)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x2EA8
 IP: Source Address = 157.54.48.151
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: ACK (xid=21274A1D)
 DHCP: Op Code (op) = 2 (0x2)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 556223005 (0x21274A1D)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 157.54.50.5
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP ACK
 DHCP: Renewal Time Value (T1) = 8 Days, 0:00:00
 DHCP: Rebinding Time Value (T2) = 14 Days, 0:00:00
 DHCP: IP Address Lease Time = 16 Days, 0:00:00
 DHCP: Server Identifier = 157.54.48.151
 DHCP: Subnet Mask = 255.255.240.0
 DHCP: Router = 157.54.48.1
 DHCP: NetBIOS Name Service = 157.54.16.154
 DHCP: NetBIOS Node Type = (Length: 1) 04
 DHCP: End of this option field

```

Wenn der Client bereits über eine von DHCP zugewiesene IP-Adresse verfügt und neu gestartet wird, fordert der Client die zuvor geleerte IP-Adresse in einem speziellen DHCPREQUEST-Paket an. Die Quelladresse ist 0.0.0.0, und das Ziel ist die Broadcast Adresse 255.255.255.255. Microsoft-Clients füllen das DHCP-Optionsfeld DHCP: angeforderte Adresse mit der zuvor zugewiesenen Adresse auf. Streng RFC-kompatible Clients füllen das ciaddr-Feld mit der angeforderten Adresse auf. Der Microsoft DHCP-Server akzeptiert beide Bedingungen.

```

IP: ID = 0x0; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 0 (0x0)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x39A6
 IP: Source Address = 0.0.0.0
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Request (xid=2757554E)
 DHCP: Op Code (op) = 1 (0x1)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 660034894 (0x2757554E)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Request
 DHCP: Client-identifier = (Type: 1) 08 00 2b 2e d8 5e
 DHCP: Requested Address = 157.54.50.5
 DHCP: Host Name = JUMBO-WS
 DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
 DHCP: End of this option field

```

An diesem Punkt reagiert der Server möglicherweise nicht. Das Verhalten des Windows NT-DHCP-Servers hängt von der Version des verwendeten Betriebssystems sowie von anderen Faktoren wie z. b. der Bereichsauswahl ab. Wenn der Server feststellt, dass der Client die Adresse weiterhin verwenden kann, bleibt er entweder unbeaufsichtigt, oder er kann den DHCPREQUEST-Vorgang übermitteln. Wenn der Server feststellt, dass der Client die Adresse nicht haben kann, sendet er eine Nack.

```

IP: ID = 0x3F1A; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 16154 (0x3F1A)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x2CBE
 IP: Source Address = 157.54.48.151
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: NACK (xid=74A005CE)
 DHCP: Op Code (op) = 2 (0x2)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 1956644302 (0x74A005CE)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP NACK
 DHCP: Server Identifier = 157.54.48.151
 DHCP: End of this option field

```

Der Client startet dann den Ermittlungsprozess, aber das DHCPDISCOVER-Paket versucht trotzdem, dieselbe Adresse zu leasen. In vielen Fällen erhält der TTH-Client dieselbe Adresse, aber dies ist nicht möglich.

```

IP: ID = 0x100; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 256 (0x100)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x38A6
 IP: Source Address = 0.0.0.0
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Discover (xid=3ED14752)
 DHCP: Op Code (op) = 1 (0x1)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 1053902674 (0x3ED14752)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Discover
 DHCP: Client-identifier = (Type: 1) 08 00 2b 2e d8 5e
 DHCP: Requested Address = 157.54.51.5
 DHCP: Host Name = JUMBO-WS
 DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
 DHCP: End of this option field

```

Den DHCP-Informationen, die vom Client von einem DHCP-Server abgerufen werden, wird eine Lease-Zeit zugeordnet. Die leasedzeit definiert, wie lange der Client die mit DHCP zugewiesenen Informationen verwenden kann. Wenn die Lease bestimmte Meilensteine erreicht, versucht der Client, seine DHCP-Informationen zu erneuern.

Verwenden Sie das Hilfsprogramm ipconfig, um IP-Informationen zu einem Windows-oder Windows for Workgroups-Client anzuzeigen. Wenn der Client Windows 95 ist, verwenden Sie winipcfg.

## <a name="references"></a>Referenzen

Weitere Informationen zu DHCP finden Sie unter RFC1541 und RFC2131. RFCs können über das Internet an zahlreichen Standorten abgerufen werden, z. b.: [http://www.rfc-editor.org/](http://www.rfc-editor.org/) und[http://www.tech-nic.qc.ca/](http://www.tech-nic.qc.ca/)
