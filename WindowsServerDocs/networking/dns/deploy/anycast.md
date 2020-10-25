---
title: Übersicht über Anycast-DNS
description: Dieses Thema enthält eine kurze Übersicht über Anycast-DNS.
ms.topic: article
ms.assetid: f9c313ac-bb86-4e48-b9b9-de5004393e06
ms.author: greglin
author: greg-lindsay
ms.openlocfilehash: 0944b8a825d10dc1338a698d511af27b8502f776
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524855"
---
# <a name="anycast-dns-overview"></a>Übersicht über Anycast-DNS

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2019

Dieses Thema enthält Informationen zur Funktionsweise von Anycast-DNS.

## <a name="what-is-anycast"></a>Was ist Anycast?

Anycast ist eine Technologie, die mehrere Routing Pfade zu einer Gruppe von Endpunkten bereitstellt, denen jeweils dieselbe IP-Adresse zugewiesen ist. Jedes Gerät in der Gruppe gibt die gleiche Adresse in einem Netzwerk an, und Routing Protokolle werden verwendet, um auszuwählen, welches Ziel das beste ist.

Anycast ermöglicht Ihnen das Skalieren eines Zustands losen Dienstanbieter (z. b. DNS oder http), indem mehrere Knoten hinter derselben IP-Adresse platziert werden und das gleichwertige Multipfad-Routing (ECMP) zum Weiterleiten des Datenverkehrs zwischen diesen Knoten verwendet wird. Anycast unterscheidet sich von Unicast, bei dem jeder Endpunkt über eine eigene, separate IP-Adresse verfügt.

## <a name="why-use-anycast-with-dns"></a>Gründe für die Verwendung von Anycast mit DNS

Mit Anycast DNS können Sie einen DNS-Server oder eine Gruppe von Servern aktivieren, um auf DNS-Abfragen basierend auf dem geografischen Standort eines DNS-Clients zu antworten. Dies kann die DNS-Antwortzeit verbessern und die DNS-Client Einstellungen vereinfachen. Anycast-DNS bietet auch eine zusätzliche Redundanz Ebene und hilft beim Schutz vor DNS-Denial-of-Service-Angriffen.

### <a name="how-anycast-dns-works"></a>Funktionsweise von Anycast-DNS

Anycast-DNS funktioniert mithilfe von Routing Protokollen wie Border Gateway Protocol (BGP), um DNS-Abfragen an einen bevorzugten DNS-Server oder eine Gruppe von DNS-Servern (z. b. eine Gruppe von DNS-Servern, die von einem Load Balancer verwaltet werden) zu senden. Dadurch kann die DNS-Kommunikation optimiert werden, indem DNS-Antworten von einem DNS-Server erhalten werden, der dem Client am nächsten ist.

Bei Anycast wird für Server, die an mehreren geografischen Standorten vorhanden sind, jeweils eine einzelne, identische IP-Adresse für Ihr lokales Gateway (Router) angekündigt. Wenn ein DNS-Client eine Abfrage an die Anycast-Adresse initiiert, werden die verfügbaren Routen ausgewertet, und die DNS-Abfrage wird an den bevorzugten Speicherort gesendet. Im Allgemeinen ist dies der nächstgelegene Speicherort auf der Grundlage der Netzwerktopologie. Siehe folgendes Beispiel.

![Vier DNS-Server, die sich an unterschiedlichen Standorten befinden, geben dieselbe Anycast-IP-Adresse für das Netzwerk an.](../../media/Anycast/anycast.png)

**Abbildung 1**: bei vier DNS-Servern, die sich an verschiedenen Standorten in einem Netzwerk befinden, wird jeweils dieselbe Anycast-IP-Adresse (Schwarze Pfeile) für das Netzwerk angekündigt. Ein DNS-Client Gerät sendet eine Anforderung an die Anycast-IP-Adresse. Netzwerkgeräte analysieren die verfügbaren Routen und senden die DNS-Abfrage des Clients an den nächstgelegenen Speicherort (blauer Pfeil).

Anycast-DNS wird heutzutage häufig zum Weiterleiten von DNS-Datenverkehr für viele globale DNS-Dienste verwendet. Beispielsweise hängt das Stamm-DNS-Server System stark von Anycast-DNS ab. Anycast funktioniert auch mit einer Vielzahl von Routing Protokollen und kann ausschließlich in Intranets verwendet werden.

## <a name="windows-server-native-bgp-anycast-demo"></a>Demo zu Windows Server Native BGP Anycast

Das folgende Verfahren veranschaulicht, wie System eigenes BGP unter Windows Server mit Anycast-DNS verwendet werden kann.

### <a name="requirements"></a>Requirements (Anforderungen)

