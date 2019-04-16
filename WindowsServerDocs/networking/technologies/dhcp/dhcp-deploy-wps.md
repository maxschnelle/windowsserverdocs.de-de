---
title: Bereitstellen von DHCP mit der WindowsPowerShell
description: In diesem Thema können Sie einen Windows Server2016 IP (Internet Protocol) Version 4 DHCP-Server bereitstellen, der automatische IP-Adressen und DHCP-Optionen für IPv4-DHCP-Clients mit einem oder mehreren Subnetzen in Ihrem Netzwerk verbunden bereitstellt.
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: article
ms.assetid: 7110ad21-a33e-48d5-bb3c-129982913bc8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2be3c02f32229c9b9ee411f5e97305776f9825d8
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-dhcp-using-windows-powershell"></a>Bereitstellen von DHCP mit der WindowsPowerShell

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Handbuch enthält Anweisungen zur Verwendung von Windows PowerShell einen IP (Internet Protocol) Version 4 Dynamic Host Configuration-Protokoll \(DHCP\) Server bereitstellen, der automatisch IP-Adressen und DHCP-Optionen IPv4-DHCP-Clients zugewiesen, die mit einem oder mehreren Subnetzen in Ihrem Netzwerk verbunden sind.

>[!NOTE]
>Dieses Dokument in Word-Format von TechNet Gallery herunterladen [bereitstellen DHCP mithilfe von Windows PowerShell in Windows Server2016](https://gallery.technet.microsoft.com/Deploy-DHCP-Using-Windows-246dd293).

Mithilfe von DHCP-Server zum Zuweisen von IP Adressen Sie speichert in Verwaltungsaufwand, da Sie nicht die TCP/IP-v4-Einstellungen für alle Netzwerkadapter auf jedem Computer in Ihrem Netzwerk manuell konfigurieren müssen. Mit DHCP TCP/IP-v4-Konfiguration wird automatisch ausgeführt, wenn ein Computer oder andere DHCP-Client mit dem Netzwerk verbunden ist.

Sie können den DHCP-Server in einer Arbeitsgruppe als eigenständigen Server oder als Teil der Active Directory-Domäne bereitstellen.

Dieses Handbuch enthält die folgenden Abschnitte.

- [Übersicht über die DHCP-Bereitstellung](#bkmk_overview)
- [Technologieübersichten](#bkmk_technologies)
- [Planen von DHCP-Bereitstellung](#bkmk_plan)
- [Mithilfe dieses Handbuchs in einem Testlabor](#bkmk_lab)
- [Bereitstellen von DHCP](#bkmk_deploy)
- [Überprüfen Sie die Serverfunktionalität](#bkmk_verify)
- [Windows PowerShell-Befehle für DHCP](#bkmk_dhcpwps)
- [Liste der Windows PowerShell-Befehle in diesem Handbuch](#bkmk_list)

## <a name="bkmk_overview"></a>Übersicht über die DHCP-Bereitstellung

Die folgende Abbildungzeigt das Szenario, das Sie mit diesem Handbuch bereitstellen können. Das Szenario umfasst einen DHCP-Server in Active Directory-Domäne. Der Server wird konfiguriert, um IP-Adressen für DHCP-Clients in zwei verschiedenen Subnetzen bereitzustellen. Die Subnetze werden durch einen Router getrennt, die DHCP-Weiterleitung aktiviert wurde.

![Einführung in die DHCP-Netzwerktopologie](../../media/Core-Network-Guide/cng16_overview.jpg)

## <a name="bkmk_technologies"></a>Technologieübersichten

Die folgenden Abschnitte enthalten eine kurze Übersicht über DHCP und TCP/IP.

### <a name="dhcp-overview"></a>Übersicht über DHCP

DHCP ist ein IP-Standard für die Vereinfachung der Verwaltung der Host-IP-Konfiguration. Der DHCP-Standard bietet für die Verwendung von DHCP-Servern als eine Möglichkeit zum dynamischen Zuweisung von IP-Adressen und sonstiger zugehöriger Konfigurationsdetails für DHCP Clients im Netzwerk zu verwalten.

DHCP ermöglicht einen DHCP-Server dynamisch zuweisen eine IP-Adresse einen Computer oder ein anderes Gerät, z.B. einem Drucker im lokalen Netzwerk, anstatt die manuelle Konfiguration von jedem Gerät mit einer statischen IP-Adresse verwenden.

Alle Computer in einem TCP/IP-Netzwerk benötigen eine eindeutige IP-Adresse, da die IP-Adresse und die zugehörige Subnetzmaske identifizieren, der Host-PC und das Subnetz, mit dem der Computer verbunden ist. Mithilfe von DHCP können Sie sicherstellen, dass alle Computer, die als DHCP-Clients konfiguriert sind, IP-Adresse erhalten, die für die Netzwerkadresse und das Subnetz geeignet ist, und Sie können mithilfe von DHCP-Optionen wie Standardgateway und DNS-Server automatisch DHCP-Clients bereitstellen, mit den Informationen, den sie benötigen in Ihrem Netzwerk ordnungsgemäß funktioniert.

TCP/IP-basierten Netzwerken verringert DHCP die Komplexität und den Umfang von Verwaltungsaufgaben, die bei der Konfiguration von Computern.

### <a name="tcpip-overview"></a>TCP/IP-Übersicht

Standardmäßig haben alle Versionen der Betriebssysteme Windows Server und Windows-Client TCP/IP-Einstellungen für IP-Version 4 Netzwerkverbindungen so konfiguriert, dass automatisch eine IP-Adresse und andere Informationen, so genannte DHCP-Optionen, von einem DHCP-Server beziehen. Aus diesem Grund müssen Sie keine TCP/IP-Einstellungen manuell konfigurieren, es sei denn, der Computer ist ein Server-Computer oder andere Geräte, die manuell konfigurierte statische IP-Adresse ist erforderlich. 

Beispielsweise wird empfohlen, dass Sie manuell konfigurieren, die IP-Adresse des DHCP-Servers und die IP-Adressen der DNS-Server und Domänencontroller, die Active Directory-Domänendienste \(AD DS\) ausgeführt werden.

TCP/IP in Windows Server2016 ist Folgendes:

-   Eine Netzwerksoftware basierend auf Industriestandard-Netzwerkprotokolle.

-   Ein Routingfähiges Netzwerkprotokoll, die die Verbindung Ihres Windows-basierten Computers auf lokalen Netzwerks (LAN) und wide Area Network (WAN)-Umgebungen unterstützt.

-   Kerntechnologien und Hilfsprogramme für die Verbindung Ihres Windows-Computers mit anderen Systemen zum Austausch von Daten.

-   Eine Grundlage für den Zugriff auf globale Internetdienste, z.B. Web- und File Transfer Protocol (FTP).

-   Ein zuverlässiges, skalierbares und plattformübergreifendes Client-/Server-Framework.

TCP/IP bietet grundlegende TCP/IP-Dienstprogramme, mit denen Windows-basierten Computern eine Verbindung herstellen und Freigeben von Informationen mit anderen Microsoft- und Nicht-Microsoft-Systemen, einschließlich:

- Windows Server 2016

- Windows10

- Windows Server2012 R2

- Windows 8.1

- Windows Server 2012

- Windows 8

- Windows Server2008 R2

- Windows 7

- Windows Server 2008

- Windowsvista

- Internet-Hosts

- Apple Macintosh-Systeme

- IBM mainframes

- UNIX- und Linux-Systeme

- Open VMS-Systeme

- Netzwerkfähige Drucker

- Tablets und Handys mit kabelgebundenen Ethernet oder drahtlose 802.11-Technologie aktiviert

## <a name="bkmk_plan"></a>Planen von DHCP-Bereitstellung

Folgendes sind die wichtigsten Planungsschritte vor der Installation der DHCP-Serverrolle.

### <a name="planning-dhcp-servers-and-dhcp-forwarding"></a>Planen der DHCP-Server und DHCP-Weiterleitung

Da DHCP-Meldungen Broadcastmeldungen sind, werden sie nicht zwischen Subnetzen über Router weitergeleitet. Wenn Sie mehrere Subnetze besitzen und DHCP-Dienst für jedes Subnetz bereitstellen möchten, müssen Sie einen der folgenden Schritteausführen:

-   Installieren Sie in jedem Subnetz einen DHCP-Server

-   Konfigurieren Sie Router so, dass DHCP-Broadcastmeldungen in Subnetzen weiterzuleiten, und konfigurieren Sie mehrere Bereiche auf dem DHCP-Server, einen Bereich pro Subnetz.

In den meisten Fällen ist die Konfiguration von Routern für die Weiterleitung von DHCP-Broadcastmeldungen kosteneffektiver als Bereitstellen eines DHCP-Servers in jedem physischen Segment des Netzwerks.

### <a name="planning-ip-address-ranges"></a>Planen der IP-Adressbereiche

Jedes Subnetz benötigen Sie einen eigenen eindeutigen IP-Adressbereich. Diese Bereiche werden auf einem DHCP-Server durch Bereiche dargestellt.

Ein Bereich ist eine administrative Gruppierung von IP-Adressen für Computer in einem Subnetz, die den DHCP-Dienst verwenden. Der Administrator erstellt zunächst einen Bereich für jedes physische Subnetz und verwendet dann den Bereich, um die von Clients verwendeten Parameter zu definieren.

Ein Bereich weist die folgenden Eigenschaften:

-   Ein IP-Adressbereich, aus der Adressen für die DHCP-Dienst-Leaseangebote verwendet ein- oder ausgeschlossen werden soll.

-   Eine Subnetzmaske, die das Subnetzpräfix für eine bestimmte IP-Adresse bestimmt.

-   Ein bei seiner Erstellung zugewiesener Bereichsname.

-   Leasedauerwerte, die DHCP-Clients zugewiesen werden, die dynamisch zugeordnete IP-Adressen zu erhalten.

-   Beliebige DHCP-Bereichsoptionen, der für die Zuordnung zu DHCP-Clients, z.B. IP-Adresse des DNS-Servers und Router/IP-Adresse des Standardgateways konfiguriert.

-   Reservierungen werden optional verwendet, um sicherzustellen, dass ein DHCP-Client immer die gleiche IP-Adresse erhält.

Führen Sie vor der Bereitstellung Ihrer Server die Subnetze und der IP-Adressbereich, die, den Sie für jedes Subnetz verwenden möchten.

### <a name="planning-subnet-masks"></a>Planen von Subnetzmasken

Netzwerk-IDs und Host-IDs innerhalb einer IP-Adresse werden mithilfe einer Subnetzmaske unterschieden. Jede Subnetzmaske ist eine 32-Bit-Zahl mit aufeinander folgende Bitgruppen von Einsen (1) zu den Netzwerk-ID und Nullen (0), um die Teile des Host-ID einer IP-Adresse zu identifizieren.

Beispielsweise ist die Subnetzmaske, die in der Regel mit der IP-Adresse 131.107.16.200 verwendet die folgenden 32-Bit-Binärzahl:

```
11111111 11111111 00000000 00000000
```

Diese Subnetzmaske Subnetznummer handelt es sich 16 eine Bits gefolgt von 16-Bit 0 (null), gibt an, dass die Netzwerk-ID und Host-ID Abschnitte dieser IP-Adresse jeweils 16Bit lang sind. In der Regel wird diese Subnetzmaske in punktierter Dezimalschreibweise als 255.255.0.0 angezeigt.

In der folgende Tabelle werden Subnetzmasken für die Internetadressklassen angezeigt.

|Address-Klasse|Bits für die Subnetzmaske|Subnetzmaske|
|-----------------|------------------------|---------------|
|Klasse A|11111111 00000000 00000000 00000000|255.0.0.0|
|Klasse-B|11111111 11111111 00000000 00000000|255.255.0.0|
|Klasse-C|11111111 11111111 11111111 00000000|255.255.255.0|

Wenn Sie einen Bereich in DHCP erstellen und Sie den IP-Adressbereich für den Bereich eingeben, stellt DHCP diese Standard-subnetzmaskenwerte bereit. In der Regel sind Standard-subnetzmaskenwerte für die meisten Netzwerke ohne spezielle Anforderungen und, wobei jedes IP-Netzwerksegment einem physischen Netzwerk entspricht, akzeptabel.

In einigen Fällen können Sie angepasste Subnetzmasken IP-Subnetzen implementieren. Mit IP-Subnetzen, können Sie den Abschnittdes Standard Host-ID-Teils einer IP-Adresse Subnetze, an denen es sich es sich um Unterabschnitte der ursprünglichen klassenbasierten Netzwerk-ID handelt

Anpassen der Länge der Subnetzmaske, können Sie die Anzahl der Bits reduzieren, die für die tatsächliche Host-ID verwendet werden

Um Probleme mit der Adressierung und Routing zu verhindern, sollten Sie sicherstellen, dass alle TCP/IP-Computer in einem Netzwerksegment die gleiche Subnetzmaske verwenden und jedem Computer oder Gerät eine eindeutige IP-Adresse hat.

### <a name="planning-exclusion-ranges"></a>Planen von Ausschlussbereichen

Wenn Sie einen Bereich auf einem DHCP-Server erstellen, geben Sie einen IP-Adressbereich, der alle IP-Adressen enthält, die der DHCP-Server DHCP-Clients, z.B. Computer und andere Geräte leasen darf. Wenn Sie fahren, und einige Server manuell konfigurieren und andere Geräte mit statischen IP-Adressen aus der gleichen IP-Adressbereich, den der DHCP-Server verwendet wird, können Sie versehentlich einen IP-Adressenkonflikt erstellen, in denen Sie und der DHCP-Server verfügen zugewiesen sowohl die IP-Adresse auf verschiedenen Geräten.

Um dieses Problem zu beheben, können Sie einen Ausschlussbereich für den DHCP-Bereich erstellen. Ein Ausschlussbereich handelt es sich um einen zusammenhängenden Bereich von IP-Adressen innerhalb des Bereichs IP-Adressbereich, die der DHCP-Server nicht verwenden darf. Wenn Sie einen Ausschlussbereich erstellen, weist der DHCP-Server nicht die Adressen in diesem Bereich zu, sodass Sie diese Adressen manuell zuweisen können, ohne einen IP-Adressenkonflikt erstellen.

Erstellen einen Ausschlussbereich für jeden Bereich können Sie IP-Adressen von der Verteilung der DHCP-Server ausschließen. Sie sollten Ausschlüsse für alle Geräte verwenden, die mit einer statischen IP-Adresse konfiguriert sind. Die ausgeschlossenen Adressen sollten alle IP-Adressen enthalten, die Sie manuell anderen Servern, Nicht-DHCP-Clients, Arbeitsstationen ohne Datenträger oder Routing- und Remotezugriff- und PPP-Clients zugewiesen.

Es wird empfohlen, dass Sie den Ausschlussbereich mit zusätzlichen Adressen für Wachstum des Netzwerks konfigurieren. Die folgende Tabelle enthält einen Beispiel Ausschlussbereich für einen Bereich mit einer IP-Adressbereich 10.0.0.1 – 10.0.0.254 und Subnetzmaske 255.255.255.0.

|Konfigurationselemente|Beispielwerte|
|-----------------------|------------------|
|Start-IP-Adresse des Ausschlussbereichs|10.0.0.1|
|End-IP-Adresse des Ausschlussbereichs|10.0.0.25|

### <a name="planning-tcpip-static-configuration"></a>Planen von statischen TCP/IP-Konfiguration

Bestimmte Geräte wie Router, DHCP-Server und DNS-Server müssen mit einer statischen IP-Adresse konfiguriert werden. Darüber hinaus müssen Sie möglicherweise weitere Geräte wie Drucker, die Sie immer sicherstellen möchten die IP-Adresse verfügen. Listen Sie die Geräte, die Sie konfigurieren statisch für jedes Subnetz möchten, und klicken Sie dann planen Sie des Ausschlussbereichs ein, die Sie auf dem DHCP-Server verwenden, um sicherzustellen, dass der DHCP-Server nicht über die IP-Adresse eines statisch konfigurierten Geräts least möchten. Ein Ausschlussbereich ist eine begrenzte Abfolge von IP-Adressen innerhalb eines Bereichs, der vom DHCP-Dienstangebot ausgeschlossen. Ausschlussbereiche stellen sicher, die alle Adressen in diesen Bereichen für DHCP-Clients im Netzwerk nicht vom Server angeboten werden.

Wenn die IP-Adressbereich eines Subnetzes 192.168.0.1 über 192.168.0.254 ist und Sie zehn Geräte, die Sie mit einer statischen IP-Adresse konfigurieren möchten, können Sie z.B. einen Ausschlussbereich für den 192.168.0 erstellen. *x* Bereich, der zehn oder mehr IP-Adressen enthält: 192.168.0.1 über 192.168.0.15.

In diesem Beispiel zehn der ausgeschlossenen IP-Adressen mit dem Server und andere Geräte mit statischen IP-Adressen konfigurieren und fünf weitere IP-Adressen für die Konfiguration neuer Geräte, die Sie in der Zukunft hinzufügen möchten, möglicherweise verfügbar bleiben. Mit diesem Ausschlussbereich bleibt der DHCP-Server über einen Adresspool von 192.168.0.16 über 192.168.0.254.

In der folgenden Tabelle werden zusätzliche Beispiel Konfigurationselemente für die AD DS und DNS bereitgestellt.

|Konfigurationselemente|Beispielwerte|
|-----------------------|------------------|
|Bindungen für die Netzwerkverbindung|Ethernet|
|DNS-servereinstellungen|DC1.corp.contoso.com|
|IP-Adresse des bevorzugten DNS-Servers|10.0.0.2|
|Bereichswerte<br /><br />1. Bereichsname<br />2. IP-Startadresse<br />3. Endet IP-Adresse<br />4. Subnetzmaske<br />5. Standardgateway (optional)<br />6. Leasedauer|1. Primären Subnetz<br />2.  10.0.0.1<br />3.  10.0.0.254<br />4.  255.255.255.0<br />5.  10.0.0.1<br />6. 8Tage|
|Betriebsmodus des IPv6-DHCP-Servers|Nicht aktiviert.|

## <a name="bkmk_lab"></a>Mithilfe dieses Handbuchs in einem Testlabor

Dieses Handbuch können zum Bereitstellen von DHCP in einem Testlabor, bevor Sie in einer Produktionsumgebung bereitstellen. 

>[!NOTE]
>Wenn Sie nicht DHCP in einer Testumgebung bereitstellen möchten, können Sie mit dem Abschnittüberspringen [DHCP bereitstellen](#bkmk_deploy).

Die Anforderungen für Ihre Umgebung unterscheiden sich je nachdem, ob Sie einen physischen Servern oder virtuellen Maschinen \(VMs\) verwenden, und gibt an, ob Sie mithilfe von Active Directory-Domäne oder einen eigenständigen DHCP-Server bereitstellen. 

Die folgende Informationen können Sie um die minimale Ressourcen zu ermitteln, die Sie mithilfe dieses Handbuchs DHCP-Bereitstellung zu testen müssen.

### <a name="test-lab-requirements-with-vms"></a>Test Lab-Anforderungen mit virtuellen Computern

Zum Bereitstellen von DHCP in einem Testlabor mit virtuellen Computern benötigen Sie die folgenden Ressourcen.

Für die Bereitstellung oder eigenständige Bereitstellung benötigen Sie einen Server, der als Hyper\-V-Host konfiguriert ist.

**Bereitstellung**

Diese Bereitstellungsmethode ist einem physischen Server, einen virtuellen Switch, zwei virtuelle Server und einen virtuellen Client:

Erstellen Sie auf dem physischen Server im Hyper-V-Manager die folgenden Elemente.

1. Ein **intern** virtuellen Switch. Erstellen Sie eine **externen** virtuellen zu wechseln, da Ihre Test-VMs ist Ihr Hyper\-V-Host in einem Subnetz, einen DHCP-Server enthält, eine IP-Adresse vom DHCP-Server empfangen wird. Darüber hinaus kann der Test DHCP-Server, den Sie bereitstellen IP-Adressen für andere Computer im Subnetz zuweisen, in der Hyper\-V-Host installiert ist.
1. Ein virtueller Computer unter Windows Server2106 konfiguriert als Domänencontroller mit Active Directory Domain Services, die mit dem internen virtuellen Switch verbunden ist, die Sie erstellt haben. Dieses Handbuch angepasst werden, muss dieser Server eine statisch konfigurierte IP-Adresse des 10.0.0.2 verfügen. Informationen zum Bereitstellen von AD DS finden Sie im Abschnitt **Bereitstellung von DC1** in der Windows Server2016 [Kernnetzwerkhandbuch](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01).
1. Eine VM mit Windows Server-2106, die Sie mithilfe dieses Handbuchs und, die als DHCP-Server konfigurieren, mit der internen virtuellen verbunden ist wechseln Sie erstellt haben. 
1. Ein VM-Betriebssystem Windows Client, der mit internen virtuellen verbunden ist wechseln Sie erstellt haben und Sie verwenden möchten, um sicherzustellen, dass der DHCP-Server dynamisch IP-Adressen und DHCP-Optionen für DHCP-Clients bereit ist.

**Standalone DHCP-Server-Bereitstellung**

Diese Bereitstellungsmethode ist einem physischen Server, einen virtuellen Switch, einen virtuellen Server und einen virtuellen Client:

Erstellen Sie auf dem physischen Server im Hyper-V-Manager die folgenden Elemente.

1. Ein **intern** virtuellen Switch. Erstellen Sie eine **externen** virtuellen zu wechseln, da Ihre Test-VMs ist Ihr Hyper\-V-Host in einem Subnetz, einen DHCP-Server enthält, eine IP-Adresse vom DHCP-Server empfangen wird. Darüber hinaus kann der Test DHCP-Server, den Sie bereitstellen IP-Adressen für andere Computer im Subnetz zuweisen, in der Hyper\-V-Host installiert ist.
1. Eine VM mit Windows Server-2106, die Sie mithilfe dieses Handbuchs und, die als DHCP-Server konfigurieren, mit der internen virtuellen verbunden ist wechseln Sie erstellt haben.
1. Ein VM-Betriebssystem Windows Client, der mit internen virtuellen verbunden ist wechseln Sie erstellt haben und Sie verwenden möchten, um sicherzustellen, dass der DHCP-Server dynamisch IP-Adressen und DHCP-Optionen für DHCP-Clients bereit ist.

### <a name="test-lab-requirements-with-physical-servers"></a>Test Lab-Anforderungen mit physischen Servern.

Zum Bereitstellen von DHCP in einem Testlabor mit physischen Servern benötigen Sie die folgenden Ressourcen.

**Bereitstellung**

Diese Bereitstellungsmethode ist ein Hub oder Switch, zwei physische Server und einem physischen Client:

1. Ein Ethernet-Hub oder Switch mit dem können Sie die physischen Computer verbinden, mit dem Ethernet-Kabel
1. Einem physischen Computer mit Windows Server2106 als Domänencontroller mit Active Directory-Domänendiensten konfiguriert. Dieses Handbuch angepasst werden, muss dieser Server eine statisch konfigurierte IP-Adresse des 10.0.0.2 verfügen. Informationen zum Bereitstellen von AD DS finden Sie im Abschnitt **Bereitstellung von DC1** in der Windows Server2016 [Kernnetzwerkhandbuch](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01).
1. Einem physischen Computer mit Windows Server-2106, die Sie als DHCP-Server konfigurieren, mithilfe dieses Handbuchs. 
1. Einem physischen Computer mit einem Windows-Clientbetriebssystem, das Sie verwenden, um zu überprüfen, ob der DHCP-Server wird dynamisch IP-Adressen und DHCP-Optionen für DHCP-Clients bereit.

>[!NOTE]
>Wenn Sie nicht über genügend Testcomputern für diese Bereitstellung verfügen, können Sie einen Testcomputer für AD DS und DHCP - verwenden, aber diese Konfiguration für Produktionsumgebungen nicht empfohlen wird.

**Standalone DHCP-Server-Bereitstellung**

Diese Bereitstellungsmethode ist ein Hub oder Switch, einem physischen Server und einem physischen Client:

1. Ein Ethernet-Hub oder Switch mit dem können Sie die physischen Computer verbinden, mit dem Ethernet-Kabel
2. Einem physischen Computer mit Windows Server-2106, die Sie als DHCP-Server konfigurieren, mithilfe dieses Handbuchs. 
3. Einem physischen Computer mit einem Windows-Clientbetriebssystem, das Sie verwenden, um zu überprüfen, ob der DHCP-Server wird dynamisch IP-Adressen und DHCP-Optionen für DHCP-Clients bereit.


## <a name="bkmk_deploy"></a>Bereitstellen von DHCP

Dieser Abschnittenthält die Beispiel-Windows PowerShell-Befehle, die Sie zum Bereitstellen von DHCP auf einem Server verwenden können. Bevor Sie mit diesen Befehlen wird auf dem Server ausführen müssen Sie die Befehle entsprechend Ihrer Umgebung und Netzwerk ändern. 

Bevor Sie die Befehle ausführen, sollten Sie z.B. Beispielwerte in den Befehlen für die folgenden Elemente ersetzen:

- Computernamen
- IP-Adressbereich für die einzelnen Bereiche (1 Bereich pro Subnetz) konfiguriert werden soll
- Gibt die Subnetmask für jeden IP-Adressbereich, die Sie konfigurieren möchten.
- Name des für die einzelnen Bereiche
- Ausschlussbereich für jeden Bereich
- DHCP-Werte, z.B. als Standardgateway, Domänenname und DNS oder WINS-Server
- Schnittstellennamen

>[!IMPORTANT]
>Überprüfen Sie und ändern Sie jeden Befehl für Ihre Umgebung, bevor Sie den Befehl ausführen.

### <a name="where-to-install-dhcp---on-a-physical-computer-or-a-vm"></a>Wo Installieren von DHCP - auf einem physischen Computer oder einem virtuellen Computer?

Sie können die DHCP-Serverrolle auf einem physischen Computer oder auf einer virtuellen Maschine installieren \(VM\), die auf einem Hyper\-V-Host installiert ist. Wenn Sie DHCP auf einem virtuellen Computer installieren, und der DHCP-Server IP-Adresszuweisungen für Computer im physischen Netzwerk bereitstellen, mit der Hyper-V-Host verbunden ist, müssen Sie den virtuellen Netzwerkadapter für die virtuellen Computer anschließen, mit einem virtuellen Hyper-V-Switch, der **externen**.

Weitere Informationen finden Sie im Abschnitt **Erstellen eines virtuellen Switches mit Hyper-V-Manager** im Thema [Erstellen eines virtuellen Netzwerks](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network).

### <a name="run-windows-powershell-as-an-administrator"></a>WindowsPowerShell als Administrator ausführen

Das folgende Verfahren können Windows PowerShell mit Administratorrechten ausführen.

1. Klicken Sie auf einem Computer unter Windows Server2016, auf **starten**, anschließend mit der Maustaste des Windows PowerShell-Symbol. Ein Menü angezeigt wird. 

2. Klicken Sie im Menü auf **weitere**, und klicken Sie dann auf **als Administrator ausführen**. Wenn Sie dazu aufgefordert werden, geben Sie die Anmeldeinformationen für ein Konto mit Administratorrechten auf dem Computer. Wenn das Benutzerkonto, mit dem Sie am Computer angemeldet sind, ein Administratorkonto Ebene ist, erhalten Sie keine administratoranmeldeaufforderung angezeigt.

3. Windows PowerShell wird mit Administratorrechten geöffnet.

### <a name="rename-the-dhcp-server-and-configure-a-static-ip-address"></a>Benennen Sie den DHCP-Server, und konfigurieren Sie eine statische IP-Adresse

Wenn Sie nicht bereits geschehen, können Sie die folgenden Windows PowerShell-Befehle zum Umbenennen des DHCP-Servers und konfigurieren eine statische IP-Adresse für den Server.

**Konfigurieren einer statischen IP-Adresse**

Sie können die folgenden Befehle auf dem DHCP-Server eine statische IP-Adresse zuweisen und so konfigurieren Sie die DHCP-Server-TCP/IP-Eigenschaften mit der richtigen DNS-Server IP-Adresse verwenden. Sie müssen die Schnittstellennamen und IP-Adressen in diesem Beispiel wird auch durch Werte ersetzen, die Sie verwenden, um Ihren Computer konfigurieren möchten.

 `New-NetIPAddress -IPAddress 10.0.0.3 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24`

 `Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 10.0.0.2`

Weitere Informationen zu diesen Befehlen finden Sie unter den folgenden Themen.

- [New-NetIPAddress](https://technet.microsoft.com/itpro/powershell/windows/tcpip/new-netipaddress)
- [Set-DnsClientServerAddress](https://technet.microsoft.com/itpro/powershell/windows/dns-client/set-dnsclientserveraddress)

**Umbenennen des Computers**

Sie können die folgenden Befehle umbenennen, und klicken Sie dann den Computer neu starten.

`Rename-Computer -Name DHCP1`

 `Restart-Computer`

Weitere Informationen zu diesen Befehlen finden Sie unter den folgenden Themen.

- [Rename-Computer](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/rename-computer)
- [Restart-Computer](https://msdn.microsoft.com/powershell/reference/4.0/microsoft.powershell.management/restart-computer)

### <a name="join-the-computer-to-the-domain-optional"></a>Hinzufügen des Computers zu der Domäne \(Optional\)

Wenn Sie den DHCP-Server in einer Active Directory-Domäne-Umgebung installieren, müssen Sie der Computer der Domäne beitreten. Öffnen Sie Windows PowerShell mit Administratorrechten, und führen Sie den folgenden Befehl nach dem Ersetzen der NetBIOS-Domänenname **CORP** mit dem Wert, der für Ihre Umgebung geeignet ist.

    Add-Computer CORP

Wenn Sie aufgefordert werden, geben Sie die Anmeldeinformationen für ein Domänenbenutzerkonto, das über die Berechtigung zum Hinzufügen eines Computers zur Domäne verfügt. 

    Restart-Computer

Weitere Informationen zum Befehl Add-Computer finden Sie unter dem folgenden Thema.

- [Add-Computer](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/add-computer)

### <a name="install-dhcp"></a>Installieren Sie DHCP

Nach dem Neustart des Computers, öffnen Sie Windows PowerShell mit Administratorrechten, und installieren Sie DHCP dann durch den folgenden Befehl ausführen.

    Install-WindowsFeature DHCP -IncludeManagementTools

Weitere Informationen zu diesem Befehl finden Sie unter dem folgenden Thema.

- [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/server-manager/install-windowsfeature)

### <a name="create-dhcp-security-groups"></a>Erstellen Sie DHCP-Sicherheitsgruppen

Um Sicherheitsgruppen zu erstellen, müssen Sie einen Network Shell-\(netsh\)-Befehl in Windows PowerShell ausführen und starten Sie den DHCP-Dienst, damit die neuen Gruppen aktiviert werden.

Beim Ausführen der folgenden Netsh-Befehl auf dem DHCP-Server, der **DHCP-Administratoren** und **DHCP-Benutzer** Sicherheitsgruppen werden erstellt, **lokale Benutzer und Gruppen** auf dem DHCP-Server.

    netsh dhcp add securitygroups

Der folgende Befehl wird den DHCP-Dienst auf dem lokalen Computer neu gestartet.

    Restart-service dhcpserver

Weitere Informationen zu diesen Befehlen finden Sie unter den folgenden Themen.

- [Network Shell (Netsh)](../netsh/netsh.md)
- [Restart-Service](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/restart-service)

### <a name="authorize-the-dhcp-server-in-active-directory-optional"></a>Autorisieren des DHCP-Servers in Active Directory-\(Optional\)

Wenn Sie DHCP in einer Umgebung installieren, müssen Sie die folgenden Schritteaus, um den DHCP-Server in der Domäne ausgeführt werden zu autorisieren ausführen.

>[!NOTE]
>Nicht autorisierte DHCP-Server, die in Active Directory-Domänen installiert werden können nicht ordnungsgemäß, und führen Sie keine IP-Adressen für DHCP-Clients leasen. Das automatische Deaktivieren der nicht autorisierte DHCP-Server ist eine Sicherheitsfunktion, die verhindert, dass nicht autorisierte DHCP-Server falsche IP-Adressen für Clients in Ihrem Netzwerk zuweisen.

Den folgenden Befehl können Sie den DHCP-Server der Liste der autorisierten DHCP-Server in Active Directory hinzufügen. 

>[!NOTE]
>Wenn Sie nicht mit eine Umgebung mit Domänen verfügen, werden Sie mit diesem Befehl nicht ausgeführt.

 `Add-DhcpServerInDC -DnsName DHCP1.corp.contoso.com -IPAddress 10.0.0.3`

Um sicherzustellen, dass der DHCP-Server in Active Directory berechtigt ist, können Sie den folgenden Befehl verwenden.

    Get-DhcpServerInDC

Folgendes sind die Ergebnisse, die in Windows PowerShell angezeigt werden.

    
        IPAddress   DnsName
        ---------   -------
        10.0.0.3    DHCP1.corp.contoso.com
    

Weitere Informationen zu diesen Befehlen finden Sie unter den folgenden Themen.

- [Add-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverindc)
- [Get-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/get-dhcpserverindc)

### <a name="notify-server-manager-that-post-install-dhcp-configuration-is-complete-optional"></a>Server-Manager, DHCP Post\-Installation, Konfiguration abgeschlossen \(Optional\) wird benachrichtigt werden

Nach Abschluss der Installation von Post\ Aufgaben, z.B. Erstellen von Sicherheitsgruppen und Autorisieren des DHCP-Server in Active Directory kann Server-Manager weiterhin eine Warnung in der Benutzeroberfläche, die besagt, dass Post\-Installationsschritte abgeschlossen sein müssen, mit dem Assistenten für die Konfiguration des DHCP-Post-Installation angezeigt.

Sie können diese Meldung Now\ unnötige und ungenaue verhindern im Server-Manager durch den folgenden Registrierungsschlüssel mit dem folgenden Windows PowerShell-Befehl konfigurieren.

    Set-ItemProperty –Path registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ServerManager\Roles\12 –Name ConfigurationState –Value 2

Weitere Informationen zu diesem Befehl finden Sie unter dem folgenden Thema.

- [Set-ItemProperty](https://msdn.microsoft.com/powershell/reference/4.0/microsoft.powershell.management/set-itemproperty?f=255&MSPPError=-2147217396)

### <a name="set-server-level-dns-dynamic-update-configuration-settings-optional"></a>Festlegen der Server auf DNS-dynamisches Update Konfiguration Einstellungen \(Optional\)

Wenn Sie den DHCP-Server dynamische DNS-Updates für DHCP-Clientcomputer ausführen möchten, können Sie den folgenden Befehl zum Konfigurieren dieser Einstellung ausführen. Dies ist ein Server festlegen, kein Bereich Ebene festlegen, damit sie alle Bereiche auswirkt, die Sie auf dem Server zu konfigurieren. Dieser Beispielbefehl wird auch den DHCP-Server zum Löschen von DNS-Ressourceneinträgen für Clients nach Ablauf der Client mindestens konfiguriert.

    Set-DhcpServerv4DnsSetting -ComputerName "DHCP1.corp.contoso.com" -DynamicUpdates "Always" -DeleteDnsRRonLeaseExpiry $True

Sie können den folgenden Befehl verwenden, so konfigurieren Sie die Anmeldeinformationen, die der DHCP-Server zu registrieren oder dessen Registrierung von Clientdatensätzen auf einem DNS-Server verwendet. In diesem Beispiel speichert Anmeldeinformationen auf einem DHCP-Server. Der erste Befehl verwendet **Get-Credential** zum Erstellen einer **PSCredential** Objekt, und dann wird das Objekt in der **$Credential** Variable. Mit dem Befehl werden Sie aufgefordert, Benutzername und Kennwort, müssen Sie sicherstellen, dass Sie Anmeldeinformationen für ein Konto angeben, das über die Berechtigung zum Aktualisieren von Ressourceneinträgen auf dem DNS-Server verfügt.

    
    $Credential = Get-Credential
    Set-DhcpServerDnsCredential -Credential $Credential -ComputerName "DHCP1.corp.contoso.com"
    

Weitere Informationen zu diesen Befehlen finden Sie unter den folgenden Themen.

- [Set-DhcpServerv4DnsSetting](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverv4dnssetting)
- [Set-DhcpServerDnsCredential](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverdnscredential)

### <a name="configure-the-corpnet-scope"></a>Konfigurieren des Suchbereichs Corpnet

Nach der DHCP-Installation abgeschlossen ist, können Sie die folgenden Befehle verwenden, konfigurieren und aktivieren Sie den Bereich Corpnet, erstellen einen Ausschlussbereich für den Bereich, und Konfigurieren der DHCP-Optionen als Standardgateway, DNS-Server IP-Adresse und DNS-Domänennamen.

    
    Add-DhcpServerv4Scope -name "Corpnet" -StartRange 10.0.0.1 -EndRange 10.0.0.254 -SubnetMask 255.255.255.0 -State Active`
    
    Add-DhcpServerv4ExclusionRange -ScopeID 10.0.0.0 -StartRange 10.0.0.1 -EndRange 10.0.0.15`
    
    Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.0.1 -ScopeID 10.0.0.0 -ComputerName DHCP1.corp.contoso.com`
    
    Set-DhcpServerv4OptionValue -DnsDomain corp.contoso.com -DnsServer 10.0.0.2
    

Weitere Informationen zu diesen Befehlen finden Sie unter den folgenden Themen.

- [Hinzufügen DhcpServerv4Scope](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverv4scope)
- [Hinzufügen DhcpServerv4ExclusionRange](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverv4exclusionrange)
- [Set-DhcpServerv4OptionValue](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverv4optionvalue)

### <a name="configure-the-corpnet2-scope-optional"></a>Konfigurieren der Corpnet2 \(Optional\) Bereich

Wenn Sie eine zweite Subnetz, der mit dem ersten Subnetz mit einem Router verfügen, DHCP-Weiterleitung aktiviert ist verbunden ist, können Sie die folgenden Befehle, einen zweiten Bereich, der mit dem Namen Corpnet2 in diesem Beispiel hinzu. In diesem Beispiel wird auch ein Ausschlussbereich und die IP-Adresse für das Standardgateway \ (die Router IP-Adresse auf der Subnet\) des Subnetzes Corpnet2.

 `Add-DhcpServerv4Scope -name "Corpnet2" -StartRange 10.0.1.1 -EndRange 10.0.1.254 -SubnetMask 255.255.255.0 -State Active`

 `Add-DhcpServerv4ExclusionRange -ScopeID 10.0.1.0 -StartRange 10.0.1.1 -EndRange 10.0.1.15`

 `Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.1.1 -ScopeID 10.0.1.0 -ComputerName DHCP1.corp.contoso.com`

Wenn Sie weitere Subnetze, die von diesem DHCP-Server verwaltet werden verfügen, können Sie diese Befehle wiederholen, die von verschiedenen Werten für alle von der Befehlsparameter Bereiche für jedes Subnetz hinzu.

>[!IMPORTANT]
>Stellen Sie sicher, dass alle Router zwischen DHCP-Clients und dem DHCP-Server für die Weiterleitung von DHCP-Nachrichten konfiguriert sind. Weitere Informationen finden Sie in der Routerdokumentation Informationen zum Konfigurieren von DHCP-Weiterleitung.

## <a name="bkmk_verify"></a>Überprüfen Sie die Serverfunktionalität

Um sicherzustellen, dass der DHCP-Server dynamische Zuweisung von IP-Adressen für DHCP-Clients bereitstellt, können Sie einen anderen Computer mit einem serviced Subnetz verbinden. Nachdem Sie das Ethernet-Kabel an den Netzwerkadapter und schalten Sie den Computer anschließen, fordert er eine IP-Adresse vom DHCP-Server. Sie können die erfolgreiche Konfiguration überprüfen, mithilfe der **Ipconfig/all** Befehl und Überprüfen der Ergebnisse, oder versuchen, durch die Konnektivitätstests ausführen, z.B. Zugriff auf Webressourcen mit Ihrem Browser oder Dateifreigaben mit Windows-Explorer oder einer anderen Anwendung.

Wenn der Client keine IP-Adresse vom DHCP-Server erhält, führen Sie die folgenden Schrittezur Problembehandlung.

1. Stellen Sie sicher, dass das Ethernet-Kabel an sowohl der Computer und Ethernet-Switches, Hub oder Router angeschlossen ist.
1. Wenn Sie die Clientcomputer in einem Netzwerksegment, die von einem Router von der DHCP-Server getrennt ist angeschlossen, stellen Sie sicher, dass der Router zum Weiterleiten von DHCP-Nachrichten konfiguriert ist.
1. Stellen Sie sicher, dass der DHCP-Server in Active Directory autorisiert ist, indem Sie mit dem folgenden Befehl zum Abrufen der Liste der autorisierten DHCP-Server aus Active Directory. [Get-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/get-dhcpserverindc).
1. Stellen Sie sicher, dass die Bereiche durch Öffnen der DHCP-Konsole aktiviert werden \ (Server-Manager **Tools**, **DHCP**\), Erweitern der Serverstruktur Bereiche, und klicken Sie dann mit der rechten Maustaste klicken überprüfen jeder Bereich. Das resultierende Menü enthält die Auswahl **aktivieren**, klicken Sie auf **aktivieren**. \ (Wenn der Bereich bereits aktiviert ist, liest die Menüoption **Deactivate**. \) 

## <a name="bkmk_dhcpwps"></a>Windows PowerShell-Befehle für DHCP

Die folgende Referenz enthält Befehl Beschreibungen und Syntax für alle DHCP-Server Windows PowerShell-Befehle für Windows Server2016. Das Thema enthält Befehle in alphabetischer Reihenfolge basierend auf dem Verb am Anfang der Befehle wie z.B. **abrufen** oder **festlegen**.

>[!NOTE]
>Sie können keine Windows Server2016-Befehle in Windows Server2012 R2 verwenden.

- [DhcpServer-Modul](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/index)

Die folgende Referenz enthält Befehl Beschreibungen und Syntax für alle DHCP-Server Windows PowerShell-Befehle für Windows Server2012 R2. Das Thema enthält Befehle in alphabetischer Reihenfolge basierend auf dem Verb am Anfang der Befehle wie z.B. **abrufen** oder **festlegen**.

>[!NOTE]
>Sie können Windows Server2012 R2-Befehle in Windows Server2016 verwenden.

- [DHCP-Server-Cmdlets in WindowsPowerShell](https://technet.microsoft.com/library/jj590751.aspx)

## <a name="bkmk_list"></a>Liste der Windows PowerShell-Befehle in diesem Handbuch

Es folgt eine einfache Liste von Befehlen und Beispielwerte, die in dieser Anleitung verwendet werden.

    
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
    


