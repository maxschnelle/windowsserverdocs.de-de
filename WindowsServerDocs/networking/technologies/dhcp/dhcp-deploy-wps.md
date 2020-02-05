---
title: Bereitstellung von DHCP mit Windows PowerShell
description: Sie können dieses Thema verwenden, um einen DHCP-Server mit Windows Server 2016 Internet Protocol (IP), Version 4, bereitzustellen, der automatische IP-Adressen und DHCP-Optionen für IPv4-DHCP-Clients bereitstellt, die mit mindestens einem Subnetz im Netzwerk verbunden sind.
ms.prod: windows-server
ms.technology: networking-dhcp
ms.topic: article
ms.assetid: 7110ad21-a33e-48d5-bb3c-129982913bc8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 16900809c2c6b877d2b5c45f1c3ca26e55c6bea9
ms.sourcegitcommit: 7df2bd3a7d07a50ace86477335ed6fbfb2dac373
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/05/2020
ms.locfileid: "77027945"
---
# <a name="deploy-dhcp-using-windows-powershell"></a>Bereitstellung von DHCP mit Windows PowerShell

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dieses Handbuch enthält Anweisungen zur Verwendung von Windows PowerShell zum Bereitstellen eines IP-Protokolls (IP) Version 4 Dynamic Host Configuration-Protokoll \(DHCP-\) Server, von dem IPv4-DHCP-Clients, die mit einem oder mehreren Subnetzen in Ihrem Netzwerk verbunden sind, automatisch IP-Adressen und DHCP-Optionen zugewiesen werden.