- Ein physisches Gerät, auf dem die Hyper-V-Rolle installiert ist.
  - Windows Server 2012 R2, Windows 10 oder höher.
- 2 Client-VMS (beliebige Betriebssysteme)
  - Die Installation von Bindungs Tools für DNS wie z. b. "Dig" wird empfohlen.
- 3 Server-VMS (Windows Server 2016 oder Windows Server 2019).
  - Wenn das Windows PowerShell-loopbackadaptermodul nicht bereits auf Server-VMS installiert ist (DC001, DC002), ist der Internet Zugriff vorübergehend erforderlich, um dieses Modul zu installieren.

### <a name="hyper-v-setup"></a>Hyper-V-Setup

Konfigurieren Sie den Hyper-V-Server wie folgt:

- 2 private virtuelle switchnetzwerke werden konfiguriert.
  - Ein Mock Internet Network 131.253.1.0/24
  - Ein Mock-Intranet-Netzwerk "10.10.10.0/24
- 2 Client-VMS werden an das 131.253.1.0/24-Netzwerk angefügt.
- 2 Server-VMS werden an das "10.10.10.0/24-Netzwerk angefügt.
- 1 der Server ist doppelt vernetzt und an die Netzwerke 131.253.1.0/24 und "10.10.10.0/24 angefügt.

### <a name="virtual-machine-network-configuration"></a>Netzwerkkonfiguration des virtuellen Computers

Konfigurieren Sie die Netzwerkeinstellungen auf virtuellen Computern mit den folgenden Einstellungen:

1.  CLIENT1, client2
  - CLIENT1:131.253.1.1
  - CLIENT2:131.253.1.2
  - Subnetzmaske: 255.255.255.0
  - DNS: 51.51.51.51
  - Gateway: 131.253.1.254
2.  Gateway (Windows Server)
  - NIC1:131.253.1.254, Subnetz 255.255.255.0
  - NIC2:10.10.10.254, Subnetz 255.255.255.0
  - DNS: 51.51.51.51
  - Gateway: 131.253.1.100 (kann bei der Demo ignoriert werden)
3.  DC001 (Windows Server)
  - NIC1:10.10.10.1
  - Subnetz: 255.255.255.0
  - DNS: 10.10.10.1
  - Gateway: 10.10.10.254
4.  DC002 (Windows Server)
  - NIC1:10.10.10.2
  - Subnetz 255.255.255.0
  - DNS: 10.10.10.2 *
  - Gateway: 10.10.10.254

   * Verwenden Sie 10.10.10.1 für DNS anfänglich, wenn Sie einen Domänen Beitritt für DC002 durchführen, damit Sie die Active Directory Domäne auf DC001 suchen können.

### <a name="configure-dns"></a>Konfigurieren des DNS

Verwenden Sie Server-Manager und die DNS-Verwaltungskonsole oder Windows PowerShell, um die folgenden Server Rollen zu installieren und auf jedem der beiden Server eine statische DNS-Zone zu erstellen.

1.  DC001, DC002
  - Installieren von Active Directory Domain Services und herauf Stufen zum Domänen Controller (optional)
  - Installieren der DNS-Rolle (erforderlich)
  - Erstellen Sie eine statische Zone (Non-AD Integrated) namens **Zone. TST** sowohl für DC001 als auch für DC002
    - Fügen Sie den einzelnen statischen Daten Satz Namen **Server** in der Zone vom Typ "txt" hinzu.
    - Daten (Text) für den TXT-Datensatz auf DC001 = **DC001**
    - Daten (Text) für den TXT-Datensatz auf DC002 = **DC002**

### <a name="configure-loopback-adapters"></a>Konfigurieren von Loopback Adaptern

Geben Sie die folgenden Befehle an einer Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten auf DC001 und DC002 ein, um Loopback Adapter zu konfigurieren.

> [!NOTE]
> Der **Install-Module-** Befehl erfordert Internet Zugriff. Dies kann erfolgen, indem die VM vorübergehend einem externen Netzwerk in Hyper-V zugewiesen wird.

