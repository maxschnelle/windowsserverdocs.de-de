---
title: Bereitstellung von DHCP mit Windows PowerShell
description: Sie können in diesem Thema verwenden, um einen Windows Server 2016 IP (Internet Protocol)-IPv4-DHCP-Server bereitzustellen, der automatische IP-Adressen und DHCP-Optionen für IPv4-DHCP-Clients, die mit einem oder mehreren Subnetzen in Ihrem Netzwerk verbunden sind, bietet.
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: article
ms.assetid: 7110ad21-a33e-48d5-bb3c-129982913bc8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8a53f6293067fa0f7014e7794696cf75f7179545
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849091"
---
# <a name="deploy-dhcp-using-windows-powershell"></a>Bereitstellung von DHCP mit Windows PowerShell

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Handbuch enthält Anweisungen zur Verwendung von Windows PowerShell zum Bereitstellen einer IP (Internet Protocol) Version 4 Dynamic Host Configuration Protocol \(DHCP\) Server, die IP-Adressen und DHCP automatisch zugewiesen, IPv4-DHCP-Optionen Clients, die mit einem oder mehreren Subnetzen in Ihrem Netzwerk verbunden sind.

>[!NOTE]
>Um dieses Dokument im Word-Format aus der TechNet Gallery herunterladen zu können, finden Sie unter [Bereitstellen von DHCP mit Windows PowerShell unter Windows Server 2016](https://gallery.technet.microsoft.com/Deploy-DHCP-Using-Windows-246dd293).

Mithilfe von DHCP-Server IP-zuzuweisen Adressen Sie speichert in Verwaltungsaufwand, da Sie nicht benötigen, um die TCP/IP-v4-Einstellungen für alle Netzwerkadapter manuell auf jedem Computer in Ihrem Netzwerk zu konfigurieren. Mit DHCP TCP/IP-v4-Konfiguration wird automatisch ausgeführt, wenn ein Computer, oder andere DHCP-Client mit dem Netzwerk verbunden ist.

Sie können den DHCP-Server in einer Arbeitsgruppe als eigenständiger Server oder als Teil einer Active Directory-Domäne bereitstellen.

Dieses Handbuch enthält die folgenden Abschnitte:

- [Übersicht über die Bereitstellung von DHCP](#bkmk_overview)
- [Technologieübersicht](#bkmk_technologies)
- [DHCP-Bereitstellung planen](#bkmk_plan)
- [Mithilfe dieses Handbuchs in einer Testumgebung](#bkmk_lab)
- [Bereitstellen von DHCP](#bkmk_deploy)
- [Überprüfen Sie die Serverfunktionalität](#bkmk_verify)
- [Windows PowerShell-Befehle für DHCP](#bkmk_dhcpwps)
- [Liste der Windows PowerShell-Befehle in diesem Handbuch](#bkmk_list)

## <a name="bkmk_overview"></a>Übersicht über die Bereitstellung von DHCP

Die folgende Abbildung zeigt das Szenario, das Sie bereitstellen können, mithilfe dieses Handbuchs. Das Szenario umfasst eine DHCP-Server in einer Active Directory-Domäne. Der Server wird konfiguriert, um IP-Adressen für DHCP-Clients in zwei verschiedenen Subnetzen bereitzustellen. Die Subnetze werden von einem Router getrennt, die DHCP-Weiterleitung aktiviert ist.

![Übersicht über die DHCP-Netzwerk-Topologie](../../media/Core-Network-Guide/cng16_overview.jpg)

## <a name="bkmk_technologies"></a>Technologieübersicht

In den folgenden Abschnitten bieten eine kurze Übersicht über DHCP und TCP/IP.

### <a name="dhcp-overview"></a>Übersicht über DHCP

DHCP ist ein IP-Standard für die Vereinfachung der Verwaltung der Host-IP-Konfiguration. Der DHCP-Standard ermöglicht DHCP-Servern die Verwaltung der dynamischen Zuweisung von IP-Adressen und sonstiger zugehöriger Konfigurationsdetails für DHCP-fähige Clients im Netzwerk.

DHCP können Sie einen DHCP-Server zu verwenden, um dynamisch eine IP-Adresse auf einem Computer oder einem anderen Gerät wie z. B. einen Drucker auf Ihrem lokalen Netzwerk und nicht jedes Gerät manuell konfigurieren, mit einer statischen IP-Adresse zuweisen.

Jeder Computer in einem TCP/IP-Netzwerk muss über eine eindeutige IP-Adresse verfügen. Zudem muss die zugehörige Subnetzmaske sowohl den Hostcomputer als auch das Subnetz angeben, an das der Computer angeschlossen ist. Durch die Verwendung von DHCP können Sie sicherstellen, dass alle als DHCP-Clients konfigurierten Computer eine für die Netzwerkadresse und das Subnetz geeignete IP-Adresse erhalten. Und durch die Verwendung von DHCP-Optionen wie Standardgateway und DNS-Server können Sie DHCP-Clients automatisch die Informationen bereitstellen, die diese benötigen, um in Ihrem Netzwerk ordnungsgemäß zu funktionieren.

Bei TCP/IP-basierten Netzwerken verringert DHCP an die Komplexität und Umfang von Verwaltungsaufgaben, die beim Konfigurieren von Computern.

### <a name="tcpip-overview"></a>Übersicht über die TCP/IP

Standardmäßig haben alle Versionen der Betriebssysteme Windows Server und Windows-Client TCP/IP-Einstellungen für IP Version 4 Netzwerkverbindungen so konfiguriert, dass automatisch eine IP-Adresse und andere Informationen, die DHCP-Optionen, von einem DHCP-Server namens beziehen. Aus diesem Grund müssen Sie keine TCP/IP-Einstellungen manuell konfigurieren, es sei denn, der Computer ist ein Server-Computer oder ein anderes Gerät, das eine manuell konfigurierte, statische IP-Adresse ist erforderlich. 

Es wird beispielsweise empfohlen, dass Sie manuell konfigurieren, die IP-Adresse des DHCP-Servers, und die IP-Adressen der DNS-Server und Domänencontroller, die Active Directory Domain Services ausgeführt werden \(AD DS\).

TCP/IP in Windows Server 2016 lautet wie folgt:

-   Eine Netzwerksoftware auf der Grundlage von Netzwerkprotokollen, die dem Industriestandard entsprechen.

-   Ein routingfähiges Unternehmensnetzwerkprotokoll, das die Verbindung Ihres Windows-Computers sowohl mit LAN- als auch mit WAN-Umgebungen unterstützt.

-   Kerntechnologien und Hilfsprogramme für die Verbindung Ihres Windows-Computers mit anderen Systemen zum Austausch von Daten.

-   Eine Grundlage für den Zugriff auf globale Internetdienste wie z. B. Web-Apps und -Protokolls FTP (File Transfer)-Server.

-   Ein zuverlässiges, skalierbares und plattformübergreifendes Client-/Server-Framework

TCP/IP stellt grundlegende TCP/IP-Hilfsprogramme bereit, mit deren Hilfe Windows-Computer Verbindungen mit anderen Microsoft- und Nicht-Microsoft-Systemen herstellen und Informationen austauschen können, beispielsweise:

- Windows Server 2016

- Windows 10

- Windows Server 2012 R2

- Windows 8.1

- Windows Server 2012

- Windows 8

- Windows Server 2008 R2

- Windows 7

- WindowsServer 2008

- Windows Vista

- Internethosts

- Apple Macintosh-Systeme

- IBM-Mainframes

- UNIX- und Linux-Systemen

- Open VMS-Systeme

- Netzwerkfähige Drucker

- Tablets und -Handys mit verkabeltes Ethernet oder drahtlose 802.11-Technologie, die aktiviert

## <a name="bkmk_plan"></a>DHCP-Bereitstellung planen

Folgendes sind die wichtigsten Planungsschritte vor der Installation der DHCP-Serverrolle.

### <a name="planning-dhcp-servers-and-dhcp-forwarding"></a>Planen von DHCP-Servern und DHCP-Weiterleitung

Da DHCP-Meldungen Broadcastmeldungen sind, werden diese von Routern nicht zwischen Subnetzen weitergeleitet. Wenn Sie mehrere Subnetze besitzen und für jedes Subnetz DHCP-Dienste bereitstellen möchten, müssen Sie folgendermaßen vorgehen:

-   Installieren Sie einen DHCP-Server in jedem Subnetz.

-   Konfigurieren Sie Router, um DHCP-Broadcastmeldungen zwischen Subnetzen weiterzuleiten, und konfigurieren Sie mehrere Bereiche auf dem DHCP-Server, einen Bereich pro Subnetz.

In den meisten Fällen ist die Konfiguration von Routern für die Weiterleitung von DHCP-Broadcastmeldungen kosteneffektiver als die Bereitstellung eines DHCP-Servers in jedem physischen Segment des Netzwerks.

### <a name="planning-ip-address-ranges"></a>Planen von IP-Adressbereichen

Jedes Subnetz muss seinen eigenen eindeutigen IP-Adressbereich besitzen. Diese Bereiche werden auf einem DHCP-Server durch Bereiche dargestellt.

Ein Bereich ist eine administrative Gruppierung von IP-Adressen für Computer in einem Subnetz, die den DHCP-Dienst verwenden. Der Administrator erstellt zunächst einen Bereich für jedes physische Subnetz und verwendet diesen dann, um die von den Clients verwendeten Parameter zu definieren.

Ein Bereich weist folgende Eigenschaften auf:

-   Einen IP-Adressbereich, von dem Adressen ein- oder ausgeschlossen werden, die für DHCP-Dienst-Leaseangebote verwendet werden.

-   Eine Subnetzmaske, die das Subnetzpräfix für eine angegebene IP-Adresse bestimmt.

-   Ein bei seiner Erstellung zugewiesener Bereichsname.

-   Leasedauerwerte, die DHCP-Clients zugewiesen werden, die dynamisch zugeordnete IP-Adressen empfangen.

-   Beliebige DHCP-Bereichsoptionen, die für die Zuordnung zu DHCP-Clients konfiguriert wurden, z. B. IP-Adresse des DNS-Servers und IP-Adresse des Routers/Standardgateways.

-   Reservierungen werden optional verwendet, um sicherzustellen, dass ein DHCP-Client immer die gleiche IP-Adresse empfängt.

Listen Sie vor der Bereitstellung Ihrer Server die Subnetze und den IP-Adressbereich auf, den Sie für jedes Subnetz verwenden möchten.

### <a name="planning-subnet-masks"></a>Planen von Subnetzmasken

Netzwerk-IDs und Host-IDs innerhalb einer IP-Adresse werden mithilfe einer Subnetzmaske unterschieden. Jede Subnetzmaske ist eine 32-Bit-Zahl, die aufeinander folgende Bitgruppen von Einsen (1) verwendet, um die Netzwerk-ID zu kennzeichnen und Nullen (0), um die Host-ID-Abschnitte der IP-Adresse zu kennzeichnen.

Beispielsweise ist die Subnetzmaske, die normalerweise mit der IP-Adresse 131.107.16.200 verwendet wird, die folgende 32-Bit-Binärzahl:

```
11111111 11111111 00000000 00000000
```

Diese Subnetzmasken-Zahl ist 16 gefolgt von 16 Bits aus Nullen, 1-Bits, der angibt, dass die Netzwerk-ID und Host-ID Abschnitte dieser IP-Adresse jeweils 16 Bit lang sind. Normalerweise wird diese Subnetzmaske in punktierter Dezimalschreibweise als 255.255.0.0. angezeigt.

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

Um dieses Problem zu beheben, können Sie einen Ausschlussbereich für den DHCP-Bereich erstellen. Einem Ausschlussbereich handelt es sich um einen zusammenhängenden Bereich von IP-Adressen innerhalb des Bereichs IP-Adressbereich an, die der DHCP-Server nicht verwenden darf. Wenn Sie einen Ausschlussbereich erstellen, weist der DHCP-Server keine Adressen aus diesem Bereich zu, sodass Sie diese Adressen manuell zuweisen können, ohne einen IP-Adresskonflikt zu verursachen.

Sie können IP-Adressen von der Verteilung durch den DHCP-Server ausschließen, indem Sie einen Ausschlussbereich für jeden Bereich erstellen. Sie sollten Ausschlüsse für alle Geräte erstellen, die mit einer statischen IP-Adresse konfiguriert sind. Die ausgeschlossenen Adressen sollten alle IP-Adressen enthalten, die Sie manuell anderen Servern, Nicht-DHCP-Clients, Arbeitsstationen ohne Datenträger oder Routing- und Remotezugriff- und PPP-Clients zugewiesen haben.

Es wird empfohlen, den Ausschlussbereich mit zusätzlichen Adressen zu konfigurieren, um für späteres Wachsen des Netzwerks vorbereitet zu sein. Die folgende Tabelle enthält einen Ausschlussbereich für Beispiel für einen Bereich mit einer IP-Adressbereich 10.0.0.1: 10.0.0.254 und einer Subnetzmaske 255.255.255.0.

|Konfigurationselemente|Beispielwerte|
|-----------------------|------------------|
|Start-IP-Adresse des Ausschlussbereichs|10.0.0.1|
|End-IP-Adresse des Ausschlussbereichs|10.0.0.25|

### <a name="planning-tcpip-static-configuration"></a>Planen einer statischen TCP/IP-Konfiguration

Einige Geräte wie Router, DHCP-Server und DNS-Server müssen mit einer statischen IP-Adresse konfiguriert werden. Möglicherweise haben Sie auch weitere Geräte wie Drucker, für die Sie sicherstellen möchten, dass sie immer die gleiche IP-Adresse besitzen. Listen Sie die Geräte für jedes Subnetz auf, die Sie statisch konfigurieren möchten, und planen Sie dann den Ausschlussbereich, den Sie auf dem DHCP-Server verwenden möchten, um sicherzustellen, dass der DHCP-Server nicht die IP-Adresse eines statisch konfigurierten Geräts least. Ein Ausschlussbereich ist eine begrenzte Abfolge von IP-Adressen innerhalb eines Bereichs, der von der Verarbeitung durch den DHCP-Dienst ausgeschlossen wird. Ausschlussbereiche stellen sicher, dass die Adressen in diesen Bereichen vom Server nicht für DHCP-Clients im Netzwerk bereitgestellt werden.

Wenn die IP-Adressbereich für ein Subnetz 192.168.0.1 bis 192.168.0.254 und Sie zehn Geräte besitzen, die Sie mit einer statischen IP-Adresse konfigurieren möchten, können Sie beispielsweise einen für den Ausschlussbereich 192.168.0. erstellen. *x* Bereich, zehn oder mehr IP-Adressen enthält: 192.168.0.1 bis 192.168.0.15.

In diesem Beispiel werden zehn der ausgeschlossenen IP-Adressen verwendet, um Server und andere Geräte mit statischen IP-Adressen zu konfigurieren, und fünf weitere IP-Adressen bleiben für die Konfiguration neuer Geräte verfügbar, die zukünftig hinzugefügt werden können. Mit diesem Ausschlussbereich verfügt der DHCP-Server noch über einen Adresspool von 192.168.0.16 bis 192.168.0.254.

Zusätzliches Beispiel von Konfigurationselementen für AD DS und DNS werden in der folgenden Tabelle bereitgestellt.

|Konfigurationselemente|Beispielwerte|
|-----------------------|------------------|
|Bindungen für die Netzwerkverbindung|Ethernet|
|DNS-Servereinstellungen|DC1.corp.contoso.com|
|Bevorzugte IP-Adresse des DNS-Servers|10.0.0.2|
|Bereichswerte<br /><br />1.  Bereichsname<br />2.  Start-IP-Adresse<br />3.  End-IP-Adresse:<br />4.  Subnetzmaske<br />5.  Standardgateway (optional)<br />6.  Leasedauer|1.  Primäres Subnetz<br />2.  10.0.0.1<br />3.  10.0.0.254<br />4.  255.255.255.0<br />5.  10.0.0.1<br />6. 8 Tage|
|Betriebsmodus des IPv6-DHCP-Servers|Nicht aktiviert|

## <a name="bkmk_lab"></a>Mithilfe dieses Handbuchs in einer Testumgebung

Sie können dieses Handbuch verwenden, DHCP in einer testumgebung bereitstellen, bevor Sie in einer produktionsumgebung bereitstellen. 

>[!NOTE]
>Wenn Sie nicht DHCP in einer testumgebung bereitstellen möchten, können Sie mit dem Abschnitt fortfahren [DHCP bereitstellen](#bkmk_deploy).

Die Anforderungen für Ihr Lab unterscheiden sich abhängig davon, ob Sie physische Server oder virtuelle Computer sind \(VMs\), und gibt an, ob Sie mithilfe von Active Directory-Domäne oder einen eigenständigen DHCP-Server bereitstellen. 

Sie können die folgende Informationen verwenden, um die minimale Ressourcen zu ermitteln, die Sie mithilfe dieses Handbuchs DHCP-Bereitstellung zu testen müssen.

### <a name="test-lab-requirements-with-vms"></a>Test Lab-Anforderungen mit virtuellen Computern

DHCP in einer testumgebung mit virtuellen Computern bereitstellen zu können, benötigen Sie die folgenden Ressourcen.

Für Bereitstellung oder eigenständige Bereitstellung, die Sie benötigen einen Server, der als einem virtuellen Hyper konfiguriert\-V-Host.

**Bereitstellung**

Diese Bereitstellungsmethode ist einem physischen Server, einen virtuellen Switch, zwei virtuelle Server und einen virtuellen Client:

Erstellen Sie auf dem physischen Server im Hyper-V-Manager die folgenden Elemente ein.

1. Eine **intern** virtuellen Switch. Erstellen Sie keine **externe** virtuellen Switch, da Wenn Ihrer Hyper\-V-Host befindet sich in einem Subnetz, das einen DHCP-Server enthält, der Test-VMs erhalten eine IP-Adresse vom DHCP-Server. Darüber hinaus kann der DHCP-Testserver, die Sie bereitstellen IP-Adressen zuweisen, auf andere Computer im Subnetz, in dem die Hyper\-V-Host installiert ist.
1. Ein virtueller Computer unter Windows Server 2016 konfiguriert, die als Domänencontroller mit Active Directory Domain Services, die mit dem internen virtuellen Switch verbunden ist, die Sie erstellt haben. Entsprechend dieser Anleitung müssen dieser Server eine statisch konfigurierte IP-Adresse 10.0.0.2. Informationen zum Bereitstellen von AD DS finden Sie im Abschnitt **Bereitstellen von DC1** in Windows Server 2016 [Core Network Guide](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01).
1. Eine VM, die unter Windows Server 2016, die Sie mit diesem Handbuch und die als DHCP-Server konfigurieren, verbunden ist, die interne virtuelle wechseln Sie erstellt haben. 
1. Ein virtueller Computer mit einem Windows-Clientbetriebssystem, das auf dem virtuellen intern verbunden ist, wechseln Sie erstellt haben und dass Sie verwenden möchten, um sicherzustellen, dass die IP-Adressen und DHCP-Optionen auf der DHCP-Server dynamisch DHCP-Clients zugewiesen wird.

**Standalone-DHCP-Server-Bereitstellung**

Diese Bereitstellungsmethode ist einem physischen Server, einen virtuellen Switch, einen virtuellen Server und einen virtuellen Client:

Erstellen Sie auf dem physischen Server im Hyper-V-Manager die folgenden Elemente ein.

1. Eine **intern** virtuellen Switch. Erstellen Sie keine **externe** virtuellen Switch, da Wenn Ihrer Hyper\-V-Host befindet sich in einem Subnetz, das einen DHCP-Server enthält, der Test-VMs erhalten eine IP-Adresse vom DHCP-Server. Darüber hinaus kann der DHCP-Testserver, die Sie bereitstellen IP-Adressen zuweisen, auf andere Computer im Subnetz, in dem die Hyper\-V-Host installiert ist.
1. Eine VM, die unter Windows Server 2016, die Sie mit diesem Handbuch und die als DHCP-Server konfigurieren, verbunden ist, die interne virtuelle wechseln Sie erstellt haben.
1. Ein virtueller Computer mit einem Windows-Clientbetriebssystem, das auf dem virtuellen intern verbunden ist, wechseln Sie erstellt haben und dass Sie verwenden möchten, um sicherzustellen, dass die IP-Adressen und DHCP-Optionen auf der DHCP-Server dynamisch DHCP-Clients zugewiesen wird.

### <a name="test-lab-requirements-with-physical-servers"></a>Test Lab-Anforderungen mit physischen Servern

Zum Bereitstellen von DHCP in einem Testlabor mit physischen Servern, benötigen Sie die folgenden Ressourcen.

**Bereitstellung**

Diese Bereitstellungsmethode ist ein Hub oder Switch, zwei physische Server und einem physischen Client:

1. Ein Ethernet-Hub oder Switch mit dem können Sie die physischen Computer verbinden, mit der Ethernet-Kabel
1. Ein physischer Computer unter Windows Server 2016 als Domänencontroller mit Active Directory Domain Services konfiguriert. Entsprechend dieser Anleitung müssen dieser Server eine statisch konfigurierte IP-Adresse 10.0.0.2. Informationen zum Bereitstellen von AD DS finden Sie im Abschnitt **Bereitstellen von DC1** in Windows Server 2016 [Core Network Guide](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01).
1. Ein physischer Computer unter Windows Server 2016, die Sie als einen DHCP-Server konfigurieren müssen, mithilfe dieses Handbuchs. 
1. Ein physischer Computer, die mit einem Windows-Clientbetriebssystem, das Sie verwenden werden, um zu überprüfen, ob dem DHCP-Server ist das IP-Adressen und DHCP-Optionen dynamisch DHCP-Clients zuordnen.

>[!NOTE]
>Wenn Sie nicht über genügend Testcomputer für diese Bereitstellung verfügen, können Sie einen Testcomputer für AD DS und DHCP - verwenden, diese Konfiguration nicht für eine produktionsumgebung wird jedoch empfohlen.

**Standalone-DHCP-Server-Bereitstellung**

Diese Bereitstellungsmethode ist ein Hub oder Switch, einem physischen Server und einem physischen Client:

1. Ein Ethernet-Hub oder Switch mit dem können Sie die physischen Computer verbinden, mit der Ethernet-Kabel
2. Ein physischer Computer unter Windows Server 2016, die Sie als einen DHCP-Server konfigurieren müssen, mithilfe dieses Handbuchs. 
3. Ein physischer Computer, die mit einem Windows-Clientbetriebssystem, das Sie verwenden werden, um zu überprüfen, ob dem DHCP-Server ist das IP-Adressen und DHCP-Optionen dynamisch DHCP-Clients zuordnen.


## <a name="bkmk_deploy"></a>Bereitstellen von DHCP

Dieser Abschnitt enthält Windows PowerShell-Beispielbefehle, mit denen Sie DHCP auf einem Server bereitstellen. Bevor Sie diese Beispielbefehle auf dem Server ausführen müssen Sie die Befehle entsprechend Ihrem Netzwerk und die Umgebung ändern. 

Bevor Sie die Befehle ausführen, sollten Sie z. B. Beispielwerte in den Befehlen für die folgenden Elemente ersetzen:

- Computernamen
- IP-Adressbereich für jeden Bereich (1-Bereich pro Subnetz) konfiguriert werden soll
- Die Netzwerksubnetz-Maske für jede IP-Adressbereich an, die Sie konfigurieren möchten.
- Name des für die einzelnen Bereiche
- Ausschlussbereich für jeden Bereich
- DHCP-Werte, z. B. das Standardgateway, Domänenname und DNS oder WINS-Server
- Schnittstellennamen

>[!IMPORTANT]
>Untersuchen Sie und ändern Sie jeden Befehl für Ihre Umgebung aus, bevor Sie den Befehl ausführen.

### <a name="where-to-install-dhcp---on-a-physical-computer-or-a-vm"></a>Installationsort der Installieren von DHCP - auf einem physischen Computer oder einem virtuellen Computer

Sie können die DHCP-Serverrolle installieren, auf einem physischen Computer oder auf einem virtuellen Computer \(VM\) auf einem virtuellen Hyper installierte\-V-Host. Wenn Sie DHCP auf einem virtuellen Computer installieren, und möchten, dass des DHCP-Servers, um IP-Adresszuweisungen auf Computern im physischen Netzwerk bereitzustellen, mit dem Hyper-V-Host verbunden ist, müssen Sie den virtuellen Netzwerkadapter für die virtuellen Computer anschließen, mit einem virtuellen Hyper-V-Switch, der **Externe**.

Weitere Informationen finden Sie im Abschnitt **Erstellen eines virtuellen Switches in Hyper-V-Manager** im Thema [Erstellen eines virtuellen Netzwerks](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network).

### <a name="run-windows-powershell-as-an-administrator"></a>Windows PowerShell als Administrator ausführen.

Sie können das folgende Verfahren verwenden, zum Ausführen von Windows PowerShell mit Administratorrechten aus.

1. Klicken Sie auf einem Computer unter Windows Server 2016, auf **starten**, per Rechtsklick das Windows PowerShell-Symbol. Ein Menü wird angezeigt. 

2. Klicken Sie im Menü auf **weitere**, und klicken Sie dann auf **als Administrator ausführen**. Wenn Sie dazu aufgefordert werden, geben Sie die Anmeldeinformationen für ein Konto, das über Administratorrechte auf dem Computer verfügt. Wenn das Benutzerkonto, mit dem Sie auf dem Computer angemeldet sind, ein Servicelevel-Administratorkonto ist, erhalten Sie eine Eingabeaufforderung nicht.

3. Windows PowerShell wird mit Administratorrechten geöffnet.

### <a name="rename-the-dhcp-server-and-configure-a-static-ip-address"></a>Benennen Sie den DHCP-Server und Konfigurieren einer statischen IP-Adresse

Wenn Sie nicht bereits geschehen, können Sie folgende Windows PowerShell-Befehle verwenden, benennen Sie den DHCP-Server, und konfigurieren eine statische IP-Adresse für den Server.

**Konfigurieren einer statischen IP-Adresse**

Sie können die folgenden Befehle aus dem DHCP-Server eine statische IP-Adresse zuweisen und so konfigurieren Sie die DHCP-Server-TCP/IP-Eigenschaften mit der richtigen DNS-Server IP-Adresse verwenden. Anstelle der Schnittstellennamen und IP-Adressen in diesem Beispiel müssen Sie die Werte angeben, mit denen Sie Ihren Computer konfigurieren möchten.

 `New-NetIPAddress -IPAddress 10.0.0.3 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24`

 `Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 10.0.0.2`

Weitere Informationen zu diesen Befehlen finden Sie unter den folgenden Themen.

- [New-NetIPAddress](https://technet.microsoft.com/itpro/powershell/windows/tcpip/new-netipaddress)
- [Set-DnsClientServerAddress](https://technet.microsoft.com/itpro/powershell/windows/dns-client/set-dnsclientserveraddress)

**Umbenennen des Computers**

Sie können die folgenden Befehle verwenden, umbenennen, und klicken Sie dann den Computer neu starten.

`Rename-Computer -Name DHCP1`

 `Restart-Computer`

Weitere Informationen zu diesen Befehlen finden Sie unter den folgenden Themen.

- [Rename-Computer](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/rename-computer)
- [Restart-Computer](https://msdn.microsoft.com/powershell/reference/4.0/microsoft.powershell.management/restart-computer)

### <a name="join-the-computer-to-the-domain-optional"></a>Fügen Sie den Computer der Domäne \(Optional\)

Wenn Sie den DHCP-Server in einer Active Directory-Domäne-Umgebung installieren, müssen Sie mit der Domäne beitritt. Öffnen Sie Windows PowerShell mit Administratorrechten, und führen Sie den folgenden Befehl nach dem Ersetzen der NetBIOS-Domänenname **CORP** mit einem Wert, der für Ihre Umgebung geeignet ist.

    Add-Computer CORP

Geben Sie bei Aufforderung die Anmeldeinformationen für ein Domänenbenutzerkonto an, die über die Berechtigung zum Hinzufügen eines Computers zur Domäne verfügt. 

    Restart-Computer

Weitere Informationen über den Befehl Add-Computer finden Sie im folgende Thema.

- [Add-Computer](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/add-computer)

### <a name="install-dhcp"></a>Installieren von DHCP

Nach dem Neustart des Computers öffnen Sie Windows PowerShell mit Administratorrechten, und klicken Sie dann die installieren Sie DHCP-mithilfe des folgenden Befehls.

    Install-WindowsFeature DHCP -IncludeManagementTools

Weitere Informationen zu diesem Befehl finden Sie im folgende Thema.

- [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/server-manager/install-windowsfeature)

### <a name="create-dhcp-security-groups"></a>Erstellen von DHCP-Sicherheitsgruppen

Um Sicherheitsgruppen zu erstellen, müssen Sie eine Netzwerk-Shell ausführen \(Netsh\) Befehl in Windows PowerShell und den DHCP-Dienst neu starten, sodass die neuen Gruppen aktiviert werden.

Beim Ausführen von des folgenden Netsh-Befehls auf dem DHCP-Server die **DHCP-Administratoren** und **DHCP-Benutzer** Sicherheitsgruppen werden in erstellt **lokale Benutzer und Gruppen** auf dem von DHCP Server.

    netsh dhcp add securitygroups

Der folgende Befehl startet den DHCP-Dienst auf dem lokalen Computer neu.

    Restart-service dhcpserver

Weitere Informationen zu diesen Befehlen finden Sie unter den folgenden Themen.

- [Netzwerkshell (Netsh)](../netsh/netsh.md)
- [Restart-Service](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/restart-service)

### <a name="authorize-the-dhcp-server-in-active-directory-optional"></a>Autorisieren Sie den DHCP-Server in Active Directory \(Optional\)

Wenn Sie DHCP in einer Umgebung installieren, müssen Sie die folgenden Schritte zum Autorisieren der DHCP-Server in der Domäne ausgeführt werden ausführen.

>[!NOTE]
>Nicht autorisierte DHCP-Server, die in Active Directory-Domänen installiert werden können nicht ordnungsgemäß, und es sind keine IP-Adressen DHCP-Clients geleast. Die automatische Deaktivierung von nicht autorisierten DHCP-Server ist eine Sicherheitsfunktion, die verhindert, dass nicht autorisierte DHCP-Server falsche IP-Adressen für Clients in Ihrem Netzwerk zuweisen.

Sie können den folgenden Befehl verwenden, den DHCP-Server zur Liste der autorisierten DHCP-Server in Active Directory hinzufügen. 

>[!NOTE]
>Wenn Sie nicht über eine domänenumgebung verfügen, führen Sie diesen Befehl nicht.

 `Add-DhcpServerInDC -DnsName DHCP1.corp.contoso.com -IPAddress 10.0.0.3`

Um sicherzustellen, dass der DHCP-Server in Active Directory berechtigt ist, können Sie den folgenden Befehl verwenden.

    Get-DhcpServerInDC

Folgen Beispielergebnisse, die in Windows PowerShell angezeigt werden.

    
        IPAddress   DnsName
        ---------   -------
        10.0.0.3    DHCP1.corp.contoso.com
    

Weitere Informationen zu diesen Befehlen finden Sie unter den folgenden Themen.

- [Add-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverindc)
- [Get-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/get-dhcpserverindc)

### <a name="notify-server-manager-that-post-install-dhcp-configuration-is-complete-optional"></a>Benachrichtigen Sie Server-Manager die Veröffentlichung\-installieren Sie DHCP-Konfiguration ist abgeschlossen \(Optional\)

Nachdem Sie Post haben\-Installationsaufgaben wie das Erstellen von Sicherheitsgruppen und autorisieren den DHCP-Server in Active Directory Server-Manager möglicherweise weiterhin eine Warnung angezeigt, in der Benutzeroberfläche, die mit dem Hinweis Dieser Beitrag\- Schritte der Installation müssen abgeschlossen werden, mithilfe des Assistenten für die DHCP-Konfiguration nach der Installation.

Sie können verhindern, dass dies nun\-nicht benötigten und fehlerhafte Nachricht angezeigt werden im Server-Manager konfigurieren Sie den folgenden Registrierungsschlüssel mit dem folgenden Windows PowerShell-Befehl.

    Set-ItemProperty –Path registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ServerManager\Roles\12 –Name ConfigurationState –Value 2

Weitere Informationen zu diesem Befehl finden Sie im folgende Thema.

- [Set-ItemProperty](https://msdn.microsoft.com/powershell/reference/4.0/microsoft.powershell.management/set-itemproperty?f=255&MSPPError=-2147217396)

### <a name="set-server-level-dns-dynamic-update-configuration-settings-optional"></a>Festlegen der Server auf dynamische DNS-Updates Konfigurationseinstellungen \(Optional\)

Wenn Sie den DHCP-Server dynamische DNS-Updates für DHCP-Clientcomputer ausführen möchten, können Sie den folgenden Befehl zum Konfigurieren dieser Einstellung ausführen. Dies ist eine Serverebene festlegen, keinen Bereich Ebene festlegen, damit sie alle Bereiche gelten, die Sie auf dem Server zu konfigurieren. Dieser Beispielbefehl konfiguriert auch den DHCP-Server, um die DNS-Ressourceneinträge für Clients löschen, wenn der Client mindestens abläuft.

    Set-DhcpServerv4DnsSetting -ComputerName "DHCP1.corp.contoso.com" -DynamicUpdates "Always" -DeleteDnsRRonLeaseExpiry $True

Sie können den folgenden Befehl verwenden, so konfigurieren Sie die Anmeldeinformationen, die der DHCP-Server zu registrieren oder die Registrierung von Clientdatensätzen auf einen DNS-Server verwendet. In diesem Beispiel speichert die Anmeldeinformationen auf einem DHCP-Server. Der erste Befehl verwendet **Get-Credential** zum Erstellen einer **PSCredential** Objekt und speichert dann das Objekt in der **$Credential** Variable. Der Befehl aufgefordert, Benutzername und Kennwort, müssen Sie sicherstellen, dass Sie Anmeldeinformationen für ein Konto angeben, die über die Berechtigung zum Aktualisieren von Datensätzen Ressource, auf dem DNS-Server verfügt.

    
    $Credential = Get-Credential
    Set-DhcpServerDnsCredential -Credential $Credential -ComputerName "DHCP1.corp.contoso.com"
    

Weitere Informationen zu diesen Befehlen finden Sie unter den folgenden Themen.

- [Set-DhcpServerv4DnsSetting](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverv4dnssetting)
- [Set-DhcpServerDnsCredential](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverdnscredential)

### <a name="configure-the-corpnet-scope"></a>Konfigurieren Sie den Bereich "Corpnet"

Nach Abschluss der Installation von DHCP, können Sie die folgenden Befehle zum Konfigurieren und aktivieren Sie den Bereich "Corpnet", erstellen einen Ausschlussbereich für den Bereich und der DHCP-Optionen für Standard-Gateway, DNS-Server IP-Adresse und DNS-Domänennamen zu konfigurieren.

    
    Add-DhcpServerv4Scope -name "Corpnet" -StartRange 10.0.0.1 -EndRange 10.0.0.254 -SubnetMask 255.255.255.0 -State Active`
    
    Add-DhcpServerv4ExclusionRange -ScopeID 10.0.0.0 -StartRange 10.0.0.1 -EndRange 10.0.0.15`
    
    Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.0.1 -ScopeID 10.0.0.0 -ComputerName DHCP1.corp.contoso.com`
    
    Set-DhcpServerv4OptionValue -DnsDomain corp.contoso.com -DnsServer 10.0.0.2
    

Weitere Informationen zu diesen Befehlen finden Sie unter den folgenden Themen.

- [Add-DhcpServerv4Scope](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverv4scope)
- [Add-DhcpServerv4ExclusionRange](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverv4exclusionrange)
- [Set-DhcpServerv4OptionValue](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverv4optionvalue)

### <a name="configure-the-corpnet2-scope-optional"></a>Konfigurieren des Suchbereichs Corpnet2 \(Optional\)

Wenn Sie ein zweites Subnetz, das mit dem ersten Subnetz mit einem Router verfügen, DHCP-Weiterleitung aktiviert ist verbunden ist, können Sie die folgenden Befehle aus, um einen zweiten Bereich, der mit dem Namen Corpnet2 für dieses Beispiel hinzuzufügen. In diesem Beispiel wird auch einen Ausschlussbereich und die IP-Adresse für das Standardgateway \(die Router-IP-Adresse im Subnetz\) des Subnetzes Corpnet2.

 `Add-DhcpServerv4Scope -name "Corpnet2" -StartRange 10.0.1.1 -EndRange 10.0.1.254 -SubnetMask 255.255.255.0 -State Active`

 `Add-DhcpServerv4ExclusionRange -ScopeID 10.0.1.0 -StartRange 10.0.1.1 -EndRange 10.0.1.15`

 `Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.1.1 -ScopeID 10.0.1.0 -ComputerName DHCP1.corp.contoso.com`

Wenn Sie zusätzliche Subnetze, die vom DHCP-Server bedient werden verfügen, können Sie diese Befehle zu wiederholen, die Verwendung von unterschiedlichen Werten für alle der Befehlsparameter, um Bereiche für jedes Subnetz hinzuzufügen.

>[!IMPORTANT]
>Stellen Sie sicher, dass alle Router zwischen den DHCP-Clients und dem DHCP-Server für die Weiterleitung von DHCP-Nachricht konfiguriert sind. Finden Sie in der Routerdokumentation, Informationen zum Konfigurieren von DHCP-Weiterleitung.

## <a name="bkmk_verify"></a>Überprüfen Sie die Serverfunktionalität

Um sicherzustellen, dass der DHCP-Server für DHCP-Clients dynamische Zuordnung von IP-Adressen bereitstellt, können Sie einen anderen Computer zu einem serviced Subnetz verbinden. Nach dem Ethernet-Kabel der Netzwerkadapter und Leistungsfähigkeit auf dem Computer herstellen, müssen sie eine IP-Adresse von dem DHCP-Server anfordern. Sie können die erfolgreiche Konfiguration überprüfen, indem Sie mit der **Ipconfig/all** Befehl und Überprüfen der Ergebnisse, oder durch Ausführen von Konnektivitätstests, wie z. B. versucht, den Zugriff auf Web-Ressourcen mit Ihrem Browser oder Dateifreigaben mit Windows Explorer oder anderen Anwendungen.

Wenn der Client keine IP-Adresse vom DHCP-Server erhält, führen Sie die folgenden Problembehandlungsschritte ausführen.

1. Stellen Sie sicher, dass das Ethernet-Kabel an sowohl des Computers und der Ethernet-Switch, Hub oder Router angeschlossen ist.
1. Wenn Sie die Client-Computer in einem Netzwerksegment, die vom DHCP-Server durch einen Router getrennt ist angeschlossen, stellen Sie sicher, dass der Router Nachrichten weiterzuleiten DHCP konfiguriert ist.
1. Stellen Sie sicher, dass der DHCP-Server in Active Directory berechtigt ist, indem Sie den folgenden Befehl zum Abrufen der Liste der autorisierten DHCP-Server aus Active Directory ausführen. [Get-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/get-dhcpserverindc).
1. Stellen Sie sicher, dass die Bereiche aktiviert werden, indem Sie die DHCP-Konsole öffnen \(Server-Manager **Tools**, **DHCP**\), erweitern die Serverstruktur, um die Bereiche, überprüfen dann rechts\-auf jeden Bereich. Wenn der daraufhin angezeigten Menü auf die Auswahl enthält **aktivieren**, klicken Sie auf **aktivieren**. \(Wenn der Bereich bereits aktiviert ist, liest die Menüauswahl **deaktivieren**.\) 

## <a name="bkmk_dhcpwps"></a>Windows PowerShell-Befehle für DHCP

Der folgende Verweis enthält Beschreibungen zu Befehlen und Syntax für alle DHCP-Server Windows PowerShell-Befehle, für Windows Server 2016. Diesem Thema sind die Befehle in alphabetischer Reihenfolge nach dem Verb am Anfang der Befehle wie z. B. **erhalten** oder **festgelegt**.

>[!NOTE]
>Sie können keine Befehle von Windows Server 2016 unter Windows Server 2012 R2 verwenden.

- [DhcpServer-Modul](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/index)

Der folgende Verweis enthält Beschreibungen zu Befehlen und Syntax für alle DHCP-Server Windows PowerShell-Befehle, für Windows Server 2012 R2. Diesem Thema sind die Befehle in alphabetischer Reihenfolge nach dem Verb am Anfang der Befehle wie z. B. **erhalten** oder **festgelegt**.

>[!NOTE]
>Sie können Windows Server 2012 R2-Befehle in Windows Server 2016 verwenden.

- [DHCP-Server-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/jj590751.aspx)

## <a name="bkmk_list"></a>Liste der Windows PowerShell-Befehle in diesem Handbuch

Es folgt eine einfache Liste mit Befehlen und Beispielwerten, die in diesem Handbuch verwendet werden.

    
    New-NetIPAddress -IPAddress 10.0.0.3 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24
    Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 10.0.0.2
    Rename-Computer -Name DHCP1
    Restart-Computer
    
    Add-Computer CORP
    Restart-Computer
    
    Install-WindowsFeature DHCP -IncludeManagementTools
    netsh dhcp add securitygroups
    Restart-service dhcpserver
    
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
    