> [!NOTE]
> Informationen zum Herunterladen dieses Dokuments im Word-Format aus der TechNet Gallery finden Sie unter Bereitstellen von [DHCP mithilfe von Windows PowerShell unter Windows Server 2016](https://gallery.technet.microsoft.com/Deploy-DHCP-Using-Windows-246dd293).

Die Verwendung von DHCP-Servern zum Zuweisen von IP-Adressen spart den Verwaltungsaufwand, da Sie die TCP/IP V4-Einstellungen für jeden Netzwerkadapter nicht auf allen Computern in Ihrem Netzwerk manuell konfigurieren müssen. Mit DHCP wird die TCP/IP V4-Konfiguration automatisch ausgeführt, wenn ein Computer oder ein anderer DHCP-Client mit dem Netzwerk verbunden ist.

Sie können den DHCP-Server in einer Arbeitsgruppe als eigenständigen Server oder als Teil einer Active Directory Domäne bereitstellen.

Dieses Handbuch enthält die folgenden Abschnitte:

- [Übersicht](#bkmk_overview)
- [Technologie Übersichten](#bkmk_technologies)
- [DHCP-Bereitstellung planen](#bkmk_plan)
- [Verwenden dieses Handbuchs in einer Test Umgebung](#bkmk_lab)
- [Bereitstellen von DHCP](#bkmk_deploy)
- [Überprüfen der Server Funktionalität](#bkmk_verify)
- [Windows PowerShell-Befehle für DHCP](#bkmk_dhcpwps)
- [Liste der Windows PowerShell-Befehle in diesem Handbuch](#bkmk_list)

## <a name="bkmk_overview"></a>Übersicht

In der folgenden Abbildung ist das Szenario dargestellt, das Sie mit diesem Handbuch bereitstellen können. Das Szenario umfasst einen DHCP-Server in einer Active Directory Domäne. Der Server ist so konfiguriert, dass er IP-Adressen für DHCP-Clients in zwei unterschiedlichen Subnetzen bereitstellt. Die Subnetze werden durch einen Router getrennt, für den die DHCP-Weiterleitung aktiviert ist.

![Übersicht über die DHCP-Netzwerktopologie](../../media/Core-Network-Guide/cng16_overview.jpg)

## <a name="bkmk_technologies"></a>Technologie Übersichten

In den folgenden Abschnitten finden Sie eine kurze Übersicht über DHCP und TCP/IP.

### <a name="dhcp-overview"></a>Übersicht über DHCP

DHCP ist ein IP-Standard für die Vereinfachung der Verwaltung der Host-IP-Konfiguration. Der DHCP-Standard ermöglicht DHCP-Servern die Verwaltung der dynamischen Zuweisung von IP-Adressen und sonstiger zugehöriger Konfigurationsdetails für DHCP-fähige Clients im Netzwerk.

DHCP ermöglicht Ihnen die Verwendung eines DHCP-Servers zum dynamischen Zuweisen einer IP-Adresse zu einem Computer oder einem anderen Gerät (z. b. einem Drucker) im lokalen Netzwerk, anstatt jedes Gerät manuell mit einer statischen IP-Adresse zu konfigurieren.

Jeder Computer in einem TCP/IP-Netzwerk muss über eine eindeutige IP-Adresse verfügen. Zudem muss die zugehörige Subnetzmaske sowohl den Hostcomputer als auch das Subnetz angeben, an das der Computer angeschlossen ist. Durch die Verwendung von DHCP können Sie sicherstellen, dass alle als DHCP-Clients konfigurierten Computer eine für die Netzwerkadresse und das Subnetz geeignete IP-Adresse erhalten. Und durch die Verwendung von DHCP-Optionen wie Standardgateway und DNS-Server können Sie DHCP-Clients automatisch die Informationen bereitstellen, die diese benötigen, um in Ihrem Netzwerk ordnungsgemäß zu funktionieren.

Bei TCP/IP-basierten Netzwerken verringert DHCP die Komplexität und die Menge an Verwaltungsaufgaben, die bei der Konfiguration von Computern anfallen.

### <a name="tcpip-overview"></a>Übersicht über TCP/IP

Standardmäßig verfügen alle Versionen von Windows Server-und Windows-Client Betriebssystemen über TCP/IP-Einstellungen für IP-Version 4-Netzwerkverbindungen, die so konfiguriert sind, dass automatisch eine IP-Adresse und andere Informationen, sogenannte DHCP-Optionen, von einem DHCP-Server Daher müssen Sie die TCP/IP-Einstellungen nicht manuell konfigurieren, es sei denn, der Computer ist ein Server Computer oder ein anderes Gerät, für das eine manuell konfigurierte statische IP-Adresse erforderlich ist. 

Es wird z. b. empfohlen, die IP-Adresse des DHCP-Servers und die IP-Adressen von DNS-Servern und Domänen Controllern, auf denen Active Directory Domain Services \(AD DS\)ausgeführt wird, manuell zu konfigurieren.

TCP/IP in Windows Server 2016 lautet wie folgt:

- Eine Netzwerksoftware auf der Grundlage von Netzwerkprotokollen, die dem Industriestandard entsprechen.

- Ein routingfähiges Unternehmensnetzwerkprotokoll, das die Verbindung Ihres Windows-Computers sowohl mit LAN- als auch mit WAN-Umgebungen unterstützt.

- Kerntechnologien und Hilfsprogramme für die Verbindung Ihres Windows-Computers mit anderen Systemen zum Austausch von Daten.

- Eine Grundlage für den Zugriff auf globale Internet Dienste, wie z. b. Web-und Dateiübertragungsprotokoll (FTP)-Server.

- Ein zuverlässiges, skalierbares und plattformübergreifendes Client-/Server-Framework

TCP/IP stellt grundlegende TCP/IP-Hilfsprogramme bereit, mit deren Hilfe Windows-Computer Verbindungen mit anderen Microsoft- und Nicht-Microsoft-Systemen herstellen und Informationen austauschen können, beispielsweise:

- Windows Server 2016

- Windows-10

- Windows Server 2012 R2

- Windows 8.1

- WindowsServer 2012

- Windows 8

- Windows Server 2008 R2

- Windows 7

- Windows Server 2008

- Windows Vista

- Internethosts

- Apple Macintosh-Systeme

- IBM-Mainframes

- UNIX-und Linux-Systeme

- Open VMS-Systeme

- Netzwerk bereite Drucker

- Tablets und Mobiltelefone mit kabelgebundener Ethernet-oder drahtlos 802,11-Technologie

## <a name="bkmk_plan"></a>DHCP-Bereitstellung planen

Im folgenden finden Sie die wichtigsten Planungsschritte vor der Installation der DHCP-Server Rolle.

### <a name="planning-dhcp-servers-and-dhcp-forwarding"></a>Planen von DHCP-Servern und DHCP-Weiterleitung

Da DHCP-Meldungen Broadcastmeldungen sind, werden diese von Routern nicht zwischen Subnetzen weitergeleitet. Wenn Sie mehrere Subnetze besitzen und für jedes Subnetz DHCP-Dienste bereitstellen möchten, müssen Sie folgendermaßen vorgehen:

- Installieren Sie einen DHCP-Server in jedem Subnetz.

- Konfigurieren Sie Router, um DHCP-Broadcastmeldungen zwischen Subnetzen weiterzuleiten, und konfigurieren Sie mehrere Bereiche auf dem DHCP-Server, einen Bereich pro Subnetz.

In den meisten Fällen ist die Konfiguration von Routern für die Weiterleitung von DHCP-Broadcastmeldungen kosteneffektiver als die Bereitstellung eines DHCP-Servers in jedem physischen Segment des Netzwerks.

### <a name="planning-ip-address-ranges"></a>Planen von IP-Adressbereichen

Jedes Subnetz muss seinen eigenen eindeutigen IP-Adressbereich besitzen. Diese Bereiche werden auf einem DHCP-Server durch Bereiche dargestellt.

Ein Bereich ist eine administrative Gruppierung von IP-Adressen für Computer in einem Subnetz, die den DHCP-Dienst verwenden. Der Administrator erstellt zunächst einen Bereich für jedes physische Subnetz und verwendet diesen dann, um die von den Clients verwendeten Parameter zu definieren.

Ein Bereich weist folgende Eigenschaften auf:

- Einen IP-Adressbereich, von dem Adressen ein- oder ausgeschlossen werden, die für DHCP-Dienst-Leaseangebote verwendet werden.

- Eine Subnetzmaske, die das Subnetzpräfix für eine angegebene IP-Adresse bestimmt.

- Ein bei seiner Erstellung zugewiesener Bereichsname.

- Leasedauerwerte, die DHCP-Clients zugewiesen werden, die dynamisch zugeordnete IP-Adressen empfangen.

- Beliebige DHCP-Bereichsoptionen, die für die Zuordnung zu DHCP-Clients konfiguriert wurden, z. B. IP-Adresse des DNS-Servers und IP-Adresse des Routers/Standardgateways.

- Reservierungen werden optional verwendet, um sicherzustellen, dass ein DHCP-Client immer die gleiche IP-Adresse empfängt.

Listen Sie vor der Bereitstellung Ihrer Server die Subnetze und den IP-Adressbereich auf, den Sie für jedes Subnetz verwenden möchten.

### <a name="planning-subnet-masks"></a>Planen von Subnetzmasken

Netzwerk-IDs und Host-IDs innerhalb einer IP-Adresse werden mithilfe einer Subnetzmaske unterschieden. Jede Subnetzmaske ist eine 32-Bit-Zahl, die aufeinander folgende Bitgruppen von Einsen (1) verwendet, um die Netzwerk-ID zu kennzeichnen und Nullen (0), um die Host-ID-Abschnitte der IP-Adresse zu kennzeichnen.

Beispielsweise ist die Subnetzmaske, die normalerweise mit der IP-Adresse 131.107.16.200 verwendet wird, die folgende 32-Bit-Binärzahl:

```
11111111 11111111 00000000 00000000
```

Diese Subnetzmasken-Nummer ist 16 1-Bit gefolgt von 16 Null Bits und gibt an, dass die Bereiche Netzwerk-ID und Host-ID dieser IP-Adresse eine Länge von 16 Bit haben. Normalerweise wird diese Subnetzmaske in punktierter Dezimalschreibweise als 255.255.0.0. angezeigt.

In der folgenden Tabelle werden Subnetzmasken für die Internetadressklassen angezeigt.

|Adressklasse|Bits für die Subnetzmaske|Subnetzmaske|
|-----------------|------------------------|---------------|
|Klasse A|11111111 00000000 00000000 00000000|255.0.0.0|
|Klasse B|11111111 11111111 00000000 00000000|255.255.0.0|
|Klasse C|11111111 11111111 11111111 00000000|255.255.255.0|

Wenn Sie einen Bereich in DHCP erstellen und den IP-Adressbereich für den Bereich eingeben, stellt DHCP diese Standard-Subnetzmaskenwerte bereit. In der Regel sind Standard-Subnetzmaskenwerte für die meisten Netzwerke ohne spezielle Anforderungen sowie für Netzwerke, bei denen jedes IP-Netzwerksegment einem physischen Netzwerk entspricht, akzeptabel.

In einigen Fällen können Sie angepasste Subnetzmasken für die Implementierung von IP-Subnetzen verwenden. Mit IP-Subnetzen können Sie den Abschnitt der Standard-Host-ID einer IP-Adresse zur Festlegung von Subnetzen unterteilen, bei denen es sich um Unterabschnitte der ursprünglichen klassenbasierten Netzwerk-ID handelt.

Wenn Sie die Länge der Subnetzmaske anpassen, können Sie die Anzahl der Bits reduzieren, die für die tatsächliche Host-ID verwendet wird.

Zur Vermeidung von Adressierungs- und Routingproblemen sollten Sie sicherstellen, dass alle TCP/IP-Computer in einem Netzwerksegment die gleiche Subnetzmaske verwenden, und dass jeder Computer und jedes Gerät eine eindeutige IP-Adresse besitzt.

### <a name="planning-exclusion-ranges"></a>Planen von Ausschlussbereichen

Wenn Sie auf einem DHCP-Server einen Bereich erstellen, geben Sie einen IP-Adressbereich an, der alle IP-Adressen enthält, die der DHCP-Server an DHCP-Clients wie Computer und andere Geräte leasen darf. Wenn Sie anschließend einige Server und andere Geräte mit statischen IP-Adressen aus dem IP-Adressbereich manuell konfigurieren, den der DHCP-Server verwendet, können Sie versehentlich einen IP-Adresskonflikt verursachen, wenn Sie und der DHCP-Server verschiedenen Geräten eine IP-Adresse zuweisen.

Um dieses Problem zu beheben, können Sie einen Ausschlussbereich für den DHCP-Bereich erstellen. Ein Ausschluss Bereich ist ein zusammenhängender Bereich von IP-Adressen innerhalb des IP-Adress Bereichs des Bereichs, der vom DHCP-Server nicht verwendet werden darf. Wenn Sie einen Ausschlussbereich erstellen, weist der DHCP-Server keine Adressen aus diesem Bereich zu, sodass Sie diese Adressen manuell zuweisen können, ohne einen IP-Adresskonflikt zu verursachen.

Sie können IP-Adressen von der Verteilung durch den DHCP-Server ausschließen, indem Sie einen Ausschlussbereich für jeden Bereich erstellen. Sie sollten Ausschlüsse für alle Geräte erstellen, die mit einer statischen IP-Adresse konfiguriert sind. Die ausgeschlossenen Adressen sollten alle IP-Adressen enthalten, die Sie manuell anderen Servern, Nicht-DHCP-Clients, Arbeitsstationen ohne Datenträger oder Routing- und Remotezugriff- und PPP-Clients zugewiesen haben.

Es wird empfohlen, den Ausschlussbereich mit zusätzlichen Adressen zu konfigurieren, um für späteres Wachsen des Netzwerks vorbereitet zu sein. In der folgenden Tabelle finden Sie einen Beispiel Ausschluss Bereich für einen Bereich mit dem IP-Adressbereich 10.0.0.1-10.0.0.254 und einer Subnetzmaske von 255.255.255.0.

|Konfigurationselemente|Beispielwerte|
|-----------------------|------------------|
|Start-IP-Adresse des Ausschlussbereichs|10.0.0.1|
|End-IP-Adresse des Ausschlussbereichs|10.0.0.25|

### <a name="planning-tcpip-static-configuration"></a>Planen einer statischen TCP/IP-Konfiguration

Einige Geräte wie Router, DHCP-Server und DNS-Server müssen mit einer statischen IP-Adresse konfiguriert werden. Möglicherweise haben Sie auch weitere Geräte wie Drucker, für die Sie sicherstellen möchten, dass sie immer die gleiche IP-Adresse besitzen. Listen Sie die Geräte für jedes Subnetz auf, die Sie statisch konfigurieren möchten, und planen Sie dann den Ausschlussbereich, den Sie auf dem DHCP-Server verwenden möchten, um sicherzustellen, dass der DHCP-Server nicht die IP-Adresse eines statisch konfigurierten Geräts least. Ein Ausschlussbereich ist eine begrenzte Abfolge von IP-Adressen innerhalb eines Bereichs, der von der Verarbeitung durch den DHCP-Dienst ausgeschlossen wird. Ausschlussbereiche stellen sicher, dass die Adressen in diesen Bereichen vom Server nicht für DHCP-Clients im Netzwerk bereitgestellt werden.

Wenn der IP-Adressbereich eines Subnetzes beispielsweise 192.168.0.1 bis 192.168.0.254 ist, und Sie zehn Geräte besitzen, die Sie mit einer statischen IP-Adresse konfigurieren möchten, können Sie einen Ausschlussbereich für den Bereich 192.168.0.*x* festlegen, der zehn oder mehr IP-Adressen enthält: 192.168.0.1 bis 192.168.0.15.

In diesem Beispiel werden zehn der ausgeschlossenen IP-Adressen verwendet, um Server und andere Geräte mit statischen IP-Adressen zu konfigurieren, und fünf weitere IP-Adressen bleiben für die Konfiguration neuer Geräte verfügbar, die zukünftig hinzugefügt werden können. Mit diesem Ausschlussbereich verfügt der DHCP-Server noch über einen Adresspool von 192.168.0.16 bis 192.168.0.254.

Weitere Beispiel Konfigurationselemente für AD DS und DNS finden Sie in der folgenden Tabelle.

|Konfigurationselemente|Beispielwerte|
|-----------------------|------------------|
|Bindungen für die Netzwerkverbindung|Ethernet|
|DNS-Servereinstellungen|DC1.corp.contoso.com|
|Bevorzugte IP-Adresse des DNS-Servers|10.0.0.2|
|Bereichs Werte<br /><br />1. Bereichs Name<br />2. Start-IP-Adresse<br />3. IP-Endadresse<br />4. Subnetzmaske<br />5. Standard Gateway (optional)<br />6. Leasedauer|1. primäres Subnetz<br />2.10.0.0.1<br />3.10.0.0.254<br />4.255.255.255.0<br />5.10.0.0.1<br />6.8 Tage|
|Betriebsmodus des IPv6-DHCP-Servers|Nicht aktiviert|

## <a name="bkmk_lab"></a>Verwenden dieses Handbuchs in einer Test Umgebung

Mit dieser Anleitung können Sie DHCP in einer Testumgebung bereitstellen, bevor Sie in einer Produktionsumgebung bereitstellen. 

> [!NOTE]
> Wenn Sie DHCP nicht in einer Testumgebung bereitstellen möchten, können Sie mit dem Abschnitt Bereitstellen von [DHCP](#bkmk_deploy)fortfahren.

Die Anforderungen für das Lab unterscheiden sich abhängig davon, ob Sie physische Server oder virtuelle Computer \(VMS\)verwenden und ob Sie eine Active Directory Domäne verwenden oder einen eigenständigen DHCP-Server bereitstellen.

Mithilfe der folgenden Informationen können Sie die minimalen Ressourcen ermitteln, die Sie zum Testen der DHCP-Bereitstellung in diesem Handbuch benötigen.

### <a name="test-lab-requirements-with-vms"></a>Test Umgebungs Anforderungen mit VMS

Zum Bereitstellen von DHCP in einer Testumgebung mit virtuellen Computern benötigen Sie die folgenden Ressourcen.

Bei der Domänen Bereitstellung oder der eigenständigen Bereitstellung benötigen Sie einen Server, der als Hyper\-V-Host konfiguriert ist.

**Domänen Bereitstellung**

Diese Bereitstellung erfordert einen physischen Server, einen virtuellen Switch, zwei virtuelle Server und einen virtuellen Client:

Erstellen Sie auf dem physischen Server im Hyper-V-Manager die folgenden Elemente:

1. Ein **interner** virtueller Switch. Erstellen Sie keinen **externen** virtuellen Switch, denn wenn sich der Hyper\-V-Host in einem Subnetz befindet, das einen DHCP-Server enthält, erhalten die virtuellen Testcomputer eine IP-Adresse vom DHCP-Server. Außerdem kann der von Ihnen bereitgestellte DHCP-Testserver anderen Computern im Subnetz, auf dem der Hyper\-V-Host installiert ist, IP-Adressen zuweisen.
1. Ein virtueller Computer unter Windows Server 2016, der als Domänen Controller mit Active Directory Domain Services konfiguriert ist, der mit dem von Ihnen erstellten internen virtuellen Switch verbunden ist. Dieser Server muss über eine statisch konfigurierte IP-Adresse von 10.0.0.2 verfügen, damit er diesem Leitfaden entspricht. Weitere Informationen zum Bereitstellen von AD DS finden Sie im Abschnitt Bereitstellen von **DC1** im Windows Server 2016- [Kern Netzwerk Handbuch](https://docs.microsoft.com/windows-server/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01).
1. Einen virtuellen Computer unter Windows Server 2016, den Sie als DHCP-Server konfigurieren, indem Sie diesen Leitfaden verwenden, der mit dem von Ihnen erstellten internen virtuellen Switch verbunden ist. 
1. Ein virtueller Computer, auf dem ein Windows-Client Betriebssystem ausgeführt wird, das mit dem von Ihnen erstellten internen virtuellen Switch verbunden ist und den Sie verwenden, um zu überprüfen, ob der DHCP-Server DHCP-Clients dynamisch IP-Adressen und DHCP-Optionen zuordnet

**Eigenständige DHCP-Server Bereitstellung**

Diese Bereitstellung erfordert einen physischen Server, einen virtuellen Switch, einen virtuellen Server und einen virtuellen Client:

Erstellen Sie auf dem physischen Server im Hyper-V-Manager die folgenden Elemente:

1. Ein **interner** virtueller Switch. Erstellen Sie keinen **externen** virtuellen Switch, denn wenn sich der Hyper\-V-Host in einem Subnetz befindet, das einen DHCP-Server enthält, erhalten die virtuellen Testcomputer eine IP-Adresse vom DHCP-Server. Außerdem kann der von Ihnen bereitgestellte DHCP-Testserver anderen Computern im Subnetz, auf dem der Hyper\-V-Host installiert ist, IP-Adressen zuweisen.
2. Einen virtuellen Computer unter Windows Server 2016, den Sie als DHCP-Server konfigurieren, indem Sie diesen Leitfaden verwenden, der mit dem von Ihnen erstellten internen virtuellen Switch verbunden ist.
3. Ein virtueller Computer, auf dem ein Windows-Client Betriebssystem ausgeführt wird, das mit dem von Ihnen erstellten internen virtuellen Switch verbunden ist und den Sie verwenden, um zu überprüfen, ob der DHCP-Server DHCP-Clients dynamisch IP-Adressen und DHCP-Optionen zuordnet

### <a name="test-lab-requirements-with-physical-servers"></a>Test Umgebungs Anforderungen mit physischen Servern

Zum Bereitstellen von DHCP in einem Testlabor mit physischen Servern benötigen Sie die folgenden Ressourcen.

**Domänen Bereitstellung**

Diese Bereitstellung erfordert einen Hub oder Switch, zwei physische Server und einen physischen Client:

1. Ein Ethernet-Hub oder-Switch, mit dem Sie die physischen Computer mit Ethernet-Kabeln verbinden können.
2. Ein physischer Computer, auf dem Windows Server 2016 ausgeführt wird und der als Domänen Controller mit Active Directory Domain Services konfiguriert ist. Dieser Server muss über eine statisch konfigurierte IP-Adresse von 10.0.0.2 verfügen, damit er diesem Leitfaden entspricht. Weitere Informationen zum Bereitstellen von AD DS finden Sie im Abschnitt Bereitstellen von **DC1** im Windows Server 2016- [Kern Netzwerk Handbuch](https://docs.microsoft.com/windows-server/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01).
3. Ein physischer Computer, auf dem Windows Server 2016 ausgeführt wird und der mithilfe dieses Handbuchs als DHCP-Server konfiguriert wird.
4. Ein physischer Computer, auf dem ein Windows-Client Betriebssystem ausgeführt wird, mit dem Sie überprüfen, ob der DHCP-Server DHCP-Clients dynamisch IP-Adressen und DHCP-Optionen zuordnet.

> [!NOTE]
> Wenn Sie nicht über genügend Testcomputer für diese Bereitstellung verfügen, können Sie einen Testcomputer sowohl für AD DS als auch für DHCP verwenden. diese Konfiguration wird jedoch für eine Produktionsumgebung nicht empfohlen.

**Eigenständige DHCP-Server Bereitstellung**

Für diese Bereitstellung ist ein Hub oder ein Switch, ein physischer Server und ein physischer Client erforderlich:

1. Ein Ethernet-Hub oder-Switch, mit dem Sie die physischen Computer mit Ethernet-Kabeln verbinden können.
2. Ein physischer Computer, auf dem Windows Server 2016 ausgeführt wird und der mithilfe dieses Handbuchs als DHCP-Server konfiguriert wird.
3. Ein physischer Computer, auf dem ein Windows-Client Betriebssystem ausgeführt wird, mit dem Sie überprüfen, ob der DHCP-Server DHCP-Clients dynamisch IP-Adressen und DHCP-Optionen zuordnet.


## <a name="bkmk_deploy"></a>Bereitstellen von DHCP

In diesem Abschnitt finden Sie Windows PowerShell-Beispiel Befehle, mit denen Sie DHCP auf einem Server bereitstellen können. Bevor Sie diese Beispiel Befehle auf dem Server ausführen, müssen Sie die Befehle so ändern, dass Sie Ihrem Netzwerk und ihrer Umgebung entsprechen. 

Vor dem Ausführen der Befehle sollten Sie z. b. die Beispiel Werte in den Befehlen für die folgenden Elemente ersetzen:

- Computer Namen
- IP-Adressbereich für jeden Bereich, den Sie konfigurieren möchten (1 Bereich pro Subnetz)
- Subnetzmaske für jeden IP-Adressbereich, den Sie konfigurieren möchten
- Bereichs Name für jeden Bereich
- Ausschluss Bereich für jeden Bereich
- DHCP-Optionswerte, z. b. Standard Gateway, Domänen Name und DNS-oder WINS-Server
- Schnittstellennamen

> [!IMPORTANT]
> Überprüfen und ändern Sie jeden Befehl für Ihre Umgebung, bevor Sie den Befehl ausführen.

### <a name="where-to-install-dhcp---on-a-physical-computer-or-a-vm"></a>Installationsort von DHCP auf einem physischen Computer oder einem virtuellen Computer?

Sie können die DHCP-Server Rolle auf einem physischen Computer oder auf einem virtuellen Computer \(VM-\) installieren, der auf einem Hyper\-V-Host installiert ist. Wenn Sie DHCP auf einem virtuellen Computer installieren und möchten, dass der DHCP-Server IP-Adress Zuweisungen für Computer in dem physischen Netzwerk bereitstellt, mit dem der Hyper-v-Host verbunden ist, müssen Sie den virtuellen VM-Netzwerkadapter mit einem **externen**virtuellen Hyper-v-Switch verbinden.

Weitere Informationen finden Sie im Abschnitt **Erstellen eines virtuellen Switches mit dem Hyper-V-Manager** im Thema [Erstellen eines virtuellen Netzwerks](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network).

### <a name="run-windows-powershell-as-an-administrator"></a>Ausführen von Windows PowerShell als Administrator

Mithilfe des folgenden Verfahrens können Sie Windows PowerShell mit Administrator Rechten ausführen.

1. Klicken Sie auf einem Computer unter Windows Server 2016 auf **Start**, und klicken Sie dann mit der rechten Maustaste auf das Windows PowerShell-Symbol. Ein Menü wird angezeigt.

2. Klicken Sie im Menü auf **mehr**, und klicken Sie dann auf **als Administrator ausführen**. Wenn Sie dazu aufgefordert werden, geben Sie die Anmelde Informationen eines Kontos ein, das über Administrator Rechte auf dem Computer verfügt. Wenn das Benutzerkonto, mit dem Sie sich bei dem Computer angemeldet haben, ein Konto auf Administrator Ebene ist, erhalten Sie keine Anmeldeaufforderung.

3. Windows PowerShell wird mit Administrator Rechten geöffnet.

### <a name="rename-the-dhcp-server-and-configure-a-static-ip-address"></a>Umbenennen des DHCP-Servers und Konfigurieren einer statischen IP-Adresse

Wenn Sie dies noch nicht getan haben, können Sie die folgenden Windows PowerShell-Befehle verwenden, um den DHCP-Server umzubenennen und eine statische IP-Adresse für den Server zu konfigurieren.

**Konfigurieren einer statischen IP-Adresse**

Sie können die folgenden Befehle verwenden, um dem DHCP-Server eine statische IP-Adresse zuzuweisen und die TCP/IP-Eigenschaften des DHCP-Servers mit der richtigen DNS-Server-IP-Adresse zu konfigurieren. Anstelle der Schnittstellennamen und IP-Adressen in diesem Beispiel müssen Sie die Werte angeben, mit denen Sie Ihren Computer konfigurieren möchten.

```
New-NetIPAddress -IPAddress 10.0.0.3 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 10.0.0.2
```

Weitere Informationen zu diesen Befehlen finden Sie in den folgenden Themen.

- [New-nettipaddress](https://docs.microsoft.com/powershell/module/nettcpip/New-NetIPAddress)
- [Set-dnsclientserveraddress](https://docs.microsoft.com/powershell/module/dnsclient/Set-DnsClientServerAddress)

**Umbenennen des Computers**

Mit den folgenden Befehlen können Sie den Computer umbenennen und dann neu starten.

```
Rename-Computer -Name DHCP1
Restart-Computer
```

Weitere Informationen zu diesen Befehlen finden Sie in den folgenden Themen.

- [Umbenennen-Computer](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/rename-computer)
- [Restart-Computer](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/restart-computer)

### <a name="join-the-computer-to-the-domain-optional"></a>Fügen Sie den Computer der Domäne hinzu, \(optional\)

Wenn Sie den DHCP-Server in einer Active Directory Domänen Umgebung installieren, müssen Sie den Computer der Domäne hinzufügen. Öffnen Sie Windows PowerShell mit Administrator Rechten, und führen Sie dann den folgenden Befehl aus, nachdem Sie den NetBIOS-Domänen Namen **Corp** mit einem Wert ersetzt haben, der für Ihre Umgebung geeignet ist.

```
Add-Computer CORP
```

Geben Sie bei entsprechender Aufforderung die Anmelde Informationen für ein Domänen Benutzerkonto ein, das über die Berechtigung zum Hinzufügen eines Computers zur Domäne verfügt. 

```
Restart-Computer
```

Weitere Informationen zum Befehl "Add-Computer" finden Sie im folgenden Thema.

- [Computer hinzufügen](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/add-computer?view=powershell-5.1)

### <a name="install-dhcp"></a>Installieren von DHCP

Nachdem der Computer neu gestartet wurde, öffnen Sie Windows PowerShell mit Administrator Rechten, und installieren Sie dann DHCP, indem Sie den folgenden Befehl ausführen.

```
Install-WindowsFeature DHCP -IncludeManagementTools
```

Weitere Informationen zu diesem Befehl finden Sie im folgenden Thema.

- [Install-Windows Feature](https://docs.microsoft.com/powershell/module/servermanager/install-windowsfeature)

### <a name="create-dhcp-security-groups"></a>Erstellen von DHCP-Sicherheitsgruppen

Zum Erstellen von Sicherheitsgruppen müssen Sie eine Netzwerkshell \(Netsh\)-Befehl in Windows PowerShell ausführen und dann den DHCP-Dienst neu starten, damit die neuen Gruppen aktiv werden.

Wenn Sie den folgenden Netsh-Befehl auf dem DHCP-Server ausführen, werden die Sicherheitsgruppen **DHCP-Administratoren** und **DHCP-Benutzer** in **lokale Benutzer und Gruppen** auf dem DHCP-Server erstellt.

```
netsh dhcp add securitygroups
```

Mit dem folgenden Befehl wird der DHCP-Dienst auf dem lokalen Computer neu gestartet.

```
Restart-Service dhcpserver
```

Weitere Informationen zu diesen Befehlen finden Sie in den folgenden Themen.

- [Network Shell (Netsh)](../netsh/netsh.md)
- [Neu starten: Dienst](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/restart-service)

### <a name="authorize-the-dhcp-server-in-active-directory-optional"></a>Autorisieren Sie den DHCP-Server in Active Directory \(optional\)

Wenn Sie DHCP in einer Domänen Umgebung installieren, müssen Sie die folgenden Schritte ausführen, um den DHCP-Server für den Betrieb in der Domäne zu autorisieren.

> [!NOTE]
> Nicht autorisierte DHCP-Server, die in Active Directory Domänen installiert sind, funktionieren nicht ordnungsgemäß und leasen IP-Adressen nicht an DHCP-Clients. Die automatische Deaktivierung nicht autorisierter DHCP-Server ist eine Sicherheitsfunktion, durch die verhindert wird, dass nicht autorisierte DHCP-Server den Clients in Ihrem Netzwerk falsche IP-Adressen zuweisen.

Mit dem folgenden Befehl können Sie den DHCP-Server der Liste der autorisierten DHCP-Server in Active Directory hinzufügen. 

> [!NOTE]
> Wenn Sie nicht über eine Domänen Umgebung verfügen, führen Sie diesen Befehl nicht aus.

```
Add-DhcpServerInDC -DnsName DHCP1.corp.contoso.com -IPAddress 10.0.0.3
```

Sie können den folgenden Befehl verwenden, um zu überprüfen, ob der DHCP-Server in Active Directory autorisiert ist.

```
Get-DhcpServerInDC
```

Im folgenden finden Sie Beispiel Ergebnisse, die in Windows PowerShell angezeigt werden.

```
IPAddress   DnsName
---------   -------
10.0.0.3    DHCP1.corp.contoso.com
```

Weitere Informationen zu diesen Befehlen finden Sie in den folgenden Themen.

- [Add-dhcpserverindc](https://docs.microsoft.com/powershell/module/dhcpserver/add-dhcpserverindc)
- [Get-dhcpserverindc](https://docs.microsoft.com/powershell/module/dhcpserver/get-dhcpserverindc)

### <a name="notify-server-manager-that-post-install-dhcp-configuration-is-complete-optional"></a>Benachrichtigen Sie Server-Manager, dass nach\-Installation der DHCP-Konfiguration \(optional\)

Nachdem Sie die Aufgaben nach der\-Installation abgeschlossen haben, z. b. das Erstellen von Sicherheitsgruppen und das autorialisieren des DHCP-Servers in Active Directory Server-Manager, wird auf der Benutzeroberfläche möglicherweise weiterhin eine Warnung angezeigt, die darauf hinweist, dass die Installationsschritte\-nach der Installation mithilfe des DHCP-Konfigurations-Assistenten nach der Installation

Sie können verhindern, dass diese Meldung jetzt\-unnötige und ungenaue Nachricht in Server-Manager angezeigt wird, indem Sie den folgenden Registrierungsschlüssel mit diesem Windows PowerShell-Befehl konfigurieren.

```
Set-ItemProperty –Path registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ServerManager\Roles\12 –Name ConfigurationState –Value 2
```

Weitere Informationen zu diesem Befehl finden Sie im folgenden Thema.

- [Set-ItemProperty](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/set-itemproperty)

### <a name="set-server-level-dns-dynamic-update-configuration-settings-optional"></a>Festlegen der Konfigurationseinstellungen für dynamische DNS-Updates auf Serverebene \(optional\)

Wenn der DHCP-Server dynamische DNS-Updates für DHCP-Client Computer ausführen soll, können Sie den folgenden Befehl ausführen, um diese Einstellung zu konfigurieren. Dabei handelt es sich um eine Einstellung auf Serverebene, nicht um eine Bereichs Ebene, sodass Sie sich auf alle Bereiche auswirkt, die Sie auf dem Server konfigurieren. Mit diesem Beispiel Befehl wird auch der DHCP-Server konfiguriert, um DNS-Ressourcen Einträge für Clients zu löschen, wenn der Client am wenigsten abläuft.

```
Set-DhcpServerv4DnsSetting -ComputerName "DHCP1.corp.contoso.com" -DynamicUpdates "Always" -DeleteDnsRRonLeaseExpiry $True
```

Sie können den folgenden Befehl verwenden, um die Anmelde Informationen zu konfigurieren, die der DHCP-Server zum Registrieren oder Aufheben der Registrierung von Client Datensätzen auf einem DNS-Server verwendet. In diesem Beispiel werden Anmelde Informationen auf einem DHCP-Server gespeichert. Der erste Befehl verwendet **Get-Credential** zum Erstellen eines **PSCredential** -Objekts und speichert das Objekt dann in der **$Credential** Variable. Der Befehl fordert Sie zur Eingabe von Benutzername und Kennwort auf. Stellen Sie also sicher, dass Sie Anmelde Informationen für ein Konto bereitstellen, das über die Berechtigung zum Aktualisieren von Ressourcen Einträgen auf Ihrem DNS
 
```
$Credential = Get-Credential
Set-DhcpServerDnsCredential -Credential $Credential -ComputerName "DHCP1.corp.contoso.com"
``` 

Weitere Informationen zu diesen Befehlen finden Sie in den folgenden Themen.

- [Set-DhcpServerv4DnsSetting](https://docs.microsoft.com/powershell/module/dhcpserver/set-dhcpserverv4dnssetting)
- [Set-dhcpserverdnscredential](https://docs.microsoft.com/powershell/module/dhcpserver/set-dhcpserverdnscredential)

### <a name="configure-the-corpnet-scope"></a>Konfigurieren des Bereichs "Corpnet"

Nachdem die DHCP-Installation abgeschlossen ist, können Sie die folgenden Befehle verwenden, um den Bereich Corpnet zu konfigurieren und zu aktivieren, einen Ausschluss Bereich für den Bereich zu erstellen und die DHCP-Optionen Standard Gateway, DNS-Server-IP-Adresse und DNS-Domänen Namen zu konfigurieren.

```
Add-DhcpServerv4Scope -name "Corpnet" -StartRange 10.0.0.1 -EndRange 10.0.0.254 -SubnetMask 255.255.255.0 -State Active    
Add-DhcpServerv4ExclusionRange -ScopeID 10.0.0.0 -StartRange 10.0.0.1 -EndRange 10.0.0.15
Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.0.1 -ScopeID 10.0.0.0 -ComputerName DHCP1.corp.contoso.com
Set-DhcpServerv4OptionValue -DnsDomain corp.contoso.com -DnsServer 10.0.0.2
```

Weitere Informationen zu diesen Befehlen finden Sie in den folgenden Themen.

- [Add-DhcpServerv4Scope](https://docs.microsoft.com/powershell/module/dhcpserver/Add-DhcpServerv4Scope)
- [Add-DhcpServerv4ExclusionRange](https://docs.microsoft.com/powershell/module/dhcpserver/Add-DhcpServerv4ExclusionRange)
- [Set-DhcpServerv4OptionValue](https://docs.microsoft.com/powershell/module/dhcpserver/Set-DhcpServerv4OptionValue)

### <a name="configure-the-corpnet2-scope-optional"></a>Konfigurieren Sie den Corpnet2-Bereich \(optional\)

Wenn Sie über ein zweites Subnetz verfügen, das mit dem ersten Subnetz mit einem Router verbunden ist, bei dem die DHCP-Weiterleitung aktiviert ist, können Sie die folgenden Befehle verwenden, um einen zweiten Bereich namens Corpnet2 für dieses Beispiel hinzuzufügen. In diesem Beispiel werden auch ein Ausschluss Bereich und die IP-Adresse für das Standard Gateway konfiguriert, \(die routerip-Adresse im Subnetz\) des Corpnet2-Subnetzes.

```
Add-DhcpServerv4Scope -name "Corpnet2" -StartRange 10.0.1.1 -EndRange 10.0.1.254 -SubnetMask 255.255.255.0 -State Active
Add-DhcpServerv4ExclusionRange -ScopeID 10.0.1.0 -StartRange 10.0.1.1 -EndRange 10.0.1.15
Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.1.1 -ScopeID 10.0.1.0 -ComputerName DHCP1.corp.contoso.com
```

Wenn Sie über zusätzliche Subnetze verfügen, die von diesem DHCP-Server gewartet werden, können Sie diese Befehle wiederholen, indem Sie unterschiedliche Werte für alle Befehlsparameter verwenden, um Bereiche für jedes Subnetz hinzuzufügen.

> [!IMPORTANT]
> Stellen Sie sicher, dass alle Router zwischen Ihren DHCP-Clients und dem DHCP-Server für die DHCP-Nachrichten Weiterleitung konfiguriert sind. Weitere Informationen zum Konfigurieren der DHCP-Weiterleitung finden Sie in der routerdokumentation.

## <a name="bkmk_verify"></a>Überprüfen der Server Funktionalität

Um zu überprüfen, ob der DHCP-Server DHCP-Clients eine dynamische Zuordnung von IP-Adressen bereitstellt, können Sie einen anderen Computer mit einem Serviced Subnetz verbinden. Nach dem Verbinden des Ethernet-Kabels mit dem Netzwerkadapter und dem Einschalten des Computers wird vom DHCP-Server eine IP-Adresse angefordert. Sie können die erfolgreiche Konfiguration überprüfen, indem Sie den Befehl **ipconfig/all** verwenden und die Ergebnisse überprüfen, oder indem Sie Konnektivitätstests durchführen, z. b. den Zugriff auf Webressourcen mit Ihrem Browser oder Dateifreigaben mit Windows Explorer oder anderen Anwendungen

Wenn der Client keine IP-Adresse vom DHCP-Server empfängt, führen Sie die folgenden Schritte zur Problembehandlung aus.

1. Stellen Sie sicher, dass das Ethernet-Kabel sowohl an den Computer als auch an den Ethernet-Switch,-Hub oder-Router angeschlossen ist.
2. Wenn Sie den Client Computer in einem Netzwerksegment angeschlossen haben, das von einem Router vom DHCP-Server getrennt ist, stellen Sie sicher, dass der Router für das Weiterleiten von DHCP-Nachrichten konfiguriert ist.
3. Stellen Sie sicher, dass der DHCP-Server in Active Directory autorisiert ist, indem Sie den folgenden Befehl ausführen, um die Liste der autorisierten DHCP-Server von Active Directory abzurufen. [Get-dhcpserverindc](https://docs.microsoft.com/powershell/module/dhcpserver/Get-DhcpServerInDC).
4. Stellen Sie sicher, dass ihre Bereiche aktiviert sind, indem Sie die DHCP-Konsole öffnen \(Server-Manager, **Tools**, **DHCP**\), erweitern Sie die Server Struktur, um Bereiche zu überprüfen, und klicken Sie dann mit der rechten\- Wenn das resultierende Menü die Auswahl **aktivieren**enthält, klicken Sie auf **aktivieren**. \(wenn der Bereich bereits aktiviert ist, liest die Menü Auswahl die Option **Deaktivieren**.\)

## <a name="bkmk_dhcpwps"></a>Windows PowerShell-Befehle für DHCP

Die folgende Referenz enthält Befehlsbeschreibungen und Syntax für alle Windows PowerShell-Befehle des DHCP-Servers für Windows Server 2016. Das Thema listet Befehle in alphabetischer Reihenfolge auf, die auf dem Verb am Anfang der Befehle basieren, z. b. **Get** oder **set**.

> [!NOTE]
> Windows Server 2016-Befehle können in Windows Server 2012 R2 nicht verwendet werden.

- [Dhcpserver-Modul](https://docs.microsoft.com/powershell/module/dhcpserver/)

Die folgende Referenz enthält Befehlsbeschreibungen und Syntax für alle Windows PowerShell-Befehle des DHCP-Servers für Windows Server 2012 R2. Das Thema listet Befehle in alphabetischer Reihenfolge auf, die auf dem Verb am Anfang der Befehle basieren, z. b. **Get** oder **set**.

> [!NOTE]
> Sie können Windows Server 2012 R2-Befehle in Windows Server 2016 verwenden.

- [DHCP-Server-Cmdlets in Windows PowerShell](https://docs.microsoft.com/windows-server/networking/technologies/dhcp/dhcp-deploy-wps)

## <a name="bkmk_list"></a>Liste der Windows PowerShell-Befehle in diesem Handbuch

Im folgenden finden Sie eine einfache Liste der Befehle und Beispiel Werte, die in diesem Handbuch verwendet werden.

```
New-NetIPAddress -IPAddress 10.0.0.3 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 10.0.0.2
Rename-Computer -Name DHCP1
Restart-Computer

Add-Computer CORP
Restart-Computer

Install-WindowsFeature DHCP -IncludeManagementTools
netsh dhcp add securitygroups
Restart-Service dhcpserver

Add-DhcpServerInDC -DnsName DHCP1.corp.contoso.com -IPAddress 10.0.0.3
Get-DhcpServerInDC

Set-ItemProperty –Path registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ServerManager\Roles\12 –Name ConfigurationState –Value 2

Set-DhcpServerv4DnsSetting -ComputerName "DHCP1.corp.contoso.com" -DynamicUpdates "Always" -DeleteDnsRRonLeaseExpiry $True

$Credential = Get-Credential
Set-DhcpServerDnsCredential -Credential $Credential -ComputerName "DHCP1.corp.contoso.com"

rem At prompt, supply credential in form DOMAIN\user, password

rem Configure scope Corpnet
Add-DhcpServerv4Scope -name "Corpnet" -StartRange 10.0.0.1 -EndRange 10.0.0.254 -SubnetMask 255.255.255.0 -State Active
Add-DhcpServerv4ExclusionRange -ScopeID 10.0.0.0 -StartRange 10.0.0.1 -EndRange 10.0.0.15
Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.0.1 -ScopeID 10.0.0.0 -ComputerName DHCP1.corp.contoso.com
Set-DhcpServerv4OptionValue -DnsDomain corp.contoso.com -DnsServer 10.0.0.2

rem Configure scope Corpnet2
Add-DhcpServerv4Scope -name "Corpnet2" -StartRange 10.0.1.1 -EndRange 10.0.1.254 -SubnetMask 255.255.255.0 -State Active
Add-DhcpServerv4ExclusionRange -ScopeID 10.0.1.0 -StartRange 10.0.1.1 -EndRange 10.0.1.15
Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.1.1 -ScopeID 10.0.1.0 -ComputerName DHCP1.corp.contoso.com
```