```PowerShell
$primary_interface = (Get-NetAdapter |?{$_.Status -eq "Up" -and !$_.Virtual}).Name
$loopback_ipv4 = '51.51.51.51'
$loopback_ipv4_length = '32'
$loopback_name = 'Loopback'
Install-Module -Name LoopbackAdapter -MinimumVersion 1.2.0.0 -Force
Import-Module -Name LoopbackAdapter
New-LoopbackAdapter -Name $loopback_name -Force
$interface_loopback = Get-NetAdapter -Name $loopback_name
$interface_main = Get-NetAdapter -Name $primary_interface
Set-NetIPInterface -InterfaceIndex $interface_loopback.ifIndex -InterfaceMetric "254" -WeakHostReceive Enabled -WeakHostSend Enabled -DHCP Disabled
Set-NetIPInterface -InterfaceIndex $interface_main.ifIndex -WeakHostReceive Enabled -WeakHostSend Enabled
Set-NetIPAddress -InterfaceIndex $interface_loopback.ifIndex -SkipAsSource $True
Get-NetAdapter $loopback_name | Set-DNSClient –RegisterThisConnectionsAddress $False
New-NetIPAddress -InterfaceAlias $loopback_name -IPAddress $loopback_ipv4 -PrefixLength $loopback_ipv4_length -AddressFamily ipv4
Disable-NetAdapterBinding -Name $loopback_name -ComponentID ms_msclient
Disable-NetAdapterBinding -Name $loopback_name -ComponentID ms_pacer
Disable-NetAdapterBinding -Name $loopback_name -ComponentID ms_server
Disable-NetAdapterBinding -Name $loopback_name -ComponentID ms_lltdio
Disable-NetAdapterBinding -Name $loopback_name -ComponentID ms_rspndr
```

### <a name="virtual-machine-routing-configuration"></a>Routing Konfiguration für virtuelle Maschinen

Verwenden Sie die folgenden Windows PowerShell-Befehle auf VMS, um das Routing zu konfigurieren.

1.  Gateway
```PowerShell
Install-WindowsFeature RemoteAccess -IncludeManagementTools
Install-RemoteAccess -VpnType RoutingOnly
Add-BgpRouter -BgpIdentifier “10.10.10.254” -LocalASN 8075
Add-BgpPeer -Name "DC001" -LocalIPAddress 10.10.10.254 -PeerIPAddress 10.10.10.1 -PeerASN 65511 –LocalASN 8075
```

2.  DC001
```PowerShell
Install-WindowsFeature RemoteAccess -IncludeManagementTools
Install-RemoteAccess -VpnType RoutingOnly
Add-BgpRouter -BgpIdentifier “10.10.10.1” -LocalASN 65511
Add-BgpPeer -Name "Labgw" -LocalIPAddress 10.10.10.1 -PeerIPAddress 10.10.10.254 -PeerASN 8075 –LocalASN 65511
Add-BgpCustomRoute -Network 51.51.51.0/24
```

3.  DC002
```PowerShell
Install-WindowsFeature RemoteAccess -IncludeManagementTools
Install-RemoteAccess -VpnType RoutingOnly
Add-BgpRouter -BgpIdentifier "10.10.10.2" -LocalASN 65511
Add-BgpPeer -Name "Labgw" -LocalIPAddress 10.10.10.2 -PeerIPAddress 10.10.10.254 -PeerASN 8075 –LocalASN 65511
Add-BgpCustomRoute -Network 51.51.51.0/24
```

### <a name="summary-diagram"></a>Zusammenfassungs Diagramm

![Lab-Setup für Native BGP Anycast-DNS-Demo](../../media/Anycast/anycast-lab.png)

**Abbildung 2**: Lab-Setup für Native BGP Anycast-DNS-Demo

## <a name="anycast-dns-demonstration"></a>Anycast-DNS-Demonstration


1.  Überprüfen des BGP-Routing auf dem Gatewayserver

    PS C: \> Get-BgpRouteInformation

    Destinationnetwork nexthop learnedfrompeer State localpref Med<br>
    ------------------ -------    --------------- ----- --------- ---<br>
    51.51.51.0/24 10.10.10.1 DC001 am besten<br>
    51.51.51.0/24 10.10.10.2 DC002 am besten<br>

2.  Überprüfen Sie auf CLIENT1 und CLIENT2, ob Sie erreichbar sind 51.51.51.51

    PS C: \> Ping 51.51.51.51

    Pingen von 51.51.51.51 mit Daten von 32 Bytes:<br>
    Antwort von 51.51.51.51: Bytes = 32 Zeit<1 MS TTL = 126<br>
    Antwort von 51.51.51.51: Bytes = 32 Zeit<1 MS TTL = 126<br>
    Antwort von 51.51.51.51: Bytes = 32 Zeit<1 MS TTL = 126<br>
    Antwort von 51.51.51.51: Bytes = 32 Zeit<1 MS TTL = 126

    Ping Statistics for 51.51.51.51:<br>
    Pakete: gesendet = 4, empfangen = 4, Verlust = 0 (0% Verlust),<br>
    Ungefähre roundtripzeiten in "Milli-seconds":<br>
    Minimal = 0 ms, Maximum = 0 ms, Average = 0 ms

    > [!NOTE]
    > Wenn ping fehlschlägt, prüfen Sie auch, ob keine Firewallregeln vorhanden sind, die ICMP blockieren.

3.  Verwenden Sie auf CLIENT1 und CLIENT2 nslookup oder dig, um den TXT-Datensatz abzufragen. Beispiele für beides sind unten dargestellt.

    PS C: \> dig Server. Zone. TST txt + Short<br>
    PS C: \> nslookup-Type = txt Server. Zone. TST 51.51.51.51

    Ein Client zeigt "DC001" an, und der andere Client zeigt "DC002" an, um zu überprüfen, ob Anycast ordnungsgemäß funktioniert.  Sie können auch vom Gatewayserver Abfragen.

4.  Deaktivieren Sie als nächstes den Ethernet-Adapter auf DC001.

    PS C: \> (Get-netadapter). Benennen<br>
    Loopback<br>
    Ethernet 2<br>
    PS C: \> Disable-NetAdapter "Ethernet 2"<br>
    Bestätigen<br>
    Möchten Sie diese Aktion wirklich ausführen?<br>
    Disable-NetAdapter ' Ethernet 2 '<br>
    [J] Ja [A] Ja, alle [N] Nein [L] Nein für alle [S] Suspend [?] Hilfe (Standard ist "Y"):<br>
    PS C: \> (Get-netadapter). Stands<br>
    Nach oben<br>
    Disabled

5.  Vergewissern Sie sich, dass DNS-Clients, die zuvor Antworten von DC001 erhalten haben, zu DC002 gewechselt haben.

    PS C: \> nslookup-Type = txt Server. Zone. TST 51.51.51.51<br>
    Server: unbekannt<br>
    Adresse: 51.51.51.51<br>

    Server. Zone. TST Text =

    "DC001"<br>
    PS C: \> nslookup-Type = txt Server. Zone. TST 51.51.51.51<br>
    Server: unbekannt<br>
    Adresse: 51.51.51.51<br>

    Server. Zone. TST Text =

    "DC002"

6.  Vergewissern Sie sich, dass die BGP-Sitzung auf DC001 mit Get-BgpStatistics auf dem Gatewayserver herunter ist.
7.  Aktivieren Sie den Ethernet-Adapter erneut auf DC001, und vergewissern Sie sich, dass die BGP-Sitzung wieder hergestellt wird und Clients DNS-Antworten von DC001 erneut erhalten.

> [!NOTE]
> Wenn ein Load Balancer nicht verwendet wird, verwendet ein einzelner Client den gleichen Back-End-DNS-Server, sofern dieser verfügbar ist. Dadurch wird ein einheitlicher BGP-Pfad für den Client erstellt. Weitere Informationen finden Sie im Abschnitt 4.4.3 of RFC4786: [EQUAL-Cost Path](https://tools.ietf.org/html/rfc4786#page-10).

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

F: ist eine gute Lösung für die Verwendung in einer lokalen DNS-Umgebung eine gute Lösung.<br>
A: Anycast-DNS funktioniert nahtlos mit einem lokalen DNS-Dienst. Allerdings ist Anycast nicht *erforderlich* , damit der DNS-Dienst skaliert werden kann.

F: welche Auswirkungen hat die Implementierung von Anycast-DNS in einer Umgebung mit einer großen Zahl (z. >50) von Domänen Controllern? <br>
A: Es gibt keine direkten Auswirkungen auf die Funktionalität. Wenn ein Lasten Ausgleichs Modul verwendet wird, ist keine zusätzliche Konfiguration auf Domänen Controllern erforderlich.

F: ist eine vom Microsoft-Kundendienst unterstützte-DNS-Konfiguration.<br>
A: Wenn Sie einen Load Balancer ohne Microsoft zum Weiterleiten von DNS-Abfragen verwenden, unterstützt Microsoft Probleme im Zusammenhang mit dem DNS-Server Dienst. Wenden Sie sich bei Problemen im Zusammenhang mit der DNS-Weiterleitung an den Lasten Ausgleichs Anbieter

F: Was ist das bewährte Verfahren für Anycast-DNS mit einer großen Zahl (z. >50) von Domänen Controllern?<br>
A: die bewährte Vorgehensweise besteht darin, einen Load Balancer an jedem geografischen Standort zu verwenden. Lasten Ausgleichs Module werden in der Regel von einem externen Anbieter bereitgestellt.

F: haben Anycast-DNS und Azure DNS ähnliche Funktionen?<br>
A: Azure DNS verwendet Anycast. Um Anycast mit Azure DNS zu verwenden, konfigurieren Sie den Load Balancer so, dass Anforderungen an den Azure DNS Server weiterleiten.